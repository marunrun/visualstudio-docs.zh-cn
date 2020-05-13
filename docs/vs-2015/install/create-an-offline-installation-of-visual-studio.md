---
title: 创建脱机安装 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
f1_keywords:
- offline installation
- offline install
- ISO
ms.assetid: 85d65709-42be-449f-9663-914bf1045089
caps.latest.revision: 22
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: a6a9707d517a8a43d9a9ca156a5f7291ecee9bee
ms.sourcegitcommit: 7b60e81414a82c6d34f6de1a1f56115c9cd26943
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81445059"
---
# <a name="create-an-offline-installation-of-visual-studio"></a>创建 Visual Studio 的脱机安装
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有关 Visual Studio 的最新文档，请参阅[创建 Visual Studio 的脱机安装](/visualstudio/install/create-an-offline-installation-of-visual-studio)或[创建 Visual Studio 的网络安装](/visualstudio/install/create-a-network-installation-of-visual-studio)。

此页面介绍如何在未连接到 Internet 时安装 Visual Studio 2015。 但是，若要执行“已断开连接的”安装，则必须首先使用连接到 Internet 的计算机创建脱机安装布局。 以下是使用方法。

> [!IMPORTANT]
> 如果脱机计算机正在运行 Windows 7 SP1 或 Windows Server 2008 R2，请参阅本主题的[脱机安装疑难解答](#BKMK_tshoot)部分中的特殊说明。  在安装 Visual Studio 2015 之前**，必须遵循这些说明。

## <a name="installing-by-creating-an-offline-installation"></a><a name="BKMK_Offline"></a> 通过创建脱机安装进行安装

#### <a name="to-create-an-offline-installation-layout"></a>创建脱机安装布局

1. 选择要从 [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20Enterprise%202015) 下载页安装的 Visual Studio 版本。

2. 将安装程序下载到文件系统上的某个位置后，运行“\<executable name> /layout”。

     例如，运行：`vs_enterprise.exe /layout D:\VisualStudio2015`

     通过使用 `/layout` 开关，你可以下载几乎所有安装包，而不仅仅是下载适用于下载计算机的安装包。 此方法可为你提供在任何地方运行此安装程序所需的文件，如果想安装原来没有安装的组件，这种方法可能会很有用。

3. 运行此命令后，将出现一个对话框，可用于更改脱机安装布局所驻留的文件夹。   接下来，单击 **"下载**"按钮。

     当包下载成功时，您应该会看到一条消息，指出 **"设置成功！已成功获取所有指定的组件。**

4. 找到之前指定的文件夹。 （例如，找到 D：\VisualStudio2015。此文件夹包含复制到共享位置或安装媒体所需的一切。

    > [!CAUTION]
    > 目前，Android SDK 不支持脱机安装体验。 如果在未连接到 Internet 的计算机上安装 Android SDK 安装程序项，则安装可能失败。 有关详细信息，请参阅本主题中的“脱机安装疑难解答”部分。

5. 从该文件位置或安装媒体运行安装。

## <a name="updating-an-offline-installation"></a>更新脱机安装
 Microsoft 发布了多个 Visual Studio 2015 更新。 若要更新 Visual Studio 安装，只需下载要从 [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20Enterprise%202015) 下载页获得的版本。 接下来，按照本主题中概述的步骤创建新的脱机安装布局，然后将其用于更新 Visual Studio 2015 的副本。

## <a name="troubleshooting-an-offline-installation"></a><a name="BKMK_tshoot"></a> 脱机安装疑难解答
 从脱机安装缓存进行脱机安装时，可能会看到提示无法安装某些组件和包的警告消息。 下表包含针对这些情况可能的解决方案。

| 组件或包 | 解决方案 |
|-|-|
| Dotfuscator 和 Analytics 社区版 5.19.1（Visual Studio 社区版、专业版和企业版，已在 Windows 7 SP1**** 和 Windows Server 2008 R2**** 上安装） | 如果脱机计算机正在运行 Windows 7 SP1**** 或 Windows Server 2008 R2****，则在安装 Visual Studio 2015 之前，必须执行以下步骤：<br /><br /> 1. 配置文件或 Web 服务器以下载 CTL 文件。<br /><br /> 2. 重定向断开的环境的 Microsoft 自动更新 URL。<br /><br /> 有关详细信息，请参阅 Microsoft TechNet 网站上的[配置受信任的根和不允许的证书](https://technet.microsoft.com/library/dn265983.aspx)页。 |
| Android SDK 安装程序（API 级别） | 必须连接 Internet 才能安装 Android SDK（API 级别）包。 如果处于受限网络上，则在安装 Visual Studio 时必须允许访问以下 URL：<br /><br /> -   `https://dl.google.com:443`<br />-   `https://dl-ssl.google.com:443`<br />-   `https://dl-ssl.google.com/android/repository/*`<br /> <br />有关如何使用代理设置解决可能的问题的详细信息，请参阅 [Visual Studio 2015 install failures (Android SDK Setup) behind a Proxy](https://blogs.msdn.microsoft.com/peterhauge/2016/09/22/visual-studio-2015-install-failures-android-sdk-setup-behind-a-proxy/)（使用代理时的 Visual Studio 2015 安装故障（Android SDK 安装程序））博客文章。 |
| Visual Studio 扩展性项模板<br /><br /> 适用于 Visual Studio 的 GitHub 扩展<br /><br /> Visual Studio 的 PowerShell 工具 | 如果在安装 Visual Studio 2015 时未连接到 Internet，则可以使用特殊离线源来生成脱机安装布局。 注意：**** 此特殊源包含 Visual Studio 2015 的最新更新。 <br /><br /> 若要创建特殊离线源，请运行以下命令：/layout *Drive:* \VisualStudio2015 /overridefeeduri *URL-to-feed-xml*<br /><br /> 例如，对于英语语言的 Visual Studio 2015 Enterprise 特殊离线源，请运行：<br /><br /> `vs_enterprise_ENU.exe /layout D:\VisualStudio2015 /overridefeeduri "https://go.microsoft.com/fwlink/?LinkID=785882&clcid0x409"`<br /><br /> 有关可用于以所选语言创建特殊离线源的 URL 的完整列表，请参阅下表。 |

 使用以下 URL 创建语言特定的特殊离线源，如上表中所述。

|       语言        |                            URL                            |
|-----------------------|-----------------------------------------------------------|
| 中文(简体)  | https://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x804 |
| 中文(繁体) | https://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x404 |
|         捷克语         | https://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x405 |
|        德语         | https://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x407 |
|        英语        | https://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x409 |
|        西班牙语        | https://go.microsoft.com/fwlink/?LinkID=785882&clcid=0xC0A |
|        法语         | https://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x40C |
|        意大利语        | https://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x410 |
|       日语        | https://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x411 |
|        朝鲜语         | https://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x412 |
|        波兰语         | https://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x415 |
|      葡萄牙语       | https://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x416 |
|        俄语        | https://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x419 |
|        土耳其语        | https://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x41F |

## <a name="see-also"></a>另请参阅

- [安装 Visual Studio](install-visual-studio-2015.md)