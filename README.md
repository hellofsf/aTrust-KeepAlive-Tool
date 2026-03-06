# aTrust KeepAlive Tool (防掉线保活工具)

这是一个轻量级的 PowerShell 脚本，旨在解决 aTrust VPN 或其他远程连接工具因长时间无操作而自动断开（Idle Timeout）的问题。

## 核心原理

该脚本通过每隔一定时间（默认 30 分钟）模拟按下键盘上的 **ScrollLock** 键，向操作系统发送“用户活动”信号。

* **ScrollLock 键**：这是一个对现代应用程序几乎无影响的按键，不会干扰你的正常打字、看视频或代码编写。
* **模拟机制**：调用 Windows Forms API 直接发送按键指令，被操作系统视为真实的用户输入。

## 使用方法
### 命令行运行

在 cmd 终端中执行([win + `]可直接调出windows终端)：

```cmd
powershell -ExecutionPolicy Bypass -File d:\explo\explo\aTrust_KeepAlive.ps1
```

如果你想自定义间隔时间（例如改为每 60 秒一次）：

```cmd
powershell -ExecutionPolicy Bypass -File d:\explo\explo\aTrust_KeepAlive.ps1 -IntervalSeconds 60
```

## 配置说明

脚本默认配置如下：

* **间隔时间**：1800 秒 (30 分钟)
* **模拟按键**：`{SCROLLLOCK}`

如果需要修改默认间隔，可以用记事本打开脚本，修改第 2 行的数值：

```powershell
[int]$IntervalSeconds = 1800  # 修改这里的数字 (单位: 秒)
```

## 常见问题

**Q: 运行脚本时闪退怎么办？**
A: 这通常是因为系统的 PowerShell 执行策略限制。请尝试以管理员身份打开 PowerShell，输入 `Set-ExecutionPolicy RemoteSigned` 并按回车确认，然后再运行脚本。

**Q: 这个脚本会影响我玩游戏或打字吗？**
A: 不会。ScrollLock 键在绝大多数现代软件中没有功能绑定。

**Q: 我需要一直开着它吗？**
A: 是的。当你需要保持 VPN 连接时请保持脚本运行。不需要时直接关闭窗口即可。
