### 安装docker镜像
```
docker run \
    --name ipsec-vpn-server \
    --env-file /data/jump/vpn/vpn.env \
    --restart=always \
    -v ikev2-vpn-data:/etc/ipsec.d \
    -v /lib/modules:/lib/modules:ro \
    -p 500:500/udp \
    -p 4500:4500/udp \
    -d --privileged \
    hwdsl2/ipsec-vpn-server
```
/data/jump/vpn/vpn.env 内容
```
# te: All the variables to this image are optional.
# See README for more information.
# To use, uncomment and replace with your own values.

# Define IPsec PSK, VPN username and password
# - DO NOT put "" or '' around values, or add space around =
# - DO NOT use these special characters within values: \ " '
VPN_IPSEC_PSK=guigudxdserver
VPN_USER=delen
VPN_PASSWORD=dxd13145

# Define additional VPN users
# - DO NOT put "" or '' around values, or add space around =
# - DO NOT use these special characters within values: \ " '
# - Usernames and passwords must be separated by spaces
# VPN_ADDL_USERS=additional_username_1 additional_username_2
# VPN_ADDL_PASSWORDS=additional_password_1 additional_password_2

# Use a DNS name for the VPN server
# - The DNS name must be a fully qualified domain name (FQDN)
# VPN_DNS_NAME=vpn.example.com

# Specify a name for the first IKEv2 client
# - Use one word only, no special characters except '-' and '_'
# - The default is 'vpnclient' if not specified
# VPN_CLIENT_NAME=your_client_name

# Use alternative DNS servers
# - By default, clients are set to use Google Public DNS
# - Example below shows Cloudflare's DNS service
# VPN_DNS_SRV1=1.1.1.1
# VPN_DNS_SRV2=1.0.0.1

# Protect IKEv2 client config files using a password
# - By default, no password is required when importing IKEv2 client configuration
# - Uncomment if you want to protect these files using a random password
# VPN_PROTECT_CONFIG=yes
```

查看当前已建立的 VPN 连接

`docker exec -it ipsec-vpn-server ipsec whack --trafficstatus`
查看日志信息
`docker logs ipsec-vpn-server -f`
