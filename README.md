# PiCanLog

一个用于树莓派 SocketCAN 数据采集的简单管理脚本。默认使用 `can0`、500 kbps，并强制开启只听模式，不会向车辆 CAN 总线发送报文。

```bash
chmod +x picanlog
./picanlog status
./picanlog start
./picanlog stop
```

日志默认保存到 `logs/can-YYYYmmdd-HHMMSS.log`，格式来自 `candump -L`，包含时间戳并可供 `canplayer` 等工具使用。

运行依赖：`bash`、`iproute2`、`usbutils`、`can-utils`，以及无需密码执行相关命令的 `sudo` 权限。使用 `./picanlog help` 查看参数和环境变量。

## Web 控制（0.1.0）

树莓派上的 uHTTPd 提供简单的 Web 控制页面，可以启动日志、停止日志、查看状态、查看日志和关闭树莓派，操作结果直接显示在按钮下方。日志列表会显示全部 `can-*.log` 文件，点击文件名即可下载。关机操作带有二次确认，提交后延迟约 3 秒执行。连接同一局域网后访问：

```text
http://192.168.1.18:8080/
```

本版本不包含日志内容在线预览、删除、分页或登录功能。每个版本的单条开发流水记录见 [DEVELOPMENT.md](DEVELOPMENT.md)。

## 车载 Wi-Fi

树莓派已配置为自动连接 iPhone 热点 `“hwy”的 iPhone`。家中 Wi-Fi 的优先级为 `10`，手机热点优先级为 `1`：家中网络可用时保持原连接，到车上仅有手机热点时自动接入。热点密码只保存在树莓派的系统 Wi-Fi 配置中，不记录在项目文件里。

“查看状态”会显示当前连接的 Wi-Fi 名称和 `wlan0` IPv4 地址。手机连接同一热点后，使用该 IPv4 地址加 `8080` 端口访问控制页面。
