shadowsocksr_for_docker
==========

Docker Images of ShadowsocksR From CentOS-7 7.3.1611 x86_64;

Support net-speeder, supervisor;

No Secure in connection-limit bandwidth-limit ban-cracker !!!;

Run shadowsocks service for 1 instance;

Default rand password;

Options -p -k -m -O -o for service;

Option value -p=1949 -k=${rand and output in docker log} -m=aes-256-cfb \
-O auth_aes128_sha1 -o http_simple_compatible;

Option Method are none aes-256-cfb aes-256-ctr camellia-256-cfb and 128/192 size;

Option Protocol are origin auth_aes128_sha1 auth_aes128_md5 auth_chain_a;

Origin Protocol Param is client numbers online;

Option Protocol Param is not support by command line;

Option Protocol compatible is bug;

Option Obfs are plain http_simple(param is host list) http_simple_compatible \
tls1.2_ticket_auth(param is time diff) tls1.2_ticket_auth_compatible;

Option Obfs Param is not support by command line;

Default with -qq --fast-open -s=0.0.0.0 -t=300 --user=nobody;

Dont support speed_limit_per_con speed_limit_per_user in config;

Dont support additional_ports additional_ports_only in config;

Dont support udp_timeout dns_ipv6 connect_verbose_info redirect in config;

Dont support multiport or user;

Dont support config manager-address forbidden-ip workers;

Dont support pid log verbose-mode;

Dont support kcptun finalspeed;

Dont support bbr;

Dont support ipv6;

Not shadowsocks dont support aes-256-gcm chacha20-ietf-poly1305;

Not libev dont support redirectmode tunnelmode;

No Optimizing in Docker without DockerHosting support include fast-open;

DockerHub: https://hub.docker.com/r/ssorg/shadowsocksr_for_docker/

Github: https://github.com/ssaz/shadowsocksr_for_docker

## Example (For Docker Hostings)

Make sure that Port and ENV SSR_PORT are the same

```
Image: ssorg/shadowsocksr_for_docker
Instance: 1
Port: 1949 tcp
ENV: SSR_PORT 1949
ENV: SSR_PASSWORD $(PasswordYouWant)
ENV: SSR_METHOD aes-256-ctr
ENV: SSR_PROTOCOL auth_aes128_sha1
ENV: SSR_OBFS http_simple_compatible
```

then docker hosting will -P a rand port and generate a rand host for the container

## Example (Best Practice)

```
docker run -d -p 19490:1949 ssorg/shadowsocksr_for_docker | cut -c 1-12 | xargs docker logs -f
```

then docker log print port, password and method.
```
----- ----- ----- ----- -----
----- ----- ----- ----- -----
----- ----- ----- ----- -----
ssr port: 1949
ssr password: XXXXXXXXXXXXXXXX
ssr method: aes-256-cfb
ssr protocol: auth_aes128_sha1
ssr obfs: http_simple_compatible
----- ----- ----- ----- -----
----- ----- ----- ----- -----
----- ----- ----- ----- -----
net-speeder eth0 [enabled]
----- ----- ----- ----- -----
...
----- ----- ----- ----- -----
----- ----- ----- ----- -----
----- ----- ----- ----- -----
```

## Example custom port

Make sure that -e ${SSR_PORT} and -p :${SSR_PORT} are the same, 
example -e 'SSR_PORT=123' -d -p XXXXX:123

```
docker run -e 'SSR_PORT=22' -d -p 2222:22 ssorg/shadowsocksr_for_docker
```

## Example custom port and password

```
docker run -e 'SSR_PORT=8080' -e 'SSR_PASSWORD=Passw0rd' \
-d -p 12345:8080 ssorg/shadowsocksr_for_docker
```

## Example custom method

```
docker run -e 'SSR_METHOD=aes-256-ctr' -d -p 12345:22 ssorg/shadowsocksr_for_docker
```

## Example Full params

```
docker run -e 'SSR_PORT=1949' -e 'SSR_PASSWORD=Passw0rd' -e 'SSR_METHOD=aes-256-ctr' \
-e 'SSR_PROTOCOL=auth_aes128_sha1' -e 'SSR_OBFS=http_simple_compatible' \
-d -p 19999:1949 ssorg/shadowsocksr_for_docker | cut -c 1-12 | xargs docker logs -f
```

## Example Disable net-speeder

```
docker run -e 'NS_OFF=true' -d -p 19490:1949 \
ssorg/shadowsocksr_for_docker | cut -c 1-12 | xargs docker logs -f
```

## Example change net-speeder device

then docker log print ip a result, pick the device.

```
docker run -e 'NS_DEVICE=eth0' -d -p 19490:1949 \
ssorg/shadowsocksr_for_docker | cut -c 1-12 | xargs docker logs -f
```

## Tips

slow since QoS, change port to 80 25 443 995 3389

-END-
