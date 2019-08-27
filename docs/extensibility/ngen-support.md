---
title: VSIX v3 中的 Ngen 支持 |Microsoft Docs
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 1472e884-c74e-4c23-9d4a-6d8bdcac043b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 24f1b0a26875bbbf8dfc4ac7db1049f7309d9aa2
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67891116"
---
# <a name="ngen-support-in-vsix-v3"></a>VSIX v3 中的 Ngen 支持

使用 Visual Studio 2017 和新的 VSIX v3 （版本 3） 扩展清单格式，扩展开发人员现在可以"ngen"在安装时其程序集。

下面是一段摘录 MSDN 介绍哪些"ngen"的作用：

>本机映像生成器 (*Ngen.exe*) 是一种工具，可以提高托管应用程序的性能。 *Ngen.exe*创建本机映像，它是包含已编译的特定于处理器的机器码的文件并将它们安装到本地计算机上的本机映像缓存。 运行时可从缓存中使用本机映像，而不必使用实时 (JIT) 编译器编译原始程序集。
>
>从[Ngen.exe （本机映像生成器）](/dotnet/framework/tools/ngen-exe-native-image-generator)

为了"ngen"程序集，VSIX 必须安装"每个实例每台计算机"。 可以通过签入"所有用户"复选框来启用此`extension.vsixmanifest`设计器：

![检查所有用户](media/check-all-users.png)

## <a name="how-to-enable-ngen"></a>如何启用 Ngen

若要启用程序集的 ngen，可以使用**属性**Visual Studio 窗口中的。

有 4 个可设置的属性：

1. **Ngen** （布尔值）-如果为 true，在 Visual Studio 安装程序将"ngen"程序集。
2. **Ngen 应用程序**（字符串）-Ngen 提供使用应用程序的机会*app.config*为了解析程序集依赖项的文件。 此值应设置为应用程序的*app.config*你想要使用 （相对于 Visual Studio 安装目录）。
3. **Ngen 体系结构**(enum)-本机编译您的程序集的体系结构。 选项为：。 NotSpecified b。 X86 c。 X64 d。 全部
4. **Ngen 优先级**（1 到 3 之间的整数）-Ngen 优先级别所述[Ngen.exe 优先级别](/dotnet/framework/tools/ngen-exe-native-image-generator#priority-levels)。

下面我们来看**属性**中操作的窗口：

![在属性中的 ngen](media/ngen-in-properties.png)

这会将元数据添加到 VSIX 项目的项目引用 *.csproj*文件：

```xml
 <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
    <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
    <Name>ClassLibrary1</Name>
    <Ngen>True</Ngen>
    <NgenApplication>vsn.exe</NgenApplication>
    <NgenArchitecture>X86</NgenArchitecture>
    <NgenPriority>2</NgenPriority>
</ProjectReference>
```

> [!NOTE]
> 如果您愿意，可以直接编辑.csproj 文件。

## <a name="extra-information"></a>额外信息

属性设计器更改应用到多个只是项目的引用;您可以在你的项目内设置项的 Ngen 元数据 （使用上文所述的相同方法） 长的项是.NET 程序集。