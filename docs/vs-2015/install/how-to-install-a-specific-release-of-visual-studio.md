---
title: 如何：安装特定版本 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
helpviewer_keywords:
- install a specific release, Visual Studio
ms.assetid: d69ad0f8-f0a0-438e-a0ef-777c4868f139
caps.latest.revision: 20
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: dde0cefabf0523484ad76ac56f7f2760de8c7acc
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63433079"
---
# <a name="how-to-install-a-specific-release-of-visual-studio"></a>如何：安装特定版本的 Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

我们会经常更新 Visual Studio 安装程序，以便你可以获得可选功能的最新优化版本。  但是，如果你想要安装 Visual Studio 2015 的早期版本（例如，包括 iOS 支持但为 Update 1 之前版本的 Visual Studio），则必须强制 Visual Studio 安装程序使用其功能清单文件的早期版本。 本文介绍了执行该操作的方法。

## <a name="installing-the-current-release"></a>安装当前版本
 自 Visual Studio 2015 初始版本起，我们已多次更新安装程序引擎和清单文件。  这意味着，如果你现在在一台连接 Internet 的干净计算机上从 [Visual Studio 下载](https://www.visualstudio.com/downloads/download-visual-studio-vs)下载 Web 安装程序，安装程序将会安装最新的 Visual Studio 2015 更新，其中包括最新产品改进以及更高版本和最新版本的可选功能和工具。

## <a name="installing-earlier-releases"></a>安装早期版本
 可以创建和装载 ISO 映像，也可以从 [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) 直接下载和启动安装程序，然后向 .exe 文件追加其他命令行参数（例如 /CustomInstallPath、/Full、/InstallSelectableItems 和 /NoRestart 等）以控制 Visual Studio 的安装方式。

 下表包括某些特定的时间点方案和所需的命令行参数，必须将这些参数传递给 Enterprise 版的安装程序。 （这些参数也适用于 Community 或 Professional 版安装程序。）

|Visual Studio 2015 版本|运行内容|要使用的命令行|安装程序执行的操作|
|--------------------------------|-----------------|--------------------------|---------------------|
|Visual Studio Enterprise（最新公开发布的版本）|包含更新的 Visual Studio Enterprise（可从 [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) 获取）|`vs_enterprise.exe` 注意：此安装的默认行为是提供最新的可选功能，因此不需要任何命令行参数。|Visual Studio 安装程序将使用最新的 feed.xml 并安装最新的文件|
|Visual Studio Enterprise Update 3（原始 Update 3，不包含任何 Update 3 之后的更新）|Visual Studio Enterprise RTM（可从 [MSDN 订阅下载页](https://msdn.microsoft.com/subscriptions/downloads/)获取）|`vs_enterprise.exe /OverrideFeedURI http://download.microsoft.com/download/6/B/B/6BBD3561-D764-4F39-AB8E-05356A122545/20160628.2/enu/feed.xml`|Visual Studio 安装程序将使用发布 Update 3 时提供的 feed.xml|
|Visual Studio Enterprise Update 2（原始 Update 2，但包含 Update 3 之前的更新）|Visual Studio Enterprise RTM（可从 [MSDN 订阅下载页](https://msdn.microsoft.com/subscriptions/downloads/)获取）|`vs_enterprise.exe /OverrideFeedURI http://download.microsoft.com/download/6/B/B/6BBD3561-D764-4F39-AB8E-05356A122545/20160620.2/enu/feed.xml`|Visual Studio 安装程序将使用发布 Update 3 之前的最新 feed.xml|
|Visual Studio Enterprise（原始 Update 2，不包含任何 Update 2 之后的更新）|Visual Studio Enterprise RTM（可从 [MSDN 订阅下载页](https://msdn.microsoft.com/subscriptions/downloads/)获取）|`vs_enterprise.exe /OverrideFeedURI http://download.microsoft.com/download/0/6/B/06BB0C5C-C767-4250-91DA-AB463377597E/20160405.3/enu/feed.xml`|Visual Studio 安装程序将使用发布 Update 2 时提供的 feed.xml|
|Visual Studio Enterprise Update 1（原始 Update 1，但包含 Update 2 之前的更新）|Visual Studio Enterprise RTM（可从 [MSDN 订阅下载页](https://msdn.microsoft.com/subscriptions/downloads/)获取）|`vs_enterprise.exe /OverrideFeedURI http://download.microsoft.com/download/3/2/A/32A1974F-D236-43C1-8981-97DDCBAEF14A/20160225.3/enu/feed.xml`|Visual Studio 安装程序将使用发布 Update 2 之前的最新 feed.xml|
|Visual Studio Enterprise Update 1（原始 Update 1，不包含任何 Update 1 之后的更新）|Visual Studio Enterprise RTM（可从 [MSDN 订阅下载页](https://msdn.microsoft.com/subscriptions/downloads/)获取）|`vs_enterprise.exe /OverrideFeedURI https://download.microsoft.com/download/3/2/A/32A1974F-D236-43C1-8981-97DDCBAEF14A/20151201.1/enu/feed.xml`|Visual Studio 安装程序将使用发布 Update 1 时提供的 feed.xml|
|Visual Studio Enterprise（原始 RTM，但带有 Update 1 之前的更新）|Visual Studio Enterprise RTM（可从  [MSDN 订阅下载页](https://msdn.microsoft.com/subscriptions/downloads/)获取）|`vs_enterprise.exe /OverrideFeedURI https://download.microsoft.com/download/3/6/1/36188D5F-479F-4A46-BF55-6AE5928D1EBB/20151102.3/enu/feed.xml`|Visual Studio 安装程序将使用发布 Update 1 之前的最新 feed.xml|
|Visual Studio Enterprise（原始 RTM，不包含任何更新）|Visual Studio Enterprise RTM（可从 [MSDN 订阅下载页](https://msdn.microsoft.com/subscriptions/downloads/)获取）|`vs_enterprise.exe /OverrideFeedURI https://download.microsoft.com/download/5/7/B/57BF5016-E4F0-4EB5-BE27-2BFA87E7723F/20150713.1/enu/feed.xml`|Visual Studio 安装程序将使用发布 RTM 时提供的 feed.xml|

> [!IMPORTANT]
> 根据你想要使用的语言，请将“enu”（英语）替换为以下值之一：
>
> - chs（简体中文）
>   - cht（繁体中文）
>   - csy（捷克语）
>   - deu（德语）
>   - esn（西班牙语）
>   - fra（法语）
>   - ita（意大利语）
>   - jpa（日语）
>   - kor（朝鲜语）
>   - plk（波兰语）
>   - ptb（葡萄牙语）
>   - rus（俄语）
>   - trk（土耳其语）

## <a name="see-also"></a>请参阅
 [Visual Studio 管理员指南](../install/visual-studio-administrator-guide.md)