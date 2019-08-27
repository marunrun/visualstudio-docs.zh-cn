---
title: Visual Studio 和 Xamarin | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: tgt-pltfrm-cross-plat
ms.topic: conceptual
ms.assetid: 1da4064f-af69-472c-8f31-98484be5f790
caps.latest.revision: 14
ms.author: crdun
manager: crdun
ms.openlocfilehash: 098d94a1aed9020271db5010e278a4aa8fc68330
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63442133"
---
# <a name="visual-studio-and-xamarin"></a>Visual Studio 和 Xamarin
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Xamarin 是一个移动应用开发平台，用于从常见的 C#/.NET 基本代码构建本机 iOS、Android 和 Windows 应用，可实现 75% 到将近 100% 的平台间代码重用。 通过 Xamarin 和 C# 编写的应用可完全访问基础平台 API 并可生成本机用户界面；由于这些应用与平台特定的包相兼容，因此几乎不影响运行时性能。 （注意：Xamarin 还支持F#，但本文档将重点介绍C#仅。 此时不支持 Visual Basic。）  
  
 更有甚者，熟悉 C#、.NET 和 Visual Studio 的开发人员使用 Xamarin 开发移动应用（包括在 Android、iOS 和 Windows 设备上进行远程调试）时将同样享受其强大功能和工作效率，而无需学习 Objective-C 或 Java 等本机编程语言。 因此，许多具有精美用户界面的高性能应用（例如 NASCAR、Aviva 和 MixRadio）都是使用 Xamarin 生成的，也就不足为奇了。  
  
 本文档将帮助评估利用 Xamarin 构建这些体验的 **Visual Studio** 完整功能。  
  
- 首先进行[设置和安装](../cross-platform/setup-and-install.md)，该过程将花费一些时间（通常是 2-4 小时，具体取决于 Internet 连接速度、已安装内容和所选选项）。  
  
- 在安装程序运行期间，可参阅[了解如何使用 Xamarin 进行移动开发](../cross-platform/learn-about-mobile-development-with-xamarin.md)，该文章将介绍什么是 Xamarin 的本质并对 Xamarin.Forms 和本机 UI 进行比较等。  
  
- 安装完成后，请[验证 Xamarin 环境](../cross-platform/verify-your-xamarin-environment.md)。  
  
- 通过完成教程[学习在 Visual Studio 中使用 Xamarin.Forms 生成应用的基础知识](../cross-platform/learn-app-building-basics-with-xamarin-forms-in-visual-studio.md)完成操作。  
  
  可通过[任意版本的 Visual Studio 2015 ](https://www.visualstudio.com/vs-2015-product-editions)（Community、Professional 和 Enterprise）使用所有Xamarin功能。 另请注意，自 2016 年 3 月 31 日起， Visual Studio 2015 的所有版本都将提供 Xamarin，不再需要单独的许可证。 对于 Visual Studio 2013，可按照[设置和安装](../cross-platform/setup-and-install.md)主题中所述单独安装 Xamarin。  
  
> [!NOTE]
> 对具有 Windows 和 Visual Studio 知识的人员而言，这些说明描述了最简单易行的计算机配置。 使用此配置，简化了整体开发体验，因为只需与 Mac 交互即可使用 iOS 模拟器和受限设备。 如果你熟知 Mac，建议在 Parallels/VMWare 中运行 Visual Studio 或使用 Xamarin Studio Community。 相关说明，请参阅 [Mac 用户的设置、安装和验证](../cross-platform/setup-install-and-verifications-for-mac-users.md)。  
  
> [!NOTE]
> 如果你在寻找基于 HTML 和 CSS 的跨平台开发解决方案，请参阅 [Visual Studio 中的跨平台开发](../cross-platform/cross-platform-mobile-development-in-visual-studio.md#HTML)中所述的 Visual Studio Tools for Apache Cordova。
