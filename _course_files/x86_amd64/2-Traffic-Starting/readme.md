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


-- now ,make changes in the application : 5-application-no-istio.yaml
-- in staff-service deployment , change image to :
   -- image: richardchesterwood/istio-fleetman-staff-service:6-placeholder







```
