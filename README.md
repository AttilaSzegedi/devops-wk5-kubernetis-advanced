# devops-wk5-kubernetis-advanced
 
 # how to check the default namespaces:
 kubectl config view --minify

 # create namespace to not use the default:
 kubectl create namespace home 
 will create a new "home" namespace
kubectl config set-context --current --namespace=home
it will made a change from current to home
the original were "kind-kind" namespace

# kustomazitan.yaml
give the required yaml files to them and CMD "kubectl kustomize ." (file location in the end) will manage in 1 comad the all file together

kubectl apply --dry-run=server parameter made validation first

kubectl apply --dry-run=server -k .
-k mean the use kustomize

# if we set namespace the normal get pods will result nothing it need to use the namspace part
kubectl get pods -n kustom

# patching
It means for the hole Kostimazion general data should be sets.
such as namespases labels.
Also could manage to override the deployment tags, such as Replicaion or image to change from defaut in specail case

# Mount files
for have env variable in file and stored in file system
problem not version, after creaton modify is difficult

get the replica set and see that the file change and apply created a new replica (9c...) kubectl get replicaset -n kustom
NAME                 DESIRED   CURRENT   READY   AGE
example-6d56879c96   0         0         0       3m6s
example-9cd4bc9c6    2         2         2       9s


We could made a roll back to get the previus verison
 kubectl rollout undo deploy/example -n kustom
It made a roll back
 kubectl get replicaset -n kustom
NAME                 DESIRED   CURRENT   READY   AGE
example-6d56879c96   2         2         2       4m14s
example-9cd4bc9c6    0         0         0       77s

if we delete means the cm (config map left there)

 kubectl delete -k ./
configmap "content-4k9b578cf2" deleted
service "example" deleted
deployment.apps "example" deleted
ingress.networking.k8s.io "example" deleted


 kubectl get cm -n kustom
NAME                 DATA   AGE
content-bbfgddmdkb   1      9m6s
kube-root-ca.crt     1      13h

need manual deletion in name space:
kubectl delete cm -l app=example -n kustom
configmap "content-bbfgddmdkb" deleted

# ingress denid all end point just left the file
with same as other patch will override the original

need to made in patch file with operato add (-op: add)
and add new section to kustomize file