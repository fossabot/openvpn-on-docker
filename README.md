[![Build Status](https://travis-ci.org/OlegGorj/openvpn-on-docker.svg?branch=master)](https://travis-ci.org/OlegGorj/openvpn-on-docker)
[![GitHub Issues](https://img.shields.io/github/issues/OlegGorJ/openvpn-on-docker.svg)](https://github.com/OlegGorJ/openvpn-on-docker/issues)
[![Average time to resolve an issue](http://isitmaintained.com/badge/resolution/OlegGorJ/openvpn-on-docker.svg)](http://isitmaintained.com/project/OlegGorJ/openvpn-on-docker "Average time to resolve an issue")
[![Percentage of issues still open](http://isitmaintained.com/badge/open/OlegGorJ/openvpn-on-docker.svg)](http://isitmaintained.com/project/OlegGorJ/openvpn-on-docker "Percentage of issues still open")
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FOlegGorj%2Fopenvpn-on-docker.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2FOlegGorj%2Fopenvpn-on-docker?ref=badge_shield)

# OpenVPN on docker container

Implementation of OpenVPN on Docker container

To setup VPN clients, generate VPN client credentials for `CLIENTNAME` without password protection; leave 'nopass' out to enter password.

```
ENDPOINT_SERVER=<external IP of bastion instance>
CLIENTNAME=openvpn

docker run --user=$(id -u) -e OVPN_CN=$ENDPOINT_SERVER  -e OVPN_SERVER_URL=tcp://$ENDPOINT_SERVER:1194 -i -v $PWD:/etc/openvpn oleggorj/openvpn ovpn_initpki nopass $ENDPOINT_SERVER

docker run --user=$(id -u) -v $PWD:/etc/openvpn -ti oleggorj/openvpn easyrsa build-client-full $CLIENTNAME nopass
```

To generate `ovpn` file:

```
docker run --user=$(id -u) -e OVPN_DEFROUTE=1 -e OVPN_SERVER_URL=tcp://$INGRESS_IP_ADDRESS:80 -v $PWD:/etc/openvpn --rm oleggorj/openvpn ovpn_getclient $CLIENTNAME > ${CLIENTNAME}.ovpn
```


## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FOlegGorj%2Fopenvpn-on-docker.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2FOlegGorj%2Fopenvpn-on-docker?ref=badge_large)