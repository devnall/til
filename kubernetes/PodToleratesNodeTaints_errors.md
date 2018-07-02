# Fixing PodToleratesNodeTaints Error

## Description of Problem

When attempting to deploy a service or pod, it hangs in `Pending` state.

If you `kubectl describe pod $POD` you see an error like `No nodes are
available that match all of the following predicates::
PodToleratesNodeTaints`.

## Fixing

Prerequisites:
* Make sure `kubectl get nodes` shows all nodes in a `Ready` state.
* Make sure the nodes have sufficient resources for the new pods via `kubectl
describe nodes`
* Make sure that the image specified in the kube manifest is availble from the
docker registry.

1. Run `kubectl describe node $(hostname) | grep -i taint`
2. Verify that you see something like `Taints:
node-role.kubernetes.io/master:NoSchedule`, which means your node is
unschedulable
3. Remove the taint from the node: `kubectl taint nodes $(hostname)
node-role.kubernetes.io/master:NoSchedule-`
4. Previous command should return something like `node {{ NODE_NAME }}
untainted`
5. You should now be able to schedule pods on the node

## Reference:

http://bertdotself.com/kubernetes-deployment-error-podtoleratesnodetaints/
https://github.com/kubernetes/kubernetes/issues/49440
