---
title: Docker 教程 - 第 2 部分：更新应用程序
description: 介绍如何更新 Docker 应用。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: e8f17047902ccf6c7fad164e788e64fe0b17cf14
ms.sourcegitcommit: fb8babf5cd72f1fc2f97ffe4ad7b62d91f325f61
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2020
ms.locfileid: "89485423"
---
# <a name="update-the-app"></a>更新应用

产品团队提出了一个小的功能请求，要求更改在没有任何待办事项的情况下显示的“空文本”。 他们希望将其转换为以下内容：

> 你还没有待办事项！ 在上面添加一个！

非常简单，对吧？ 接下来进行更改。

## <a name="update-the-source-code"></a>更新源代码

1. 在 `src/static/js/app.js` 文件中，更新第 56 行以使用新的空文本。

    ```diff
    -                <p className="text-center">No items yet! Add one above!</p>
    +                <p className="text-center">You have no todo items yet! Add one above!</p>
    ```

1. 使用之前使用的相同命令生成映像的更新版本。

    ```bash
    docker build -t getting-started .
    ```

1. 使用更新后的代码启动新容器。

    ```bash
    docker run -dp 3000:3000 getting-started
    ```

**哎呀！** 可能会显示以下错误（ID 将有所不同）：

```bash
docker: Error response from daemon: driver failed programming external connectivity on endpoint laughing_burnell 
(bb242b2ca4d67eba76e79474fb36bb5125708ebdabd7f45c8eaf16caaabde9dd): Bind for 0.0.0.0:3000 failed: port is already allocated.
```

发生了什么情况？ 新容器无法启动，因为旧容器仍在运行。 出现这种问题的原因是该容器正在使用主机的端口 3000，并且计算机上只有一个进程（包括容器）可以侦听特定端口。 若要解决此问题，请删除旧容器。

## <a name="replace-the-old-container"></a>替换旧容器

若要删除容器，首先需要停止此容器。 容器停止后才可将其删除。 可通过两种方式删除旧容器。 根据需要选择最适合的路径。

### <a name="remove-a-container-using-the-cli"></a>使用 CLI 删除容器

1. 使用 `docker ps` 命令获取容器的 ID。

    ```bash
    docker ps
    ```

1. 使用 `docker stop` 命令停止容器。

    ```bash
    # Swap out <the-container-id> with the ID from docker ps
    docker stop <the-container-id>
    ```

1. 容器停止后，可使用 `docker rm` 命令将其删除。

    ```bash
    docker rm <the-container-id>
    ```

> [!TIP]
> 可通过将“force”标志添加到 `docker rm` 命令，使用单个命令停止和删除容器。 例如：`docker rm -f <the-container-id>`

### <a name="remove-a-container-using-the-docker-view"></a>使用 Docker 视图删除容器

如果打开了 VS Code 扩展，可通过两次单击删除容器！ 这肯定比查找容器 ID 并将其删除要容易得多。

1. 打开扩展后，导航到容器并右键单击。

1. 单击“删除”选项。

1. 确认删除后，大功告成！

![Docker 视图 - 删除容器](media/vs-removing-container.png)

### <a name="start-the-updated-app-container"></a>启动更新后的应用容器

1. 现在启动更新后的应用。

    ```bash
    docker run -dp 3000:3000 getting-started
    ```

1. 在 [http://localhost:3000](http://localhost:3000) 刷新浏览器，应该会显示更新后的帮助文本！

![更新后的应用程序包含更后新的空文本](media/todo-list-updated-empty-text.png)

## <a name="recap"></a>概括

虽然你可以生成更新，但你可能已注意到两个问题：

- 待办事项列表中的所有现有项都已消失！ 这并不是一个很好的应用！ 稍后我们将讨论这一点。
- 如此小的更改涉及很多步骤。 在下一部分中，你将了解如何无需每次进行更改时重新生成和启动新容器即可实现代码更新。

在了解“暂留”之前，你将快速了解如何与他人共享这些映像。

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [共享应用](share-your-app.md)
