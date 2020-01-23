---
title: MSBuild 目标 Framework 和目标平台 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: df6517c5-edd6-4cc4-97ad-b3cdfc78e799
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b32960d46b4c7ae9b37cfec6cff97eb0540b868a
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75596770"
---
# <a name="msbuild-target-framework-and-target-platform"></a>MSBuild 目标框架和目标平台
可以生成要在目标框架  （.NET Framework 的一个特定版本）和目标平台  （一种特定的软件体系结构）上运行的项目。  例如，可将一个应用程序的目标设定为在与 802x86 处理器系列 (“x86”) 兼容的 32 位平台上的 .NET Framework 2.0 上运行。 目标框架与目标平台的组合称为“目标上下文”  。

> [!IMPORTANT]
> 本文介绍了指定目标框架的旧方法。 SDK 风格的项目支持不同的目标框架，例如 netstandard。 有关详细信息，请参阅[目标框架](/dotnet/standard/frameworks)。

## <a name="target-framework-and-profile"></a>目标框架和配置文件
 目标框架是将在其上运行项目的特定 .NET Framework 版本。 需要规范目标框架，因为它将启用专用于该框架版本的编译器功能和程序集引用。

 目前，以下版本的 .NET Framework 可供使用：

- .NET Framework 2.0（包含在 Visual Studio 2005 中）

- .NET Framework 3.0（包含在[!INCLUDE[wiprlhext](../debugger/includes/wiprlhext_md.md)] 中）

- .NET Framework 3.5（包含在[!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] 中）

- .NET Framework 4.5.2

- .NET Framework 4.6（包含在[!INCLUDE[vs_dev14](../misc/includes/vs_dev14_md.md)] 中）

- .NET Framework 4.6.1

- .NET Framework 4.6.2

- .NET Framework 4.7

- .NET Framework 4.7.1

- .NET Framework 4.7.2

- .NET Framework 4.8

在可供引用的各程序集的列表中，.NET Framework 的版本各不相同。 例如，不能生成 Windows Presentation Foundation (WPF) 应用程序，除非项目面向 .NET Framework 3.0 或更高版本。

目标框架是在项目文件中的 `TargetFrameworkVersion` 属性中指定的。 可通过在 Visual Studio 集成开发环境 (IDE) 中使用项目属性页来更改项目的目标框架。 有关详细信息，请参阅[如何：面向 .NET Framework 的某个版本](../ide/visual-studio-multi-targeting-overview.md)。 `TargetFrameworkVersion` 的可用值包括 `v2.0`、`v3.0`、`v3.5`、`v4.5.2`、`v4.6`、`v4.6.1`、`v4.6.2`、`v4.7`、`v4.7.1`、`v4.7.2` 和 `v4.8`。

```xml
<TargetFrameworkVersion>v4.0</TargetFrameworkVersion>
```

 目标概况  是目标框架的一个子集。 例如，.NET Framework 4 客户端配置文件不包括对 MSBuild 程序集的引用。

 > [!NOTE]
 > 目标配置文件仅适用于[可移植类库](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library)。

 目标配置文件是在项目文件中的 `TargetFrameworkProfile` 属性中指定的。 可通过在 IDE 中使用项目属性页中的目标框架控件来更改目标概况。

```xml
<TargetFrameworkVersion>v4.0</TargetFrameworkVersion>
<TargetFrameworkProfile>Client</TargetFrameworkProfile>
```

## <a name="target-platform"></a>目标平台
 平台  是定义特定运行时环境的硬件和软件的组合。 例如，应用于对象的

- `x86` 指定在 Intel 80x86 处理器或等效处理器上运行的 32 位 Windows 操作系统。

- `x64` 指定在 Intel x64 处理器或等效处理器上运行的 64 位 Windows 操作系统。

- `Xbox` 指定 Microsoft Xbox 360 平台。

目标平台  是指将在其上运行生成项目的特定平台。 目标平台是在项目文件中的 `PlatformTarget` 生成属性中指定的。 可通过在 IDE 中使用项目属性页或**配置管理器**来更改目标平台。

```xml
<PropertyGroup>
   <PlatformTarget>x86</PlatformTarget>
</PropertyGroup>

```

目标配置  是目标平台的一个子集。 例如，`x86``Debug` 配置不包括大多数代码优化项。 目标配置是在项目文件中的 `Configuration` 生成属性中指定的。 可通过使用项目属性页或**配置管理器**来更改目标配置。

```xml
<PropertyGroup>
   <PlatformTarget>x86</PlatformTarget>
   <Configuration>Debug</Configuration>
<PropertyGroup>

```

## <a name="see-also"></a>请参阅
- [多定向](../msbuild/msbuild-multitargeting-overview.md)
