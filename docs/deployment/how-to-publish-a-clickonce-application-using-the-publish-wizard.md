---
title: 使用发布向导发布 ClickOnce 应用程序
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, publishing
- deploying applications [ClickOnce], Publish wizard
- Windows applications, ClickOnce deployments
- publishing, ClickOnce
ms.assetid: 2e4aa67c-4445-4f7b-9e03-9acb95829127
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 518252ac24dc45036587de114f68cd0a77b8c5b8
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382297"
---
# <a name="how-to-publish-a-clickonce-application-using-the-publish-wizard"></a>如何：使用发布向导发布 ClickOnce 应用程序
ClickOnce 应用程序必须发布到文件共享或路径、FTP 服务器或可移动媒体，才能供用户使用。 可以使用发布向导发布应用程序；与发布相关的其他属性位于“项目设计器”的“发布”页中********。 有关详细信息，请参阅[发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)。

在运行发布向导前，应适当地设置发布属性。 例如，如果要指定密钥为 ClickOnce 应用程序签名，则可以在“项目设计器”的“签名”页中执行该操作********。 有关详细信息，请参阅[保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)。

> [!NOTE]
> 当使用 ClickOnce 安装多个版本的应用程序时，安装会将应用程序的早期版本移动到位于你指定的发布位置的名为“Archive”的文件夹中**。 按照这种方式对早期版本进行存档，可以使安装目录与早期版本所在的文件夹分开。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你的当前设置或版本。 若要更改设置，请单击 **“工具”** 菜单上的 **“导入和导出设置”** 。 有关详细信息，请参阅[重置设置](../ide/environment-settings.md#reset-settings)。

## <a name="to-publish-to-a-file-share-or-path"></a>发布到文件共享或路径

1. 在“解决方案资源管理器”中，选择应用程序项目****。

2. 在 "**生成**" 菜单上，单击 "**发布***项目名称*"。

    出现“发布向导”。

3. 在“要在何处发布应用程序?”页上，使用显示的格式之一输入有效的 FTP 服务器地址或有效的文件路径，然后单击“下一步”********。

4. 在“用户如何安装应用程序?”页面中，选择用户安装应用程序的位置****：

   - 如果用户从网站安装，则单击“从网站”，并输入与上一步中输入的文件路径相对应的 URL****。 单击“下一步”****。 （此选项通常在将 FTP 地址指定为发布位置时使用。 不支持从 FTP 直接下载。 因此，必须在此处输入 URL。）

   - 如果用户将直接从文件共享安装应用程序，请单击“从 UNC 路径或文件共享”，然后单击“下一步”********。 （此选项用于形式为“c:\deploy\myapp”或“\\\server\myapp”的发布位置。****）

   - 如果用户从可移动媒体安装，则单击“从 CD-ROM 或 DVD-ROM”，然后单击“下一步”********。

5. 在“该应用程序可以脱机使用吗?”页上，单击适当的选项****：

   - 如果要使应用程序在用户与网络断开连接时也可以运行，则单击“是，该应用程序可以联机或脱机使用”****。 “开始”菜单上将创建应用程序的快捷方式****。

   - 如果要从发布位置直接运行应用程序，则单击“否，该应用程序只能联机使用”****。 “开始”菜单上不创建快捷方式****。

     单击 **“下一步”** 以继续。

6. 单击“完成”以发布应用程序****。

    发布状态显示在状态通知区域中。

## <a name="to-publish-to-a-cd-rom-or-dvd-rom"></a>发布到 CD-ROM 或 DVD-ROM

1. 在“解决方案资源管理器”中，右击应用程序项目，然后单击“属性”********。

    此时将显示 "**项目设计器**"。

2. 单击“发布”选项卡在“项目设计器”中打开“发布”页，然后单击“发布向导”按钮****************。

    出现“发布向导”。

3. 在“要在何处发布应用程序?”页中，输入发布应用程序的文件路径或 FTP 位置（如“d:\deploy”）******。 然后单击 **“下一步”** 以继续。

4. 在“用户如何安装应用程序?”页上，单击“从 CD-ROM 或 DVD-ROM”，然后单击“下一步”************。

   > [!NOTE]
   > 如果希望在将 CD-ROM 插入驱动器时自动运行安装，请打开“项目设计器”中的“发布”页，并单击“选项”按钮，然后在“发布选项”向导中，选择“对于 CD 安装，插入 CD 时自动启动安装程序”********************。

5. 如果在 CD-ROM 上发布应用程序，可能会希望从网站提供更新。 在“应用程序将到哪里检查更新?”页中，选择更新选项****：

   - 如果应用程序将检查更新，则单击“该应用程序将从下列位置检查更新”，然后输入发布更新的位置****。 该位置可以是文件位置、网站或 FTP 服务器。

   - 如果应用程序不检查更新，则单击“该应用程序将不检查更新”****。

     单击 **“下一步”** 以继续。

6. 单击“完成”以发布应用程序****。

    发布状态显示在状态通知区域中。

   > [!NOTE]
   > 完成发布后，必须使用 CD 刻录机或 DVD 刻录机从步骤 3 中指定的位置将文件复制到 CD-ROM 或 DVD-ROM 媒体。

## <a name="see-also"></a>请参阅

- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [使用 ClickOnce 部署 Office 解决方案](../vsto/deploying-an-office-solution-by-using-clickonce.md)