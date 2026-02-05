# PolyHermes 安装使用

## 一.登录你的 VPS 控制台

推荐选择 Ubuntu 24.04 LTS

安装完成后，会生成新的公网 IP（记录下来）

SSH 登录 VPS：

ssh root@<VPS公网IP>
```bash
sudo -i

```


更新：
```bash
sudo apt update
sudo apt upgrade -y

```

## 二.下载并安装宝塔面板（官方推荐脚本）

```bash
curl -sSO http://download.bt.cn/install/install-ubuntu_6.0.sh && bash install-ubuntu_6.0.sh
```

安装过程中会提示用户名、密码、面板端口

安装完成后会显示 宝塔面板登录地址

注意记录用户名、密码和端口



## 三.宝塔安装PolyHermes

打开浏览器访问宝塔面板地址：

http://<VPS公网IP>:<宝塔端口>

在 软件管理 → 安装环境 安装必需组件：

Docker / Docker Compose

Nginx（可选，做反向代理 + HTTPS）

宝塔面板可以直接用 Web UI 管理端口和防火墙，非常方便

## 四.部署 PolyHermes

在宝塔面板 终端 或 SSH 中执行：

```bash
mkdir -p ~/polyhermes && cd ~/polyhermes
curl -fsSL https://raw.githubusercontent.com/WrBug/PolyHermes/main/deploy-interactive.sh -o deploy.sh
chmod +x deploy.sh
./deploy.sh
```

按提示填写数据库密码等信息并记录
开启


安装完成后开启docker的日常dubug
：
```bash
# 停止 Docker
sudo systemctl stop docker

# 备份并清空配置
sudo mv /etc/docker/daemon.json /etc/docker/daemon.json.bak 2>/dev/null

# 写入新配置
sudo tee /etc/docker/daemon.json <<'EOF'
{
  "log-level": "debug",
  "debug": true
}
EOF

# 启动 Docker
sudo systemctl start docker

# 验证
docker info | grep -i debug
```
显示Debug Mode: true即开启成功


通过宝塔开放端口

宝塔面板 → 安全 → 防火墙

添加允许 （PolyHermes Web UI）8080 端口

如果需要 HTTPS，可以直接使用宝塔自带的 一键 SSL 证书


## 五.访问 PolyHermes Web UI
http://<VPS公网IP>:8080

### 账户管理→→→添加账户

钱包导入推荐小狐狸Metamask

授权登录polymarket

并在再钱包充值pol和usdc 转入polymarket

返回小狐狸点击左上角account →→→三个点→→→账户详情→→→私钥

复制到PolyHermes即可

### 跟单交易

跟单配置----Leader 管理----跟单模版----回测

首先再Leader管理理填写巨鲸钱包地址和设置跟单模版 回测以后就可以开始跟单了


### 系统管理

API健康 延迟越低越好

### RPC节点管理  目前全网唯一 特此感谢WrBug

没有十年金融经验撸不出这么完美的路

自行添加测试 可添加收费版更优










