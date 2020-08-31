---
title: Docker 教程-第2部分：更新应用
description: 介绍如何更新 Docker 应用。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 4a1cba71481608803522336ad5c0f6b6354bca32
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176681"
---
# <a name="update-the-app"></a>更新应用

作为小型功能请求，如果没有任何待办事项列表项，产品团队会要求你更改 "空文本"。 他们要将其转换为以下内容：

> 尚未获得 todo 项！ 在上面添加一个！

非常简单，对吧？ 我们来做更改。

## <a name="update-the-source-code"></a>更新源代码

1. 在 `src/static/js/app.js` 文件中，将第56行更新为使用新的空文本。

    ```diff
    -                <p className="text-center">No items yet! Add one above!</p>
    +                <p className="text-center">You have no todo items yet! Add one above!</p>
    ```

1. 使用之前使用的相同命令生成映像的更新版本。

    ```bash
    docker build -t getting-started .
    ```

1. 使用更新的代码启动新的容器。

    ```bash
    docker run -dp 3000:3000 getting-started
    ```

**哎呀！** 你可能会看到类似于下面的错误 (Id 将不同) ：

```bash
docker: Error response from daemon: driver failed programming external connectivity on endpoint laughing_burnell 
(bb242b2ca4d67eba76e79474fb36bb5125708ebdabd7f45c8eaf16caaabde9dd): Bind for 0.0.0.0:3000 failed: port is already allocated.
```

那么，会发生什么情况呢？ 新容器无法启动，因为你的旧容器仍在运行。 出现这种问题的原因是，该容器使用的是主机端口3000，并且计算机上只有一个进程 (容器) 可以侦听特定端口。 若要解决此问题，请删除旧容器。

## <a name="replace-the-old-container"></a>替换旧容器

若要删除容器，首先需要停止此容器。 停止后，可以将其删除。 可以通过两种方式删除旧容器。 可以随意选择最适合的路径。

### <a name="remove-a-container-using-the-cli"></a>使用 CLI 删除容器

1. 使用命令获取容器的 ID `docker ps` 。

    ```bash
    docker ps
    ```

1. 使用 `docker stop` 命令停止容器。

    ```bash
    # Swap out <the-container-id> with the ID from docker ps
    docker stop <the-container-id>
    ```

1. 容器停止后，可以使用命令将其删除 `docker rm` 。

    ```bash
    docker rm <the-container-id>
    ```

> [!TIP]
> 可以通过将 "强制" 标志添加到命令，在单个命令中停止和删除容器 `docker rm` 。 例如：`docker rm -f <the-container-id>`

### <a name="remove-a-container-using-the-docker-dashboard"></a>使用 Docker 面板删除容器

如果打开 VS Code 扩展，则可以通过两次单击删除容器！ 当然，必须查找容器 ID 并将其删除。

1. 打开扩展后，导航到容器并右键单击。

1. 单击 " **删除** " 选项。

1. 确认删除操作已完成！

![Docker 仪表板-删除容器](media/vs-removing-container.png)

### <a name="start-the-updated-app-container"></a>启动更新的应用容器

1. 现在，请启动更新后的应用程序。

    ```bash
    docker run -dp 3000:3000 getting-started
    ```

1. 刷新您的浏览器 [http://localhost:3000](http://localhost:3000) ，您应该会看到更新的帮助文本！

![更新的应用程序包含更新的空文本](media/todo-list-updated-empty-text.png)

## <a name="recap"></a>概括

虽然你可以构建更新，但你可能已经注意到了两个问题：

- 待办事项列表中的所有现有项都已消失！ 这并不是一个很好的应用！ 稍后我们将对此进行讨论。
- 此类小更改涉及到 *许多* 步骤。 在即将推出的部分中，你将了解如何在每次进行更改时，无需重新生成并启动新容器即可查看代码更新。

在了解暂留之前，你将迅速了解如何与他人共享这些图像。

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [共享应用](share-your-app.md)
