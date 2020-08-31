---
title: Docker 教程-第6部分：多容器应用
description: 如何在容器之间设置网络，以及如何为 MySQL 数据库添加容器。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 9513a3414a38aa02f6a4607a8c95bbf02c0e1cf6
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176665"
---
# <a name="multi-container-apps"></a>多容器应用

至此，你一直在使用单容器应用。 但现在会将 MySQL 添加到应用程序堆栈。 通常会出现以下问题-"MySQL 在何处运行？ 将它安装在同一个容器中或单独运行？ " 通常， **每个容器都应执行一项操作，并执行此操作。** 原因如下：

- 有一个很好的机会，就是必须以不同于数据库的方式缩放 Api 和前端
- 单独的容器允许版本和更新版本隔离
- 虽然您可以在本地为数据库使用容器，但您可能希望在生产环境中为数据库使用托管服务。 您不希望在应用程序中提供您的数据库引擎。
- 运行多个进程将需要进程管理器 (容器只启动一个进程) ，这会增加容器启动/关闭的复杂性。

还有更多原因。 因此，你将更新应用程序，使其如下所示：

![已连接到 MySQL 容器的待办事项应用](media/multi-app-architecture.png)

## <a name="container-networking"></a>容器网络

请记住，默认情况下，容器在同一台计算机上以隔离方式运行，并且不知道其他进程或容器。 那么，如何允许一个容器与另一个容器对话？ 答案是 **网络**。 现在，无需成为网络工程师 (个万岁！ ) 。 只需记住此规则 .。。

> [!NOTE]
> 如果两个容器位于同一网络上，则它们可以相互通信。 如果不是，则不能。

## <a name="start-mysql"></a>启动 MySQL

可以通过两种方式在网络上放置容器：在 "开始" 中分配容器或连接现有容器。 现在，你将首先创建网络，并在启动时附加 MySQL 容器。

1. 创建网络。

    ```bash
    docker network create todo-app
    ```

1. 启动 MySQL 容器并将其连接到网络。 我们还将定义一些环境变量，数据库将使用这些变量来初始化数据库 (参见 [MySQL Docker Hub 列表](https://hub.docker.com/_/mysql/) 中的 "环境变量" 部分，)  (` \ ` 在 Windows PowerShell 中将这些字符替换为 `` ` ``) 。

    ```bash
    docker run -d \
        --network todo-app --network-alias mysql \
        -v todo-mysql-data:/var/lib/mysql \
        -e MYSQL_ROOT_PASSWORD=secret \
        -e MYSQL_DATABASE=todos \
        mysql:5.7
    ```

    您还会看到您指定了 `--network-alias` 标志。 稍后我们将回来。

    > [!TIP]
    > 你会注意到，这里使用的是卷名， `todo-mysql-data` 并将其装载到 `/var/lib/mysql` ，后者是 MySQL 存储其数据的位置。 但是，你永远不会运行 `docker volume create` 命令。 Docker 认识到你想要使用命名卷，并自动为你创建一个。

1. 若要确认数据库是否已启动并运行，请连接到数据库，并验证其是否已连接。

    ```bash
    docker exec -it <mysql-container-id> mysql -p
    ```

    出现密码提示时，键入 " **机密**"。 在 MySQL shell 中列出数据库，并验证是否可以看到 `todos` 数据库。

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

    个万岁! 你的数据库已准备就绪，可供 `todos` 使用！

## <a name="connect-to-mysql"></a>连接到 MySQL

现在，你已了解 MySQL 已启动并正在运行，接下来让我们使用！ 但问题在于 .。。帮助? 如果在同一网络中运行另一个容器，如何查找容器 (记住每个容器都有自己的 IP 地址) ？

若要解决此问题，你将使用 [nicolaka/netshoot](https://github.com/nicolaka/netshoot) 容器，该容器附带了 *很多* 用于排查或调试网络问题的工具。

1. 使用映像启动新的容器 `nicolaka/netshoot` 。 请确保将其连接到同一网络。

    ```bash
    docker run -it --network todo-app nicolaka/netshoot
    ```

1. 在容器中，使用 `dig` 命令，它是一个有用的 DNS 工具。 查找主机名的 IP 地址 `mysql` 。

    ```bash
    dig mysql
    ```

    你会看到如下所示的输出：

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

    在 "答案" 部分中，你将看到一个 `A` 记录， `mysql` 该记录将解析为 `172.23.0.2` (你的 IP 地址最有可能具有不同的值) 。 虽然 `mysql` 此主机名不是有效的主机名，但 Docker 仍可将其解析为具有该网络别名的容器的 IP 地址 (记住 `--network-alias` 前面使用的标志？ ) 。

    这意味着 .。。应用只需连接到名为的主机 `mysql` ，该主机就会与数据库进行通信！ 这并不是这么简单！

## <a name="run-your-app-with-mysql"></a>通过 MySQL 运行你的应用

Todo 应用支持设置几个环境变量来指定 MySQL 连接设置。 它们分别是：

- `MYSQL_HOST` -正在运行的 MySQL 服务器的主机名
- `MYSQL_USER` -用于连接的用户名
- `MYSQL_PASSWORD` -用于连接的密码
- `MYSQL_DB` -连接后要使用的数据库

> [!WARNING]
> **通过环境变量设置连接设置** 虽然使用环境变量来设置连接设置通常是可以进行开发的，但在生产中运行应用程序时，强烈建议不要使用环境变量。 若要了解原因，请参阅 [为何不应将环境变量用于机密数据](https://diogomonica.com/2017/03/27/why-you-shouldnt-use-env-variables-for-secret-data/)。
> 更安全的机制是使用容器业务流程框架提供的机密支持。 在大多数情况下，这些机密作为文件装载到正在运行的容器中。 你将看到许多应用程序 (包括 MySQL 映像和 todo 应用程序) 还支持使用带有后缀的环境变量 `_FILE` 指向包含文件的文件。
> 例如，设置 `MYSQL_PASSWORD_FILE` var 将导致应用将所引用文件的内容用作连接密码。 Docker 不会执行任何操作来支持这些 env var。 应用需要知道如何查找变量并获取文件内容。

完成所有说明后，启动开发就绪容器！

1. 指定上述每个环境变量，并将该容器连接到应用网络， (将这些 ` \ ` 字符替换为 `` ` `` Windows PowerShell) 中的字符。

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

1. 如果查看容器的日志 (`docker logs <container-id>`) ，你应该会看到一条消息，指示它使用的是 MySQL 数据库。

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

1. 在浏览器中打开应用程序，并向 todo 列表添加几个项。

1. 连接到 MySQL 数据库，并证明正在将项目写入数据库。 请记住，密码是 **机密**。

    ```bash
    docker exec -ti <mysql-container-id> mysql -p todos
    ```

    在 MySQL shell 中运行以下命令：

    ```plaintext
    mysql> select * from todo_items;
    +--------------------------------------+--------------------+-----------+
    | id                                   | name               | completed |
    +--------------------------------------+--------------------+-----------+
    | c906ff08-60e6-44e6-8f49-ed56a0853e85 | Do amazing things! |         0 |
    | 2912a79e-8486-4bc3-a4c5-460793a575ab | Be awesome!        |         0 |
    +--------------------------------------+--------------------+-----------+
    ```

    很明显，你的表看起来会有所不同，因为它包含你的项。 但是，你应该看到它们存储在那里！

如果你快速查看 Docker 扩展，你会看到运行了两个应用容器。 但这并不是真正的指出，它们在单个应用中组合在一起。 稍后你将了解如何使其更好！

![显示两个未分组应用容器的 Docker 扩展](media/vs-multi-container-app.png)

## <a name="recap"></a>概括

此时，你的应用程序将其数据存储在单独的容器中运行的外部数据库中。 你已经了解了有关容器网络的一些信息，并了解了如何使用 DNS 来执行服务发现。

不过，有一个很好的机会，那就是启动此应用程序所需的一切。 必须创建网络、启动容器、指定所有环境变量、公开端口和其他信息！ 这是一件很多需要记住的事情，确实要将其传递给其他人更难。

在下一部分中，我们将讨论 Docker Compose。 使用 Docker Compose，你可以更轻松地共享你的应用程序堆栈，让其他人通过单个 (和简单的) 命令来快速启动它们！

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [使用 Docker Compose](use-docker-compose.md)
