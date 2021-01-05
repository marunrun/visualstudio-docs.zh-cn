---
title: VSIX v3 中的 Ngen 支持 |Microsoft Docs
description: 了解如何启用本机映像生成器，这是一个扩展开发人员可以用来提高托管应用程序性能的工具。
ms.custom: SEO-VS-2020
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 1472e884-c74e-4c23-9d4a-6d8bdcac043b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 064176a0a28e3621e796bf60ede552f9cda155b0
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97864036"
---
# <a name="ngen-support-in-vsix-v3"></a>VSIX v3 中的 Ngen 支持

在 Visual Studio 2017 和新的 VSIX v3 (版本 3) 扩展清单格式中，扩展开发人员现在可以在安装时 "ngen" 其程序集。

下面是 MSDN 的摘录，其中说明了 "ngen" 的作用：

>本机映像生成器 (*Ngen.exe*) 是改进托管应用程序性能的工具。 *Ngen.exe* 创建本机映像（包含已编译的处理器特定机器代码的文件），并将其安装到本地计算机上的本机映像缓存中。 运行时可从缓存中使用本机映像，而不必使用实时 (JIT) 编译器编译原始程序集。
>
>from [Ngen.exe (本机映像生成器) ](/dotnet/framework/tools/ngen-exe-native-image-generator)

若要将程序集作为 "ngen"，必须安装 VSIX "每台计算机的实例"。 可以通过选中设计器中的 "所有用户" 复选框来启用此功能 `extension.vsixmanifest` ：

![检查所有用户](media/check-all-users.png)

## <a name="how-to-enable-ngen"></a>如何启用 Ngen

若要为程序集启用 ngen，可以使用 Visual Studio 中的 " **属性** " 窗口。

可以设置四个属性：

1. **Ngen** (布尔) -如果为 true，则 Visual Studio 安装程序将 "Ngen" 程序集。
2. **Ngen 应用程序** (字符串) -Ngen 提供了使用应用程序的 *app.config* 文件来解析程序集依赖项的机会。 应将此值设置为要使用的应用程序，该应用程序的 *app.config* 需要使用 (相对于 Visual Studio 安装目录的) 。
3. **Ngen 体系结构** (枚举) -本机编译程序集的体系结构。 选项为：。 NotSpecified b。 X86 c。 X64 d。 全部
4. **Ngen 优先级** (1 到 3) 之间的整数-ngen 优先级别记录在 [Ngen.exe 优先级别](/dotnet/framework/tools/ngen-exe-native-image-generator#priority-levels)。

下面是 " **属性** " 窗口中的 "操作"：

![属性中的 ngen](media/ngen-in-properties.png)

这会将元数据添加到 VSIX 项目的 *.csproj* 文件中的项目引用：

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
> 如果愿意，可以直接编辑 .csproj 文件。

## <a name="extra-information"></a>额外的信息

属性设计器的更改仅适用于项目引用;只要项是 .NET 程序集，就可以使用) 以上所述的相同方法，在项目内部为项目设置 Ngen 元数据 (。
