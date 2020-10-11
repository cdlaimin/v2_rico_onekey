# v2_rico_onekey
sspanel-v3-后端一键v2ray对接

# 安装方式
systemctl stop firewalld.service.   //关闭防火墙
docker version > /dev/null || curl -fsSL get.docker.com | bash    //安装docker容器
service docker restart    //重启docker容器

mkdir v2ray-agent //创建文件夹 
cd v2ray-agent //进入目录
curl https://raw.githubusercontent.com/john8911/v2_rico_onekey/main/install.sh -o install.sh && chmod +x install.sh && bash install.sh

# 前端食用方式
// ws 示例
后端IP或域名;10550;16;ws;;path=/v2ray|host=xxxx.com

// ws + tls (Caddy 提供)
后端IP或域名;0;16;tls;ws;path=/v2ray|host=xxxx.com|inside_port=10550

// ws + tls (套CDN)
后端IP或域名;0;16;tls;ws;path=/v2ray|host=xxxx.com|inside_port=10550|server=oxxxx.com|outside_port=443



// nat ws 示例
后端IP或域名;11120;16;ws;;path=/v2ray|host=xxxx.com

// nat ws + tls (Caddy 提供)
后端IP或域名;0;16;tls;ws;path=/v2ray|host=xxxx.com|inside_port=10550|outside_port=11120

如果外部链接的端口是0或者不填，则默认监听本地127.0.0.1:inside_port
如果外部端口设定不是0或者空，则监听 0.0.0.0:外部设定端口，此端口为所有用户的单端口，此时 inside_port 弃用。
默认使用Caddy镜像来提供tls，控制代码不会生成tls相关的配置。Caddyfile可以在Docker/Caddy_V2ray文件夹里面找到。
Nat鸡如果要用ws+tls，则需要使用outside_port=xxx，php后端会生成订阅时候，使用outside_port覆盖port部分。 outside_port是内部映射端口，建议内网和外网的两个端口数值一致。
