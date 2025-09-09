# auth

## minikube setup (linux)

1. minikube herunterladen: [download](https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download)
2. treiber etc konfigurieren: `minikube config set driver kvm2 && minikube config set memory 4G`
3. cluster starten: `minikube start`
4. ing installieren: `minikube addons enable ingress`

funktioniert btw noch nicht mit dem frontend weil CORS und so

## keycloak installieren:

1. `kubectl apply -f keycloak.yaml`
2. `kubectl apply -f keycloak-ingress.yaml`

## theme

https://github.com/MAXIMUS-DeltaWare/material-keycloak-theme
einfach `./copy_theme.sh` machen, nachdem keycloak online ist.

danach das realm mit `realm-export.json` installieren.

## defaults

realm: `sau`

client: `default`

das mit dem "passwort ändern" muss man pro-account festlegen

hier kann man das testen: https://www.keycloak.org/app/#url=https://keycloak.sau-portal.de&realm=sau&client=default
