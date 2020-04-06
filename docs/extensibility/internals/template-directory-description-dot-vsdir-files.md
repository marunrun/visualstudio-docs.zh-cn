---
title: 模板目录描述 （.Vsdir） 文件 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704691"
---
# <a name="template-directory-description-vsdir-files"></a>模板目录说明 (.Vsdir) 文件
模板目录描述文件 （.vsdir） 是一个文本文件，使集成开发环境 （IDE） 能够在对话框中显示与项目关联的文件夹、向导 .vsz 文件和模板文件。 内容包括每个文件或文件夹的一条记录。 引用位置中的所有 .vsdir 文件都将合并，尽管通常只提供一个 .vsdir 文件来描述多个文件夹、向导或模板文件。

 文件夹（子目录）、在 .vsdir 文件中引用的文件和 .vsdir 文件本身都位于同一目录中。 当 IDE 运行向导或在 **"新项目**"或 **"添加新项目"** 对话框中显示文件夹或文件时，IDE 将检查包含已执行文件的目录，以确定是否存在 .vsdir 文件。 如果找到 .vsdir 文件，IDE 会读取该文件以确定它是否包含已执行或显示的文件夹或文件的条目。 如果找到条目，IDE 将使用信息执行向导或显示内容。

 以下代码示例来自\<envSDK>_BscPrj_BscPrj_BscPrjProjectItem_Source_Files注册表项中的文件 SourceFiles.vsdir：

```
HeaderFile.h|{E59935A1-6156-11d1-87A6-00A0C91E2A46}|#125|130|#126|0|0|0|#127
SourceFile.cpp|{E59935A1-6156-11d1-87A6-00A0C91E2A46}|#122|110|#123|0|0|0|#124
```

 在这种情况下，两个记录位于一个文件中。 新行（回车符）分隔每个记录。 每行表示不同的文件类型。 管道（&#124;）字符分隔每个记录中的字段。 单个目录可以包含多个具有不同文件名的 .vsdir 文件，也可以为每个文件类型具有一个 .vsdir 文件。

## <a name="fields"></a>字段
 下表列出了为每个记录指定的字段。

| 字段 | 说明 |
| - | - |
| 相对路径名称（RelPath 名称） | 文件夹、模板或 .vsz 文件的名称，如 headerfile.h 或 MyWizard.vsz。 此字段也可以是用于表示文件夹的名称。 |
| [clsid 包] | VSPackage 的 GUID，用于在 VSPackage 的卫星动态链接库 （DLL） 资源中访问本地化字符串，如本地化名称、描述、图标资源 Id 和建议的 BaseName。 如果未提供 DLLPath，则应用图标资源 Id。 **注：** 此字段是可选的，除非前面的一个或多个字段是资源标识符。 此字段对于与不本地化其文本的第三方向导对应的第三方向导对应的 .vsdir 文件通常为空。 |
| 本地化名称 | 模板文件或向导的本地化名称。 此字段可以是窗体"#ResID"的字符串或资源标识符。 此名称显示在"**添加新项目"** 对话框中。 **注：** 如果本地化名称是资源标识符，则需要 [clsid 包]。 |
| 排序优先级 | 表示此模板文件或向导的相对优先级的整数。 例如，如果此项的值为 1，则此项将显示在值为 1 的其他项旁边，并领先于排序值为 2 或更大的所有项。<br /><br /> 排序优先级相对于同一目录中的项。 同一目录中可能有多个 .vsdir 文件。 在这种情况下，所有 中的项<em>。</em>该目录中的 vsdir 文件将合并。 具有相同优先级的项目按显示名称的区分大小写的词典顺序列出。 该`_wcsicmp`函数用于对项目进行排序。<br /><br /> .vsdir 文件中未描述的项包括大于 .vsdir 文件中列出的最大优先级编号的优先级编号。 结果是这些项目位于显示列表的末尾，而不考虑其名称。 |
| 描述 | 模板文件或向导的本地化说明。 此字段可以是窗体"#ResID"的字符串或资源标识符。 选中**项目**时，此字符串将显示在"**新项目"或"添加新项目**"对话框中。 |
| DLLPath 或 [clsid 包] | 用于加载模板文件或向导的图标。 使用 IconResourceId 将图标加载为 .dll 或 .exe 文件中的资源。 此 .dll 或 .exe 文件可以通过使用完整路径或使用 VSPackage 的 GUID 进行标识。 VSPackage 的实现 DLL 用于加载图标（而不是卫星 DLL）。 |
| 图标资源 Id | DLL 或 VSPackage 实现 DLL 中的资源标识符，用于确定要显示的图标。 |
| 标志<xref:Microsoft.VisualStudio.Shell.Interop.__VSDIRFLAGS>（ ） | 用于禁用或启用"**添加新项目**"对话框上的 **"名称**和**位置**"字段。 **"标志"** 字段的值是所需位标志组合的十进制等效项。<br /><br /> 当用户在 **"新建"** 选项卡上选择项目时，项目将确定在首次显示"**添加新项目"** 对话框时是否显示"名称"字段和"位置"字段。 通过 .vsdir 文件的项目只能控制字段是否启用，在选择项目时是否禁用。 |
| 建议的基本名称 | 表示文件、向导或模板的默认名称。 此字段是窗体"#ResID"的字符串或资源标识符。 IDE 使用此值为项提供默认名称。 此基值附加了整数值，以使名称唯一，例如 MyFile21.asp。<br /><br /> 在上一个列表中，描述、DLLPath、图标资源Id、标志和建议BaseNumber仅适用于模板和向导文件。 这些字段不适用于文件夹。 这一事实在\<EnvSDK>_BscPrj_BscPrj_BscPrjProjectItems 注册表项中的 BscPrjProjectItems 文件中的代码中进行了说明。 此文件包含三个记录（每个文件夹一个），每个记录有四个字段：RelPathName、[clsidPackage]、本地化名称和排序优先级。<br /><br /> `General&#124;{E59935A1-6156-11d1-87A6-00A0C91E2A46}&#124;#110&#124;100`<br /><br /> `Source_Files&#124;{E59935A1-6156-11d1-87A6-00A0C91E2A46}&#124;#111&#124;110`<br /><br /> `Env&#124;{E59935A1-6156-11d1-87A6-00A0C91E2A46}&#124;#112&#124;120` |

 创建向导文件时，还应考虑以下问题。

- 任何没有有意义的数据的非必需字段都应包含 0（零）作为占位符。

- 如果未提供本地化名称，则向导文件中将使用相对路径名称。

- DLLPath 覆盖图标位置的 clsid 包。

- 如果未定义图标，IDE 将默认图标替换为具有该扩展名的文件。

- 如果未提供建议的基本名称，则使用"项目"。

- 如果删除 .vsz 文件、文件夹或模板文件，还必须从 .vsdir 文件中删除其关联的记录。

## <a name="see-also"></a>请参阅
- [向导](../../extensibility/internals/wizards.md)
- [向导 (.Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
