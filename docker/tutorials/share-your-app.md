---
title: Docker 教程 - 第 3 部分：共享应用
description: 介绍如何使用 Docker Hub 注册表共享 Docker 映像。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 46f91b3bf163f3847492a7727fa72a39908d441c
ms.sourcegitcommit: fb8babf5cd72f1fc2f97ffe4ad7b62d91f325f61
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2020
ms.locfileid: "89485530"
---
# <a name="share-your-app"></a>共享应用

现在我们已生成了映像，让我们来进行共享！ 要共享 Docker 映像，必须使用 Docker 注册表。 默认注册表为 Docker Hub，我们使用过的所有映像都源于此处。

## <a name="create-a-repo"></a>创建存储库

要推送映像，首先需要在 Docker Hub 上创建存储库。

1. 转到 [Docker Hub](https://hub.docker.com)，并在必要时登录。

1. 单击“创建存储库”按钮。

1. 关于存储库名称，请使用 `getting-started`。 确保将“可见性”设置为 `Public`。

1. 单击“创建”按钮！

在页面右侧，可看到名为“Docker 命令”的部分。 此部分提供了一个示例命令，需要运行该命令才能推送到此存储库。

![包含推送示例的 Docker 命令](media/push-command.png)

## <a name="push-the-image"></a>推送映像

1. 在命令行中，尝试运行在 Docker Hub 上看到的推送命令。 请注意，应在运行命令时使用你自己的命名空间，而不是“docker”。

    ```plaintext
    $ docker push docker/getting-started
    The push refers to repository [docker.io/docker/getting-started]
    An image does not exist locally with the tag: docker/getting-started
    ```

    为什么失败了？ 推送命令在查找名为 docker/getting-started 的映像，但并未找到。 如果运行 `docker image ls`，则不会出现此情况。

    要修复此问题，需要“标记”已生成的现有映像，为其指定一个不同的名称。

1. 使用 `docker login -u <username>` 命令登录 Docker Hub。

1. 使用 `docker tag` 命令为 `getting-started` 映像指定一个新名称。 确保将 `<username>` 替换为 Docker ID。

    ```bash
    docker tag getting-started <username>/getting-started
    ```

1. 现在再次尝试推送命令。 如果要从 Docker Hub 复制值，则可以删除 `tagname` 部分，因为并未向映像名称添加标记。 如果未指定标记，Docker 将使用名为 `latest` 的标记。

    ```bash
    docker push <username>/getting-started
    ```

    也可以在 Docker 视图的“映像”部分中右键单击映像标记，然后依次选择“推送...”、“连接注册表...”和“Docker Hub”，而不使用命令行。

## <a name="run-the-image-on-a-new-instance"></a>在新的实例上运行映像

现在已生成映像并将其推送到注册表中，请尝试在从未见过此容器映像的全新实例上运行应用！ 要进行此操作，将使用 Play with Docker。

1. 打开浏览器，转到 [Play with Docker](http://play-with-docker.com)。

1. 使用 Docker Hub 帐户登录。

1. 登录后，单击左侧栏中的“+ 添加新实例”链接。 （如果没有看到该链接，请将浏览器页面调宽一点。）几秒钟后，浏览器中会打开一个终端窗口。

    ![Play with Docker“添加新实例”](media/pwd-add-new-instance.png)

1. 在终端中，启动新推送的应用。

    ```bash
    docker run -dp 3000:3000 <username>/getting-started
    ```

    应该会看到映像已下推并最终启动！

1. 单击出现的 3000 徽章，应该可以看到带有修改内容的应用！ 太好了！ 如果未显示 3000 徽章，可单击“打开端口”按钮，并键入 3000。

## <a name="recap"></a>概括

本部分介绍了如何通过将映像推送到注册表来共享映像。 然后转到了一个全新的实例，并能够运行新推送的映像。 这在 CI 管道中非常常见，在此管道中，将创建映像并将其推送到注册表，然后生产环境可以使用映像的最新版本。

现在已你明了，回想一下在上一部分结束时，如果重启应用，你将丢失所有待办事项列表项。 这显然不是好的用户体验，因此接下来你将了解如何在重启时保留数据！

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [保留数据库](persist-your-data.md)