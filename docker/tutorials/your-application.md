---
title: Docker 教程 - 第 1 部分：生成并运行待办事项列表示例应用
description: 概述在 Node.js 中运行的待办事项列表示例应用。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: b8470c8d7708bc51916a6f57f5aa135c3267e355
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89176677"
---
# <a name="build-and-run-the-todo-sample-app"></a>生成并运行待办事项示例应用

在本教程的其余部分中，你将使用在 Node.js 中运行的简单待办事项列表管理器。 如果你不熟悉 Node.js，别担心！ 我们并不需要实际的 JavaScript 经验！

当前，你的开发团队规模很小，你只需构建一个应用来证明 MVP（最低可行产品）。 你想要展示它的工作原理和功能，而不考虑它如何为大型团队、多个开发者等工作。

![待办事项列表管理器屏幕截图](media/todo-list-sample.png)

## <a name="get-the-app"></a>获取应用

在运行应用程序之前，需要将应用程序源代码放到计算机上。 对于实际项目，通常会克隆存储库。 但在本教程中，你已创建了包含应用程序的 ZIP 文件。

1. [下载 ZIP](/assets/app.zip)。 打开 ZIP 文件，并确保将内容解压缩。

1. 解压缩后，使用你最喜爱的代码编辑器打开项目。 如果需要编辑器，可以使用 [Visual Studio Code](https://code.visualstudio.com/)。 你应该会看到 `package.json` 和两个子目录（`src` 和 `spec`）。

    ![Visual Studio Code 打开并加载了应用的屏幕截图](media/ide-screenshot.png)

## <a name="building-the-apps-container-image"></a>生成应用的容器映像

若要生成应用程序，需要使用 `Dockerfile`。 Dockerfile 只是用于创建容器映像的指令脚本，它基于文本。 如果你以前创建过 Dockerfile，可能会在下面的 Dockerfile 中发现一些缺陷。 但是，不必担心！ 我们会仔细检查它们。

1. 在与文件 `package.json` 相同的文件夹中创建一个名为 `Dockerfile` 的文件，并包含以下内容。

    ```dockerfile
    FROM node:12-alpine
    WORKDIR /app
    COPY . .
    RUN yarn install --production
    CMD ["node", "/app/src/index.js"]
    ```

    请检查文件 `Dockerfile` 是否没有类似于 `.txt` 的文件扩展名。 某些编辑器可能会自动追加此文件扩展名，这会导致下一步出现错误。

1. 如果尚未执行此操作，请打开终端，然后转到包含 `Dockerfile` 的 `app` 目录。 现在，使用 `docker build` 命令生成容器映像。

    ```bash
    docker build -t getting-started .
    ```

    此命令使用 Dockerfile 生成新的容器映像。 你可能已经注意到，下载了很多“层”。 这是因为你指示生成器从 `node:12-alpine` 映像开始。 但是，由于你的计算机上没有该映像，因此需要下载该映像。

    下载映像后，你将映像复制到了自己的应用程序中，然后使用 `yarn` 安装了应用程序的依赖项。 `CMD` 指令指定从此映像启动容器时要运行的默认命令。

    最后，`-t` 标志标记你的映像。 可以简单地把这想象为最终映像的用户可读名称。 由于你将映像命名为 `getting-started`，因此可以在运行容器时引用该映像。

    `docker build` 命令末尾的 `.` 告诉 Docker 应在当前目录中查找 `Dockerfile`。

## <a name="starting-an-app-container"></a>启动应用容器

现在你已拥有映像，可以运行应用程序了！ 为此，请使用 `docker run` 命令（还记得前面的命令吗？）。

1. 使用 `docker run` 命令启动容器，并指定刚刚创建的映像的名称：

    ```bash
    docker run -dp 3000:3000 getting-started
    ```

    还记得 `-d` 和 `-p` 标志吗？ 你以“分离”模式（在后台）运行新容器，并在主机的端口 3000 到容器的端口 3000 之间创建映射。 如果没有端口映射，你将无法访问应用程序。

1. 几秒后，打开 Web 浏览器转到 [http://localhost:3000](http://localhost:3000)。
    你应该会看到应用！

    ![空待办事项列表](media/todo-list-empty.png)

1. 继续添加一两个项，看看它是否按预期工作。 可以将项标记为完成项和删除项。 前端已成功将项存储在后端！ 很简单，是吧？

此时，你应有一个正在运行的待办事项列表管理器，其中包含几个项，这些项全部由你生成！ 现在，让我们做一些更改，并了解如何管理容器。

如果你快速查看 VS Code 扩展，你应该会看到两个容器正在运行（此教程容器和你刚启动的应用容器）！

![正在运行教程容器和应用容器的 Docker 扩展](media/vs-two-containers.png)

## <a name="recap"></a>概括

在这一小节中，你了解了有关生成容器映像的基础知识，并为此创建了 Dockerfile。 生成映像后，你启动了容器并看到了正在运行的应用！

接下来，你将对应用进行修改，并了解如何使用新映像更新正在运行的应用程序。 在此过程中，你将了解其他一些有用的命令。

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [更新应用](update-your-app.md)