### CoreOS Fleet
This is a heat template that can be used to start up a three node CoreOS cluster using etcd autodiscovery to establish the etcd cluster across the nodes.  The only parameter required is the discovery URL.

### Usage
1.  Launch your cluster:
```
$ DISCOVERY_URL=$(curl -s https://discovery.etcd.io/new)
$ heat stack-create -f coreos_fleet.template --parameters="discovery_url=$DISCOVERY_URL" coreos_fleet
```
2.  Verify etcd is working:
```
$ ETCD_PEER=$(heat output-show coreos_fleet coreos1_public_ip | sed -e 's/"//g')
$ etcdctl --peers ${ETCD_PEER}:4001 ls /
```

### Credits
I lifted the basic template straight from [Scott Lowe's gist repo](https://gist.github.com/lowescott/43ea98cf49ff91445d0f), with minor modifications.