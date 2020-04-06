---
title: 实现单文件生成器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- custom tools, implementing
- projects [Visual Studio SDK], extensibility
- projects [Visual Studio SDK], managed custom tools
ms.assetid: fe9ef6b6-4690-4c2c-872c-301c980d17fe
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e700d09277edbb04b30676d3965b6c996d0a11f3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707658"
---
# <a name="implementing-single-file-generators"></a>实现单个文件生成器
自定义工具（有时称为单个文件生成器）可用于扩展 和[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)][!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]项目系统。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 自定义工具是实现接口的<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>COM 组件。 使用此接口，自定义工具将单个输入文件转换为单个输出文件。 转换的结果可能是源代码或任何其他有用的输出。 自定义工具生成的代码文件的两个示例是响应可视化设计器中的更改和使用 Web 服务描述语言 （WSDL） 生成的文件生成的代码。

 加载自定义工具或保存输入文件时，项目系统将调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A>该方法，并将引用传递给<xref:Microsoft.VisualStudio.Shell.Interop.IVsGeneratorProgress>回调接口，以便该工具可以向用户报告其进度。

 自定义工具生成的输出文件将添加到依赖于输入文件的项目中。 项目系统根据自定义工具的实现返回的字符串自动确定输出文件的名称<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A>。

 自定义工具必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>接口。 或者，自定义工具支持<xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite>接口从输入文件以外的源检索信息。 在任何情况下，在可以使用自定义工具之前，必须将其注册到系统或[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]本地注册表中。 有关注册自定义工具的详细信息，请参阅[注册单个文件生成器](../../extensibility/internals/registering-single-file-generators.md)。

## <a name="see-also"></a>请参阅
- [向可视化设计器公开类型](../../extensibility/internals/exposing-types-to-visual-designers.md)
