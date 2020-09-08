---
title: Docker 教程 - 第 5 部分：使用绑定装载
description: 介绍如何使用绑定装载来控制主机上的装载点。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 6474179a0714f2407ac37e724b997139206a91fb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89176676"
---
# <a name="use-bind-mounts"></a>使用绑定装载

在上一章中，你已了解并使用命名卷将数据保留在数据库中。 如果只是想要存储数据，则命名卷非常有用，因为你不必担心数据的存储位置。

使用绑定装载，你可以控制主机上的确切装载点。 你可以使用它来保留数据，但是它通常用于向容器提供其他数据。 在处理应用程序时，你可以使用绑定装载将源代码装载到容器中，以使其查看代码更改、做出响应并让你立即看到更改。

对于基于节点的应用程序，[nodemon](https://npmjs.com/package/nodemon) 是查看文件更改，然后重启应用程序的好工具。 大多数其他语言和框架中都有等效的工具。

## <a name="quick-volume-type-comparisons"></a>快速卷类型比较

绑定装载和命名卷是 Docker 引擎附带的两种主要卷类型。 但是，还可以使用其他卷驱动程序来支持其他用例（[SFTP](https://github.com/vieux/docker-volume-sshfs)、[Ceph](https://ceph.com/geen-categorie/getting-started-with-the-docker-rbd-volume-plugin/)、[NetApp](https://netappdvp.readthedocs.io/en/stable/)、[S3](https://github.com/elementar/docker-s3-volume) 等）。

| 属性 | 命名卷 | 绑定挂载 |
| -------- | ------------- | ----------- |
| 主机位置 | Docker 选择 | 由你控制 |
| 装载示例（使用 `-v`） | my-volume:/usr/local/data | /path/to/data:/usr/local/data |
| 使用容器内容填充新卷 | 是 | 否 |
| 支持卷驱动程序 | 是 | 否 |

## <a name="start-a-dev-mode-container"></a>启动开发模式容器

要运行容器以支持开发工作流，请执行以下操作：

- 将源代码装载到容器中
- 安装所有依赖项，包括“dev”依赖项
- 启动 nodemon 以查看文件系统更改

1. 请确保没有运行任何以前的 `getting-started` 容器。

1. 运行以下命令（在 Windows PowerShell 中，请将 ` \ ` 字符替换为 `` ` ``）。 你将了解接下来会发生什么：

    ```bash
    docker run -dp 3000:3000 \
        -w /app -v ${PWD}:/app \
        node:12-alpine \
        sh -c "yarn install && yarn run dev"
    ```

    - `-dp 3000:3000` - 与以前相同。 在分离（后台）模式下运行并创建端口映射
    - `-w /app` - 设置运行命令的“工作目录”或当前目录
    - `-v ${PWD}:/app` - 将当前目录从容器中的主机绑定装载到 `/app` 目录
    - `node:12-alpine` - 要使用的映像。 请注意，这是 Dockerfile 中应用的基本映像
    - `sh -c "yarn install && yarn run dev"` - 命令。 我们正在使用 `sh`（alpine 没有 `bash`）启动 shell，并运行 `yarn install` 来安装所有依赖项，然后运行 `yarn run dev`。 如果你查看 `package.json`，将看到 `dev` 脚本正在启动 `nodemon`。

1. 可以使用 `docker logs -f <container-id>` 来查看日志。 当你看到以下内容时，便知道自己已准备就绪：

    ```bash
    docker logs -f <container-id>
    $ nodemon src/index.js
    [nodemon] 1.19.2
    [nodemon] to restart at any time, enter `rs`
    [nodemon] watching dir(s): *.*
    [nodemon] starting `node src/index.js`
    Using sqlite database at /etc/todos/todo.db
    Listening on port 3000
    ```

    查看完日志后，请按 `Ctrl`+`C` 退出。

1. 现在，对应用进行更改。 在 `src/static/js/app.js` 文件中，将“添加项”按钮更改为“添加” 。 此更改将位于第 109 行。

    ```diff
    -                         {submitting ? 'Adding...' : 'Add Item'}
    +                         {submitting ? 'Adding...' : 'Add'}
    ```

1. 只需刷新页（或打开页），就可以立即在浏览器中看到所做的更改。 节点服务器可能需要几秒钟才能重启，因此，如果出现错误，请在几秒钟后尝试刷新。

    ![更新后的“添加”按钮标签的屏幕截图](media/updated-add-button.png)

1. 你可以随意进行任何其他所需更改。 完成后，请停止容器并使用 `docker build -t getting-started .` 生成新映像。

使用绑定装载在本地开发设置中非常常见。 其优点是开发计算机无需安装所有生成工具和环境。 使用单个 `docker run` 命令，将会拉取开发环境并准备就绪。 你将在以后的步骤中了解 Docker Compose，因为这将有助于简化你的命令（你已经获得了许多标志）。

## <a name="recap"></a>概括

此时，你可以保留数据库并快速响应投资者和创始人的需求。 太好了！ 但你知道吗？ 我们收到了好消息！

你的项目已被选中用于未来开发！

为了准备进行生产，你需要将数据库从 SQLite 迁移到可以更好缩放的位置。 为简单起见，你将保留关系数据库并切换应用程序，以使用 MySQL。 但是如何运行 MySQL？ 如何允许容器相互通信？ 接下来将你了解相关信息！

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [多容器应用](multi-container-apps.md)