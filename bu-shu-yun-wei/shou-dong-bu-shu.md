---
description: 本章介绍如何将开发完成后项目部署到生产服务器
---

# 手动部署

1. 在开发环境完成开发后，使用 `git` 或 `rsync` 将当前目录推送到生产服务器，要求`store` 目录和必需存在
2.  如果项目中使用到了`Node` 钩子服务（如果没有跳过第2 3步），需要将`custom-ts` 目录（要求`generated` 目录不能为空）也推送到生产服务器，同时需要在生产服务器上安装好`node` 环境，参考[https://github.com/nvm-sh/nvm#installing-and-updating](https://github.com/nvm-sh/nvm#installing-and-updating)教程完成安装\


    {% code title="install-node.sh" overflow="wrap" lineNumbers="true" %}
    ```bash
    ‌curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
    nvm install stable
    node -v
    ```
    {% endcode %}
3.  定位到服务器中项目所在目录，先进入钩子目录，启动钩子服务\


    {% code title="" overflow="wrap" lineNumbers="true" %}
    ```bash
    ‌cd custom-ts
    npm install
    npm run build
    npm i -g pm2
    # 以上命令都只需要执行一次
    pm2 start
    # 查看启动日志
    pm2 logs 0
    # 后续重启使用
    pm2 restart 0
    # 更多pm2使用方法请参考 https://pm2.keymetrics.io/docs/usage/quick-start/
    ```
    {% endcode %}
4.  进入项目根目录，启动`Fireboom` \


    {% code title="start-fireboom.sh" overflow="wrap" lineNumbers="true" %}
    ```bash
    ‌./fireboom start

    ```
    {% endcode %}

    该方式将挂起命令行，可以使用`systemctl` 方式启动。在`/usr/lib/systemd/system/` 目录中新建`fb.service` ，内容如下\


    {% code title="fb.service" %}
    ```sh
    ‌[Unit]
    Description=Fireboom server
    After=syslog.target network.target

    [Service]
    Type=simple
    # 根据实际路径来修改
    WorkingDirectory=/path/to/fb/server
    # 根据实际路径来修改
    ExecStart=/path/to/fb/server/fireboom start
    Restart=on-failure

    [Install]
    WantedBy=multi-user.target
    ```
    {% endcode %}

    然后执行 \


    {% code title="fb.sh" overflow="wrap" lineNumbers="true" %}
    ```sh
    # 重新加载
    systemctl daemon-reload
    # 开机自启
    systemctl enable fb
    # 启动
    systemctl start fb
    # 查看日志
    systemctl status fb
    ```
    {% endcode %}
