---
title: FXC 任务 | Microsoft Docs
ms.date: 03/10/2019
ms.topic: reference
f1_keywords:
- vc.task.fxc
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (C++), FXC task
- FXC task (MSBuild (C++))
author: corob-msft
ms.author: corob
ms.workload:
- multiple
ms.openlocfilehash: 67958a1a1ebb2ff382d0896e2fbaec6105c0c785
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77279284"
---
# <a name="fxc-task"></a>FXC 任务

在生成过程中使用 HLSL 着色器编译器。

## <a name="parameters"></a>参数

下表介绍了 FXC 任务的参数  。

|参数|说明|
|---------------|-----------------|
|**AdditionalIncludeDirectories**|可选的 string[]  参数。<br/><br/>指定一个或多个要添加到包含路径中的目录；存在多个目录时，请用分号分隔。<br/><br/>请使用 `/I[path]`。|
|**AdditionalOptions**|可选的 string  参数。|
|**AllResourcesBound**|可选的 bool  参数。<br/><br/>编译器假定着色器可引用的所有资源已绑定，并且在着色器执行期间处于良好状态。 适用于着色器模型 5.1 及更高版本。<br/><br/>请使用 `/all_resources_bound`。|
|**AssemblerOutput**|可选的 string  参数。<br/><br/>指定汇编语言输出文件的内容。<br/><br/>请使用 `/Fc, /Fx`。<br/><br/>**NoListing**<br/>**AssemblyCode**，使用 `Fc`。<br/>**AssemblyCodeAndHex**，使用 `Fx`。|
|**AssemblerOutputFile**|可选的 string  参数。<br/><br/>指定程序集代码清单文件的文件名。|
|**CompileD2DCustomEffect**|可选的 bool  参数。<br/><br/>编译包含像素着色器的 Direct2D 自定义效果。 请勿用于顶点或计算自定义效果。|
|**ConsumeExportFile**|可选的 string  参数。|
|**DisableOptimizations**|可选的 bool  参数。<br/><br/>禁用优化。<br/><br/>`/Od` 是指 `/Gfp`，但输出可能与 `/Od /Gfp` 不同。|
|**EnableDebuggingInformation**|可选的 bool  参数。<br/><br/>启用调试信息。|
|**EnableUnboundedDescriptorTables**|可选的 bool  参数。<br/><br/>通知编译器：着色器可能包含具有未绑定范围的资源数组的声明。 适用于着色器模型 5.1 及更高版本。<br/><br/>请使用 `/enable_unbounded_descriptor_tables`。|
|**EntryPointName**|可选的 string  参数。<br/><br/>为着色器指定入口点名称。<br/><br/>请使用 `/E[name]`。|
|**GenerateExportFile**|可选的 string  参数。|
|**GenerateExportShaderProfile**|可选的 string  参数。|
|**HeaderFileOutput**|可选的 string  参数。<br/><br/>为包含对象代码的头文件指定名称。<br/><br/>请使用 `/Fh [name]`。|
|**ObjectFileOutput**|可选的 string  参数。<br/><br/>为对象文件指定名称。<br/><br/>请使用 `/Fo [name]`。|
|**PreprocessorDefinitions**|可选的 string[]  参数。<br/><br/>为源文件定义预处理符号。|
|**SetRootSignature**|可选的 string  参数。<br/><br/>将根签名附加到着色器字节码。 适用于着色器模型 5.0 及更高版本。<br/><br/>请使用 `/setrootsignature`。|
|**ShaderModel**|可选的 string  参数。<br/><br/>指定着色器模型。 部分着色器类型只能与最新的着色器模型搭配使用。<br/><br/>请使用 `/T [type]_[model]`。|
|**ShaderType**|可选的 string  参数。<br/><br/>指定着色器的类型。<br/><br/>请使用 `/T [type]_[model]`。<br/><br/>**Effect**，使用 `fx`。<br/>**Vertex**，使用 `vs`。<br/>**Pixel**，使用 `ps`。<br/>**Geometry**，使用 `gs`。<br/>**Hull**，使用 `hs`。<br/>**Domain**，使用 `ds`。<br/>**Compute**，使用 `cs`。<br/>**Library**，使用 `lib`。<br/>**RootSignature**，生成根签名对象。|
|**源**|必需的 ITaskItem  参数。|
|**SuppressStartupBanner**|可选的 bool  参数。<br/><br/>取消显示启动版权标志和信息消息。<br/><br/>请使用 `/nologo`。|
|**TrackerLogDirectory**|可选的 string  参数。|
|**TreatWarningAsError**|可选的 bool  参数。<br/><br/>将所有编译器警告视为错误。<br/><br/>对于新项目，最好在所有编译中使用 `/WX`；对所有警告进行解析可确保将可能难以发现的代码缺陷减至最少。|
|**VariableName**|可选的 string  参数。<br/><br/>为头文件中的变量名称指定名称。<br/><br/>请使用 `/Vn [name]`。|

## <a name="see-also"></a>另请参阅

[任务参考](../msbuild/msbuild-task-reference.md)