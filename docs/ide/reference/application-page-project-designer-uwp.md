---
title: 适用于 UWP 应用的应用程序属性页
ms.date: 01/23/2018
ms.topic: reference
f1_keywords:
- AppPackage.Properties.Application
helpviewer_keywords:
- Application page [UWP project]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 3c8f72d4e1d1caeacd5dfefef5310dc2cef83b92
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77173078"
---
# <a name="application-property-page-uwp-projects"></a>应用程序属性页（UWP 项目）

使用“应用程序”  属性页来指定通用 Windows 平台 (UWP) 项目的程序集和包信息，以及 Windows 10 目标版本。

![应用程序属性页](media/application-page-uwp.png)

若要访问“应用程序”  页，请在“解决方案资源管理器”  中选择项目节点。 然后在菜单栏上依次选择“项目”   > “属性”  。 “属性页”随即在“应用程序”  选项卡上打开。

## <a name="general-section"></a>“常规”部分

 程序集名称 &mdash; 指定将保存程序集清单的输出文件的名称。

若要以编程方式访问此属性，请参阅 <xref:VSLangProj.ProjectProperties.AssemblyName%2A>。

 默认命名空间 &mdash; 为添加到项目中的文件指定基命名空间。 有关命名空间的详细信息，请参阅[命名空间（C# 编程指南）](/dotnet/csharp/programming-guide/namespaces/)、[命名空间 (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/namespaces)，或[命名空间 (C ++)](/cpp/cpp/namespaces-cpp)。

若要以编程方式访问此属性，请参阅 <xref:VSLangProj.ProjectProperties.RootNamespace%2A>。

 程序集信息 &mdash; 选择此按钮将显示[“程序集信息”对话框](../../ide/reference/assembly-information-dialog-box.md)。

 包清单 &mdash; 选择此按钮将打开清单设计器。 此外，还可以通过选择“解决方案资源管理器”中的 Package.appxmanifest 文件来访问清单设计器。 有关详细信息，请参阅[使用清单设计器配置包](/windows/msix/package/packaging-uwp-apps#configure-your-project)。

## <a name="targeting-section"></a>“设定目标”部分

可通过本部分中的下拉列表，为应用设置目标版本和最低版本的 Windows 10。 建议将目标设定为 Windows 10 的最新版本，如果你正在开发企业应用，那么也可支持较旧的最低版本。 有关要选择的 Windows 10 版本的详细信息，请参阅[选择 UWP 版本](/windows/uwp/updates-and-versions/choose-a-uwp-version)。

有关 Visual Studio 中的平台目标信息，请参阅[平台目标](/visualstudio/productinfo/vs2017-compatibility-vs#platform-targeting)。

## <a name="see-also"></a>另请参阅

- [创建你的第一个 UWP 应用](/windows/uwp/get-started/your-first-app)
- [选择 UWP 版本](/windows/uwp/updates-and-versions/choose-a-uwp-version)
