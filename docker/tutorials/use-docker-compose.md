---
title: Docker 教程-第7部分：使用 Docker Compose
description: 描述如何安装和使用 Docker Compose。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 81f70612b05920ea58c752a878831f1d6de34098
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176663"
---
# <a name="use-docker-compose"></a>使用 Docker Compose

[Docker Compose](https://docs.docker.com/compose/) 是一种用于帮助定义和共享多容器应用程序的工具。 使用撰写，你可以创建一个 YAML 文件来定义服务，并使用单个命令来快速启动所有内容或将所有内容全部拉出。

使用撰写的 *大* 优点是，你可以在文件中定义应用程序堆栈，使其保持在项目存储库的根目录中， (现在) 控制版本，并可轻松使其他人参与你的项目。 有些人只需克隆你的存储库并启动撰写应用。 事实上，你可能会在 GitHub/GitLab 上看到相当多的项目。

那么，您如何开始呢？

## <a name="install-docker-compose"></a>安装 Docker Compose

如果为 Windows 或 Mac 安装了 Docker Desktop，则已 Docker Compose！ 已安装 Docker Compose 的 "Play"。 如果你使用的是 Linux 计算机，则需要使用 [此处的说明](https://docs.docker.com/compose/install/)安装 Docker Compose。

安装完成后，你应该能够运行以下内容并查看版本信息。

```bash
docker-compose version
```

## <a name="create-the-compose-file"></a>创建撰写文件

1. 在应用程序项目的根目录中，创建一个名为的文件 `docker-compose.yml` 。

1. 在撰写文件中，我们首先定义架构版本。 在大多数情况下，最好使用最新的受支持版本。 您可以查看当前架构版本和兼容性矩阵的 [撰写文件引用](https://docs.docker.com/compose/compose-file/) 。

    ```yaml
    version: "3.7"
    ```

1. 接下来，定义要作为应用程序的一部分运行的服务 (或容器) 列表。

    ```yaml hl_lines="3"
    version: "3.7"

    services:
    ```

现在，你将一次开始将服务迁移到撰写文件中。

## <a name="define-the-app-service"></a>定义应用服务

请记住，这是用于定义应用程序容器 (` \ ` `` ` `` 在 Windows PowerShell) 中替换字符的命令。

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

1. 首先，为容器定义服务项和映像。 可以为服务选取任意名称。 该名称将自动成为网络别名，这在定义 MySQL 服务时将非常有用。

    ```yaml hl_lines="4 5"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
    ```

1. 通常，你会看到与定义接近的命令 `image` ，但不要求排序。 接下来，将该文件移到该文件中。

    ```yaml hl_lines="6"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
    ```

1. `-p 3000:3000`通过为服务定义来迁移部分命令 `ports` 。 此处将使用 [简短语法](https://docs.docker.com/compose/compose-file/#short-syntax-1) ，但也有更详细的 [长语法](https://docs.docker.com/compose/compose-file/#long-syntax-1) 可用。

    ```yaml hl_lines="7 8"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
          - 3000:3000
    ```

1. 接下来，使用和定义同时迁移工作目录 (`-w /app`) 和卷映射 (`-v ${PWD}:/app`) `working_dir` `volumes` 。 卷还具有[简短](https://docs.docker.com/compose/compose-file/#short-syntax-3)[的语法。](https://docs.docker.com/compose/compose-file/#long-syntax-3)

   Docker Compose 卷定义的一个优点是，可以使用当前目录中的相对路径。

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

1. 最后，使用密钥迁移环境变量定义 `environment` 。

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

现在，可以定义 MySQL 服务了。 用于该容器的命令是以下 (替换 ` \ ` `` ` `` Windows PowerShell) 中的字符：

```bash
docker run -d \
  --network todo-app --network-alias mysql \
  -v todo-mysql-data:/var/lib/mysql \
  -e MYSQL_ROOT_PASSWORD=secret \
  -e MYSQL_DATABASE=todos \
  mysql:5.7
```

1. 首先，定义新服务并将其命名为 `mysql` 自动获取网络别名。 指定要使用的映像。

    ```yaml hl_lines="6 7"
    version: "3.7"

    services:
      app:
        # The app service definition
      mysql:
        image: mysql:5.7
    ```

1. 接下来，定义卷映射。 当你运行容器时 `docker run` ，会自动创建命名卷。 但是，在用撰写运行时不会发生这种情况。 需要在顶级部分定义卷 `volumes:` ，然后在服务配置中指定装入点。只需仅提供卷名，就会使用默认选项。 不过，还有 [更多可用选项](https://docs.docker.com/compose/compose-file/#volume-configuration-reference) 。

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

此时，完成 `docker-compose.yml` 内容应如下所示：

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

现在您已经有了该 `docker-compose.yml` 文件，可以启动了！

1. 首先，请确保应用程序和数据库的其他副本没有运行 (`docker ps` 和 `docker rm -f <ids>`) 。

1. 使用命令启动应用程序堆栈 `docker-compose up` 。 添加 `-d` 标志以便在后台运行所有内容。 或者，您可以右键单击您的撰写文件，然后为 VS Code 侧栏选择 " **撰写** " 选项。 

    ```bash
    docker-compose up -d
    ```

    运行此操作时，应会看到如下所示的输出：

    ```plaintext
    Creating network "app_default" with the default driver
    Creating volume "app_todo-mysql-data" with default driver
    Creating app_app_1   ... done
    Creating app_mysql_1 ... done
    ```

    你会注意到该卷和网络已创建！ 默认情况下，Docker Compose 会自动为应用程序堆栈创建一个网络 (这就是你未在组合文件) 中定义一个网络的原因。

1. 使用命令查看日志 `docker-compose logs -f` 。 你将看到每个服务中的日志交错为一个流。 如果要监视与计时相关的问题，这种方法非常有用。 该 `-f` 标志 "跟随" 了日志，因此在生成时将显示实时输出。

    如果你尚未这样做，你会看到如下所示的输出：

    ```plaintext
    mysql_1  | 2019-10-03T03:07:16.083639Z 0 [Note] mysqld: ready for connections.
    mysql_1  | Version: '5.7.27'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server (GPL)
    app_1    | Connected to mysql db at host mysql
    app_1    | Listening on port 3000
    ```

    服务名称显示在行的开头 (通常彩色) 以帮助区分消息。 若要查看特定服务的日志，可以将服务名称添加到日志命令的末尾 (例如， `docker-compose logs -f app`) 。

    > [!TIP]
    > 正在**等待 DB，然后再启动应用**当应用程序启动时，该应用程序实际上会处于运行状态，并在尝试连接到 it.Docker 没有任何内置支持，以便在启动另一个容器之前完全启动、运行并准备好运行。 对于基于节点的项目，可以使用 [等待端口](https://github.com/dwmkerr/wait-port) 依赖项。 其他语言/框架有类似的项目。

1. 此时，你应该能够打开你的应用程序并查看其运行情况。 嗨！ 你会看到一个命令！

## <a name="see-the-app-stack-in-the-docker-extension"></a>请参阅 Docker 扩展中的应用堆栈

如果查看 Docker 扩展，可以使用 "齿轮" 和 "group by" 更改分组选项。 在此实例中，你想要查看按撰写项目名称分组的容器：

![VS Extension with 撰写](media/vs-app-project-collapsed.png)

如果向下旋转网络，你将看到在 "撰写" 文件中定义的两个容器。

![结合展开的 VS 扩展](media/vs-app-project-expanded.png)

## <a name="tear-it-all-down"></a>全部抽出

准备好将其全部拉出后，只需运行 `docker-compose down` ，或右键单击 VS Code Docker 扩展的 "容器" 列表中的应用程序，然后选择 " **撰写**"。 容器将停止，网络将被删除。

> [!WARNING]
> **删除卷** 默认情况下，在运行时不会删除撰写文件中的命名卷 `docker-compose down` 。 如果要删除这些卷，则需要添加该 `--volumes` 标志。

销毁后，可以切换到另一个项目，运行 `docker-compose up` 该项目并准备好加入该项目！ 这实际上并不是这么简单！

## <a name="recap"></a>概括

在本部分中，你已了解 Docker Compose 以及它如何帮助大幅简化多服务应用程序的定义和共享。 您创建了一个撰写文件，方法是将所使用的命令转换为相应的撰写格式。

此时，您将开始总结教程。 不过，有几个有关映像构建的最佳实践需要涵盖，因为使用的 Dockerfile 有一个大问题。 那么，让我们看看吧！

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [映像构建最佳实践](image-building-best-practices.md)
