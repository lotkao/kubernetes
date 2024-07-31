# K8s Cheat Sheet

## Deleting the undeletable

### Force delete a pod
```bash
kubectl delete pod <pod-name> --grace-period=0 --force -n <namespace>
```

### Force delete an ALB Ingress
Sometimes the ingress wont delete itself due to configuration conflicts, which make it wait indefinitely.

The solution is edit the Ingress and remove the `finalizers`:
```bash
  finalizers:
    - ingress.k8s.aws/resources
```
After deleting these lines, and saving your changes, the ingress should get deleted.
