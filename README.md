# auth

## minikube setup (linux)

1. minikube herunterladen: [download](https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download)
2. treiber etc konfigurieren: `minikube config set driver kvm2 && minikube config set memory 4G`
3. cluster starten: `minikube start`
4. ing installieren: `minikube addons enable ingress`

## keycloak installieren:

1. `kubectl apply -f keycloak.yaml`
2. `kubectl apply -f keycloak-ingress.yaml`


## theme
https://github.com/MAXIMUS-DeltaWare/material-keycloak-theme
prepare configmap: `kubectl create configmap kc-theme --from-file material`


## defaults
realm: `sau`
client: `default`
