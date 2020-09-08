---
title: Docker 教程 - 第 7 部分：使用 Docker Compose
description: 介绍如何安装和使用 Docker Compose。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 81f70612b05920ea58c752a878831f1d6de34098
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89176663"
---
# <a name="use-docker-compose"></a>使用 Docker Compose

[Docker Compose](https://docs.docker.com/compose/) 是一种工具，用于帮助定义和共享多容器应用程序。 通过 Compose，你可以创建 YAML 文件来定义服务，并且只需一个命令，就可以启动或清理所有内容。

使用 Compose 的巨大优点是，你可以在文件中定义应用程序堆栈，使其位于项目存储库的根目录下（它现在受版本控制），并方便其他人参与你的项目。 其他人只需克隆你的存储库即可开始撰写应用。 事实上，你可能会看到 GitHub/GitLab 上的很多项目现在都是这样做的。

那么，如何开始？

## <a name="install-docker-compose"></a>安装 Docker Compose

如果你为 Windows 或 Mac 安装了 Docker Desktop，则你已拥有 Docker Compose！ Play-with-Docker 实例也已安装 Docker Compose。 如果你使用的是 Linux 计算机，则需要按照[此处的说明](https://docs.docker.com/compose/install/)安装 Docker Compose。

安装后，你应该能够运行以下内容并查看版本信息。

```bash
docker-compose version
```

## <a name="create-the-compose-file"></a>创建 Compose 文件

1. 在应用项目的根目录中，创建名为 `docker-compose.yml` 的文件。

1. 在 Compose 文件中，我们将首先定义架构版本。 在大多数情况下，最好使用支持的最新版本。 你可以查看 [Compose 文件参考](https://docs.docker.com/compose/compose-file/)获取当前架构版本和兼容性矩阵。

    ```yaml
    version: "3.7"
    ```

1. 接下来，定义要作为应用程序的一部分运行的服务（或容器）列表。

    ```yaml hl_lines="3"
    version: "3.7"

    services:
    ```

现在，你将开始一次将服务迁移到 Compose 文件中。

## <a name="define-the-app-service"></a>定义应用服务

请记住，这是用于定义应用容器的命令（在 Windows PowerShell 中，请将 `` ` `` 字符替换为 ` \ `）。

```bash
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

1. 首先，定义容器的服务项和映像。 你可为服务选择任何名称。 该名称将自动成为网络别名，这在定义 MySQL 服务时非常有用。

    ```yaml hl_lines="4 5"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
    ```

1. 通常，你会看到命令接近 `image` 定义，尽管对排序没有要求。 接下来，将其移到该文件中。

    ```yaml hl_lines="6"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
    ```

1. 通过为服务定义 `ports` 来迁移命令的 `-p 3000:3000` 部分。 你将在此使用[短语法](https://docs.docker.com/compose/compose-file/#short-syntax-1)，但此处还提供了更详细的[长语法](https://docs.docker.com/compose/compose-file/#long-syntax-1)。

    ```yaml hl_lines="7 8"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
          - 3000:3000
    ```

1. 接下来，使用 `working_dir` 和 `volumes` 定义迁移工作目录 (`-w /app`) 和卷映射 (`-v ${PWD}:/app`)。 卷还有[短语法](https://docs.docker.com/compose/compose-file/#short-syntax-3)和[长语法](https://docs.docker.com/compose/compose-file/#long-syntax-3)。

   Docker Compose 卷定义的一个优点是你可以使用当前目录中的相对路径。

    ```yaml hl_lines="9 10 11"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
          - 3000:3000
        working_dir: /app
        volumes:
          - ./:/app
    ```

1. 最后，使用 `environment` 键迁移环境变量定义。

    ```yaml hl_lines="12 13 14 15 16"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
          - 3000:3000
        working_dir: /app
        volumes:
          - ./:/app
        environment:
          MYSQL_HOST: mysql
          MYSQL_USER: root
          MYSQL_PASSWORD: secret
          MYSQL_DB: todos
    ```

### <a name="define-the-mysql-service"></a>定义 MySQL 服务

现在，可以定义 MySQL 服务了。 用于该容器的命令如下（在 Windows PowerShell 中，请将 ` \ ` 字符替换为 `` ` ``）：

```bash
docker run -d \
  --network todo-app --network-alias mysql \
  -v todo-mysql-data:/var/lib/mysql \
  -e MYSQL_ROOT_PASSWORD=secret \
  -e MYSQL_DATABASE=todos \
  mysql:5.7
```

1. 首先，定义新服务并将其命名为 `mysql`，以便它自动获取网络别名。 同时指定要使用的映像。

    ```yaml hl_lines="6 7"
    version: "3.7"

    services:
      app:
        # The app service definition
      mysql:
        image: mysql:5.7
    ```

1. 接下来，定义卷映射。 使用 `docker run` 运行容器时，会自动创建命名卷。 但是，使用 Compose 运行时，则不会。 你需要在最上面的 `volumes:` 部分定义卷，然后在服务配置中指定装载点。只需仅提供卷名，即可使用默认选项。 不过，还有[很多可用选项](https://docs.docker.com/compose/compose-file/#volume-configuration-reference)。

    ```yaml hl_lines="8 9 10 11 12"
    version: "3.7"

    services:
      app:
        # The app service definition
      mysql:
        image: mysql:5.7
        volumes:
          - todo-mysql-data:/var/lib/mysql
    
    volumes:
      todo-mysql-data:
    ```

1. 最后，只需指定环境变量。

    ```yaml hl_lines="10 11 12"
    version: "3.7"

    services:
      app:
        # The app service definition
      mysql:
        image: mysql:5.7
        volumes:
          - todo-mysql-data:/var/lib/mysql
        environment: 
          MYSQL_ROOT_PASSWORD: secret
          MYSQL_DATABASE: todos
    
    volumes:
      todo-mysql-data:
    ```

此时，完整的 `docker-compose.yml` 应如下所示：

```yaml
version: "3.7"

services:
  app:
    image: node:12-alpine
    command: sh -c "yarn install && yarn run dev"
    ports:
      - 3000:3000
    working_dir: /app
    volumes:
      - ./:/app
    environment:
      MYSQL_HOST: mysql
      MYSQL_USER: root
      MYSQL_PASSWORD: secret
      MYSQL_DB: todos

  mysql:
    image: mysql:5.7
    volumes:
      - todo-mysql-data:/var/lib/mysql
    environment: 
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: todos

volumes:
  todo-mysql-data:
```

## <a name="run-the-application-stack"></a>运行应用程序堆栈

现在你已经有了 `docker-compose.yml` 文件，启动它吧！

1. 首先，确保应用和数据库的其他副本未运行（`docker ps` 和 `docker rm -f <ids>`）。

1. 使用 `docker-compose up` 命令启动应用程序堆栈。 添加 `-d` 标志以在后台运行所有内容。 或者，你可以右键单击 Compose 文件，然后选择 VS Code 侧边栏上的“启动”选项。 

    ```bash
    docker-compose up -d
    ```

    运行此操作时，你应该会看到如下输出：

    ```plaintext
    Creating network "app_default" with the default driver
    Creating volume "app_todo-mysql-data" with default driver
    Creating app_app_1   ... done
    Creating app_mysql_1 ... done
    ```

    你会注意到已创建卷和网络！ 默认情况下，Docker Compose 会自动创建一个专门针对应用程序堆栈的网络（这就是为什么你在 Compose 文件中没有定义网络）。

1. 使用 `docker-compose logs -f` 命令查看日志。 你将看到来自每个服务的日志交汇形成一个流。 当你想要关注与时间相关的问题时，这非常有用。 `-f` 标志指示“跟踪”日志，因此会在生成时显示实时输出。

    如果尚未这样做，你会看到如下所示的输出：

    ```plaintext
    mysql_1  | 2019-10-03T03:07:16.083639Z 0 [Note] mysqld: ready for connections.
    mysql_1  | Version: '5.7.27'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server (GPL)
    app_1    | Connected to mysql db at host mysql
    app_1    | Listening on port 3000
    ```

    服务名称显示在行的开头（通常为彩色），以帮助区分消息。 如果要查看特定服务的日志，可以将服务名称添加到日志命令的末尾（例如 `docker-compose logs -f app`）。

    > [!TIP]
    > **在启动应用前等待 DB** 当应用启动时，它实际上会等待 MySQL 启动并准备就绪，然后再尝试连接到它。Docker 没有任何内置支持，无法等待另一个容器完全启动、运行并准备就绪，然后再启动另一个容器。 对于基于节点的项目，你可以使用 [wait-port](https://github.com/dwmkerr/wait-port) 依赖项。 其他语言/框架有类似的项目。

1. 此时，你应能够打开应用并看到它正在运行。 嗨！ 你只需要一个命令！

## <a name="see-the-app-stack-in-the-docker-extension"></a>请参阅 Docker 扩展中的应用堆栈

如果查看 Docker 扩展，可以使用“cog”和“group by”更改分组选项。 在本例中，你希望查看按 Compose 项目名称分组的容器：

![带 Compose 的 VS 扩展](media/vs-app-project-collapsed.png)

如果关闭网络，你将看到在 Compose 文件中定义的两个容器。

![带已扩展 Compose 的 VS 扩展](media/vs-app-project-expanded.png)

## <a name="tear-it-all-down"></a>全部清理

当你准备好全部清理时，只需运行 `docker-compose down`，或者在 VS Code Docker 扩展的容器列表中，右键单击应用程序，然后选择“停止”。 容器将停止，网络将删除。

> [!WARNING]
> **删除卷** 默认情况下，运行 `docker-compose down` 时，Compose 文件中的命名卷不会删除。 如果要删除卷，则需要添加 `--volumes` 标志。

清理后，你可以切换到另一个项目，运行 `docker-compose up`，并准备好参与该项目！ 真的没有比这更简单的了！

## <a name="recap"></a>概括

在本部分中，你了解了 Docker Compose，以及它如何帮助显著简化多服务应用程序的定义和共享。 你通过将所使用的命令转换为适当的 Compos 格式，创建了 Compos 文件。

接下来，我们将对教程进行总结。 但是，我们还将介绍一些有关映像生成的最佳做法，因为你使用的 Dockerfile 存在较大的问题。 那么，让我们来看看吧！

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [映像生成最佳做法](image-building-best-practices.md)
