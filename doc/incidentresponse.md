# Incident Response

## Containment

Isolating intruder elements by quarantining the source of the attacks.

```
kubectl label pod -n attack -l app=attack "quarantine=true" --overwrite
```

## Evidence Collection

Collect the flow, dns, http, and alert event logs and other relevent evidnce. 



**Congratulations! You have finished all the labs in the workshop.**



>Follow the cleanup instructions on the [main page](https://github.com/tigera-solutions/detect-and-mitigate-container-based-threats#workshop-modules) if needed.
