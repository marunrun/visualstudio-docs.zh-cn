---
title: 向视觉设计器公开类型 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- types [Visual Studio SDK], exposing to visual designers
- designers [Visual Studio SDK], exposing types
- custom tools, exposing types to visual designers
ms.assetid: a7a32ad4-3a0a-4eb8-a6ac-491c42885639
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9067f88b4bf1334e23a548bc6a2cbeb3eac6ad33
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708437"
---
# <a name="expose-types-to-visual-designers"></a>向可视化设计器公开类型
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]必须在设计时访问类和类型定义才能显示可视化设计器。 类从预定义的程序集集加载，其中包括当前项目的完整依赖项集（引用及其依赖项）。 可视化设计人员可能还需要访问在自定义工具生成的文件中定义的类和类型。

 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]和[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]项目系统支持通过临时可移植可执行文件（临时 P）访问生成的类和类型。 自定义工具生成的任何文件都可以编译到临时程序集中，以便可以从这些程序集加载类型并公开给设计人员。 每个自定义工具的输出都编译成单独的临时 PE，此临时编译的成败仅取决于是否可以编译生成的文件。 即使项目可能无法作为一个整体进行构建，但各个临时 P 可能仍可供设计人员使用。

 项目系统完全支持跟踪对自定义工具的输出文件的更改，前提是这些更改是运行自定义工具的结果。 每次运行自定义工具时，都会生成新的临时 PE，并将适当的通知发送给设计人员。

> [!NOTE]
> 由于临时程序可执行生成文件发生在后台，因此在编译失败时不会向用户报告任何错误。

 利用临时 PE 支持的自定义工具必须遵循以下规则：

- **生成设计时间源**必须在注册表中设置为 1。

     没有此设置，则不执行任何程序可执行文件编译。

- 生成的代码必须与全局项目设置的语言相同。

     无论自定义工具在注册表中<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A>设置为 1 时，无论自定义工具作为请求的扩展报告**GeneratesDesignTimeSource**什么，都会编译临时 PE。 扩展不需要是 *.vb、.cs**.cs*或 *.jsl;* 它可以是任何扩展。

- 自定义工具生成的代码必须有效，并且必须仅使用执行完时<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A>项目中存在的引用集自行编译。

     编译临时 PE 时，提供给编译器的唯一源文件是自定义工具输出。 因此，使用临时 PE 的自定义工具必须生成可独立于项目中其他文件编译的输出文件。

## <a name="see-also"></a>请参阅
- [BuildManager 对象的简介](https://msdn.microsoft.com/library/50080ec2-c1c9-412c-98ef-18d7f895e7fa)
- [实现单文件生成器](../../extensibility/internals/implementing-single-file-generators.md)
- [注册单文件生成器](../../extensibility/internals/registering-single-file-generators.md)
