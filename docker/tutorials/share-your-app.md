---
title: Docker 教程-第3部分：共享你的应用
description: 介绍如何使用 Docker Hub 注册表共享 Docker 映像。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: d5bd7a2d79bf6da710fd0f5803c2415781160143
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176679"
---
# <a name="share-your-app"></a>共享应用

现在，我们已构建了一个映像，接下来让我们分享！ 若要共享 Docker 映像，必须使用 Docker 注册表。 默认注册表为 Docker Hub，并是所有已使用的映像来自的位置。

## <a name="create-a-repo"></a>创建存储库

若要推送映像，首先需要在 Docker Hub 上创建存储库。

1. 如果需要，请参阅 [Docker Hub](https://hub.docker.com) 并登录。

1. 单击 " **创建存储库** " 按钮。

1. 对于存储库名称，请使用 `getting-started` 。 请确保可见性为 `Public` 。

1. 单击 " **创建** " 按钮！

如果你查看该页的右侧，你会看到一个名为 **Docker 命令**的部分。 这将提供一个示例命令，你需要运行该命令来推送到此存储库。

![带推送示例的 Docker 命令](media/push-command.png)

## <a name="push-the-image"></a>推送映像

1. 在命令行中，尝试运行在 Docker Hub 上看到的推送命令。 请注意，你的命令将使用你的命名空间，而不是 "docker"。

    ```plaintext
    $ docker push docker/getting-started
    The push refers to repository [docker.io/docker/getting-started]
    An image does not exist locally with the tag: docker/getting-started
    ```

    为什么会失败？ 推送命令正在查找名为 docker/入门的映像，但找不到该映像。 如果运行 `docker image ls` ，则不会显示任何一个。

    若要解决此问题，需要 "标记" 现有映像，以便为其指定其他名称。

1. 使用命令登录到 Docker 中心 `docker login -u <username>` 。

1. 使用 `docker tag` 命令为 `getting-started` 图像指定一个新名称。 请确保用 `<username>` DOCKER ID 替换。

    ```bash
    docker tag getting-started <username>/getting-started
    ```

1. 现在尝试再次尝试推送命令。 如果要从 Docker 中心复制值，则可以删除该 `tagname` 部分，因为未向映像名称添加标记。 如果未指定标记，Docker 将使用名为的标记 `latest` 。

    ```bash
    docker push <username>/getting-started
    ```

## <a name="run-the-image-on-a-new-instance"></a>在新实例上运行映像

既然已生成映像并将其推送到注册表中，请尝试在从未见过此容器映像的全新实例上运行该应用！ 为此，你将使用 Play with Docker。

1. 打开浏览器以 [播放 Docker](http://play-with-docker.com)。

1. 用 Docker 中心帐户登录。

1. 登录后，单击左侧栏中的 "+ 添加新实例" 链接。  (如果看不到，请将浏览器稍微缩小一次。 ) 几秒钟后，浏览器中将打开一个终端窗口。

    ![播放 Docker 添加新实例](media/pwd-add-new-instance.png)

1. 在终端中，启动刚刚推送的应用。

    ```bash
    docker run -dp 3000:3000 <username>/getting-started
    ```

    你应会看到图像已拉取并最终启动！

1. 出现3000徽章后，请单击它，你会看到该应用进行修改！ 个万岁! 如果未显示3000徽章，可以单击 " **打开端口** " 按钮，然后键入3000。

## <a name="recap"></a>概括

本部分介绍了如何通过将映像推送到注册表来共享映像。 然后，你将转到一个新的实例，并且能够运行刚刚推送的映像。 这在 CI 管道中非常常见，在此管道中，管道将创建映像并将其推送到注册表，然后生产环境可以使用最新版本的映像。

至此，你已明白了，请记住，在最后一部分结束时，重新启动应用后，你将丢失所有 todo 列表项。 这显然不是一个很好的用户体验，因此你将了解如何在重新启动后保存数据！

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [持久保存数据库](persist-your-data.md)