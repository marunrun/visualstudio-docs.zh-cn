---
title: 指定要复制文件的位置 |Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- publishing, specifying location
- Publish Location property
ms.assetid: 6c552700-dda3-49fe-af98-4717344fda07
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ec54a2d3150b0e8e11b19d2ca739324d7388f1f0
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63407656"
---
# <a name="how-to-specify-where-visual-studio-copies-the-files"></a>如何：指定 Visual Studio 复制文件的位置
使用 ClickOnce 发布应用程序时，“`Publish Location`”属性指定放置应用程序文件和清单的位置。 这可以是文件路径或 FTP 服务器的路径。

 可以在“项目设计器”的“发布”页上或使用发布向导指定 `Publish Location` 属性。 有关详细信息，请参阅[如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

> [!NOTE]
> 当使用 ClickOnce 安装多个版本的应用程序时，安装会将应用程序的早期版本移动到位于你指定的发布位置的名为“Archive”的文件夹中。 按照这种方式对早期版本进行存档，可以使安装目录与早期版本所在的文件夹分开。

### <a name="to-specify-a-publishing-location"></a>指定发布位置

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击“发布”选项卡。

3. 在“发布位置”字段中，使用以下格式之一输入发布位置：

   - 若要发布到文件共享或磁盘路径，请使用 UNC 路径 (\\\\Server\ApplicationName) 或文件路径 (C:\Deploy\ApplicationName) 输入路径。

   - 若要发布到 FTP 服务器，请使用格式 <em>ftp://ftp.microsoft.com/\<ApplicationName></em> 输入路径。

     请注意，“发布位置”框中必须存在文本才能使浏览（“...”）按钮正常工作。

## <a name="see-also"></a>请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)