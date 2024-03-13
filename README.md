### rabbitmq-server-install-bash

RabbitMQ Server 一键安装脚本.

```bash
curl -s https://raw.githubusercontent.com/joesdu/rabbitmq-server-install-bash/main/install.sh | sudo bash
```

根据官网的描述支持如下操作系统:
| 系统版本 | 代号 | 在 Docker 运行系统后测试结果 |
| :-------------- | :------: | :------ |
| Ubuntu 23.10 | jammy | 未测试,低版本能通过,应该没问题 |
| Ubuntu 23.04 | jammy | 未测试,低版本能通过,应该没问题 |
| Ubuntu 22.04 | jammy | 通过 |
| Ubuntu 20.04 | focal | 通过 |
| Ubuntu 18.04 | bionic | 包源 Erlang 版本低,需要自己解决 |
| Debian Bookworm | bullseye | 部分源报错,但是不影响结果.测试通过 |
| Debian Bullseye | bullseye | 部分源报错,但是不影响结果.测试通过 |
| Debian Sid | bullseye | 未通过,lsb_release -rs 获取不到系统版本号 |

但是通过实际测试还是建议使用较新的版本,因为旧版的系统包源较旧,可能会出现 Erlang 的版本太低的问题.个人推荐 Ubuntu 23.04

#### 自己如何测试?

对于想要自己测试的小伙伴,可以通过 Docker 或者其他方式进行测试,如虚拟机等.这里我将我使用 Docker 的步骤写一下.

- 首先在本地运行 Docker 服务,这里以 Ubuntu 23.04 为例.我使用的是 Windows 的 Docker Desktop

```bash
# Windows命令
docker run -itd --name ubuntu-test ubuntu:23.04
# Linux命令
sudo docker run -itd --name ubuntu-test ubuntu:23.04
```

- 当镜像不存在的时候,会自动从远端拉取镜像,稍作等待即可.完成后,运行命令获取容器 ID.

```bash
# Windows
docker ps -a
# Linux
sudo docker ps -a
```

- 一般会输出如下信息

```text
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS          PORTS     NAMES
81af81473202   ubuntu:23.04   "/bin/bash"   13 seconds ago   Up 12 seconds             ubuntu-test
```

- 接下来复制容器 ID 并执行如下命令进入容器命令行

```bash
# Windows
docker exec -it 81af81473202 /bin/bash
# Linux
sudo docker exec -it 81af81473202 /bin/bash
```

- 进入容器后,首先对容器进行包源更新.以及安装一些必要的依赖.

```bash
# 更新包源
apt update
# 安装一些软件
apt install curl htop sudo -y
```

- 安装完成后我们还需要安装 lsb-release,一般正常安装的系统中会存在这个依赖.

```bash
apt update && apt install -y lsb-release && apt clean all
```

- 等待完成后,即可运行我们的一键安装脚本进行安装.

```bash
curl -s https://raw.githubusercontent.com/joesdu/rabbitmq-server-install-bash/main/install.sh | sudo bash
```

- 完成后运行 rabbitmq

```bash
sudo service rabbitmq-server start
```

- 然后使用 htop 查看运行情况.
