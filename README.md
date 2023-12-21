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

