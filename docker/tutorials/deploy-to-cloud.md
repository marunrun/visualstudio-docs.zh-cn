---
title: Docker 教程 - 第 9 部分：部署到云
description: 将 docker 应用部署到云服务中进行托管。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 661f9f6833b5ac5d42aacde7f228b042bef00bb0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89176689"
---
# <a name="deploy-to-the-cloud"></a>部署到云

你已在本地运行了应用，可以开始考虑在云中运行，以便其他人访问和使用。 为此，将使用 Docker 上下文。 上下文是指当前正在使用容器的位置。 现在只有“默认”上下文，因此需要添加云上下文并将应用部署到其中。

## <a name="create-your-cloud-context"></a>创建云上下文

1. 首先，可通过查看 Docker 面板的上下文部分来查看已有的上下文：

   ![仅显示默认上下文](media/defaultcontext.png)

应该只能看到本地工作的默认上下文。

1. 要部署到云，需要创建新的 ACI 上下文，但要执行此操作，首先需要使用 Azure 帐户扩展对 Azure 进行身份验证。

   ![添加 Azure 扩展](media/addazureextension.png)

如果还没有 Azure 帐户，需要先设置一个。

1. 现在可以创建新的 ACI 上下文。 可通过单击 Docker 视图“上下文”部分的加号按钮来执行此操作。

   ![创建 ACI 上下文](media/createnewcontext.png)

系统随即询问你想要在哪个资源组下运行这些容器。 使用箭头键选择现有组，或使用默认选项以使用新组。

![选择资源组](media/selectresourcegroup.png)

现在可看到列出的 ACI 上下文，并且可以右键单击该上下文，使其成为当前获得焦点/正在使用的上下文：

![可选择新的 ACI 上下文](media/listofcontexts.png)

## <a name="run-containers-in-the-cloud"></a>在云中运行容器

1. 现在，使用 ACI 上下文并运行容器。

   ```bash
   docker context use myacicontext
   docker run  -dp 3000:3000 <username>/getting-started
   ```

1. 运行此容器后，请查看上下文中的容器。

   ![在 ACI 上下文中运行的容器](media/contextcontainer.png)

1. 要检查此容器是否正常运行，可以右键单击正在运行的容器，然后选择“在浏览器中查看”。

   ![ACL 中使用公共 IP 的容器](media/containerinaci.png)

可以看到容器使用公共 IP 运行并且正常运行！

1. 现在可查看正在运行的容器，以查看其工作方式。 可以首先查看容器日志：
 
 ```bash
   docker logs distracted-jackson
   ```

1. 还可以执行到容器中，就像执行到本地容器中一样。
 
 ```bash
   docker exec -it distracted-jackson sh
   ```

1. 最后，如需清理工作空间并确保不会因继续运行测试容器而产生任何费用，只需右键单击正在运行的容器，然后选择“删除”。

## <a name="recap"></a>概括

太好了，现在你已获取工作负载并首次成功地将其部署到云。 所有相关操作都可从命令行完成，也可通过使用 `docker run` 和 `docker compose up` 来运行多容器应用程序，从 ACI 上下文中完成。 有关在云中运行容器的详细信息，请阅读有关[使用 ACI](https://docs.docker.com/engine/context/aci-integration/) 的扩展文档。

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [后续步骤](whats-next.md)
