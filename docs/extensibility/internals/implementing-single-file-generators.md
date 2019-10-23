---
title: 实现单文件生成器 |Microsoft Docs
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
ms.openlocfilehash: 69bde665e62d063b6bab8784634777eeea02e941
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72727179"
---
# <a name="implementing-single-file-generators"></a>实现单个文件生成器
自定义工具（有时称为单个文件生成器）可用于扩展 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中的 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 和 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 项目系统。 自定义工具是实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> 接口的 COM 组件。 使用此接口，自定义工具将单个输入文件转换为一个输出文件。 转换的结果可以是源代码，也可以是任何有用的输出。 自定义工具生成的代码文件的两个示例是生成的代码，以响应可视化设计器中的更改和使用 Web 服务描述语言（WSDL）生成的文件。

 加载自定义工具或保存输入文件时，项目系统会调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A> 方法，并传递对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsGeneratorProgress> 回调接口的引用，由此工具可向用户报告其进度。

 自定义工具生成的输出文件将添加到项目中，并对输入文件产生依赖关系。 项目系统根据 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A> 的自定义工具的实现返回的字符串，自动确定输出文件的名称。

 自定义工具必须实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> 接口。 自定义工具还支持 <xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite> 接口，以便从输入文件以外的源中检索信息。 在任何情况下，你都必须将其注册到系统或 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 本地注册表中，然后才能使用自定义工具。 有关注册自定义工具的详细信息，请参阅[注册单个文件生成器](../../extensibility/internals/registering-single-file-generators.md)。

## <a name="see-also"></a>请参阅
- [向可视化设计器公开类型](../../extensibility/internals/exposing-types-to-visual-designers.md)