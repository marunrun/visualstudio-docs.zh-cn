---
title: R 和 Docker 容器
description: 如何在 Visual Studio 中设置适用于 R 的 Docker 容器并连接至这些容器。
ms.date: 12/04/2017
ms.topic: conceptual
author: kraigb
ms.author: kraigb
ms.reviewer: karthiknadig
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 8c5b4278ab50aac96703f03e74c014d29831f22e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62810117"
---
# <a name="use-docker-containers-with-r-tools-for-visual-studio"></a>配合使用 Docker 容器和针对 Visual Studio 的 R 工具

针对 Visual Studio 的 R 工具 (RTVS) 版本 1.3+ 同[Docker for Windows](https://www.docker.com/docker-windows) 一起安装，支持使用 Docker 容器。

## <a name="create-a-container"></a>创建容器

1. 选择“工作区”窗口（“R 工具” > “窗口” > “工作区”）右上角的“容器”按钮      。 如果未安装 Docker for Windows，则窗口中会显示通知，并提供下载链接。 安装 Docker 可能需要重启计算机。

    ![针对 Visual Studio 的 R 工具 (VS2017) 中的工作区窗口，其中包含“容器”命令](media/container-workspaces-window.png)

1. 在“容器”窗口中，选择“创建”   ：

    ![在“容器”窗口中创建命令](media/containers-window-create.png)

1. 在对话框中填写所需信息并选择“创建”  。 输入的凭据也用于在 Linux 上创建帐户，稍后登录时可使用此帐户。

    ![在创建容器时输入容器名称和凭据](media/containers-window-create-fill.png)

1. RTVS 生成映像需要一些时间。 Visual Studio 中的“输出”窗口显示进程，但是在下载较长映像时可能不会有太大作用，请做好耐心等待的准备  。 生成映像后，RTVS 启动容器，该容器随即出现在“容器”窗口中  。 右侧的控件可停止、删除和重启容器。

    ![显示完整容器的容器窗口](media/containers-window-created.png)

## <a name="connect-to-a-container"></a>连接到容器

1. “工作区”窗口的“本地运行容器”部分显示在端口 5444 上运行 RTVS 守护程序的容器   。 （有关如何配置守护程序的详细信息，请参阅[适用于 Linux 的远程 R Server](setting-up-remote-r-service-on-linux.md)。）

    ![显示可用容器的工作区窗口](media/workspaces-window-running-containers.png)

1. 要连接到容器，请双击容器名称或选择右侧的向前箭头按钮。 连接后，可看见“R 交互”窗口（请参阅[使用 R 交互窗口](interactive-repl-for-r-in-visual-studio.md)）  ：

    ![针对容器打开的工作区窗口和 REPL 窗口](media/workspaces-window-container-connected.png)

## <a name="use-custom-built-images"></a>使用自定义生成的映像

RTVS 可检测使用自定义生成的映像（例如以下 docker 文件中描述的 microsoft/rtvs 映像）创建的容器，并支持对其进行管理。 此处使用的基础映像预先安装了 rtvs-daemon、R 3.4.2 和通用 R 程序包。 **注意**：可根据需要更改此处显示的用户名和密码。

```docker
FROM microsoft/rtvs:1.3-ub1604-r3.4.2
RUN useradd --create-home ruser1
RUN echo "ruser1:foobar" | chpasswd

#Install additional R packages. You may have to install OS dependencies, see package info or error messages during build.
#RUN Rscript --vanilla -e "install.packages(c('AzureML','wordcloud'), repos = 'http://cran.us.r-project.org');"
```

使用以下命令生成映像，根据需要更改容器名称（`--name` 参数）：

```bash
docker build -t my-rtvs-image:latest .
docker run -p 6056:5444 --name my-rtvs-container my-rtvs-image:latest rtvsd
```

`-p 6056:5444` 参数将端口 6056 映射到内部端口 5444，以便 RTVS 检测 rtvs-daemon。 “工作区”窗口中列出了公开容器端口 5444 的所有容器  。 然后可以使用“工作区”窗口，通过用户名 `<<unix>>\ruser1` 和密码“foobar”连接到容器，除非在 docker 文件中指定了不同的凭据  。
