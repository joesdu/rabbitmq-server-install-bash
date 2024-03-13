### rabbitmq-server-install-bash

RabbitMQ Server 一键安装脚本.

```bash
curl -s https://raw.githubusercontent.com/joesdu/rabbitmq-server-install-bash/main/install.sh | sudo bash
```

根据官网的描述支持如下操作系统:
| 系统版本 | 代号 |
| :-------------- | :------: |
| Ubuntu 23.04 | jammy |
| Ubuntu 22.04 | jammy |
| Ubuntu 20.04 | focal |
| Ubuntu 18.04 | bionic |
| Debian Bookworm | bullseye |
| Debian Bullseye | bullseye |
| Debian Sid | bullseye |

但是通过实际测试还是建议使用较新的版本,因为旧版的系统包源较旧,可能会出现 Erlang 的版本太低的问题.个人推荐 Debian 12 以及 Ubuntu 23.04
