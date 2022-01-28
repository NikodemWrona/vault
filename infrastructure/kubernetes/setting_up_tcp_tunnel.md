### Code snippets how to setup the TCP tunnel on k8s cluster to connect to services that are only accessible from inside the internal network

First I need a connection to *k8s* cluster via *kubectl*.

Then in first terminal window I need to create a *TCP tunnel*

```bash
kubectl run $PODNAME -n $NAMESPACE --image alpine/socat  --restart=Never --rm -it "TCP-LISTEN:$SERVICE_PORT,fork" "TCP-CONNECT:$SERVICE_URL:5432"
```

After that in other terminal window I need to *forward port* from *cluster* to my local machine through created pod

```bash
kubectl port-forward -n $NAMESPACE $PODNAME $LOCAL_PORT:$SERVICE_PORT
```
