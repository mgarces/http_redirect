# http_redirect
This is a simple NGINX container, that can be use to redirect port 80 to a URL on port 443, because AWS ALB does not support this on their side. It should be fairly simple for ALB to define a rule to redirect port 80 to 443 on AWS side, but no, it needs to hit downstream first. This is bad architecture, imho, but this is what we have for now.

## How to use
Edit docker-compose.yml and change *NGINX_PORT* and *NGINX_HOST* with your preferences.
Example:
```
NGINX_HOST=www.domain.com
NGINX_PORT=80
```

After this, run it with"
```
docker-compose up -d
```
Simple as that!

## Final steps
Just create 2 target groups on AWS Load Balancer, one that points to your redirect, and listen on port 80, and another, that listens on port 443 (with valid certificate), that points to your final destination (for example, some webapp running on port 8080).