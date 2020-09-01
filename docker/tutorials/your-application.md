---
title: Docker 教程-第1部分：生成并运行待办事项列表示例应用
description: Node.js 中运行的待办事项列表示例应用的概述。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: b8470c8d7708bc51916a6f57f5aa135c3267e355
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176677"
---
# <a name="build-and-run-the-todo-sample-app"></a>生成并运行 todo 示例应用

在本教程的其余部分中，你将使用在 Node.js 中运行的简单待办事项列表管理器。 如果你不熟悉 Node.js，别担心！ 不需要真正的 JavaScript 体验！

此时，你的开发团队非常小，你只是构建一个应用来证明你的 MVP (最小可行的产品) 。 您想展示它的工作原理以及它能够执行的操作，而无需考虑它如何适用于大型团队、多个开发人员等。

![待办事项列表管理器屏幕快照](media/todo-list-sample.png)

## <a name="get-the-app"></a>获取应用

在运行应用程序之前，需要将应用程序源代码获取到计算机上。 对于实际项目，通常将克隆存储库。 但在本教程中，您已创建了一个包含该应用程序的 ZIP 文件。

1. [下载 ZIP](/assets/app.zip)。 打开 ZIP 文件，确保提取内容。

1. 提取后，使用你最喜欢的代码编辑器打开项目。 如果你需要一个编辑器，则可以使用 [Visual Studio Code](https://code.visualstudio.com/)。 应该会看到 `package.json` 和两个子目录 (`src` 和 `spec`) 。

    ![加载了应用程序 Visual Studio Code 打开的屏幕截图](media/ide-screenshot.png)

## <a name="building-the-apps-container-image"></a>构建应用的容器映像

若要生成应用程序，需要使用 `Dockerfile` 。 Dockerfile 只是一种基于文本的说明脚本，用于创建容器映像。 如果你之前创建了 Dockerfile，则可能会在下面的 Dockerfile 中看到一些缺点。 不过，别担心！ 我们将通过它们。

1. `Dockerfile`在包含以下内容的文件所在的文件夹中创建名为的文件 `package.json` 。

    ```dockerfile
    FROM node:12-alpine
    WORKDIR /app
    COPY . .
    RUN yarn install --production
    CMD ["node", "/app/src/index.js"]
    ```

    请检查文件 `Dockerfile` 是否没有文件扩展名 `.txt` ，例如。 某些编辑器可能会自动附加此文件扩展名，这会导致在下一步中出现错误。

1. 如果尚未执行此操作，请打开终端并使用发送到该 `app` 目录 `Dockerfile` 。 现在使用命令构建容器映像 `docker build` 。

    ```bash
    docker build -t getting-started .
    ```

    此命令使用 Dockerfile 来生成新的容器映像。 您可能已注意到，已经下载了很多 "层"。 这是因为您指示要从图像中启动的生成器 `node:12-alpine` 。 但由于您的计算机上没有该映像，因此需要下载该映像。

    下载映像后，会在应用程序中复制并用于 `yarn` 安装应用程序的依赖项。 `CMD`指令指定从此映像启动容器时要运行的默认命令。

    最后， `-t` 标志标记为图像。 将此视为最终映像的用户可读名称。 由于已命名了映像 `getting-started` ，因此在运行容器时，可以引用该图像。

    `.`命令末尾处的 `docker build` 指示 Docker 应该 `Dockerfile` 在当前目录中查找。

## <a name="starting-an-app-container"></a>启动应用容器

现在，你已有了一个映像，请运行该应用程序！ 为此，请使用 `docker run` 命令 (记住，从早期版本开始 ) 。

1. 使用命令启动容器 `docker run` ，并指定刚创建的映像的名称：

    ```bash
    docker run -dp 3000:3000 getting-started
    ```

    记住 `-d` 和 `-p` 标志？ 你正在 "已分离" 模式下运行新容器 (在后台) ，并在主机的端口3000与容器的端口3000之间创建映射。 如果没有端口映射，将无法访问该应用程序。

1. 几秒钟后，请在 web 浏览器中打开 [http://localhost:3000](http://localhost:3000) 。
    应该会看到应用！

    ![空的待办事项列表](media/todo-list-empty.png)

1. 继续操作并添加一个或两个项目，看看它按预期方式工作。 可以将项标记为 "完成" 和 "移除项"。 前端已成功存储后端中的项！ 很简单，是吧？

此时，您应该有一个正在运行的待办事项列表管理器，其中包含一些项，所有项目均由您生成！ 现在，让我们进行一些更改，了解如何管理容器。

如果你快速查看 VS Code 扩展，你应该会看到你现在运行的两个容器 (本教程和刚刚启动的应用容器) ！

![运行教程和应用容器的 Docker 扩展](media/vs-two-containers.png)

## <a name="recap"></a>概括

本部分介绍了构建容器映像并创建了 Dockerfile 的基础知识。 构建映像后，开始使用容器并看到正在运行的应用！

接下来，你将修改应用程序，并了解如何使用新映像更新正在运行的应用程序。 在此过程中，您将学习其他一些有用的命令。

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [更新应用](update-your-app.md)