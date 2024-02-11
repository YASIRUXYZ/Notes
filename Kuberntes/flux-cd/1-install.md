### ` Install Flux v2 on kubernetes ✅`

> [!note]  
> ## Install Flux v2 on kubernetes control plane : ↓↓↓

1. go to [Flux_V2](https://github.com/fluxcd/flux2/releases/) release page
2. copy [flux_2.2.2_linux_amd64.tar.gz](https://github.com/fluxcd/flux2/releases/download/v2.2.2/flux_2.2.2_linux_amd64.tar.gz) link
3. install flux on your control plane node (kuberntes installed vps) ↓

```diff
curl -o /tmp/flux.tar.gz -sLO https://github.com/fluxcd/flux2/releases/download/v2.2.2/flux_2.2.2_linux_amd64.tar.gz
/usr/local/bin/flux
tar -C /tmp/ -zxvf /tmp/flux.tar.gz
mv /tmp/flux /usr/local/bin/flux
chmod +x /usr/local/bin/flux
```
4. check Flux_V2 ready to deploy in kubernetes ↓
```
flux check --pre
```

> [!note]  
> ## Install Flux v2 on kubernetes cluster : ↓↓↓

### Well need to generate a [personal access token (PAT)](https://github.com/settings/personal-access-tokens/new) that can create repositories by checking all permissions uder the repo

1. bootstrap using this command on control plane (flux installed) ↓
#Before use command change this values in the command
```yaml
<YOUR_GITHUB_USERNAME> : your github username
<YOUR_GITHUB_CONTROL_REPO> : make new repository for run flux
<YOUR_MAIN_BRANCH> : change main branch or use "main" as by default
```
```md
flux bootstrap github \
  --components-extra=image-reflector-controller,image-automation-controller \
  --owner=<YOUR_GITHUB_USERNAME> \
  --token-auth \
  --repository=<YOUR_GITHUB_CONTROL_REPO> \
  --path=./clusters/home \
  --branch=<YOUR_MAIN_BRANCH> \
  --persona
```

2. get 1st pull from repo ` (Your code[NOT KUBERNETES]) `
   1) open your vscode (code editor)
   2) connect to your github repository(before you made for flux[YOUR_GITHUB_CONTROL_REPO]) 
   3) run pull command ` "git pull" `

> [!tip]
> check git repository file structure like this
```diff
 ══ cluster ══ home ══ flux-system
+                        ╠═════ gotk-components.yaml (auto)
+                        ╠═════ gotk-sync.yaml       (auto)
+                        ╚═════ kustomization.yaml   (auto)
``` 