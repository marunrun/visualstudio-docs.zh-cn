---
title: Docker 教程 - 第 6 部分：多容器应用
description: 如何在容器之间设置网络连接，以及如何为 MySQL 数据库添加容器。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 9513a3414a38aa02f6a4607a8c95bbf02c0e1cf6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89176665"
---
# <a name="multi-container-apps"></a>多容器应用

到目前为止，你使用的一直是单容器应用。 但是，现在你将向应用程序堆栈添加 MySQL。 经常会出现以下问题：“MySQL 将在哪里运行？ 是将它安装在同一容器中，还是单独运行它？” 一般来说，每个容器都应执行一项操作，而且要完成得很好。 有几个原因：

- 这是很好的机会使用与数据库不同的方式缩放 API 和前端
- 单独的容器会使你的版本和更新版本相互隔离
- 虽然你可在本地对数据库使用容器，但在生产环境中，你可能需要对数据库使用托管服务。 你到时不希望将你的数据库引擎与你的应用一起提供。
- 运行多个进程将要求使用进程管理器（容器仅启动一个进程），这会让容器启动/关闭更加复杂。

当然还有其他一些原因。 因此，你将更新你的应用程序，使它按如下方式工作：

![已连接到 MySQL 容器的待办事项应用](media/multi-app-architecture.png)

## <a name="container-networking"></a>容器网络

请记住，容器在默认情况下以隔离方式运行，它们完全不知道同一计算机上有其他进程或容器。 那么，如何使容器能够彼此通信？ 答案就是网络连接。 现在，你不一定非要是网络工程师（这一点太棒了！）。 只需记住以下规则…

> [!NOTE]
> 如果两个容器在同一网络上，那么它们可彼此通信。 如果没在同一网络上，则没法通信。

## <a name="start-mysql"></a>启动 MySQL

有两种方法可将容器放在网络上：在启动时进行分配，或者连接现有容器。 现在，你将先创建网络，然后在启动时附加 MySQL 容器。

1. 创建网络。

    ```bash
    docker network create todo-app
    ```

1. 启动 MySQL 容器并将它附加到网络。 我们还将定义一些环境变量，数据库将使用这些变量来初始化数据库（请参见 [MySQL Docker Hub 列表](https://hub.docker.com/_/mysql/)中的“环境变量”部分）（需在 Windows PowerShell 中将 ` \ ` 字符替换为 `` ` ``）。

    ```bash
    docker run -d \
        --network todo-app --network-alias mysql \
        -v todo-mysql-data:/var/lib/mysql \
        -e MYSQL_ROOT_PASSWORD=secret \
        -e MYSQL_DATABASE=todos \
        mysql:5.7
    ```

    你还将看到你指定了 `--network-alias` 标志。 我们稍后将回来讲解这一点。

    > [!TIP]
    > 你会注意到，你在这里使用的是卷名称 `todo-mysql-data` 并将它装载到 `/var/lib/mysql`（即 MySQL 存储其数据的位置）。 但是，你从未运行过 `docker volume create` 命令。 Docker 识别到你想要使用命名卷，并自动为你创建了一个。

1. 若要确认你已启动并运行数据库，请连接到该数据库并验证它是否已连接。

    ```bash
    docker exec -it <mysql-container-id> mysql -p
    ```

    出现密码输入提示时，键入 secret。 在 MySQL shell 中，列出数据库并验证确保你看见 `todos` 数据库。

    ```cli
    mysql> SHOW DATABASES;
    ```

    你应该会看到如下所示的输出：

    ```plaintext
    +--------------------+
    | Database           |
    +--------------------+
    | information_schema |
    | mysql              |
    | performance_schema |
    | sys                |
    | todos              |
    +--------------------+
    5 rows in set (0.00 sec)
    ```

    太好了！ 你拥有 `todos` 数据库，而且它已可供使用！

## <a name="connect-to-mysql"></a>连接到 MySQL

现在你知道 MySQL 已启动且在运行，接下来使用它吧！ 但是，问题是如何使用？ 如果在同一网络中运行其他容器，你如何找到该容器？（请记住，每个容器有自己的 IP 地址）

要弄清楚这一点，你将使用 [nicolaka/netshoot](https://github.com/nicolaka/netshoot) 容器，它与有助于排查或调试网络问题的很多工具一起提供。

1. 使用 `nicolaka/netshoot` 映像启动新的容器。 请确保将它连接到同一网络。

    ```bash
    docker run -it --network todo-app nicolaka/netshoot
    ```

1. 在容器中使用 `dig` 命令，它是一种有用的 DNS 工具。 查找主机名 `mysql` 的 IP 地址。

    ```bash
    dig mysql
    ```

    你将看到如下所示的输出…

    ```text
    ; <<>> DiG 9.14.1 <<>> mysql
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 32162
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

    ;; QUESTION SECTION:
    ;mysql.             IN  A

    ;; ANSWER SECTION:
    mysql.          600 IN  A   172.23.0.2

    ;; Query time: 0 msec
    ;; SERVER: 127.0.0.11#53(127.0.0.11)
    ;; WHEN: Tue Oct 01 23:47:24 UTC 2019
    ;; MSG SIZE  rcvd: 44
    ```

    在“答案部分”，你将看到 `mysql` 的 `A` 记录，它解析为 `172.23.0.2`（你的 IP 地址很可能具有不同的值）。 虽然 `mysql` 通常不是有效的主机名，但 Docker 能够将它解析为具有该网络别名的容器的 IP 地址。（还记得你之前使用过的 `--network-alias` 标志吗？）

    这意味着你的应用只需连接到名为 `mysql` 的主机，该主机会与数据库通信！ 没有比这更简单的了！

## <a name="run-your-app-with-mysql"></a>使用 MySQL 运行应用

待办事项应用支持设置几个环境变量来指定 MySQL 连接设置。 它们是：

- `MYSQL_HOST` - 正在运行的 MySQL 服务器的主机名
- `MYSQL_USER` - 要用于连接的用户名
- `MYSQL_PASSWORD` - 要用于连接的密码
- `MYSQL_DB` - 连接后要使用的数据库

> [!WARNING]
> **通过环境变量设定连接设置** 虽然对于开发来说，通常可使用环境变量来设定连接设置，但在生产环境中运行应用程序时，强烈建议不要这样做。 若要了解原因，请参阅 [Why you shouldn't use environment variables for secret data](https://diogomonica.com/2017/03/27/why-you-shouldnt-use-env-variables-for-secret-data/)（为何不该对机密数据使用环境变量）。
> 更安全的机制是使用容器编排框架提供的机密支持。 在大多数情况下，这些机密作为文件装载到正在运行的容器中。 你会看到很多应用（包括 MySQL 映像和待办事项应用）也支持带 `_FILE` 后缀的环境变量，其中该后缀指向包含文件本身的文件。
> 例如，设置 `MYSQL_PASSWORD_FILE` 变量将导致应用将所引用的文件的内容用作连接密码。 Docker 不会执行任何操作来支持这些环境变量。 你的应用将需要知道要查找变量并获取文件内容。

现已了解上面所有的内容，来启动你的开发就绪容器吧！

1. 指定上述每个环境变量，并将容器连接到你的应用网络（在 Windows PowerShell 中将 ` \ ` 替换为 `` ` ``）。

    ```bash hl_lines="3 4 5 6 7"
    docker run -dp 3000:3000 \
      -w /app -v ${PWD}:/app \
      --network todo-app \
      -e MYSQL_HOST=mysql \
      -e MYSQL_USER=root \
      -e MYSQL_PASSWORD=secret \
      -e MYSQL_DB=todos \
      node:12-alpine \
      sh -c "yarn install && yarn run dev"
    ```

1. 如果查看容器的日志 (`docker logs <container-id>`)，你应会看到有消息指出它正在使用 MySQL 数据库。

    ```plaintext hl_lines="7"
    # Previous log messages omitted
    $ nodemon src/index.js
    [nodemon] 1.19.2
    [nodemon] to restart at any time, enter `rs`
    [nodemon] watching dir(s): *.*
    [nodemon] starting `node src/index.js`
    Connected to mysql db at host mysql
    Listening on port 3000
    ```

1. 在浏览器中打开应用，然后向待办事项列表中添加一些项。

1. 连接到 MySQL 数据库，证明这些项将写入数据库。 请记住，密码是 secret。

    ```bash
    docker exec -ti <mysql-container-id> mysql -p todos
    ```

    在 MySQL shell 中，运行以下命令：

    ```plaintext
    mysql> select * from todo_items;
    +--------------------------------------+--------------------+-----------+
    | id                                   | name               | completed |
    +--------------------------------------+--------------------+-----------+
    | c906ff08-60e6-44e6-8f49-ed56a0853e85 | Do amazing things! |         0 |
    | 2912a79e-8486-4bc3-a4c5-460793a575ab | Be awesome!        |         0 |
    +--------------------------------------+--------------------+-----------+
    ```

    很明显，你的表看起来不一样，因为它包含了你添加的项。 但是，你应会看到它就存储在那里！

如果快速查看 Docker 扩展，你将看到你有两个应用容器正在运行。 但是，这并不是真的指它们在一个应用中分组到一起。 你很快就将了解如何改进它！

![显示两个未分组的应用容器的 Docker 扩展](media/vs-multi-container-app.png)

## <a name="recap"></a>概括

目前，你有一个应用程序，它现在将自己的数据存储到在单独容器中运行的外部数据库中。 你学习了一点关于容器网络连接的知识，了解了可如何使用 DNS 执行服务发现。

但是，很有可能你开始对启动此应用程序而需要的所有操作感到有点不知所措。 你必须创建网络、启动容器、指定所有环境变量，还必须公开端口等等！ 有很多要记住的内容，当然要将知识传授给别人就更难。

在下一部分，我们将讨论 Docker Compose。 有了 Docker Compose，你可以轻松得多的方式共享应用程序堆栈，让其他人只用一个（简单的）命令就能运行它们！

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [使用 Docker Compose](use-docker-compose.md)
