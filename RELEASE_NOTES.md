# palserver-GUI 自定义构建(Windows 专用增强版)

基于官方 v2.10.0,包含以下自定义修复与增强:

- **修复 Docker 游戏端口映射 bug**(自定义端口时连接超时的根因)
- **Docker 实例游戏目录持久化**(GUI 重启不再重新下载 5GB 服务端)
- **Docker 后端 REST 公告链路修复**(容器化 agent 可正常发游戏公告/倒计时)
- **游戏容器镜像构建上下文与代理支持**(限速/被墙环境可正常构建)

## Windows 使用说明

1. 下载 `palserver-agent-windows.zip` 解压到任意目录
2. 运行 `palserver-agent.exe`,浏览器会自动打开 `http://localhost:8250`
3. 创建实例时选择「原生」运行方式(Windows 本机 = 原生 Windows 服务端,支持全部 mod 生态:PalDefender / PalSchema / 创意工坊)
4. 首次启动会自动下载服务端(约 6GB);若下载缓慢请给系统挂代理
5. 管理界面:浏览器访问 http://localhost:8250;默认本机管理无需密码

原版功能与说明见官方仓库:palserver-gui/palserver-gui
