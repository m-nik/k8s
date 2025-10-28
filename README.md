# k8s

#### k alias 
```sh
if [ -f /etc/bash_completion ] && ! shopt -oq posix; then
    . /etc/bash_completion
fi
alias k="kubectl"
source <(kubectl completion bash)
complete -o default -F __start_kubectl k
```



#### Get pods deployed on specific nodes
```sh
kubectl get pod -A --field-selector spec.nodeName=worker1
```
