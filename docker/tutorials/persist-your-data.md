---
title: Docker 教程 - 第 4 部分：保留数据
description: 了解如何在数据库中保留数据，以及如何通过装载卷将目录共享到容器中。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 34b3cb9465c1efb946260917d755729e25c4e259
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89176662"
---
# <a name="persist-your-data"></a> 保留数据

或许你没注意到，每次启动容器时都会完全清除待办事项列表。 为什么会这样？ 让我们深入了解容器的工作方式。

## <a name="the-containers-filesystem"></a>容器的文件系统

容器运行时，会将映像中的各种层用于其文件系统。 每个容器还会获取自己的“暂存空间”用于创建、更新或删除文件。 任何更改都在另一容器中不可见，即使它们使用的是同一映像也是如此。

### <a name="see-this-in-practice"></a>在实践中了解这一点

要查看它的实际应用情况，你将启动两个容器，并在每个容器中创建一个文件。 你会发现在一个容器中创建的文件不能在另一个容器中使用。

1. 启动 `ubuntu` 容器，它将创建一个名为 `/data.txt` 的文件，其随机数介于 1 至 10000 之间。

    ```bash
    docker run -d ubuntu bash -c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"
    ```

    如果你有兴趣了解该命令，可启动 bash shell 并调用两个命令（这就是它有 `&&` 的原因）。 第一部分会选取一个随机数字，并将其写入 `/data.txt`。 第二个命令只是监视文件以使容器保持运行。

1. 验证是否可使用 `exec` 进入容器来查看输出。 为此，请打开 VS Code 扩展，然后单击“附加 Shell”选项。 这将使用 `exec` 在 VS Code 终端内的容器中打开 shell。

    ![VS Code 将打开 CLI 进入 Ubuntu 容器中](media/attach_shell.png)

    你将看到在 Ubuntu 容器中运行 shell 的终端。 运行以下命令，查看 `/data.txt` 文件的内容。 然后再次关闭此终端。

    ```bash
    cat /data.txt
    ```

    如果你更喜欢使用命令行，可使用 `docker exec` 命令执行该操作。 你需要获取容器的 ID（使用 `docker ps` 获取），并使用以下命令获取内容。

    ```bash
    docker exec <container-id> cat /data.txt
    ```

    你应会看到一个随机数字！

1. 现在再启动一个 `ubuntu` 容器（同一映像），你会看到没有相同的文件。

    ```bash
    docker run -it ubuntu ls /
    ```

    然后进行查找！ 这里没有 `data.txt` 文件！ 这是因为它只写入第一个容器的暂存空间。

1. 然后，使用 `docker rm -f` 命令删除第一个容器。

## <a name="container-volumes"></a>容器卷

在上一次试验中，你看到每个容器在每次启动时都从映像定义开始。 虽然容器可创建、更新和删除文件，但删除容器时这些更改将会丢失，而且所有更改都不影响该容器。 通过卷，你可改变这一切。

[卷](https://docs.docker.com/storage/volumes/)提供将容器的特定文件系统路径连接回主机的功能。 如果已装载容器中的目录，则主机上还会显示该目录中的更改。 如果在容器重启时装载该目录，你会看到相同的文件。

有两种主要类型的卷。 这两种类型最终都会使用，但首先使用的是“命名卷”。

## <a name="persist-your-todo-data"></a>保留代办事项数据

默认情况下，待办事项应用将其数据存储在 [SQLite 数据库](https://www.sqlite.org/index.html) (`/etc/todos/todo.db`) 中。 如果你不熟悉 SQLite，不必担心！ 它只是一个关系数据库，其中的所有数据都存储在单个文件中。 虽然这不是大型应用程序的最佳选择，但它适用于小型演示。 稍后，我们将讨论如何将其切换到实际的数据库引擎。

由于该数据库是单个文件，因此如果可将该文件保留在主机上并使其可用于下一个容器，那么它应该能从上次退出的位置继续。 通过创建卷并将其附加（通常称为“装载”）到存储数据的目录，可保留数据。 当容器写入 `todo.db` 文件时，它会保留在卷中的主机上。

如上所述，你将使用“命名卷”。 将命名卷仅看作是一个数据桶。 Docker 会维护磁盘上的物理位置，你只需记住卷的名称即可。 每次使用该卷时，Docker 都将确保提供正确的数据。

1. 使用 `docker volume create` 命令创建卷。

    ```bash
    docker volume create todo-db
    ```

1. 在仪表板中再次停止待办事项应用容器（或使用 `docker rm -f <id>` 停止），因为它在不使用永久卷的情况下仍在运行。

1. 启动待办事项应用容器，但添加 `-v` 标志来指定卷装载。 你要使用命名卷并将其装载到 `/etc/todos`，这将捕获在该路径中创建的所有文件。

    ```bash
    docker run -dp 3000:3000 -v todo-db:/etc/todos getting-started
    ```

1. 容器启动后，打开应用并向待办事项列表添加几个项。

    ![已添加到待办事项列表的项](media/items-added.png)

1. 删除待办事项应用的容器。 使用仪表板或 `docker ps` 获取 ID，然后使用 `docker rm -f <id>` 将其删除。

1. 使用上述相同命令启动新容器。

1. 打开应用。 你应会看到你的项目仍在列表中！

1. 查看完列表后，删除容器。

太好了！ 你现在已了解如何保留数据！

> [!TIP]
> 虽然命名卷和绑定装载（稍后我们将讨论它）是默认 Docker 引擎安装支持的两种主要类型的卷，但有许多卷驱动程序插件可用于支持 NFS、SFTP 和 NetApp 等！ 当你开始在群集环境中使用 Swarm 和 Kubernetes 等在多个主机上运行容器时，这一点尤其重要。

## <a name="dive-into-your-volume"></a>深入了解你的卷

很多人常常会问：“使用命名卷时，Docker 实际将数据存储在哪里？” 如果想知道，可使用 `docker volume inspect` 命令。

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

`Mountpoint` 是磁盘上实际存储数据的位置。 请注意在大多数计算机上，你需要有根目录访问权限才能从主机访问此目录。 但，事实就是这样！

> [!NOTE]
> **直接在 Docker Desktop 上访问卷数据** 在 Docker Desktop 中运行时，Docker 命令实际上在计算机上的小型虚拟机 (VM) 中运行。 若要查看 Mountpoint 目录的实际内容，首先需要进入该 VM。 在 WSL 2 中，这位于 WSL 2 发行版中，可通过文件资源管理器进行访问。

## <a name="recap"></a>概括

此时，你有一个可在重启后继续运行的应用程序！ 你可将其展示给投资者，希望他们对此感兴趣！

但你之前已了解，为每个更改重新生成映像需要相当长的时间。 有一种更好的方法来改变这种情况，对吧？ 更好的方法是使用绑定装载（前面提到过）！ 我们现在来看看吧！

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [使用绑定装载](use-bind-mounts.md)
