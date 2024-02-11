> [!info]  
> # Update Image Verison In Kubernetes Deployment Using Flux: ↓↓↓
>
> 1. Add ` image-registry.yaml ` To Uour App Folder
> #Before use command change this values in the command
> ```yaml
> <SET_IMAGEREPO_NAME> : make name for identified image tags
> <IMAGE_NAME> : docker image name (you can use ghcr.io)
> <DOCKER_ACCESS_NAME> : docker images access create name (before you created in automation setup process)
> ```
> ```md
> apiVersion: image.toolkit.fluxcd.io/v1beta2
> kind: ImageRepository
> metadata:
>   name: <SET_IMAGEREPO_NAME>
>   namespace: flux-system
> spec:
>   image: <IMAGE_NAME>
>   interval: 1m0s
>   secretRef:
>     name: <DOCKER_ACCESS_NAME>
> ```
> 
> 2. Add ` image-policy.yaml ` To Uour App Folder
> #Before use command change this values in the command
> ```yaml
> <SET_IMAGEPOLICY_NAME> : crate name for identified for image policy
> <SET_IMAGEREPO_NAME> : before your crated (for identified image tags)
> <VERSION_RANGE_START> : set check version range start (default 0.0.0)
> <VERSION_RANGE_END> : set check version range end (default 99999.99.99)
> ```
> ```md
> apiVersion: image.toolkit.fluxcd.io/v1beta2
> kind: ImagePolicy
> metadata:
>   name: <SET_IMAGEPOLICY_NAME>
>   namespace: flux-system
> spec:
>   imageRepositoryRef:
>     name: <SET_IMAGEREPO_NAME>
>   policy:
>     semver:
>       range: ">= <VERSION_RANGE_START> < <VERSION_RANGE_END>"
> ```
> 
> 3. Add auto update tag to your **` developent.yaml `**
> #Before use change this values
> ```yaml
> <ADD_CUSTOM_VERSION> : add image version (default 0.0.0)
> <IMAGE_NAME> : docker image name (you can use ghcr.io)
> <SET_IMAGEPOLICY_NAME> : before you crated image policy name
> ```
> ### {"$imagepolicy": "flux-system:<SET_IMAGEPOLICY_NAME>"}
> ```md
> containers:
>     - name: CONTAINER NAME
>       image: <IMAGE_NAME>:<ADD_CUSTOM_VERSION> # {"$imagepolicy": "flux-system:<SET_IMAGEPOLICY_NAME>"}
>       imagePullPolicy: Always
> ```
>
> 4. Make new git repo flie structure like this
```diff
 ══ cluster ══ home ══ flux-system
               ║         ╠═════ gotk-components.yaml
               ║         ╠═════ gotk-sync.yaml
               ║         ╚═════ kustomization.yaml
               ╠══════ main-system
               ║         ╠═════ automation.yaml
               ║         ╚═════ secret.yaml
               ╠══════ app-name-1
               ║         ╠═════ deployment.yaml
               ║         ╠═════ secret.yaml
               ║         ╚═════ service.yaml
+              ║         ╠═════ image-registry.yaml
+              ║         ╚═════ image-policy.yaml
               ╚══════ app-name-2
                         ╠═════ deployment.yaml
                         ╠═════ secret.yaml
                         ╠═════ ingress.yaml
                         ╚═════ service.yaml
+                        ╠═════ image-registry.yaml
+                        ╚═════ image-policy.yaml

```