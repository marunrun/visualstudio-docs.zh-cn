---
title: MSBuild 15 中的新增功能 | Microsoft Docs
ms.date: 03/01/2017
ms.topic: conceptual
ms.assetid: 9976b6fd-d052-4017-b848-35b5bf4b2f66
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
monikerRange: '>=vs-2017'
ms.openlocfilehash: 2503040e074a62422d4c7c904f5ad3a2bd84d6c1
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77631024"
---
# <a name="whats-new-in-msbuild-15"></a>MSBuild 15 中的新增功能

MSBuild 现已推出，属于 [.NET Core SDK](https://www.microsoft.com/net/download/core)，且可在 Windows、macOS 和 Linux 上生成 .NET Core 项目。

## <a name="changed-path"></a>更改的路径

 MSBuild 现安装于每版 Visual Studio 下的文件夹中。 例如，C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\MSBuild。  也可使用下面的 PowerShell 模块查找 MSBuild：[vssetup.powershell](https://github.com/Microsoft/vssetup.powershell)。

 全局程序集缓存中不再安装 MSBuild。 若要以编程方式引用 MSBuild，请使用 NuGet 包。 有关详细信息，请参阅[更新 MSBuild 15.0 的现有应用程序](../msbuild/updating-an-existing-application.md)。

## <a name="changed-properties"></a>更改的属性

 下列 MSBuild 属性已因新版本号而更新。

- 此版工具的 `MSBuildToolsVersion` 为 15.0。 程序集版本为 15.1.0.0。

- `MSBuildToolsPath` 不再具有固定位置。 默认情况下，该文件位于与 Visual Studio 安装位置相对的 MSBuild\15.0\Bin 文件夹中，但 Visual Studio 安装位置可在安装时进行更改。 

- 注册表中不再设置 `ToolsVersion` 值。

- `SDK35ToolsPath` 和 `SDK40ToolsPath` 属性指向与此版 Visual Studio 一起打包的 .NET Framework SDK（例如，对于 4.X 工具，则指向 10.0A）。

## <a name="updates"></a>更新

- [项目元素](../msbuild/project-element-msbuild.md)具有新的 `SDK` 属性。 此外，`Xmlns` 属性现也是可选项。 有关 `SDK` 属性的详细信息，请参阅[如何：使用 MSBuild 项目 SDK](../msbuild/how-to-use-project-sdk.md)；[包、元包和框架](/dotnet/core/packages)；以及 [.NET Core 的 csproj 格式的新增内容](/dotnet/core/tools/csproj)。
- 目标外的[项元素](../msbuild/item-element-msbuild.md)具有新的 `Update` 属性。 此外，已放弃对 `Remove` 属性的限制。
- Directory.Build.props  是用户定义文件，对目录下的项目提供自定义选项。 除非 `ImportDirectoryBuildTargets` 属性设为 false，否则该文件将从 Microsoft.Common.props 自动导入。 Directory.Build.targets 由 Microsoft.Common.targets 导入。  
- 名称不与当前属性列表冲突的元数据可选择性地表示为属性。 有关详细信息，请参阅[项元素](../msbuild/item-element-msbuild.md)。

## <a name="new-property-functions"></a>新的属性函数

- 如果 `EnsureTrailingSlash` 尚不存在，它将向路径添加尾部斜杠。
- `NormalizePath` 组合路径元素，并确保输出字符串具有当前操作系统的正确目录分隔符字符。
- `NormalizeDirectory` 组合路径元素、确保尾部斜杠，并确保输出字符串具有当前操作系统的正确目录分隔符字符。
- `GetPathOfFileAbove` 返回此文件前紧邻的文件的路径。 它在功能上等效于调用 `<Import Project="$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), dir.props))\dir.props" />`

## <a name="see-also"></a>另请参阅

- [MSBuild](../msbuild/msbuild.md)
