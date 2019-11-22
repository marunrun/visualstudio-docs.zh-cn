---
title: 介绍基于 .NET Framework 的国际应用程序 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- strings [Visual Studio], localizing
- Web applications [.NET Framework], globalization
- Windows Forms, globalization
- localization [Visual Studio], culture setting
- fallback resources
- culture, setting
- globalization [Visual Studio], culture setting
- resources [Visual Studio], localization
- localization [Visual Studio], .NET localization model
- Assembly Resource file template
- resources [Visual Studio], fallback system
- international applications [Visual Studio], about international applications
- globalization [Visual Studio], international applications
- ASP.NET, globalization
- resource files, fallback processes
- user interface, culture setting
ms.assetid: b0788993-e62d-4f68-8235-5f87b1d48525
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f394cca9a248b5304a165f68a60b966d8e3684b2
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74291374"
---
# <a name="introduction-to-international-applications-based-on-the-net-framework"></a>介绍基于 .NET Framework 的国际应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中，世界通用的应用程序的创建包括两个部分：全球化（设计可以适应不同区域性的应用程序的过程）和本地化（为特定区域性转换资源的过程）。 有关为国际受众设计应用程序的常规信息，请参阅[开发全球通用应用程序的最佳做法](https://msdn.microsoft.com/library/f08169c7-aad8-4ec3-9a21-9ebd3b89986c)。

 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 本地化模型由同时包含应用程序代码和回退资源的主要程序集组成 - 字符串、图像和用于最初开发应用程序时所使用的语言的其他对象。 每个本地化应用程序都会有附属程序集或仅包含经本地化的资源的程序集。 因为主程序集始终包含回退资源，如果在本地化附属程序集中找不到资源，<xref:System.Resources.ResourceManager> 将尝试以层级方式加载它，最终回退到主程序集的资源中。 [用于本地化的资源的分层组织](../ide/hierarchical-organization-of-resources-for-localization.md)中对资源回退系统有更详细的解释。

 应考虑使用的一个本地化资源是一个用于所有 Microsoft 本地化产品的术语表。 此 CSV 文件包含超过 12,000 个英语术语，以及最多 59 种不同语言的术语翻译。 该术语表可从 [Microsoft Terminology Translations](https://go.microsoft.com/fwlink/?LinkId=128146)（Microsoft 术语翻译）网页下载。

 Windows 窗体应用程序的项目系统可同时为回退和每个所需的其他 UI 区域性生成资源文件。 将回退资源文件构建到主程序集中，然后将特定于区域性的资源文件构建到附属程序集中（每个 UI 区域性一个）。 构建项目时，资源文件将从 Visual Studio XML 格式 (.resx) 编译为中间二进制格式 (.resources)，然后嵌入到附属程序集中。

 借助可同时用于 Windows 窗体和 Web 窗体的项目系统，用户可使用程序集资源文件模板构建资源文件、访问资源以及构建项目。 附属程序集将随主程序集一并创建。

 执行本地化应用程序时，其外观由两个区域性值确定。 （区域性  是一组与用户语言、环境和区域性惯例相关的用户首选项信息。）UI 区域性设置确定将加载哪些资源。 UI 区域性在 Web.config 文件和页面指令中设置为 `UICulture`，在 Visual Basic 或 Visual C# 代码中设置为 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A>。 区域性设置确定值的格式，如日期、数字、货币等。 区域性在 Web.config 文件和页面指令中设置为 `Culture`，在 Visual Basic 或 Visual C# 代码中设置为 <xref:System.Globalization.CultureInfo.CurrentCulture%2A>。

## <a name="see-also"></a>另请参阅
 <xref:System.Globalization> <xref:System.Resources>
 [全球化和本地化应用程序](../ide/globalizing-and-localizing-applications.md)[安全性和已本地化的附属程序集](../ide/security-and-localized-satellite-assemblies.md)
