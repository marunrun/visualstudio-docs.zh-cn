---
title: 自定义起始页 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.startpage
- VS.StartPage.HowDoI
- vs.ToolsOptionsPages.Startup
helpviewer_keywords:
- Start Page [Visual Studio]
- customizing Start Page [Visual Studio]
- Visual Studio Start page
ms.assetid: 925d42eb-ec34-426e-ad81-19db8630e536
caps.latest.revision: 48
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f1c3dfb145e70665156c921cc9a6f740539bc4e6
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665842"
---
# <a name="customizing-the-start-page-for-visual-studio"></a>自定义 Visual Studio 的起始页
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过多种默认方式来自定义 Visual Studio 的起始页，例如，显示“打开项目”  对话框或打开最近加载的解决方案。 你也可以显示自定义起始页，此起始页是在工具窗口中运行的 Windows Presentation Foundation (WPF) XAML 页，并且可以运行 Visual Studio 的内部命令。

## <a name="customizing-the-default-start-page"></a>自定义默认起始页

1. 在菜单栏上，依次选择“工具”  、“选项”  。

2. 展开“环境”  ，然后选择“启动”  。

3. 在“启动时”  列表中，选择所需的自定义项。

## <a name="show-a-custom-start-page"></a>显示自定义起始页

1. 通过以下方式之一安装自定义起始页：

    - 从 [Visual Studio Marketplace](https://marketplace.visualstudio.com/)、其他网站或本地 Intranet 中的页上安装起始页。

        > [!NOTE]
        > 如果你希望使用面向早期版本 Visual Studio 的页，则可以使用 Visual Studio SDK 升级此页。 请参阅[如何：升级 Visual Studio 自定义起始页](../misc/how-to-upgrade-a-visual-studio-custom-start-page.md)。

         打开包含自定义起始页的 .vsix 文件，或复制起始页文件并将其粘贴到计算机上的“%USERPROFILE% \My Documents\Visual Studio 2015\StartPages”文件夹  。

    - 如果你已安装 Visual Studio SDK，请创建你自己的起始页。

         请参阅[创建自己的起始页](../misc/creating-your-own-start-page.md)。

2. 在菜单栏上，依次选择“工具”  、“选项”  。

3. 展开“环境”  ，然后选择“启动”  。

4. 在“自定义起始页”  列表中，选择所需的页。

> [!NOTE]
> 如果自定义起始页中的错误导致 Visual Studio 崩溃，则可以使用安全模式下启动 Visual Studio，然后将其设置为使用默认起始页。 请参阅 [/SafeMode (devenv.exe)](../ide/reference/safemode-devenv-exe.md)。

## <a name="see-also"></a>另请参阅
 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3) [创建自己的起始页](../misc/creating-your-own-start-page.md)
