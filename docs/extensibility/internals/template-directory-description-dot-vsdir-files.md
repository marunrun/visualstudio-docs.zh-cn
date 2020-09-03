---
title: 模板目录说明 (。Vsdir) 文件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .vsdir files
- VSDIR files
- template directory description files
ms.assetid: 9df51800-190e-4662-b685-fdaafcff1400
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 16ba609d5b05d565a12b38bd19e9a777851ced5b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80704691"
---
# <a name="template-directory-description-vsdir-files"></a>模板目录说明 (.Vsdir) 文件
模板目录说明文件 () 是一个文本文件，该文件可使集成开发环境 (IDE) 显示与对话框中的项目相关联的文件夹、向导 .vsz 文件和模板文件。 内容包含每个文件或文件夹的一条记录。 尽管仅提供了一个 vsdir 文件来描述多个文件夹、向导或模板文件，但引用的位置中的所有 vsdir 文件都将合并。

 文件夹 (子目录) ，在 vsdir 文件中引用的文件，并且该文件本身都位于同一个目录中。 当 IDE 运行向导或在 " **新建项目** " 或 " **添加新项** " 对话框中显示文件夹或文件时，ide 将检查包含已执行文件的目录，以确定是否存在一个 vsdir 文件。 如果找到了一个 vsdir 文件，则 IDE 将读取该文件，以确定它是否包含用于执行或显示的文件夹或文件的项。 如果找到了一个条目，IDE 将使用执行向导或显示内容中的信息。

 下面的代码示例来自 \<EnvSDK> \bscprj\bscprj\bscprjprojectitems\ Source_Files 注册表项中的文件 SourceFiles：

```
HeaderFile.h|{E59935A1-6156-11d1-87A6-00A0C91E2A46}|#125|130|#126|0|0|0|#127
SourceFile.cpp|{E59935A1-6156-11d1-87A6-00A0C91E2A46}|#122|110|#123|0|0|0|#124
```

 在这种情况下，一个文件中有两个记录。 换行 (回车符) 分隔每条记录。 每行表示不同的文件类型。 管道 ( 将每个记录中的字段隔开) 字符。 单个目录可以包含多个文件名称不同的 vsdir 文件，也可以为每个文件类型使用一个 vsdir 文件。

## <a name="fields"></a>字段
 下表列出了为每个记录指定的字段。

| 字段 | 说明 |
| - | - |
| 相对路径名 (RelPathName)  | 文件夹、模板或 .vsz 文件的名称，如 HeaderFile 或 MyWizard。 此字段还可以是用于表示文件夹的名称。 |
| {clsidPackage} | 支持访问本地化字符串的 VSPackage 的 GUID，例如 LocalizedName、Description、IconResourceId 和 SuggestedBaseName，在 VSPackage 的附属动态链接库中 (DLL) 资源。 如果未提供 DLLPath，则适用 IconResourceId。 **注意：**  此字段是可选的，除非以前的一个字段是资源标识符。 对于与不本地化文本的第三方向导对应的 vsdir 文件，此字段通常为空白。 |
| LocalizedName | 模板文件或向导的本地化名称。 此字段可以是 "#ResID" 形式的字符串或资源标识符。 此名称将显示在 " **添加新项** " 对话框中。 **注意：**  如果 LocalizedName 是资源标识符，则需要 {clsidPackage}。 |
| SortPriority | 一个整数，表示此模板文件或向导的相对优先级。 例如，如果此项的值为1，则此项将显示在值为1且早于排序值为2或更大的所有项的其他项的旁边。<br /><br /> 排序优先级相对于同一目录中的项。 同一个目录中可能有多个 vsdir 文件。 在这种情况下，从所有的项 <em>。</em>合并该目录中的 vsdir 文件。 具有相同优先级的项将在显示名称的不区分大小写的字典顺序中列出。 `_wcsicmp`函数用于对项进行排序。<br /><br /> 不在 vsdir 文件中描述的项包括比 vsdir 文件中列出的最高优先级数字大的优先级数。 结果就是这些项位于显示列表的末尾，而不考虑它们的名称。 |
| 说明 | 模板文件或向导的本地化说明。 此字段可以是 "#ResID" 形式的字符串或资源标识符。 选择该项时，此字符串出现在 " **新建项目** " 或 " **添加新项** " 对话框中。 |
| DLLPath 或 {clsidPackage} | 用于加载模板文件或向导的图标。 使用 IconResourceId 将该图标作为资源从 .dll 或 .exe 文件加载。 可以通过使用完整路径或使用 VSPackage 的 GUID 来标识此 .dll 或 .exe 文件。 VSPackage 的实现 DLL 用于加载)  (附属 DLL 的图标。 |
| IconResourceId | DLL 或 VSPackage 实现 DLL 中用于确定要显示的图标的资源标识符。 |
| 标志 (<xref:Microsoft.VisualStudio.Shell.Interop.__VSDIRFLAGS>)  | 用于禁用或启用 "**添加新项**" 对话框中的 "**名称**" 和 "**位置**" 字段。 " **标志** " 字段的值是所需位标志的组合的十进制等效项。<br /><br /> 当用户在 " **新建** " 选项卡上选择项时，项目将确定 " **添加新项** " 对话框首次显示时是否显示 "名称" 字段和 "位置" 字段。 一个项，通过一个 vsdir 文件，只可以控制在选定该项时是否启用和禁用这些字段。 |
| SuggestedBaseName | 表示文件、向导或模板的默认名称。 此字段是字符串或 "#ResID" 形式的资源标识符。 IDE 使用此值提供项的默认名称。 此基值追加了一个整数值，以使名称唯一，如 MyFile21。<br /><br /> 在上面的列表中，Description、DLLPath、IconResourceId、Flags 和 SuggestedBaseNumber 仅适用于模板和向导文件。 这些字段不适用于文件夹。 \BscPrj\BscPrj\BscPrjProjectItems 注册表项中的 BscPrjProjectItems 文件中的代码演示了这一事实 \<EnvSDK> 。 此文件包含三个记录，每个文件夹 (一个记录，每个记录有四个字段) ： RelPathName、{clsidPackage}、LocalizedName 和 SortPriority。<br /><br /> `General&#124;{E59935A1-6156-11d1-87A6-00A0C91E2A46}&#124;#110&#124;100`<br /><br /> `Source_Files&#124;{E59935A1-6156-11d1-87A6-00A0C91E2A46}&#124;#111&#124;110`<br /><br /> `Env&#124;{E59935A1-6156-11d1-87A6-00A0C91E2A46}&#124;#112&#124;120` |

 创建向导文件时，还应考虑以下问题。

- 没有有意义的数据的任何非必选字段应包含 0 (零) 作为占位符。

- 如果未提供本地化名称，则在向导文件中使用相对路径名称。

- DLLPath 重写图标位置的 clsidPackage。

- 如果未定义图标，则 IDE 会将具有该扩展名的文件替换为默认图标。

- 如果未提供任何建议的基名称，则使用 "项目"。

- 如果删除 .vsz 文件、文件夹或模板文件，还必须从 vsdir 文件中删除其关联记录。

## <a name="see-also"></a>另请参阅
- [向导](../../extensibility/internals/wizards.md)
- [向导 (.Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
