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

## config

man *MUSS* in client -> client scopes -> microprofile-jwt aktivieren, weil sonst keine rollen angezeigt werden. 

## theme

https://github.com/MAXIMUS-DeltaWare/material-keycloak-theme
einfach `./copy_theme.sh` machen, nachdem keycloak online ist.

danach das realm mit `realm-export.json` installieren.

## defaults

realm: `sau`

client: `default`

das mit dem "passwort ändern" muss man pro-account festlegen

hier kann man das testen: https://www.keycloak.org/app/#url=https://keycloak.sau-portal.de&realm=sau&client=default


## testtokens erstellen

um backend-dienste etc zu testen, braucht man am besten echte tokens. Man bekommt diese, indem:

1. eine instanz vom root-ui starten. dabei muss man darauf achten, dass z.b `keycloak.sau-portal.de` als provider hinterlegt ist
2. so ein anti-cors browser plugin installieren. ansonsten funktioniert die anmeldung lokal nicht (firefox: "CORS everywhere")
3. den token aus dem browser storage von folgendem key extrahieren: oidc.user:http://keycloak.sau-portal.de/realms/sau:default (müsste das erste ding in dem json objekt sein)
4. (optional) diesen b64 string kann man dann auf https://jwt.io validieren
5. diesen dann als `Authorization` header nutzen.


### root-ui oidc config:
```diff
diff --git a/src/main.tsx b/src/main.tsx
index 6592ca0..2a2be80 100644
--- a/src/main.tsx
+++ b/src/main.tsx
@@ -6,7 +6,7 @@ import App from "./components/App";
 import { AuthProvider, useAuth } from "react-oidc-context";
 import { WebStorageStateStore } from "oidc-client-ts";
 
-const oidcAuthority = "http://localhost:8080"
+const oidcAuthority = "http://keycloak.sau-portal.de"
 
 // you can use this for scope config: https://authts.github.io/oidc-client-ts/interfaces/UserManagerSettings.html#scope
 // other config params go here aswell
```
