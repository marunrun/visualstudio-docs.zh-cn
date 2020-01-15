---
title: 多目标项目
description: 本文档概述了如何在 Visual Studio for Mac 中设置多目标项目。
ms.topic: overview
author: jmatthiesen
ms.author: jomatthi
ms.date: 12/12/2019
ms.assetid: 2a561af4-f1fe-493e-9a53-aa6d77d15498
ms.openlocfilehash: 3d1372ab5bd08ce164352293ec9d341ca567e3d5
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75439042"
---
# <a name="projects-with-multiple-target-frameworks"></a>具有多个目标框架的项目
在 Visual Studio for Mac 中，可将 Xamarin 或 .NET Core 项目配置为在若干 .NET Framework 版本的任一版本和若干系统平台的任一平台上运行。 例如，可以将项目设定为在 .NET Framework 4.6 和 .NET Core 3.1 上运行。 

有关目标框架的详细信息，请参阅[目标框架](/dotnet/standard/frameworks)。

> [!NOTE] 
> 本主题适用于 Visual Studio for Mac。 对于 Windows 上的 Visual Studio，请参阅[框架定位概述](/visualstudio/ide/visual-studio-multi-targeting-overview)。

## <a name="targeting-multiple-frameworks"></a>面向多个框架

目标框架在项目文件中指定，可通过右键单击项目并选择“工具”>“编辑文件”  命令来编辑。 指定单个目标框架时，使用 TargetFramework 元素。 以下控制台应用项目文件演示了如何以 .NET Core 3.0 为目标：

```XML
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.0</TargetFramework>
  </PropertyGroup>

</Project>
```

将复数形式的 TargetFrameworks 元素与多个目标框架一起使用：

```XML
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard1.4;net40;net45</TargetFrameworks>
  </PropertyGroup>
```

详细了解如何[面向多个框架](/dotnet/standard/frameworks#how-to-specify-target-frameworks)。

## <a name="working-with-code-in-a-multi-target-project"></a>处理多目标项目中的代码
当你在具有多个目标框架的项目中编辑 C# 文件时，可以指定想要用于指导编辑器体验的目标框架（例如，如果使用该框架不支持的 API，则显示警告）。 可以使用编辑器窗口左上角的“目标框架”  选择器来更改目标框架。

![使用“目标框架”选择器更改位于编辑器窗口顶部的目标框架](media/project-multitargeting-framework-selector.png)

有时，需要根据应用程序面向的平台调用不同 API。 为此，可以编写条件代码来编译特定平台的代码：

```C#
public class MyClass
{
    static void Main()
    {
#if NET40
        Console.WriteLine("Target framework: .NET Framework 4.0");
#elif NET45  
        Console.WriteLine("Target framework: .NET Framework 4.5");
#else
        Console.WriteLine("Target framework: .NET Standard 1.4");
#endif
    }
}
```

编写代码时，你将在 IntelliSense 自动完成建议中看到警告，从而知晓应用程序支持的任何目标框架是否缺少特定 API。

![IntelliSense 中显示警告消息，API 将不适用于指定的目标框架。 示例文本：命名空间 System.Buffers、SharedUtils (netstandard2.0) - 不可用。 你可以使用导航栏切换上下文。](media/project-multitargeting-intellisense-warnings.png)

## <a name="see-also"></a>请参阅

- [框架定位概述 (Windows)](/visualstudio/ide/visual-studio-multi-targeting-overview)
- [SDK 样式项目中的目标框架](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
