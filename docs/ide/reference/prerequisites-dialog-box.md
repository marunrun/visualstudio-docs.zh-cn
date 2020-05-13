---
title: “系统必备”对话框
ms.date: 06/29/2018
ms.technology: vs-ide-deployment
ms.topic: reference
f1_keywords:
- Microsoft.VisualStudio.Publish.BaseProvider.Dialog.Bootstrapper
helpviewer_keywords:
- Prerequisites dialog box
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0ecbba1a1c5e8670fd9adcafdfed8cec21dd3912
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75567900"
---
# <a name="prerequisites-dialog-box"></a>“系统必备”对话框

“系统必备”对话框指定安装哪些必备组件、如何安装以及组件包的安装顺序  。

![Visual Studio 中的“系统必备”对话框](media/prerequisites-dialog-box.png)

要访问该对话框，请在解决方案资源管理器中选择项目节点，然后选择“项目” > “属性”    。 项目设计器出现时，选择“发布”选项卡，然后选择“系统必备”    。 对于安装项目，在“项目”  菜单上单击“属性”  。 “属性页”  对话框出现后，单击“系统必备”  。

## <a name="uielement-list"></a>UIElement 列表

|元素|描述|
|-------------|-----------------|
|**创建用于安装系统必备组件的安装程序**|将应用程序的系统必备组件包含到安装程序 (Setup.exe) 中，以便在安装应用程序之前按照依赖顺序安装这些组件  。 默认情况下，该选项是选中的。 如果没有选择此选项，则不会创建 Setup.exe  。|
|**选择要安装的系统必备组件**|指定是否安装 .NET Framework 和 C++ 运行时库等组件。<br /><br />例如，通过选中“SQL Server 2012 Express”旁边的复选框，可以指定安装程序必须验证目标计算机上是否安装有此组件，如果没有则进行安装  。<br /><br />有关每个系统必备包的详细信息，请参阅[系统必备信息](#prerequisites-information)。|
|**从组件供应商的网站下载系统必备组件**|指定从供应商网站上安装系统必备组件。 这是默认选项。|
|**从与我的应用程序相同的位置下载系统必备组件**|指定从与应用程序相同的位置安装系统必备组件。 这会将所有系统必备包复制到发布位置。 要让此选项正常工作，系统必备包必须位于开发计算机上。|
|**从下列位置下载系统必备组件**|指定从输入的位置安装系统必备组件。 可使用“浏览”  按钮选择位置。|

> [!NOTE]
> 有关在何处放置必备组件的信息。请参阅[创建引导程序包](../../deployment/creating-bootstrapper-packages.md#create-custom-bootstrapper-packages)。

## <a name="prerequisites-information"></a>系统必备信息

出现在“系统必备”  对话框中的系统必备组件可能与下面列表中的不同。 第一次打开对话框时将自动设置 **“系统必备”对话框**中所列的必备组件包。 如果随后更改项目的目标框架，则必须手动选择必备组件，以便与新目标框架相匹配。

|元素|描述|
|-------------|-----------------|
|**.NET Framework 3.5 SP1**|此程序包会安装下列系统必备组件：<br /><br /> - .NET Framework 2.0、3.0 和 3.5 版<br />- 支持 32 位 (x86) 和 64 位 (x64) 操作系统上的所有 .NET Framework 版本。<br />- 与程序包一起安装的每个 .NET Framework 版本的语言包。<br />- .NET Framework 2.0 和 3.0 服务包。<br /><br /> .NET Framework 3.0 随 Windows Vista 一起提供，.NET Framework 3.5 随 Visual Studio 一起提供。 .NET Framework 3.5 是针对 32 位操作系统进行编译且目标框架设置为“.NET Framework 3.5”  的所有 Visual Basic 和 C# 项目的必需组件，也是针对 64 位操作系统编译的 Visual Basic 和 C# 项目的必需组件。 （不支持 IA64。）注意，默认情况下 Visual Basic 和 C# 项目是针对所有 CPU 体系结构进行编译的。 有关详细信息，请参阅 [Framework 定位概述](../../ide/visual-studio-multi-targeting-overview.md)和[部署 64 位应用的必备条件](../../deployment/deploying-prerequisites-for-64-bit-applications.md)。|
|**Microsoft .NET Framework 4.x**|此包为 x86 和 x64 平台安装 .NET Framework 4.x。|
|**Microsoft System CLR Types for SQL Server 2014 (x64 和 x86)**|此包为 x64 或 x86 平台安装 Microsoft System CLR Types for SQL Server 2014。|
|**SQL Server 2008 R2 Express**|此包安装 Microsoft SQL Server 2008 R2 Express，这是 Microsoft SQL Server 2008 R2 的免费版，是适用于小型网站、服务器或桌面应用程序的理想数据库。 它可免费用于开发和生产。|
|**SQL Server 2012 Express**|此包安装 Microsoft SQL Server 2012 Express。|
|**SQL Server 2012 Express LocalDB**|此包安装 Microsoft SQL Server 2012 Express LocalDB。|
|**Visual C++ "14" 运行时库 (ARM)**|此程序包将为 Itanium 体系结构安装 Visual C++ 运行库，以便为 Microsoft Windows 操作系统编程提供例程。 这些例程可自动处理许多 C 和 C++ 语言没有提供的常见编程任务。<br /><br /> 有关详细信息，请参阅 [C 运行时库参考](/cpp/c-runtime-library/c-run-time-library-reference)。|
|**Visual C++ "14" 运行时库 (x64)**|此程序包将为 x64 操作系统安装 Visual C++ 运行库，以便为 Microsoft Windows 操作系统编程提供例程。 这些例程可自动处理许多 C 和 C++ 语言没有提供的常见编程任务。<br /><br /> 有关详细信息，请参阅 [C 运行时库参考](/cpp/c-runtime-library/c-run-time-library-reference)。|
|**Visual C++ "14" 运行时库 (x86)**|此程序包将为 x86 操作系统安装 Visual C++ 运行库，以便为 Microsoft Windows 操作系统编程提供例程。 这些例程可自动处理许多 C 和 C++ 语言没有提供的常见编程任务。<br /><br /> 有关详细信息，请参阅 [C 运行时库参考](/cpp/c-runtime-library/c-run-time-library-reference)。|

## <a name="see-also"></a>请参阅

- [“项目设计器”->“发布”页](../../ide/reference/publish-page-project-designer.md)
- [应用程序部署必备](../../deployment/application-deployment-prerequisites.md)
- [部署 64 位应用程序的必备组件](../../deployment/deploying-prerequisites-for-64-bit-applications.md)
- [Framework 定位概述](../../ide/visual-studio-multi-targeting-overview.md)
