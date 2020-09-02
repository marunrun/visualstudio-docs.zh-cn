---
title: 如何使用 ClickOnce 应用程序安装必备组件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], prerequisites
- prerequisites, ClickOnce
- components, bootstrapping
ms.assetid: e964fca5-fdfd-47cf-a1c9-7fb96b1c88b5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ce4ad97439d330a6fc51e741e9ea05ef53a5798a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85382375"
---
# <a name="how-to-install-prerequisites-with-a-clickonce-application"></a>如何：与 ClickOnce 应用程序一起安装系统必备组件
所有 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序都需要在计算机上安装 .NET Framework 的正确版本，然后才能运行该计算机; 许多应用程序也有其他必备组件。 发布 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时，可以选择要与应用程序一起打包的一组系统必备组件。 在安装时，将针对每个先决条件执行检查，以确定它是否已存在;如果不是，则会在安装应用程序之前安装该 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。

 你还可以指定组件的下载位置，而不是打包和发布必备组件。 例如，你可以在安装时使用包含所有必备组件的安装程序的集中式文件共享或 Web 位置，而不是在每个应用程序中包含先决条件-在安装时，将从该位置下载和安装组件。

> [!IMPORTANT]
> 在发布第一个应用程序之前，应将必备安装程序包添加到开发计算机 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 有关详细信息，请参阅 [如何：将必备组件与 ClickOnce 应用程序结合使用](../deployment/how-to-include-prerequisites-with-a-clickonce-application.md)。

 系统必备组件在 "**必备组件**" 对话框中管理，可从 "**项目设计器**" 的 "**发布**" 窗格访问。

> [!NOTE]
> 除了预先确定的先决条件列表，你还可以将你自己的组件添加到该列表中。 有关详细信息，请参阅 [创建引导程序包](../deployment/creating-bootstrapper-packages.md)。

### <a name="to-specify-prerequisites-to-install-with-a-clickonce-application"></a>指定要与 ClickOnce 应用程序一起安装的先决条件

1. 在 **解决方案资源管理器**中选择一个项目后，在 " **项目** " 菜单上单击 " **属性**"。

2. 选择 " **发布** " 窗格。

3. 单击 " **先决条件** " 按钮以打开 " **系统必备** " 对话框。

4. 在 **“系统必备”** 对话框中，确保选中 **“创建用于安装系统必备组件的安装程序”** 复选框。

5. 在 " **必备项** " 列表中，检查要安装的组件，然后单击 **"确定"**。

     选定的组件将与您的应用程序一起打包和发布。

### <a name="to-specify-a-different-download-location-for-prerequisites"></a>为必备组件指定不同的下载位置

1. 在 **解决方案资源管理器**中选择一个项目后，在 " **项目** " 菜单上单击 " **属性**"。

2. 选择 " **发布** " 窗格。

3. 单击 " **先决条件** " 按钮以打开 " **系统必备** " 对话框。

4. 在 **“系统必备”** 对话框中，确保选中 **“创建用于安装系统必备组件的安装程序”** 复选框。

5. 在 " **指定系统必备组件的安装位置** " 部分中，选择 **"从以下位置下载系统必备组件**"。

6. 从下拉列表中选择一个位置，或者输入 URL、文件路径或 FTP 位置，然后单击 **"确定"。**

    > [!NOTE]
    > 必须确保指定组件的安装程序存在于指定位置。

## <a name="see-also"></a>请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)