---
title: Docker 教程-Docker 入门
description: 多步骤教程，其中介绍了使用 Docker 与 Visual Studio Code 相关的基础知识。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
next_page: app.md
ms.openlocfilehash: 9961810ad408a384db46439235b0b7acab325062
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176680"
---
# <a name="tutorial-get-started-with-docker"></a>教程： Docker 入门

在本教程中，你将了解如何创建和部署 Docker 应用，包括使用多个包含数据库的容器，以及如何使用 Docker Compose。 你还可以将容器化应用部署到 Azure。

## <a name="start-the-tutorial"></a>开始教程

如果已运行该命令以开始学习教程，恭喜！  如果没有，请打开命令提示符或 bash 窗口，并运行以下命令：

```cli
docker run -d -p 80:80 docker/getting-started
```

你会注意到使用了几个标志。 下面是一些详细信息：

- `-d` -在后台运行处于分离模式 (容器) 
- `-p 80:80` -将主机的端口80映射到容器中的端口80
- `docker/getting-started` -要使用的映像

> [!TIP]
> 可以合并单字符标志以缩短完整命令。
> 例如，可以将上面的命令编写为：
>
> ```cli
> docker run -dp 80:80 docker/getting-started
> ```

## <a name="the-vs-code-extension"></a>VS Code 扩展

在开始之前，我们想要突出显示 Docker VS Code 扩展，这使你可以快速查看计算机上运行的容器。 它使你可以快速访问容器日志，让你可以在容器中获取 shell，并使你能够轻松管理容器生命周期， (停止、删除等) 。

若要访问该扩展，请按照 [此处](https://code.visualstudio.com/docs/containers/overview)的说明进行操作。 使用左侧的 Docker 图标打开 Docker 视图。 如果现在打开扩展，将看到此教程正在运行！ 以下 (容器名称 `angry_taussig`) 为随机创建的名称。 因此，您很可能会有不同的名称。

![在 Docker 扩展中运行的教程容器](media/vs-tutorial-in-extension.png)

## <a name="what-is-a-container"></a>什么是容器

现在，你已运行容器，什么 *是* 容器？ 简而言之，容器只是计算机上的另一个进程，该进程与主机上的所有其他进程隔离。 此隔离利用 [内核命名空间和 cgroups](https://medium.com/@saschagrunert/demystifying-containers-part-i-kernel-space-2c53d6979504)，这些功能已在 Linux 中长时间使用。 Docker 已努力使这些功能易学，易于使用。

> [!NOTE]
> **从头开始创建容器** 如果你想要了解如何从头开始构建容器，Liz 大米的安全性包含一个在其中从头开始创建容器的视频：
>
> [!VIDEO https://www.youtube-nocookie.com/embed/8fi7uSYlOdc]

## <a name="what-is-a-container-image"></a>什么是容器映像

运行容器时，它使用独立的文件系统。 此自定义文件系统由 **容器映像**提供。 由于映像包含容器的文件系统，因此它必须包含运行应用程序所需的所有项目-所有依赖项、配置、脚本、二进制文件等。 映像还包含容器的其他配置，例如环境变量、要运行的默认命令以及其他元数据。

稍后我们将深入探讨映像，涵盖分层、最佳实践等主题。

> [!NOTE]
> 如果你熟悉 `chroot` ，请将容器视为的扩展版本 `chroot` 。 文件系统只是来自映像。 但是，当只使用 chroot 时，容器会添加其他隔离。

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [应用程序](your-application.md)
