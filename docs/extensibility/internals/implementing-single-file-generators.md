---
title: 实现单个文件生成器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- custom tools, implementing
- projects [Visual Studio SDK], extensibility
- projects [Visual Studio SDK], managed custom tools
ms.assetid: fe9ef6b6-4690-4c2c-872c-301c980d17fe
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 44a7207bf7d846381ea0cbf678ca7afe3d3d177b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66335095"
---
# <a name="implementing-single-file-generators"></a>实现单个文件生成器
自定义工具，有时称为单文件生成器 — 可用于扩展[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]和[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]项目中的系统[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 自定义工具是实现的 COM 组件<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>接口。 使用此接口，自定义工具将单个输入的文件转换为单个输出文件。 转换的结果可能是源代码中，或任何其他输出这一点非常有用。 自定义工具生成的代码文件的两个示例是在响应中的可视化设计器和使用 Web 服务描述语言 (WSDL) 生成的文件的更改生成代码。

 当加载自定义工具，或保存该输入的文件时，项目系统会调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A>方法，并将传递到引用<xref:Microsoft.VisualStudio.Shell.Interop.IVsGeneratorProgress>回调接口，凭此工具可以向用户报告其进度。

 自定义工具生成的输出文件添加到输入文件的依赖项目。 项目系统会自动确定的基于自定义工具的实现返回的字符串的输出文件名称<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A>。

 必须实现一个自定义工具<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>接口。 （可选） 自定义工具支持<xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite>接口以从输入文件以外的源中检索信息。 在任何情况下，您可以使用自定义工具之前，必须注册它与系统中或在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]本地注册表。 注册自定义工具的详细信息，请参阅[注册单个文件生成器](../../extensibility/internals/registering-single-file-generators.md)。

## <a name="see-also"></a>请参阅
- [向可视化设计器公开类型](../../extensibility/internals/exposing-types-to-visual-designers.md)