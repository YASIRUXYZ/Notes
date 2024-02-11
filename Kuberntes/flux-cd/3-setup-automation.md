> [!note]  
> ## setup flux automation image update: ↓↓↓
>
>1. Add **` automation.yaml `** to ` main system `
>```md
>apiVersion: image.toolkit.fluxcd.io/v1beta1
>kind: ImageUpdateAutomation
>metadata:
>  name: flux-system
>  namespace: flux-system
>spec:
>  git:
>    checkout:
>      ref:
>        branch: main
>    commit:
>      author:
>        email: fluxcdbot@users.noreply.github.com
>        name: fluxcdbot
>    push:
>      branch: main
>  interval: 1m0s
>  sourceRef:
>    kind: GitRepository
>    name: flux-system
>  update:
>    path: ./clusters/home
>    strategy: Setters
>```

> [!tip]
> ### how make docker login data string
> 1) Make **` github package view access string `**
> ```md
> echo -n "<GITHUB_USERNAME>:<PAT_TOKEN_VIEW_IMAGE>" | base64
> ```
> 2) Make **` docker login data string `** using ` github package view access string `
> ```md
> echo -n  `{"auths":{"ghcr.io":{"auth":`<GITHUB_PACKAGE_VIEW_STRING>`}}}` | base64
> ```

> [note]
>2. Add **` secret.yaml `** to ` main system ` for get access
>#Before use command change this values in the command
>```yaml
><DOCKER_ACCESS_NAME> : make secrete name for access docker images later
><IMAGE_LIST_LOGIN> : docker login data string 
>```
>```md
>kind: Secret
>type: kubernetes.io/dockerconfigjson
>apiVersion: v1
>metadata:
>  name: <DOCKER_ACCESS_NAME>
>  namespace: flux-system
>  labels:
>    app: git
>data:
>  .dockerconfigjson: <IMAGE_LIST_LOGIN>
>```
>
>3. make new git repo flie structure like this
```diff
 ══ cluster ══ home ══ flux-system
               ║         ╠═════ gotk-components.yaml
               ║         ╠═════ gotk-sync.yaml
               ║         ╚═════ kustomization.yaml
               ╠══════ main-system
+              ║         ╠═════ automation.yaml
+              ║         ╚═════ secret.yaml
               ╠══════ app-name-1
               ║         ╠═════ deployment.yaml
               ║         ╠═════ secret.yaml
               ║         ╚═════ service.yaml
               ╚══════ app-name-2
                         ╠═════ deployment.yaml
                         ╠═════ secret.yaml
                         ╠═════ ingress.yaml
                         ╚═════ service.yaml
```
