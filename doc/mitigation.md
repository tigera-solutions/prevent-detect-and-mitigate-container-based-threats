# Mitigation

## Enable Workload-centric Web Application Firewall (WAF) 

The Workload-centric WAF will detect and block OWASP Top 10 and other attacks, allowing you to continue operating and giving you time to patch the vulnerability.

```
kubectl apply -f workshop/waf
```

```
kubectl patch applicationlayer tigera-secure --type='merge' -p '{"spec":{"webApplicationFirewall":"Enabled"}}'
```

## Enable Zerotrust Access Controls

Reduce the attack surface using the Security Policy Recommender to recommend a security policy to protect the vulnerable `java-app`.


[Next -> Module 8](incidentresponse.md)
