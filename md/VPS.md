# 使用VPS 搭配 DNS - UNLOCK

相较于VPS 或者路由器之类的部署方式与其他方式要复杂的多

推荐适用 dnsmasq 和 AdGuard Home

## 1. 部署 DNS 服务器

### 方法一 使用 dnsmasq

#### 1.1 安装 dnsmasq

```bash
sudo apt install -y dnsmasq
```

#### 1.2 配置 dnsmasq

编辑 `/etc/dnsmasq.conf`，添加以下内容：

```ini
server=8.8.8.8
server=8.8.4.4
no-resolv
address=/example.com/IP
```

将 `example.com` 替换为需要解析的域名，`IP` 替换服务器ip。

#### 1.3 启动 dnsmasq

```bash
sudo systemctl enable dnsmasq
sudo systemctl restart dnsmasq
```

### 方法二使用AdGuard Home

### 2.1 安装 AdGuard Home

```
curl -sSL https://raw.githubusercontent.com/AdguardTeam/AdGuardHome/master/scripts/install.sh | sh
```

### 2.2 配置 AdGuard Home

启动 AdGuard Home 并进行初始设置：

```
sudo systemctl start AdGuardHome
sudo systemctl enable AdGuardHome
```

AdGuard Home 默认运行在 `http://YOUR_VPS_IP:3000`，打开浏览器访问该地址，按照向导进行配置。

### 2.3 配置自定义解析规则

在 AdGuard Home Web 界面中，进入 `DNS 设置`，添加以下内容到 `自定义解析`：

```
example.com IP
```

将 `example.com` 替换为需要解析的域名，`IP` 替换为你的VPS IP

### 3. 应用 SNI Proxy 与 DNS 解析

#### 3.1 设置本地 DNS 解析

在客户端设备上，将 DNS 服务器地址改为你的 VPS 地址。

#### 3.2 验证 DNS 解析

在本地执行：

```bash
dig example.com @IP
```

如果返回的是你的 VPS IP，则 DNS 配置成功。

#### 3.3 测试 SNI Proxy

在本地浏览器打开 `https://example.com`，如果能够访问，说明 SNI Proxy 工作正常。

### 4 .配置防火墙

```bash
sudo ufw allow 53/tcp
sudo ufw allow 53/udp
sudo ufw allow 443/tcp
sudo ufw allow 80/tcp
sudo ufw enable
```

