---
title: 对 MSBuild 问题进行故障排除并为其创建日志
ms.date: 06/27/2019
ms.technology: vs-ide-compile
ms.topic: troubleshooting
helpviewer_keywords:
- msbuild logs"
author: corob-msft
ms.author: corob
manager: jillfra
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.description: Generate build logs for msbuild projects to collect helpful information when troubleshooting issues.
ms.openlocfilehash: 24df9f7c44ea2dbb9e9899abf68823683422da71
ms.sourcegitcommit: 9a7fb8556a5f3dbb4459122fefc7e7a8dfda753a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2020
ms.locfileid: "87235064"
---
# <a name="troubleshoot-and-create-logs-for-msbuild-problems"></a>对 MSBuild 问题进行故障排除并为其创建日志

以下过程可以帮助你诊断 Visual Studio 项目中的生成问题，并在必要时创建日志以发送给 Microsoft 进行调查。

## <a name="a-property-value-is-ignored"></a>一个属性值被忽略

如果项目属性看上去设置为特定值，但对生成没有影响，请按照下列步骤进行操作：

1. 打开与你的 Visual Studio 版本对应的 Visual Studio 开发人员命令提示符。
1. 在替换解决方案路径、配置和项目名称的值后，运行以下命令：

    ```cmd
    msbuild /p:SolutionDir="c:\MySolutionDir\";Configuration="MyConfiguration";Platform="Win32" /pp:out.xml MyProject.vcxproj
    ```

    此命令将生成一个“预处理”msbuild 项目文件 (out.xml)。 你可以在该文件中搜索特定属性以查看其定义位置。

属性的最后一个定义是生成使用了什么。 如果设置了两次属性，则第二个值将覆盖第一个值。 此外，MSBuild 还会评估多个传递中的项目：

- PropertyGroups 和 Imports
- ItemDefinitionGroups
- ItemGroups
- 目标

因此，给定以下顺序：

```xml
<PropertyGroup>
   <MyProperty>A</MyProperty>
</PropertyGroup>
<ItemGroup>
   <MyItems Include="MyFile.txt"/>
</ItemGroup>
<ItemDefinitionGroup>
  <MyItems>
      <MyMetadata>$(MyProperty)</MyMetadata>
  </MyItems>
</ItemDefinitionGroup>
<PropertyGroup>
   <MyProperty>B</MyProperty>
</PropertyGroup>
```

在生成期间，“MyFile.txt”项的“MyMetadata”值将评估为“B”（不是“A”，也不是空）

## <a name="incremental-build-is-building-more-than-it-should"></a>增量生成的生成超出预期

如果 MSBuild 不必要地重新生成项目或项目项，请创建详细的生成日志或二进制生成日志。 你可以在该日志中搜索不必要地生成或编译的文件。 输出的内容与以下类似：

```output
  Task "CL"

  Using cached input dependency table built from:

  F:\test\Project1\Project1\Debug\Project1.tlog\CL.read.1.tlog

  Outputs for F:\TEST\PROJECT1\PROJECT1\PROJECT1.CPP:
  F:\TEST\PROJECT1\PROJECT1\DEBUG\PROJECT1.OBJ
  Project1.cpp will be compiled because F:\TEST\PROJECT1\PROJECT1\PROJECT1.H was modified at 6/5/2019 12:37:09 PM.

  Outputs for F:\TEST\PROJECT1\PROJECT1\PROJECT1.CPP:
  F:\TEST\PROJECT1\PROJECT1\DEBUG\PROJECT1.OBJ

  Write Tracking Logs:
  Debug\Project1.tlog\CL.write.1.tlog
```

如果是在 Visual Studio IDE 中生成（输出窗口详细程度为详细），输出窗口将显示每个项目不是最新的原因：

```output
1>------ Up-To-Date check: Project: Project1, Configuration: Debug Win32 ------

1>Project is not up-to-date: build input 'f:\test\project1\project1\project1.h' was modified after the last build finished.
```

## <a name="create-a-binary-msbuild-log"></a>创建二进制 msbuild 日志

1. 打开你的 Visual Studio 版本的开发人员命令提示符
1. 从命令提示符中运行以下命令之一。 （记得使用你的实际项目和配置值。）：

    ```cmd
    Msbuild /p:Configuration="MyConfiguration";Platform="x86" /bl MySolution.sln
    ```

    or

    ```cmd
    Msbuild /p:/p:SolutionDir="c:\MySolutionDir\";Configuration="MyConfiguration";Platform="Win32" /bl MyProject.vcxproj
    ```

将在运行 MSBuild 的目录中创建 Msbuild.binlog 文件。 你可以使用 [Msbuild 结构化日志查看器](http://www.msbuildlog.com/)查看和搜索该文件。

## <a name="create-a-detailed-log"></a>创建详细的日志

1. 从 Visual Studio 主菜单中，转到“工具” > “选项” > “项目和解决方案” >“生成并运行”。
1. 在两个组合框中，将“Msbuild 项目生成详细程度”设置为“详细”。 上面的组合框控制“输出窗口”中的生成详细程度，第二个组合框控制生成期间在每个项目的中间目录中创建的 \<projectname\>.log 文件中的生成详细程度。
2. 从 Visual Studio 开发人员命令提示符中，输入以下命令之一，替换你的实际路径和配置值：

    ```cmd
    Msbuild /p:Configuration="MyConfiguration";Platform="x86" /fl MySolution.sln
    ```

    or

    ```cmd
    Msbuild /p:/p:SolutionDir="c:\MySolutionDir\";Configuration="MyConfiguration";Platform="Win32" /fl MyProject.vcxproj
    ```

    将在运行 msbuild 的目录中创建 Msbuild.log 文件。

## <a name="see-also"></a>请参阅

- [Visual Studio 故障排除](/troubleshoot/visualstudio/welcome-visual-studio/)
