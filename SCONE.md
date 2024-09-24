- Model
- Controller
- Contorller
	- open-loop
	- closed-loop
- Goad task(Objective), Combination of Measures
- Optimizer




```
更新系统并安装 XRDP

bash

sudo apt update
sudo apt install xrdp

2. 确保 GNOME 桌面环境已安装

由于您已经在使用 GNOME，可以跳过这一步。如果尚未安装，可以使用以下命令：

bash

sudo apt install ubuntu-desktop

3. 配置 XRDP 使用 GNOME 桌面环境

编辑 /etc/xrdp/startwm.sh 文件，替换其内容为以下内容：

bash

#!/bin/sh
if [ -r /etc/default/locale ]; then
  . /etc/default/locale
  export LANG LANGUAGE
fi

gnome-session

保存并关闭文件。
4. 确保 XRDP 使用 Xorg 而非 Wayland

GNOME 默认使用 Wayland，但 XRDP 需要使用 Xorg。您需要禁用 Wayland。

编辑 /etc/gdm3/custom.conf 文件，找到以下行：

ini

#WaylandEnable=false

将其修改为：

ini

WaylandEnable=false

保存并关闭文件。
5. 重启 GDM3 服务

bash

sudo systemctl restart gdm3

6. 允许任何用户启动 X 会话

编辑 /etc/X11/Xwrapper.config 文件，将 allowed_users 设置为 anybody：

bash

sudo sed -i 's/allowed_users=.*/allowed_users=anybody/' /etc/X11/Xwrapper.config

7. 配置多用户支持

    编辑 polkit 规则

    创建文件 /etc/polkit-1/localauthority.conf.d/02-allow-colord.conf，添加以下内容：

    javascript

    polkit.addRule(function(action, subject) {
        if ((action.id == "org.freedesktop.color-manager.create-device" ||
             action.id == "org.freedesktop.color-manager.create-profile" ||
             action.id == "org.freedesktop.color-manager.delete-device" ||
             action.id == "org.freedesktop.color-manager.delete-profile" ||
             action.id == "org.freedesktop.color-manager.modify-device" ||
             action.id == "org.freedesktop.color-manager.modify-profile") &&
            subject.isInGroup("users")) {
            return polkit.Result.YES;
        }
    });

8. 重启 XRDP 服务

bash

sudo systemctl restart xrdp

9. 配置防火墙

确保防火墙允许 RDP 连接（默认端口为 3389）：

bash

sudo ufw allow 3389

10. 创建多个用户账号（如果需要）

为每个需要远程连接的用户创建单独的账号：

bash

sudo adduser username

11. 测试连接

从客户端计算机使用 RDP 客户端（例如 Windows 的远程桌面连接）连接到 Ubuntu 机器的 IP 地址。每个用户使用各自的用户名和密码进行登录。
注意事项：

    性能考虑：GNOME 桌面环境较为资源密集，确保您的 Ubuntu 机器有足够的硬件资源（CPU、内存）来支持多用户同时连接。
    安全性：RDP 默认没有强加密，建议在 VPN 内部使用，或者配置 XRDP 使用 SSL 证书进行加密。
    Wayland 与 XRDP：由于 XRDP 目前不支持 Wayland，我们通过禁用 Wayland 来确保 XRDP 正常工作。
    可能的限制：即使按照上述步骤配置，使用 GNOME 桌面环境的 XRDP 可能仍会遇到性能或兼容性问题。如果遇到困难，您可能需要考虑使用其他轻量级桌面环境，如 XFCE 或 MATE，以获得更好的稳定性和性能。
    端口安全：如果不需要，避免公开暴露 3389 端口到互联网。

希望这些步骤能帮助您成功配置 XRDP 与 GNOME 桌面环境，实现多用户同时通过 RDP 连接到您的 Ubuntu 电脑。如果您有任何疑问或需要进一步的帮助，请随时提问！


ChatGPT can make mistakes. Check important info.
```