# utiliser docker avec le vpn (ipsec)

le principe est de configurer le source nat pour envoyer les packets de docker vers le vpn :

```
sudo iptables -j SNAT -t nat -I POSTROUTING 1 -o <vpn_link> -d 0.0.0.0/0 -s <docker_fixed_cidr> --to-source <ipsec_vpn_ip>
```

voir les links :

```
ip link
```

exemple de résultat (le link utilisé pour se connecter au vpn, ex ici enp0s31f6, correspond à <vpn_link>) :
Il convient de choisir le bon nom du lien dans la liste ci dessous. Pour connaitre ce dernier, il faut aller dans
`param > interface connecté (filaire ou wifi) > onglet identité > la fin de l'adresse MAC il y a le nom du link`

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp0s31f6: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1400 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
link/ether 28:f1:0e:28:17:ee brd ff:ff:ff:ff:ff:ff
3: wlp1s0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT group default qlen 1000
link/ether e4:a4:71:43:36:b8 brd ff:ff:ff:ff:ff:ff
4: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN mode DEFAULT group default
link/ether 02:42:8e:7e:e5:88 brd ff:ff:ff:ff:ff:ff
```

Pour voir les ip de la patte de sortie (avec le link utilisé pour se connecter au vpn en paramètre), ex :

```
ip addr show dev enp0s31f6 => nom du lien
```

exemple de résultat, la deuxième ipv4 en 10.x.x.x est la valeur de <ipsec*vpn_ip> :
*(10.x.x.x c'est l'ip renseigné pour le vpn)\_

```
2: enp0s31f6: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1400 qdisc fq_codel state UP group default qlen 1000
link/ether 28:f1:0e:28:17:ee brd ff:ff:ff:ff:ff:ff
inet 192.168.1.20/24 brd 192.168.1.255 scope global dynamic noprefixroute enp0s31f6
valid_lft 37698sec preferred_lft 37698sec
inet 10.0.1.143/32 scope global enp0s31f6
valid_lft forever preferred_lft forever
inet6 2a01:e0a:212:74c0:a945:c35f:dee2:63d/64 scope global temporary dynamic
valid_lft 86179sec preferred_lft 80702sec
inet6 2a01:e0a:212:74c0:ecbb:9022:b5e9:e9f2/64 scope global dynamic mngtmpaddr noprefixroute
valid_lft 86179sec preferred_lft 86179sec
inet6 fe80::cc1:2f24:ebcf:9306/64 scope link noprefixroute
valid_lft forever preferred_lft forever
```

pour voir les adresses ip de docker :

```
docker network inspect bridge
```

contenu exemple, il faut retenir la valeur IPAM.Config.Subnet pour la valeur <docker_fixed_cidr> :

```
[
    {
    "Name": "bridge",
    "Id": "0cfdb9a1136cd868783907701bc0a80066f87d62bce63cdf96ee861bdf6398c1",
    "Created": "2020-03-26T08:51:38.268961821+01:00",
    "Scope": "local",
    "Driver": "bridge",
    "EnableIPv6": false,
    "IPAM": {
        "Driver": "default",
        "Options": null,
        "Config": [
            {
            "Subnet": "192.168.100.0/24",
            "Gateway": "192.168.100.254"
            }
        ]
    },
    "Internal": false,
    "Attachable": false,
    "Ingress": false,
    "ConfigFrom": {
        "Network": ""
    },
    "ConfigOnly": false,
    "Containers": {},
    "Options": {
        "com.docker.network.bridge.default_bridge": "true",
        "com.docker.network.bridge.enable_icc": "true",
        "com.docker.network.bridge.enable_ip_masquerade": "true",
        "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
        "com.docker.network.bridge.name": "docker0",
        "com.docker.network.driver.mtu": "1400"
    },
    "Labels": {}
    }
]
```

dans notre exemple, le snat sera :

```
sudo iptables -j SNAT -t nat -I POSTROUTING 1 -o enp0s31f6 -d 0.0.0.0/0 -s 192.168.100.0/24 --to-source 10.0.1.143
```

Pour tester on peut faire

```
curl -I https://rundeck.tesfesses.io
```
