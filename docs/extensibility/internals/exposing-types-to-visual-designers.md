---
title: 向可视化设计器公开类型 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80708437"
---
# <a name="expose-types-to-visual-designers"></a>向可视化设计器公开类型
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 必须能够在设计时访问类和类型定义，才能显示可视化设计器。 从一组预定义的程序集加载类，这些程序集包括当前项目 (引用及其依赖项) 的完整依赖项集。 可视化设计器还可能需要访问自定义工具所生成的文件中定义的类和类型。

 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]和 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 项目系统通过临时的可执行文件 (临时的 pe) 来支持访问生成的类和类型。 自定义工具生成的任何文件都可以编译为临时程序集，以便可以从这些程序集加载类型并将其公开给设计器。 每个自定义工具的输出编译到单独的临时 PE 中，此临时编译的成功或失败只取决于是否可以编译生成的文件。 尽管项目可能不会作为一个整体进行生成，但设计器仍可以使用单个临时的 Pe。

 项目系统提供对自定义工具的输出文件的跟踪更改的完全支持，前提是这些更改是运行自定义工具的结果。 每次运行自定义工具时，都会生成一个新的临时 PE，并向设计器发送相应的通知。

> [!NOTE]
> 由于临时程序可执行文件的生成文件在后台发生，因此如果编译失败，则不会向用户报告任何错误。

 利用临时 PE 支持的自定义工具必须遵循以下规则：

- 在注册表中， **GeneratesDesignTimeSource**必须设置为1。

     如果没有此设置，则不会进行程序可执行文件编译。

- 生成的代码必须与全局项目设置的语言相同。

     无论自定义工具在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A> 注册表中将 **GeneratesDesignTimeSource** 设置为1，都将编译临时 PE，而不考虑自定义工具将报告为请求的扩展的内容。 扩展不需要为 *.vb*、 *.cs*或 *jsl*;它可以是任何扩展。

- 自定义工具生成的代码必须有效，并且它必须在完成执行后仅使用项目中存在的一组引用进行编译 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A> 。

     编译临时 PE 时，提供给编译器的唯一源文件是自定义工具输出。 因此，使用临时 PE 的自定义工具必须生成可以独立于项目中的其他文件进行编译的输出文件。

## <a name="see-also"></a>请参阅
- [BuildManager 对象简介](https://msdn.microsoft.com/library/50080ec2-c1c9-412c-98ef-18d7f895e7fa)
- [实现单文件生成器](../../extensibility/internals/implementing-single-file-generators.md)
- [注册单文件生成器](../../extensibility/internals/registering-single-file-generators.md)
