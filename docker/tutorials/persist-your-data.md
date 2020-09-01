---
title: Docker 教程-第4部分：保存数据
description: 了解如何保存数据库中的数据，以及如何通过装载卷将目录共享到容器中。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 34b3cb9465c1efb946260917d755729e25c4e259
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176662"
---
# <a name="persist-your-data"></a> 保留数据

如果你没有注意到，则每次启动容器时都会清除待办事项列表。 为什么会这样？ 让我们深入了解容器的工作方式。

## <a name="the-containers-filesystem"></a>容器的文件系统

容器运行时，会将映像中的各种层用于其文件系统。 每个容器还会获取自己的 "暂存空间" 以创建、更新或删除文件。 *即使*在其他容器中使用相同的映像，也不会显示任何更改。

### <a name="see-this-in-practice"></a>在实践中查看这一点

若要查看此操作，你将启动两个容器，并在每个容器中创建一个文件。 你会看到，在一个容器中创建的文件不能在另一个容器中使用。

1. 启动一个 `ubuntu` 容器，它将创建一个名为的文件，该文件的 `/data.txt` 随机数介于1到10000之间。

    ```bash
    docker run -d ubuntu bash -c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"
    ```

    如果你对该命令感到好奇，则启动 bash shell，并调用两个命令 (为什么其 `&&`) 。 第一部分选取单个随机数，并将其写入 `/data.txt` 。 第二个命令只是监视文件以使容器保持运行。

1. 验证是否可以使用 `exec` 获取到容器中的输出。 为此，请打开 VS Code 扩展，并单击 " **附加 Shell** " 选项。 这将使用在 `exec` VS Code 终端内的容器中打开 shell。

    ![VS Code 在 ubuntu 容器中打开 CLI](media/attach_shell.png)

    你将看到在 Ubuntu 容器中运行 shell 的终端。 运行以下命令以查看文件的内容 `/data.txt` 。 再次关闭此终端。

    ```bash
    cat /data.txt
    ```

    如果你更喜欢使用命令行，可以使用 `docker exec` 命令来执行相同的操作。 你需要获取容器的 ID (用于 `docker ps`) 并使用以下命令获取内容。

    ```bash
    docker exec <container-id> cat /data.txt
    ```

    应该会看到一个随机数字！

1. 现在， `ubuntu`)  (相同的图像启动另一个容器，你会看到没有相同的文件。

    ```bash
    docker run -it ubuntu ls /
    ```

    并查找！ 这里没有任何 `data.txt` 文件！ 这是因为它只写入第一个容器的暂存空间。

1. 继续使用命令删除第一个容器 `docker rm -f` 。

## <a name="container-volumes"></a>容器卷

在上一次试验中，你看到每个容器在每次启动时都从映像定义开始。 容器可以创建、更新和删除文件，当删除容器并且将所有更改隔离到容器时，这些更改将会丢失。 通过卷，您可以更改所有这些。

[卷](https://docs.docker.com/storage/volumes/) 提供将容器的特定 filesystem 路径连接回主机的功能。 如果已装入容器中的目录，则在主机上还会显示该目录中的更改。 如果跨容器重启装载同一目录，则会看到相同的文件。

有两种主要类型的卷。 最终将使用这两个，但会开始使用 **命名卷**。

## <a name="persist-your-todo-data"></a>保留 Todo 数据

默认情况下，todo 应用程序将其数据存储在的 [SQLite 数据库](https://www.sqlite.org/index.html) 中 `/etc/todos/todo.db` 。 如果你不熟悉 SQLite，则无需担心！ 它只是一个关系数据库，其中的所有数据都存储在一个文件中。 虽然这不适用于大型应用程序，但它适用于小型演示。 稍后我们将讨论如何将其切换到实际的数据库引擎。

由于数据库是一个文件，如果可以将该文件保存在主机上并使其可供下一个容器使用，则应该能够从最后一个容器的位置开始。 通过创建卷并附加 (通常称为 "装载" ) 它存储数据的目录，你可以保留数据。 当容器写入 `todo.db` 文件时，它将保留在卷中的主机上。

如上所述，将使用 **命名卷**。 将命名卷视为只是一个数据桶。 Docker 维护磁盘上的物理位置，只需记住卷的名称。 每次使用该卷时，Docker 都将确保提供正确的数据。

1. 使用命令创建卷 `docker volume create` 。

    ```bash
    docker volume create todo-db
    ```

1. 在仪表板中再次停止 todo 应用容器 (或使用 `docker rm -f <id>`) ，因为它仍在运行，无需使用永久性卷。

1. 启动 todo 应用容器，但添加 `-v` 标记以指定卷装入。 将使用命名卷并将其装载到 `/etc/todos` ，这将捕获在该路径中创建的所有文件。

    ```bash
    docker run -dp 3000:3000 -v todo-db:/etc/todos getting-started
    ```

1. 容器启动后，打开应用并向 todo 列表添加几个项。

    ![添加到 todo 列表的项](media/items-added.png)

1. 删除 todo 应用的容器。 使用仪表板或 `docker ps` 获取 ID，然后将 `docker rm -f <id>` 其删除。

1. 使用上面的相同命令启动新容器。

1. 打开应用。 你应看到你的项目仍在列表中！

1. 完成签出列表后，请继续操作并删除容器。

个万岁! 你现在已经了解了如何持久保存数据！

> [!TIP]
> 命名卷和 bind 装载 (我们将在一分钟内谈论) 是默认 Docker 引擎安装支持的两种主要类型的卷，有许多可用的卷驱动程序插件支持 NFS、SFTP、NetApp 等！ 当你开始在群集环境中使用 Swarm、Kubernetes 的多个主机上运行容器时，这一点尤其重要。

## <a name="dive-into-your-volume"></a>深入了解你的卷

许多人通常会问： "在使用命名卷时，Docker 在何处 *实际* 存储我的数据？" 如果想知道，可以使用 `docker volume inspect` 命令。

```bash
docker volume inspect todo-db
[
    {
        "CreatedAt": "2019-09-26T02:18:36Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/todo-db/_data",
        "Name": "todo-db",
        "Options": {},
        "Scope": "local"
    }
]
```

`Mountpoint`是存储数据的磁盘上的实际位置。 请注意，在大多数计算机上，你需要具有从主机访问此目录的根访问权限。 但就是这样！

> [!NOTE]
> **直接在 Docker Desktop 上访问卷数据** 在 Docker Desktop 中运行时，Docker 命令实际上是在计算机上的小型 VM 内运行的。 如果要查看 *装载* 点目录的实际内容，需要首先获取 VM 的内部内容。 在 WSL 2 中，这属于 WSL 2 发行版，可以通过文件资源管理器进行访问。

## <a name="recap"></a>概括

此时，您有一个可以在重新启动后继续运行的正常运行的应用程序！ 你可以将其展示给投资者，希望他们能够抓住你的愿景！

但是，在前面看到，为每个更改重新生成映像需要相当长的时间。 有一种更好的更改方法，对吧？ 使用 bind 装载 (我们前面提到的) ，有一种更好的方法！ 现在我们来看看吧！

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [使用 bind 装载](use-bind-mounts.md)
