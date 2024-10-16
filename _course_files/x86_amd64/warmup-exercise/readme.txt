-- if creating kubeadm cluster , it shud be min 2 vcpu and 4 gb ram


alias k=kubectl
  504  k get nodes
  505  minikube status
  506  minikube start --driver virtualbox --no-vtx-check --memory 4096
  507  k get pods
  508  k get nodes
  509  minikube status




--- after applying 3-kiali-secret.yaml, before installing ur application pods ..

-- make sure to enable sidecar injection by creating a label for ur specified namespace


k describe ns default
  540  k label ns default istio-injection=enabled
  541  k describe ns default


-- after this go ahead with the 4th file : 4-application-full-stack.yaml

 k apply -f 4-application-full-stack.yaml
  538  k get pods
  539  clear
  540  k get pods -A
  542  minikube ip



http://192.168.59.101:30080/   , to access our application ..

--  to access kiali :

http://192.168.59.101:31000
-- go to graph >> default ns and see the complete graph of our app





--- to find out the problem btw staff service and driver-monitorig service :


https://istio.io/latest/docs/tasks/traffic-management/request-timeouts/


   --- check the jaeger for finding the issue :
       http://54.207.221.4:31001/

    ---- requests are taking very long time to process 



  ---- to fix the request taking long and to to terminate requests whch are taking long time or more than 1 second ....
        fix yr 4th yaml as below :



kind: VirtualService
metadata:
  name: fleetman-driver-monitoring
spec:
  hosts:
  - 2oujlno5e4.execute-api.us-east-1.amazonaws.com
  http:
  - match:
    - port: 80
    timeout: 1s
    route:
    - destination:
        host: 2oujlno5e4.execute-api.us-east-1.amazonaws.com




------





