---
title: .NET Framework 目标错误疑难解答 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- vs.FrameworkTargetingErrors
- MSBuild.ResolveAssemblyReference.FailedToResolveReferenceBecausePrimaryAssemblyInExclusionList
helpviewer_keywords:
- targeting .NET Framework version [Visual Studio]
- versions [Visual Studio], .NET Framework Client Profile
- multi-targeting
- multitargeting
- .NET Framework Client Profile
ms.assetid: 830e3e45-9a93-4279-a249-75b84599aefb
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 1c496fd457e80220bb2ea4a2f032cef9508d9dcb
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77631596"
---
# <a name="troubleshoot-net-framework-targeting-errors"></a>.NET Framework 目标错误疑难解答

本主题介绍可能由引用问题导致的 MSBuild 错误以及解决这些错误的方法。

## <a name="you-have-referenced-a-project-or-assembly-that-targets-a-different-version-of-the-net-framework"></a>已引用面向不同版本的 .NET Framework 的项目或程序集

 可以创建一些应用程序，这些应用程序引用的项目或程序集面向 .NET Framework 的不同版本。 例如，可以创建面向 .NET Framework 4 的客户端配置文件，但引用面向 .NET Framework 2.0 的程序集的应用程序。 但是，如果创建的项目面向早期版本的 .NET Framework，则不能在该项目中设置对面向 .NET Framework 4 或 .NET Framework 4 本身的项目或程序集的引用。 若要解决此错误，请确保应用程序面向的配置文件与该应用程序引用的项目或程序集所面向的配置文件兼容。

## <a name="you-have-re-targeted-a-project-to-a-different-version-of-the-net-framework"></a>已将项目重新面向不同版本的 .NET Framework

 如果更改应用程序的 .NET Framework 的目标版本，则 Visual Studio 将更改某些引用，并可能需要手动更新某些引用。 例如，如果将应用程序更改为面向 .NET Framework 3.5 Service Pack 1，并且该应用程序具有依赖于 .NET Framework 4 的客户端配置文件的资源或设置，则可能出现先前提到的某个错误。

 若要解决应用程序设置，请打开“解决方案资源管理器”  ，选择“显示所有文件”  ，然后在 Visual Studio 的 XML 编辑器中编辑“app.config”  文件。 在设置中更改版本，以匹配相应版本的 .NET Framework。 例如，可以将版本设置从 4.0.0.0 更改为 2.0.0.0。 同样，对于已添加资源的应用程序，打开“解决方案资源管理器”  ，选择“显示所有文件”  按钮，展开“我的项目”  (Visual Basic) 或“属性”  (C#)，然后在 Visual Studio 的 XML 编辑器中编辑“Resources.resx”  文件。 将版本设置从 4.0.0.0 更改为 2.0.0.0。

 如果应用程序具有资源，例如图标、位图或设置（如数据连接字符串），则还可以通过移除“项目设计器”  的“设置”  页上的所有项，然后重新添加所需设置来解决此错误。

## <a name="you-have-re-targeted-a-project-to-a-different-version-of-the-net-framework-and-references-do-not-resolve"></a>已将项目重新面向其他版本的 .NET Framework 并且引用不能解析

 如果将项目重新设置为面向其他版本的 .NET Framework，则在某些情况下引用可能无法正确解析。 对程序集的显式完全限定的引用通常会导致此问题，但可以通过删除不能解析的引用，然后将其添加回项目来解决该问题。 作为替代方法，可以编辑项目文件以替换引用。 首先，删除以下窗体的引用：

```xml
<Reference Include="System.ServiceModel, Version=3.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089, processorArchitecture=MSIL" />
```

 然后，将它们替换为简单的窗体：

```xml
<Reference Include="System.ServiceModel" />
```

> [!NOTE]
> 关闭并重新打开项目后，还应重新生成该项目以确保所有引用正确解析。

## <a name="see-also"></a>请参阅

- [如何：面向 .NET Framework 的某个版本](../ide/visual-studio-multi-targeting-overview.md)
- [.NET Framework 客户端配置文件](/dotnet/framework/deployment/client-profile)
- [框架定位概述](../ide/visual-studio-multi-targeting-overview.md)
- [多定向](../msbuild/msbuild-multitargeting-overview.md)
