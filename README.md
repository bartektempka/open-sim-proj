## Installing open-simulator

Clone this repository, e.g.
```bash
gh repo clone bartektempka/open-sim-proj
cd open-sim-proj
git submodule update --init
```

NOTE:
Here I also included a fork of hotelReservation form DeathStarBench repository with some modifications to make it work with the simulator. (added port protocols and added memory requests to pods)

Add open-simulator as submodule:

Build the project
```bash
cd open-simulator
make
```

test the installation by running the simulator:

```bash
make test
```

After testing installation return to open-sim-proj folder
```bash
cd ..
```

### First look
Then we can run the simulator
with
```bash
./open-simulator/bin/simon apply -i -f simon-config.yaml
```

We will see a prompt to choose the application we want to simulate.
Choose `hotelReservation` and then all nodes to report their status.
We get output like this:

```
Pod Info
master-1
Pod                                              | CPU Requests | Memory Requests | APP Name
kube-system/coredns-5p7d5l4v7x                   | 100m(5%)     | 70Mi(6%)        |         
kube-system/etcd-master-1                        | 100m(5%)     | 100Mi(9%)       |         
kube-system/kube-apiserver-master-1              | 250m(12%)    | 0(0%)           |         
kube-system/kube-controller-manager-master-1     | 200m(10%)    | 0(0%)           |         
kube-system/kube-proxy-master-7zdrxwpv2t         | 0(0%)        | 0(0%)           |         
kube-system/kube-scheduler-master-1              | 100m(5%)     | 0(0%)           |         
kube-system/metrics-server-95ldbzrg8n-twtpj49q9k | 1(50%)       | 500Mi(48%)      |         

master-2
Pod                                                  | CPU Requests | Memory Requests | APP Name        
default/mongodb-recommendation-bcl2qxdz5l-slfjkw6fkp | 100m(2%)     | 0(0%)           | hotelReservation
default/mongodb-reservation-6bnfld44tg-s2b79wzg9g    | 100m(2%)     | 0(0%)           | hotelReservation
default/mongodb-user-6zkvlr27w4-mwgqmr97v7           | 100m(2%)     | 0(0%)           | hotelReservation
kube-system/coredns-bg64x5rvdc                       | 100m(2%)     | 70Mi(6%)        |                 
kube-system/etcd-master-2                            | 100m(2%)     | 100Mi(9%)       |                 
kube-system/kube-apiserver-master-2                  | 250m(6%)     | 0(0%)           |                 
kube-system/kube-controller-manager-master-2         | 200m(5%)     | 0(0%)           |                 
kube-system/kube-proxy-master-227jv5h2ll             | 0(0%)        | 0(0%)           |                 
kube-system/kube-scheduler-master-2                  | 100m(2%)     | 0(0%)           |                 

master-3
Pod                                          | CPU Requests | Memory Requests | APP Name        
default/geo-84gbwxhrvr-htwdbqlp2t            | 100m(2%)     | 256Mi(25%)      | hotelReservation
default/reservation-v95snlwbrg-cpbrztl59r    | 100m(2%)     | 0(0%)           | hotelReservation
default/user-62cphsws6v-rjsvww46c6           | 100m(2%)     | 0(0%)           | hotelReservation
kube-system/coredns-j96g2dwlbd               | 100m(2%)     | 70Mi(6%)        |                 
kube-system/etcd-master-3                    | 100m(2%)     | 100Mi(9%)       |                 
kube-system/kube-apiserver-master-3          | 250m(6%)     | 0(0%)           |                 
kube-system/kube-controller-manager-master-3 | 200m(5%)     | 0(0%)           |                 
kube-system/kube-proxy-master-vd8ldwqmk2     | 0(0%)        | 0(0%)           |                 
kube-system/kube-scheduler-master-3          | 100m(2%)     | 0(0%)           |                 

worker-fast
Pod                                             | CPU Requests | Memory Requests | APP Name        
default/jaeger-ngvkb52w5k-jq2rmvzw8m            | 100m(2%)     | 0(0%)           | hotelReservation
default/memcached-profile-mzz5jr6wt2-jtkxj86nnt | 100m(2%)     | 0(0%)           | hotelReservation
default/memcached-rate-c7frn7pnzj-v87hv4xlfx    | 100m(2%)     | 0(0%)           | hotelReservation
default/memcached-reserve-bf6tjrks64-hcs7qxn72q | 100m(2%)     | 0(0%)           | hotelReservation
default/mongodb-geo-6bwtlpnqs5-6z2qzhnmq2       | 100m(2%)     | 1Gi(50%)        | hotelReservation
default/mongodb-profile-2lzwqxxdz8-lxjzktbct8   | 100m(2%)     | 0(0%)           | hotelReservation
default/mongodb-rate-s525l92qrl-m989g84gf8      | 100m(2%)     | 0(0%)           | hotelReservation
default/profile-qmkpttj767-pqv295fwm5           | 100m(2%)     | 0(0%)           | hotelReservation
default/rate-ltszvg6fvh-8j2qz9rz58              | 100m(2%)     | 0(0%)           | hotelReservation
default/recommendation-npzr6rr6p2-g4dxc6kbrq    | 100m(2%)     | 0(0%)           | hotelReservation
default/search-gs7sjp2l8x-654k4p5kcd            | 100m(2%)     | 0(0%)           | hotelReservation
kube-system/kube-proxy-worker-gcnw7744w9        | 0(0%)        | 0(0%)           |                 

worker-slow
Pod                                      | CPU Requests | Memory Requests | APP Name        
default/consul-dhl6tbqfkr-mjd7ph52kn     | 100m(50%)    | 0(0%)           | hotelReservation
default/frontend-q2dg4btzc6-x99pt797z9   | 100m(50%)    | 256Mi(51%)      | hotelReservation
kube-system/kube-proxy-worker-6twmqrnmr7 | 0(0%)        | 0(0%)           |        
```
It tells us that our app will work on our cluster and how much resources it will use.

### More Intensive App
Let's try to an app that uses more resources then the cluster has.

We run the simulator with the same command as before:
```bash
./open-simulator/bin/simon apply -i -f simon-config.yaml
```
and choose `hotelReservation-memoryIntensive` application.
We will get a prompt that says that the application is too intensive for the cluster and it will not be able to run.

```
? there are still 13 pod(s) that can not be scheduled when add 0 nodes, you can:
```

We can then choose to add more nodes specified in newNode directory.

Lets choose `add node(s)` and then add `1` node.

Now the simulator will add a new node to the cluster and try to run the application again.
Let's choose all nodes to report their status.
We will get output like this:

```
Pod Info
master-1
Pod                                              | CPU Requests | Memory Requests | APP Name
kube-system/coredns-mmzgtxzs95                   | 100m(5%)     | 70Mi(6%)        |         
kube-system/etcd-master-1                        | 100m(5%)     | 100Mi(9%)       |         
kube-system/kube-apiserver-master-1              | 250m(12%)    | 0(0%)           |         
kube-system/kube-controller-manager-master-1     | 200m(10%)    | 0(0%)           |         
kube-system/kube-proxy-master-c5hv5x84x5         | 0(0%)        | 0(0%)           |         
kube-system/kube-scheduler-master-1              | 100m(5%)     | 0(0%)           |         
kube-system/metrics-server-vdrz8frrwz-kr7s59rk68 | 1(50%)       | 500Mi(48%)      |         

master-2
Pod                                          | CPU Requests | Memory Requests | APP Name                        
default/consul-h6pm8zwkrc-n48mhtzb4j         | 100m(2%)     | 512Mi(50%)      | hotelReservation-memoryIntensive
kube-system/coredns-ck82kgk28k               | 100m(2%)     | 70Mi(6%)        |                                 
kube-system/etcd-master-2                    | 100m(2%)     | 100Mi(9%)       |                                 
kube-system/kube-apiserver-master-2          | 250m(6%)     | 0(0%)           |                                 
kube-system/kube-controller-manager-master-2 | 200m(5%)     | 0(0%)           |                                 
kube-system/kube-proxy-master-ggmb48ldhb     | 0(0%)        | 0(0%)           |                                 
kube-system/kube-scheduler-master-2          | 100m(2%)     | 0(0%)           |                                 

master-3
Pod                                          | CPU Requests | Memory Requests | APP Name                        
default/frontend-vqrc9vfc88-dxprp5zw4n       | 100m(2%)     | 512Mi(50%)      | hotelReservation-memoryIntensive
kube-system/coredns-b648hzx5cm               | 100m(2%)     | 70Mi(6%)        |                                 
kube-system/etcd-master-3                    | 100m(2%)     | 100Mi(9%)       |                                 
kube-system/kube-apiserver-master-3          | 250m(6%)     | 0(0%)           |                                 
kube-system/kube-controller-manager-master-3 | 200m(5%)     | 0(0%)           |                                 
kube-system/kube-proxy-master-slkxcwpn98     | 0(0%)        | 0(0%)           |                                 
kube-system/kube-scheduler-master-3          | 100m(2%)     | 0(0%)           |                                 

simon-g8zcj
Pod                                                  | CPU Requests | Memory Requests | APP Name                        
default/memcached-rate-69kwlv2f4z-qxncctsk7j         | 100m(2%)     | 512Mi(6%)       | hotelReservation-memoryIntensive
default/memcached-reserve-nv5jsj82xp-6f6fx8j26t      | 100m(2%)     | 512Mi(6%)       | hotelReservation-memoryIntensive
default/mongodb-profile-fbn7dj6lfl-547cbb7vx4        | 100m(2%)     | 512Mi(6%)       | hotelReservation-memoryIntensive
default/mongodb-rate-4wnf7bxtpr-tprq8lt2t8           | 100m(2%)     | 512Mi(6%)       | hotelReservation-memoryIntensive
default/mongodb-recommendation-jmz4sw698k-vnhh9tjrbc | 100m(2%)     | 512Mi(6%)       | hotelReservation-memoryIntensive
default/mongodb-reservation-r7dq82stft-wtp9v89nnz    | 100m(2%)     | 512Mi(6%)       | hotelReservation-memoryIntensive
default/mongodb-user-76gbljjxr8-shtw4m47ck           | 100m(2%)     | 512Mi(6%)       | hotelReservation-memoryIntensive
default/profile-8qxp9wwx6h-xhkrpxf9qj                | 100m(2%)     | 512Mi(6%)       | hotelReservation-memoryIntensive
default/rate-x7jsrc768p-r55pzdnzjq                   | 100m(2%)     | 512Mi(6%)       | hotelReservation-memoryIntensive
default/recommendation-5xd2rw56f5-5j2p2kmrmb         | 100m(2%)     | 512Mi(6%)       | hotelReservation-memoryIntensive
default/reservation-rwwvzgbvm9-ptzfhsgk8k            | 100m(2%)     | 512Mi(6%)       | hotelReservation-memoryIntensive
default/search-bjlxfxjm74-95wxbx67gb                 | 100m(2%)     | 512Mi(6%)       | hotelReservation-memoryIntensive
default/user-plcw7p7snz-rb649g75ck                   | 100m(2%)     | 512Mi(6%)       | hotelReservation-memoryIntensive
kube-system/kube-proxy-worker-xn245vjfd9             | 0(0%)        | 0(0%)           |                                 

worker-fast
Pod                                             | CPU Requests | Memory Requests | APP Name                        
default/geo-lfwmqrhprm-fmqz7ttwfb               | 100m(2%)     | 512Mi(25%)      | hotelReservation-memoryIntensive
default/jaeger-bjkcbdtzbt-kvnpbcmghz            | 100m(2%)     | 512Mi(25%)      | hotelReservation-memoryIntensive
default/memcached-profile-xswhj2f4t9-krqxsg5dzm | 100m(2%)     | 512Mi(25%)      | hotelReservation-memoryIntensive
default/mongodb-geo-6lxjvmhkgf-t664m9544b       | 100m(2%)     | 512Mi(25%)      | hotelReservation-memoryIntensive
kube-system/kube-proxy-worker-k25drk84f4        | 0(0%)        | 0(0%)           |                                 

worker-slow
Pod                                      | CPU Requests | Memory Requests | APP Name
kube-system/kube-proxy-worker-jx55gdqd8q | 0(0%)        | 0(0%)           |       §
```

As we see a lot of pods are running on the much stronger new node.

Here we test the deployment mostly based on memory usage but we can also add the affinity rules, more resource requests and limits to the pods to make the simulation more realistic.

### Replicate an existing cluster
We can modify simon-config.yaml to replicate an existing cluster by adding path to kubeconfig file.

```yaml
apiVersion: simon/v1alpha1
kind: Config
metadata:
  name: simon-config
spec:
  cluster:
    kubeConfig: /root/.kube/config
```

We can then run the simulator with the same command as before:
```bash
./open-simulator/bin/simon apply -i -f simon-config.yaml
```
This will create a cluster that is identical to the one in the kubeconfig file.

### Simulating Deploying Applications:
We can also simulate deploying applications to the running cluster.
But I didn't manage to make it work tried it with aws and kind clusters.

