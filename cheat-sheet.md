# K8s Cheat Sheet

## Deleting the undeletable

### Force delete a pod
```bash
kubectl delete pod <pod-name> --grace-period=0 --force -n <namespace>
```

## AWS Specific

### Add new EKS cluster to local kube config
```bash
aws eks update-kubeconfig --region <region-code> --name <cluster-name>
```

### Force delete an ALB Ingress
Sometimes the ingress wont delete itself due to configuration conflicts, which make it wait indefinitely.

The solution is edit the Ingress and remove the `finalizers`:
```bash
  finalizers:
    - ingress.k8s.aws/resources
```
After deleting these lines, and saving your changes, the ingress should get deleted. You may have to delete an orphaned Target Group via the AWS console.
