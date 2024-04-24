以下の方法で動かしました。

#### Vagrant

手元にansibleをインストールして`vagrant up`すればprovisioningが実行される。

benchからappのIPアドレスを指定して負荷をかける。

```shell
# appのIPアドレスを調べる
$ vagrant ssh app
$ ip a

3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:37:2b:2c brd ff:ff:ff:ff:ff:ff
    inet 172.28.128.6/24 brd 172.28.128.255 scope global dynamic enp0s8
       valid_lft 444sec preferred_lft 444sec
    inet6 fe80::a00:27ff:fe37:2b2c/64 scope link
       valid_lft forever preferred_lft forever

# benchで負荷をかける
$ vagrant ssh bench
$ sudo su - isucon
$ /home/isucon/private_isu.git/benchmarker/bin/benchmarker -u /home/isucon/private_isu.git/benchmarker/userdata -t http://172.28.128.6
```
####結果
```{"pass":false,"score":0,"success":0,"fail":8,"messages":["response code should be 200, got 502 (POST /login)","response code should be 200, got 502 (POST /register)"]}```
