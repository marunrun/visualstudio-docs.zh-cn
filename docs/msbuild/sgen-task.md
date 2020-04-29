---
title: SGen 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#SGen
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- SGen task [MSBuild]
- MSBuild, SGen task
ms.assetid: 22c5ade4-4159-4667-b891-0c1aa06f4df5
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cbf18c4477a164ec2e25a5ed4b2105f6fdad9130
ms.sourcegitcommit: 93859158465eab3423a0c0435f06490f0a456a57
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "82167431"
---
# <a name="sgen-task"></a>SGen 任务

创建指定程序集中的类型的 XML 序列化程序集。 此任务将包装 XML 序列化程序生成器工具 (Sgen.exe)  。 有关详细信息，请参阅 [XML 序列化程序生成器工具 (Sgen.exe)](/dotnet/framework/serialization/xml-serializer-generator-tool-sgen-exe)。

## <a name="parameters"></a>参数

 下表描述了 `SGen` 任务的参数。

| 参数 | 描述 |
|-----------------------------| - |
| `BuildAssemblyName` | 必选 `String` 参数。<br /><br /> 要为其生成序列化代码的程序集。 |
| `BuildAssemblyPath` | 必选 `String` 参数。<br /><br /> 要生成序列化代码的程序集的路径。 |
| `DelaySign` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则指定仅需要将公钥放在程序集中。 如果为 `false`，则指定需要完全签名的程序集。<br /><br /> 此参数无任何效果，除非与 `KeyFile` 或 `KeyContainer` 参数配合使用。 |
| `KeyContainer` | 可选 `String` 参数。<br /><br /> 指定保存密钥对的容器。 这样将会通过将公钥插入程序集清单来对程序集签名。 然后，此任务使用私钥对最终程序集进行签名。 |
| `KeyFile` | 可选 `String` 参数。<br /><br /> 指定要用于对程序集进行签名的密钥对或公钥。 编译器在程序集清单中插入公钥，然后使用私钥对最终的程序集进行签名。 |
| `Platform` | 可选 `String` 参数。<br /><br /> 获取或设置用于生成输出程序集的编译器平台。 此参数可以具有 `x86`、`x64` 或 `anycpu` 的值。 默认值为 `anycpu`。 |
| `References` | 可选 `String[]` 参数。<br /><br /> 指定由需要 XML 序列化的类型引用的程序集。 |
| `SdkToolsPath` | 可选 `String` 参数。<br /><br /> 指定 SDK 工具（例如 resgen.exe）的路径  。 |
| `SerializationAssembly` | 可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含生成的序列化程序集。 |
| `SerializationAssemblyName` | 可选 `String` 参数。<br /><br /> 指定生成的序列化程序集的名称。 |
| `ShouldGenerateSerializer` | 必选 `Boolean` 参数。<br /><br /> 如果为 `true`，则 SGen 任务应生成序列化程序集。 |
| `Timeout` | 可选 `Int32` 参数。<br /><br /> 指定终止任务可执行文件之前的时间量（以毫秒为单位）。 默认值是 `Int.MaxValue`，指示没有超时期限。 |
| `ToolPath` | 可选 `String` 参数。<br /><br /> 指定任务从中加载基础可执行文件 (sgen.exe) 的位置  。 如果未指定此参数，则任务会使用与运行 MSBuild 的框架版本对应的 SDK 安装路径。 |
| `Types` | 可选 `String[]` 参数。<br /><br /> 获取或设置要为其生成序列化代码的特定类型的列表。 SGen 将仅生成这些类型的序列化代码。 |
| `UseProxyTypes` | 必选 `Boolean` 参数。<br /><br /> 如果为 `true`，则 SGen 任务仅生成 XML Web service 代理类型的序列化代码。 |

[!INCLUDE [ToolTaskExtension arguments](includes/tooltaskextension-base-params.md)]

## <a name="see-also"></a>请参阅

- [任务参考](../msbuild/msbuild-task-reference.md)
- [任务](../msbuild/msbuild-tasks.md)
- [MSBuild 概念](../msbuild/msbuild-concepts.md)
