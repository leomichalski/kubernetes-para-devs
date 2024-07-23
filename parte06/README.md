# Controller Pattern

Mais em <https://kubernetes.io/pt-br/docs/concepts/architecture/controller/>

## Control Loop

Em robótica, é muito comum o uso de "loops de controle" (control loops). Um exemplo de control loop é um termostato de uma sala.

Quando você define a temperatura, isso indica ao termostato sobre o seu estado desejado. O termostato atua de forma a trazer o estado atual mais perto do estado desejado, ligando ou desligando o equipamento.

No Kubernetes, controladores são loops de controle que observam o estado do seu cluster, e então fazer ou requisitar mudanças onde necessário. Cada controlador tenta mover o estado atual do cluster mais perto do estado desejado.

## Trecho de Código

A seguinte função executa a lógica principal do "control loop" do recurso do tipo StatefulSet.

```go
func (ssc *defaultStatefulSetControl) UpdateStatefulSet(ctx context.Context, set *apps.StatefulSet, pods []*v1.Pod) (*apps.StatefulSetStatus, error) {
	set = set.DeepCopy() // set is modified when a new revision is created in performUpdate. Make a copy now to avoid mutation errors.

	// list all revisions and sort them
	revisions, err := ssc.ListRevisions(set)
	if err != nil {
		return nil, err
	}
	history.SortControllerRevisions(revisions)

	currentRevision, updateRevision, status, err := ssc.performUpdate(ctx, set, pods, revisions)
	if err != nil {
		errs := []error{err}
		if agg, ok := err.(utilerrors.Aggregate); ok {
			errs = agg.Errors()
		}
		return nil, utilerrors.NewAggregate(append(errs, ssc.truncateHistory(set, pods, revisions, currentRevision, updateRevision)))
	}

	// maintain the set's revision history limit
	return status, ssc.truncateHistory(set, pods, revisions, currentRevision, updateRevision)
}
```

Em <https://github.com/kubernetes/kubernetes/blob/77c3859aeee97d6d118d9494c950766a4c296734/pkg/controller/statefulset/stateful_set_control.go#L79-L100>
