```
 cd Istio/
  169  ls
  170  cd _course_files/
  171  ls
  172  cd x86_amd64/
  173  ls
  174  cd 2-Traffic-
  175  cd 2-Traffic-Starting/
  176  ls
  177  k get pods -A
  178  alias k=kubectl
  179  k get pods -A
  180  ls
  181  k apply -f 1-istio-init.yaml 
  182  k apply -f 2-istio-minikube.yaml 
  183  ls
  184  k apply -f 4-label-default-namespace.yaml 
  185  clear
  186  k get pods -A
  187  ls
  188  cat 5-application-no-istio.yaml 
  189  ls
  190  vi readme.md
  191  ls
  192  k apply -f 5-application-no-istio.yaml 
  193  k get pods



"Introducing Canaries"

-- now ,make changes in the application : 5-application-no-istio.yaml
-- in staff-service deployment , change image to :
   -- image: richardchesterwood/istio-fleetman-staff-service:6-placeholder


-- we reverted te image , now we will deploy newer version using canary deployment 

--- now implement canary using normal kubernetes by adding 1 more deployment yaml file like below :


---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: staff-service-safe-version
spec:
  selector:
    matchLabels:
      app: staff-service
  replicas: 1
  template: # template for the pods
    metadata:
      labels:
        app: staff-service
    spec:
      containers:
      - name: staff-service
        image: richardchesterwood/istio-fleetman-staff-service:6-placeholder
        env:
        - name: SPRING_PROFILES_ACTIVE
          value: production-microservice
        imagePullPolicy: Always
        ports:
        - containerPort: 8080
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: staff-service-risky-version
spec:
  selector:
    matchLabels:
      app: staff-service
  replicas: 1
  template: # template for the pods
    metadata:
      labels:
        app: staff-service
    spec:
      containers:
      - name: staff-service
        image: richardchesterwood/istio-fleetman-staff-service:6
        env:
        - name: SPRING_PROFILES_ACTIVE
          value: production-microservice
        imagePullPolicy: Always
        ports:
        - containerPort: 8080
---

---- traffic will now split 50:50 ..... observe in kiali in workload graph ... and also u can ovserved in app itself...

--- to effectively do it using istio : lets say i wanna send 1 % traffoic to risky version evern if im having less no of pods ..
 -- go to kiali -- go to fleetman-staff-service  >> actions >>> Create Weighted Routing :
  --- it will create a virtual service and a destination rule ....



```
