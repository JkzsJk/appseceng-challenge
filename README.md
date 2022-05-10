# Documentation for AppSecEng Challenge
The numbered list here corresponds to the 5 exercises listed in the AppSecEng challenge PDFs. They are the actions I have taken to POC on my end (or would have done but didn't manage to) to fulfil the requirements.
1. Installed/using [`duckdns-go` Helm Chart](https://artifacthub.io/packages/helm/ebrianne/duckdns-go) created/maintained by [Eldwan Brianne](https://github.com/ebrianne).
  - ```bash
    helm upgrade --install install duckdns --namespace default --set duckdns.domains=jkzs --set duckdns.token=7c2db1a6-fb0b-4b11-a117-97f77a168d55 ebrianne/duckdns-go
    ```
    - For refreshing/updating my machine's current public IP on DuckDNS
  - Installed/using Wordpress Helm Chart from [charts/bitnami/wordpress at master · bitnami/charts](https://github.com/bitnami/charts/tree/master/bitnami/wordpress/).
    - ```bash
      cd bitnami-wordpress
      helm upgrade --install bitnami-wordpress --set wordpressUsername=admin --set wordpressPassword=password --set mariadb.auth.rootPassword=secretpassword .
      ```
  - As for HTTPS and certificate, my go-to would be Let's Encrypt.
  - Would deploy a LoadBalancer to front my local K8s cluster, but unfortunately I ran out of credit to provision one via AWS.
2. Follow guidelines from `CIS_NGINX_Benchmark_v1.0.0.pdf` to enforce certain security policies, to name a few:
  - _Ensure NGINX only listens for network connections on authorized ports_
  - _Ensure access logging is enabled_
  - _Ensure HTTP is redirected to HTTPS_
  - _Ensure a trusted certificate and trust chain is installed_
  - _Ensure only modern TLS protocols are used_
  - Would apply the equivalent of these configurations in `bitnami-wordpress` Helm Chart ingress/NGINX section in the `values.yaml`.
3. Scan my code base (e.g. my Helm Charts) with SonarQube (could have locally host one to scan the repo), or using Harbor Claire to scan my Docker Images to be compliant with OWSAP.
4. Would prefer to use Cloudflare's DDOS protection, install Cloudflare's Wordpress plugin, create Cloudflare API token to integrate with my Wordpress site.
  - Downloaded `cloudflare-plugin/cloudflare.4.9.1.zip` from [Free DDoS protection for WordPress | Cloudflare UK](https://www.cloudflare.com/en-gb/integrations/wordpress/free-ddos-protection-wordpress/), uploaded & installed Cloudflare plugin onto Wordpress.

P.S. Reference screenshots are available in the `archive/` folder.