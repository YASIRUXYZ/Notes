> [!info]  
> ## Deploy kubernetes deployment using flux: ↓↓↓
> 
> 1. Add basic deployment yaml
> ```
> add your own deployment
> ```
> 2. Create git repo flie structure like this 
 ```diff
  ══ cluster ══ home ══ flux-system
                ║         ╠═════ gotk-components.yaml
                ║         ╠═════ gotk-sync.yaml
                ║         ╚═════ kustomization.yaml
                ╠══════ app-name-1
 +              ║         ╠═════ deployment.yaml
 +              ║         ╠═════ secret.yaml
 +              ║         ╚═════ service.yaml
                ╚══════ app-name-2
 +                        ╠═════ deployment.yaml
 +                        ╠═════ secret.yaml
 +                        ╠═════ ingress.yaml
 +                        ╚═════ service.yaml
 ```