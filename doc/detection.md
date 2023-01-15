# Detection


## Enable Deep Packet Inspection

Detect exploitation attempts by evaluating workload traffic against intrusion detection signatures.

Calico Cloud's Kubernetes native deep packet inspection allows us to choose the java-app workload and examine the traffic against Snort signatures.

Take a look.

```
apiVersion: projectcalico.org/v3
kind: DeepPacketInspection
metadata:
  name: java-app-dpi
  namespace: java-app
spec:
  selector: 'app == "java-app"'
```

Enable deep packet inspection for the vulnerable java-app workload.

```
kubectl apply -f workshop/dpi
```

## Enable eBPF based Container Threat Detection

Detect the presence of malicious files and processes in compromised workloads.

Turn on Container Threat Detection for your cluster nodes in the Calico Cloud web ui.  Yes, it's really that easy.

![intro](img/cc-enable-treat-detection.png)

In order to move quickly during the workshop, we will shorten the time interval for alerts to trigger by setting the period to 1 minute, instead of the default 15 minutes.

```
kubectl -n tigera-runtime-security annotate daemonset runtime-reporter unsupported.operator.tigera.io/ignore="true"
kubectl -n tigera-runtime-security get daemonset.apps/runtime-reporter -o yaml | sed 's/15m/1m/g' | kubectl apply -f -
```

## Dynamic Service and Threat Graph

Expose reconnaissance gathering and exploitation attempts. Observe data exfiltration of sensitive information leaving the cluster. 

Enable Application layer visibility and turn it on for our vulnerable `java-app`.

```
kubectl apply -f workshop/dsg
kubectl annotate svc java-app -n java-app projectcalico.org/l7-logging=true
```

Apply Global Alerts to enable signature-based anomaly detection.

```
kubectl apply -f workshop/alerts
```


```
kubectl patch felixconfiguration default --patch-file workshop/felix/felix.yaml
```

[Next -> Module 6](exploitation.md)
