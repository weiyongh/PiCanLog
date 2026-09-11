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
