---
title: VSIX v3 中的 Ngen 支持 |微软文档
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 1472e884-c74e-4c23-9d4a-6d8bdcac043b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cb75b9256ca937106235fa7a7d66d9cec71c9c60
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702404"
---
# <a name="ngen-support-in-vsix-v3"></a>VSIX v3 中的 Ngen 支持

借助 Visual Studio 2017 和新的 VSIX v3（版本 3）扩展清单格式，扩展开发人员现在可以在安装时"ngen"其程序集。

以下是 MSDN 的摘录，其中解释了"ngen"的作用：

>本机映像生成器 （*Ngen.exe*） 是提高托管应用程序性能的工具. *Ngen.exe*创建本机映像，这些映像包含编译的特定于处理器的计算机代码，并将它们安装到本地计算机上的本机映像缓存中。 运行时可从缓存中使用本机映像，而不必使用实时 (JIT) 编译器编译原始程序集。
>
>来自[Ngen.exe（本机图像生成器）](/dotnet/framework/tools/ngen-exe-native-image-generator)

为了"ngen"一个组件，VSIX 必须安装"每台计算机的实例"。 这可以通过选中`extension.vsixmanifest`设计器中的"所有用户"复选框来启用：

![检查所有用户](media/check-all-users.png)

## <a name="how-to-enable-ngen"></a>如何启用 Ngen

要为程序集启用 ngen，可以使用 Visual Studio 中的 **"属性**"窗口。

可以设置 4 个属性：

1. **Ngen** （布尔） - 如果为 true，Visual Studio 安装程序将"ngen"程序集。
2. **Ngen 应用程序**（字符串） - Ngen 提供了使用应用程序*的应用程序.config*文件来解决程序集依赖项的机会。 此值应设置为要使用*的应用程序。* 相对于 Visual Studio 安装目录）。
3. **Ngen 体系结构**（枚举） - 用于本机编译程序集的体系结构。 选项是： a. 未指定 b. X86 c. X64 d. 全部
4. **Ngen 优先级**（介于 1 和 3 之间的整数） - Ngen 优先级级别记录在[Ngen.exe 优先级](/dotnet/framework/tools/ngen-exe-native-image-generator#priority-levels)级别。

下面是 **"属性**"窗口的操作：

![ngen 在 属性](media/ngen-in-properties.png)

这将在 VSIX 项目的 *.csproj*文件内向项目引用添加元数据：

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
> 如果您愿意，可以直接编辑 .csproj 文件。

## <a name="extra-information"></a>额外信息

属性设计器更改不仅适用于项目引用，还应用于项目引用。只要项目是 .NET 程序集，也可以为项目内的项设置 Ngen 元数据（使用上述相同的方法）。
