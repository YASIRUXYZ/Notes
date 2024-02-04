> [!CAUTION]  
> flux 127.0.0.1:8080: connect: connection refused

1. give kubernetes access to flux ↓
```
mkdir ~/.kube
sudo k3s kubectl config view --raw | tee ~/.kube/config
chmod +x ~/.kube/config
```

2. check Flux_V2 ready to deploy in kubernetes ↓
```
flux check --pre
```