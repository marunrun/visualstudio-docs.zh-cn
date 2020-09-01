---
title: Docker 教程-第9部分：部署到云
description: 将 docker 应用部署到云服务进行托管。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 661f9f6833b5ac5d42aacde7f228b042bef00bb0
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176689"
---
# <a name="deploy-to-the-cloud"></a>部署到云

现在，你已在本地运行你的应用程序，你可以开始考虑在云中运行它，让其他人可以访问它并利用它。 为此，你将使用 Docker 上下文。 上下文是指您当前正在使用容器的位置。 现在，你只具有 "默认" 上下文，因此你需要添加一个云并将你的应用部署到该上下文。

## <a name="create-your-cloud-context"></a>创建云上下文

1. 首先，你可以通过查看 Docker 面板的 "上下文" 部分来查看你的上下文：

   ![仅显示默认上下文](media/defaultcontext.png)

你只应查看本地工作的默认上下文。

1. 若要部署到云，需要创建新的 ACI 上下文，但要执行此操作，首先需要使用 Azure 帐户扩展对 Azure 进行身份验证。

   ![正在添加 Azure 扩展](media/addazureextension.png)

如果还没有 Azure 帐户，则需要设置它。

1. 现在可以创建新的 ACI 上下文。 可以通过单击 Docker 视图的 " **上下文** " 部分中的加号按钮来执行此操作。

   ![创建 ACI 上下文](media/createnewcontext.png)

这会询问你要在其下运行这些容器的资源组。 使用箭头键选择现有组，或使用默认选项以使用新组。

![选择资源组](media/selectresourcegroup.png)

现在，你可以看到列出的 ACI 上下文，并可右键单击该上下文，使其成为当前焦点/使用上下文：

![可以选择新的 ACI 上下文](media/listofcontexts.png)

## <a name="run-containers-in-the-cloud"></a>在云中运行容器

1. 现在，请使用 ACI 上下文并运行容器。

   ```bash
   docker context use myacicontext
   docker run  -dp 3000:3000 <username>/getting-started
   ```

1. 运行此程序后，请查看上下文中的容器。

   ![在 ACI 上下文中运行的容器](media/contextcontainer.png)

1. 若要检查此项是否正常工作，可以右键单击正在运行的容器，然后选择 " **在浏览器中查看**"。

   ![具有公共 IP 的 ACI 中的容器](media/containerinaci.png)

而且，您可以看到容器正在公共 IP 中运行并且工作正常！

1. 现在，可以查看正在运行的容器，查看其工作方式。 首先，可以查看容器日志：
 
 ```bash
   docker logs distracted-jackson
   ```

1. 你还可以执行到容器中，就像使用本地容器一样。
 
 ```bash
   docker exec -it distracted-jackson sh
   ```

1. 最后，若要清除工作空间，并确保不会向继续运行测试容器付费，只需右键单击正在运行的容器，然后选择 " **删除**"。

## <a name="recap"></a>概括

好了，你现在已获得工作负荷并首次成功地将其部署到云。 你可以使用从命令行中执行所有这些操作 `docker run` ，也可以使用 `docker compose up` 运行多容器应用程序，也可以使用运行多容器应用程序。 若要了解有关在云中运行容器的详细信息，请阅读 [有关使用 ACI](https://docs.docker.com/engine/context/aci-integration/)的扩展文档。

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [后续操作](whats-next.md)
