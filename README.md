# PolyHermes 安装使用

## 一.登录你的 VPS 控制台

推荐选择 Ubuntu 24.04 LTS

安装完成后，会生成新的公网 IP（记录下来）

SSH 登录 VPS：

ssh root@<VPS公网IP>


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

按提示填写数据库密码等信息

安装完成后启动容器：
...base
docker compose -f docker-compose.prod.yml up -d
docker compose -f docker-compose.prod.yml ps
...

前端默认映射 VPS 8080 端口

MySQL 默认映射 VPS 3307 端口

步骤 5：通过宝塔开放端口

宝塔面板 → 安全 → 防火墙

添加允许 TCP 8080（PolyHermes Web UI）

如果需要 HTTPS，可以直接使用宝塔自带的 一键 SSL 证书

## 五.访问 PolyHermes Web UI
http://<VPS公网IP>:8080

如果 HTTPS 配置好：

https://<VPS公网IP>:8080


宝塔面板可以实时管理容器、端口、防火墙，非常直观
