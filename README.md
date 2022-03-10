
# HPA Kubernetes cluster

## Initialize cluster

- Firstable, you need to create a cluster in [Elastic Kubernetes Service](https://us-west-2.console.aws.amazon.com/eks)

    [Here](https://docs.aws.amazon.com/eks/latest/userguide/getting-started.html), we have the instructions

- After that, we need to create a node group with these tags
```
    Key                                     | Value
    k8s.io/cluster-autoscaler/<my-cluster>	| owned
    k8s.io/cluster-autoscaler/enabled	    | TRUE
```
- When the nodeGroup is ready whe need to deploy the next files:
  - The next files will always be executed with `kubectl apply -f <FILE>`
  - deploy the `deploy.yml` for a simple web page.
  - deploy the `service.yml` for a simple web page.
  - deploy the `hpa.yml` for a hpa image.
  - deploy the `service-hpa.yml` for a hpa conncetion.
  - deploy the `hpa-deploy.yml` for a hpa in kubernetes.
  - deploy the `hpa-deploy.yml` for a hpa in kubernetes.
  - **Create accounts with identity role**
  - create an account for `aws-load-balancer-controller`.
  - create an account for `external-dns`.
  - create an account for `autoscaler`.
  - **Deploy service accounts**
  - deploy the `service-account.yml` for the load balancer.
  - deploy the `service-account-dns.aml` for the external dns with route 53.
  - deploy the `service-account.yml` for the load balancer.
  - **Ingress**
  - deploy the `ingress.yml` for the ingress with alb and dns.

### For to do a test
- You can run `kubectl run -it test --image=busybox -- sh`;
- When you are in the container you can do many requests to http://hpa-test in a loop, with those requests the pod will grow with many pods and when the node won't be able to create more pods, the autoscaler will create another node, and when you stop the loop that node or nodes will be killed.