---
title: 本地化工具
ms.date: 02/15/2019
ms.topic: reference
helpviewer_keywords:
- globalization [Visual Studio]
- Visual Basic code, international applications
- C#, international applications
- localization [Visual Studio]
- world-ready applications
- international applications [Visual Studio]
ms.assetid: 4d9815ae-3e80-4b4d-933d-f8309aee18d5
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 886c31eb76a2cd440f1f8189aaacf592e43d34fa
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72603447"
---
# <a name="develop-globalized-and-localized-apps"></a>开发全球化和本地化应用

Visual Studio 利用 [.NET](/dotnet/standard/globalization-localization/) 中内置的服务来简化面向国际受众的开发。

例如，Windows 窗体应用的项目系统可同时为回退 UI 区域性和每个附加 UI 区域性生成资源文件。 在 Visual Studio 中构建项目时，资源文件将从 Visual Studio XML 格式 (.resx) 编译为中间二进制格式 (.resources)，然后嵌入到附属程序集中。 有关详细信息，请参阅 [Visual Studio 中的资源文件](/dotnet/framework/resources/creating-resource-files-for-desktop-apps#VSResFiles)和[创建桌面应用的附属程序集](/dotnet/framework/resources/creating-satellite-assemblies-for-desktop-apps)。

## <a name="bidirectional-languages"></a>双向语言

通过使用 Visual Studio，可以创建能正确显示从右向左书写的语言（包括阿拉伯语和希伯来语）文本的应用程序。 对于某些功能，只需设置属性即可。 而在其他一些情况下，必须通过代码来实现功能。

> [!NOTE]
> 要输入和显示双向语言，必须使用已配置相应语言的 Windows 版本。 可以是安装了适当语言包的英文版 Windows，或者是已相应本地化的 Windows 版本。

### <a name="apps-that-support-bidirectional-languages"></a>支持双向语言的应用

- Windows 应用

   你可以创建完全双向的应用程序，包括支持双向文本、从右到左的读取顺序以及镜像（用于翻转窗口、菜单、对话框等的布局）。 除镜像外，这些功能都作为默认功能或属性设置提供。 某些功能（例如消息框）本身就支持镜像。 但在其他情况下，必须通过代码实现镜像。 有关详细信息，请参阅 [Windows 窗体应用程序的双向支持](/dotnet/framework/winforms/advanced/bi-directional-support-for-windows-forms-applications)。

- Web 应用

   Web 服务支持发送和接收 UTF-8 及 Unicode 文本，从而使它们适用于涉及双向语言的应用程序。 Web 客户端应用程序需借助浏览器的用户界面，因此，Web 应用程序中的双向支持程度取决于用户的浏览器对这些双向功能的支持程度。 在 Visual Studio 中，创建的应用程序可以支持阿拉伯语或希伯来语文本、从右向左读取顺序、文件编码和本地区域性设置。 有关详细信息，请参阅 [ASP.NET Web 应用程序的双向支持](https://msdn.microsoft.com/Library/5576f9b1-9b86-41ef-8354-092d366bcd03)。

> [!NOTE]
> 控制台应用不包括对双向语言的文本支持。 这是 Windows 与控制台应用程序搭配使用方式的结果。

## <a name="see-also"></a>请参阅

- [对 Visual Studio 中双向语言的支持](use-bidirectional-languages.md)
- [全球化和本地化 .NET 应用](/dotnet/standard/globalization-localization/)
- [.NET 应用中的资源](/dotnet/framework/resources/)