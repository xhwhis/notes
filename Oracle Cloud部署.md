Oracle Cloud部署

arm上部署情qinglong、vaultwarden、caddy、v2ray

amd64上部署focalboard、appflowy、caddy（暂定）



安装podman

```sh
dnf install -y podman
```



安装qinglong、vaultwarden

```sh
mkdir ql
podman run -d --privileged --name qinglong -v $PWD/ql:/ql/data -p 5700:5700 --restart always docker.io/whyour/qinglong:latest
```

```sh
mkdir vw
podman run -d --privileged --name vaultwarden -v $PWD/vw/:/data/:Z -e ROCKET_PORT=8080 -p 8080:8080 --restart always docker.io/vaultwarden/server:latest
```

```sh
mkdir maiark
podman run -d --privileged --name maiark -v $PWD/maiark:/MaiARK -p 8082:8082 --restart always docker.io/kissyouhunter/maiark:latest
```



安装caddy

```sh
dnf install 'dnf-command(copr)'
dnf copr enable @caddy/caddy
dnf install -y caddy
```

firewall配置

```sh
firewall-cmd --add-service=http --permanent
firewall-cmd --add-service=https --permanent
firewall-cmd --reload
```

Caddyfile

```
ql.whis.me {
	tls hi@whis.me
	encode gzip
	reverse_proxy :5700 {
		header_up X-Real-IP {remote_host}
	}
}

jd.whis.me {
	tls hi@whis.me
	encode gzip
	reverse_proxy :8082 {
		header_up X-Real-IP {remote_host}
	}
}

vw.whis.me {
	tls hi@whis.me
	encode gzip
	reverse_proxy :8080 {
		header_up X-Real-IP {remote_host}
	}
}
```

```sh
caddy fmt --overwrite /etc/caddy/Caddyfile
```

启动caddy

```sh
systemctl enable --now caddy.service
systemctl status caddy
```
