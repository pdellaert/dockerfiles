BIRD container
==============

This image is based on the [Alpine](https://hub.docker.com/_/alpine/) Edge image and deploys the latest available [BIRD](https://bird.network.cz/) package in the [Alpine edge testing repositories](https://pkgs.alpinelinux.org/package/edge/testing/x86/bird).

It `EXPOSE`s port `179` for use with BGP specifically, but could be extended to support other protocols as well. 

You will have to provide a path to a folder with the `bird.conf` file, which has to be mounted on container creation in `/etc/bird`. 

Usage
-----

Create a folder and create a `bird.conf` file in it, and add a proper BIRD configuration in it.

```
$ mkdir bird
$ vim bird/bird.conf
```

Next, start run the image:

```
docker run -d -v `pwd`/bird:/etc/bird:rw --name bird pdellaert/bird:latest
```

You can check the status using `docker logs`:

```
$ docker logs bird
bird: device1: Initializing
bird: static1: Channel ipv4 connected to table master4
bird: static1: Initializing
bird: bgp1: Channel ipv4 connected to table master4
bird: bgp1: Initializing
bird: device1: Starting
bird: device1: Scanning interfaces
bird: device1: State changed to up
bird: Chosen router ID 192.168.99.10 according to interface eth0
bird: static1: Starting
bird: static1: State changed to up 
```

You can also use the `birdcl` CLI to execute more complex inspections:
```
$ docker exec -it bird birdcl
BIRD 2.0.2 ready.
bird> show status
BIRD 2.0.2
Router ID is 192.168.99.10
Current server time is 2018-09-02 00:42:06.283
Last reboot on 2018-09-02 00:37:22.665
Last reconfiguration on 2018-09-02 00:37:22.665
Daemon is up and running
bird> show protocols
Name       Proto      Table      State  Since         Info
device1    Device     ---        up     00:37:22.665
static1    Static     master4    up     00:37:22.665
bgp1       BGP        ---        up     00:37:26.481  Established
```

Acknowledgments
---------------

Thanks to [pierky](https://hub.docker.com/r/pierky/bird/) for his initial version of the BIRD image. 

Author
------

Philippe Dellaert - https://dellaert.org - [@pdellaert](https://twitter.com/pdellaert)

