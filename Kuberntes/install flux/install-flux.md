***Install Flux v2 on kubernetes***

> [!note]  
> Install Flux v2 on kubernetes control plane ↓

1. go to [Flux_V2](https://github.com/fluxcd/flux2/releases/) release page
2. copy [flux_2.2.2_linux_amd64.tar.gz](https://github.com/fluxcd/flux2/releases/download/v2.2.2/flux_2.2.2_linux_amd64.tar.gz) link
3. install flux on your control plane node ↓

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
> Install Flux v2 on kubernetes cluster ↓
