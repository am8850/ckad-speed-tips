# Time saving tips when taking the CKAD

Speed tips for taking the CKAD studies:

## Practice a lot

## Setup aliases

```bash
alias k=kubectl
alias kg='kubectl get'
alias kc='kubectl create'
alias kd='kubectl delete'
alias kset='kubectl config set-context --current --namespace='
```

> Note: It is better if you can add them to ~/.bashrc or ~/.zshrc. Then execute ```source ~/.bashrc``` or ```source ~/.zshrc```

## Setup your ~/.vimrc or ~/.nanorc

```bash
set tab=2
set tabtosapce
```

## Create some yaml ahead of time and use this yaml when needed

```bash
k run nginx --image=nginx --restart=Never --port=80 --requests="cpu=250m,memory=128Mi" --limits=cpu=500m,memory=250Mi" -o yaml --dry-run=client > npod.yaml

k run busybox --image=busybox --restart=Never -o yaml  --dry-run=client -- /bin/sh -c 'while true;do sleep1;done' > npod.yaml

k create deployment web --image=nginx:alpine --port=80 --replicas=3 -o yaml --dry-run=client > deploy.yaml
```

> Note: Use this generated yaml when you need some pod yaml. It will save you from time from having to type this long commands every time.

> Note: You can use a similar technique for deployments and services

```bash
# overwrite testpod.yaml file
cat npod.yaml > testpod.yaml

# append to testpod.yaml file
cat npod.yaml >> testpod.yaml
```

## Don't forget your grep

```
k describe po/nginx | grep -i status

k logs nginx | grep -i information
```

## Tmux

- If tmux is available monitor your changes in a second pane

```bash
watch kubect get all -o wide 
```

## POD, PVC, PV, SC

- A Pod uses a PVC which in turn uses a PV which in turn can use a SC.
