# Attacking Kubernetes (A work in progress)

### A field guide for cloud ninjas and red teams
![image](https://user-images.githubusercontent.com/24460340/169073810-c0a06695-2f0f-492d-8283-a129b8e9ab3c.png)
 
### Note: 
sorry this is sort of a dump of notes at the moment. Hopefully I will organize this eventually.

Disclaimer: Use these tips only on clusters you are authorized to be infiltrating.

## Recon
- kubernetes ports (official documentation) https://kubernetes.io/docs/reference/ports-and-protocols/
- run kubolt to find public unauthenticated kubernetes clusters https://github.com/averonesis/kubolt
  - follow up with recon using `kubehunter --remote 192.168.0.0` 
- manually enumerate for unauthenticated access to kubelet api
  - `port 10255` (old) and `port 10250` is the https kubelet api
  - `https://NODE_IP:10250/pods`
  - `https://NODE_IP:10250/spec` 
  - `https://NODE_IP:10250/exec`

## Initial Foothold
- Typosquatting
  - Create a malicious image in a public container registry with a name similar to a real image. The backdoor planted in your malicious image will allow you a foothold in the container
- stolen service account credentials

## Enumeration (inside pod)
- `env | grep KUBE`
  - this should expose IP's and service ports    
- is there a service account token mounted in this pod?
  - run `kubectl auth can-i --list`
  - check in `/var/run/secrets/kubernetes.io/serviceaccount/token`
- "i have a service account token... what next"
  - `curl https://kubernetes.default/api/v1/namespaces/default/pods/ --header "Authorization: Bearer ${TOKEN}" --insecure`
  - `kubectl --token="$(<${DIR}/token)" --certificate-authority="${DIR}/ca.crt" get pods`
  - `kubectl --token="$(<${DIR}/token)" --insecure-skip-tls-verify get pods`
  - `kubectl --token="$(<${DIR}/token)" -k get buckets ack-test-smoke-s3 -o yaml` 
  - source: "Hacking Kubernetes" page 181
- enumerate DNS to find IP's and Domains associated with the cluster
  - `openssl s_client -connect kubernetes.default:443 \
  < /dev/null 2>/dev/null |
  openssl x509 -noout -text | grep -E "DNS:|IP Address:"`
  - source: "Hacking Kubernetes" page 183 
- check for dangerous default settings
  - (cloud) can this pod access cloud resources? 
  - is there no security context present? (dangerous default)
  - can this pod see and talk to every other pod on the cluster? (dangerous default)
  - can this pod query host and pod metadata via environment variables? (dangerous default)
  - is network traffic between pods unencrypted? (dangerous default) 
- enumerate the mounted volumes in the `/mnt/foo` directory for useful information  
- api access?
 - kube-api is where secrets live. Query the API for secrets!
 
## Container Escape 

## Privilege Escalation

## Establish Persistence

### Sources 
- "Hacking Kubernetes: Threat Driven Analysis and defense" by Andew Martin and Michael Hausenblas
- https://book.hacktricks.xyz/cloud-security/pentesting-kubernetes/
