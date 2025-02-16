## 本地解锁使用 DNS - UNLOCK

### 方法一  使用代理软件

​	首先讲一讲普遍使用的Clash系列软件和V2ray系列软件,这些软件有着大量的适用群体!

#### V2ray :

​	第一步我们需要找到DNS设置我们需要将一下配置填入配置项中

```json
{
  "hosts": {
    "{需要解锁的域名1}": "{您获取的服务器地址1}",
    "{需要解锁的域名2}": "{您获取的服务器地址1}",
    "{需要解锁的域名3}": "{您获取的服务器地址2}"
  },
  "servers": [
    {
      "address": "1.1.1.1",
      "domains": [
        "geosite:geolocation-!cn"
      ],
      "expectIPs": [
        "geoip:!cn"
      ]
    },
    {
      "address": "223.5.5.5",
      "domains": [
        "geosite:cn"
      ],
      "expectIPs": [
        "geoip:cn"
      ]
    },
    "8.8.8.8",
    "https://dns.google/dns-query"
  ]
}
```

​	第二步需要将您需要解锁的域名加入直连名单,打开路由设置并添加路由集,添加您需要解锁的域名改为直连模式.然后开启代理.

#### Clash :

​	clash较为简单 直接一部到位,在全局扩展配置中填入即可

```
hosts:
  需要解锁的域名1: 您获取的服务器地址1
  需要解锁的域名2: 您获取的服务器地址1
  需要解锁的域名3: 您获取的服务器地址2
```

### 方法二  重写本地HOST 
直接编写本地host 或者使用[switchhosts](https://switchhosts.vercel.app/zh) 来编写,推荐第二种比较适合不熟悉电脑的用户

### 方法三  搭建本地DNS服务
使用适合系统的adguard Home Acrylic 等的软件搭配使用

