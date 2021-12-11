## Reason

I'm using nginx as daemonset, rather than kubernetes ingress, along with Let's Encrypt as SSL. One issue I face is the renewal of the certificate every 3 months.

## Solution

Another certbot auto updater script. Only differnce is this is a complete package. You can just change few variables, apply to your cluster, and forget about SSL.

## How to use
1. open certbot-autoupdater.yaml
2. Change following variables 
  - `DOMAIN` Change the value it to your domain name. For example, dev.myorg.com.
  - `EMAIL` Change the value it to which email address you want SSL related news should come to.
  - `ingress-cert` Change it to your ssl secret name in kuberentes. For example it can be `nginx-certificate` or so.
  - If you created the certificate using `kubectl crete secret --type ..` the key will be `tls.key` and `tls.crt`. If that's different, please search and change that too. Refer line number 62 and 63
3. Apply the configuration
  - Note: This app should be running on the same namespace as your nginx deployment/daemonset.
  - `kubectl apply -f certbot-autoupdater.yaml -n <namespace of nginx deployment>`
