---
title: Docker 教程-第5部分：使用绑定装载
description: 描述如何使用 bind 装载来控制主机上的装入点。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 6474179a0714f2407ac37e724b997139206a91fb
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176676"
---
# <a name="use-bind-mounts"></a>使用 bind 装载

在上一章中，已了解并使用 **命名卷** 在数据库中保留数据。 如果只是想要存储数据，则命名卷非常好，因为无需担心数据的存储 *位置* 。

利用 **bind 装载**，可以控制主机上的确切装载点。 您可以使用它来持久保存数据，但通常用于向容器提供额外的数据。 在处理应用程序时，可以使用 bind 装载将源代码装载到容器中，让它查看代码更改和响应，并让你立即看到更改。

对于基于节点的应用程序， [nodemon](https://npmjs.com/package/nodemon) 是一种很好的工具，用于监视文件更改，然后重新启动应用程序。 在大多数其他语言和框架中都有等效的工具。

## <a name="quick-volume-type-comparisons"></a>快速卷类型比较

绑定装载和命名卷是 Docker 引擎附带的两种主要类型的卷。 不过，还可以使用额外的卷驱动程序来支持 ([SFTP](https://github.com/vieux/docker-volume-sshfs)、 [Ceph](https://ceph.com/geen-categorie/getting-started-with-the-docker-rbd-volume-plugin/)、 [NetApp](https://netappdvp.readthedocs.io/en/stable/)、 [S3](https://github.com/elementar/docker-s3-volume)及更) 的其他用例。

| 属性 | 命名卷 | 绑定挂载 |
| -------- | ------------- | ----------- |
| 主机位置 | Docker 选择 | 你控制 |
| 使用) 安装示例 (`-v` | 我的卷：/usr/本地/数据 | /path/to/data:/usr/local/data |
| 用容器内容填充新卷 | 是 | 否 |
| 支持卷驱动程序 | 是 | 否 |

## <a name="start-a-dev-mode-container"></a>启动开发模式容器

若要运行容器以支持开发工作流，请执行以下操作：

- 将源代码装载到容器中
- 安装所有依赖项，包括 "dev" 依赖项
- 启动 nodemon 以监视文件系统更改

1. 请确保没有任何以前 `getting-started` 运行的容器。

1. 运行以下命令 (` \ ` `` ` `` 在 Windows PowerShell 中将字符替换为) 。 你将了解以下内容：

    ```bash
    docker run -dp 3000:3000 \
        -w /app -v ${PWD}:/app \
        node:12-alpine \
        sh -c "yarn install && yarn run dev"
    ```

    - `-dp 3000:3000` -与以前相同。 在已分离 (后台) 模式下运行，并创建端口映射
    - `-w /app` -设置运行命令的 "工作目录" 或当前目录
    - `-v ${PWD}:/app`-bind 将当前目录从容器中的主机装载到目录中 `/app`
    - `node:12-alpine` -要使用的映像。 请注意，这是应用从 Dockerfile 的基本映像
    - `sh -c "yarn install && yarn run dev"` -命令。 我们正在使用 `sh` (alpine 没有 `bash`) 和运行 `yarn install` 来安装 *所有* 依赖项，然后运行 `yarn run dev` 。 如果你查看 `package.json` ，将看到 `dev` 脚本正在启动 `nodemon` 。

1. 您可以使用来监视日志 `docker logs -f <container-id>` 。 当您看到以下内容时，您将知道您已准备就绪：

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

    监视日志完成后，请按命中退出 `Ctrl` + `C` 。

1. 现在，请更改应用程序。 在 `src/static/js/app.js` 文件中，更改 " **添加项** " 按钮，只需说 " **添加**"。 此更改将位于第109行。

    ```diff
    -                         {submitting ? 'Adding...' : 'Add Item'}
    +                         {submitting ? 'Adding...' : 'Add'}
    ```

1. 只需刷新页面 (或将其打开) ，就能立即看到浏览器中反映的更改。 节点服务器可能需要几秒钟才能重新启动，因此，如果出现错误，请在几秒钟后尝试刷新。

    !["添加" 按钮的已更新标签的屏幕截图](media/updated-add-button.png)

1. 随意进行任何其他更改。 完成后，请停止容器并使用生成新映像 `docker build -t getting-started .` 。

对于本地开发设置，使用绑定装载 *非常* 常见。 优点在于开发计算机无需安装所有生成工具和环境。 使用单个 `docker run` 命令，开发环境会被拉取并准备就绪。 你将在以后的步骤中了解 Docker Compose，因为这将有助于简化你的命令 (你已经获得了大量标志) 。

## <a name="recap"></a>概括

此时，你可以保留数据库并快速响应投资者和创始人的需求和需求。 个万岁! 但猜到什么呢？ 您收到了精彩新闻！

**你的项目已选择以供将来开发！**

若要为生产做好准备，需要将数据库从 SQLite 迁移到可以更好地扩展的内容。 为简单起见，你将继续使用关系数据库，并切换应用程序以使用 MySQL。 但如何运行 MySQL 呢？ 如何允许容器相互通信？ 接下来将了解相关信息！

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [多容器应用](multi-container-apps.md)