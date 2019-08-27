---
title: 如何：指定最终用户将从安装的位置 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], specifying an installation URL
- URLs, specifying an installation URL
- installation, specifying installation an URL
- Installation URL property
ms.assetid: 04a804bf-ed55-4a7a-a1e6-f63ed99c0276
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ee3ce7e405a69dccd759e4c52bac84c28e431a4a
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67890565"
---
# <a name="how-to-specify-the-location-where-end-users-will-install-from"></a>如何：指定最终用户从中进行安装的位置
发布时[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序中，用户可以下载和安装应用程序的位置不一定是最初在其中发布应用程序的位置。 例如，在某些组织中开发人员可能会发布到暂存服务器，应用程序，然后管理员将移动应用程序到 Web 服务器。

在这种情况下，可以使用`Installation URL`属性来指定用户将可以下载应用程序的 Web 服务器。 这是必需的以便应用程序清单知道在何处查找更新。

`Installation URL`属性可以设置上**发布**页**项目设计器**。

> [!NOTE]
> `Installation URL`也可以使用设置属性**发布向导**。 有关更多信息，请参见[如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

### <a name="to-specify-an-installation-url"></a>若要指定安装 URL

1. 在“解决方案资源管理器”  中选择了项目的情况下，在“项目”  菜单上单击“属性”  。

2. 单击“发布”选项卡  。

3. 在安装 URL 字段中，输入使用完全限定的 URL 使用以下格式的安装位置 *http://www.microsoft.com/ApplicationName* ，或使用以下格式的 UNC 路径 *\\ \Server\ApplicationName*.

## <a name="see-also"></a>请参阅
- [如何：指定 Visual Studio 复制文件的位置](../deployment/how-to-specify-where-visual-studio-copies-the-files.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)