---
title: 实现单个文件生成器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- custom tools, implementing
- projects [Visual Studio SDK], extensibility
- projects [Visual Studio SDK], managed custom tools
ms.assetid: fe9ef6b6-4690-4c2c-872c-301c980d17fe
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e2ca842f05692d5d47ed42470f58f2be0bb45007
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68192699"
---
# <a name="implementing-single-file-generators"></a>实现单个文件生成器
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

自定义工具，有时称为单文件生成器 — 可用于扩展[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]和[!INCLUDE[csprcs](../../includes/csprcs-md.md)]项目中的系统[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 自定义工具是实现的 COM 组件<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>接口。 使用此接口，自定义工具将单个输入的文件转换为单个输出文件。 转换的结果可能是源代码中，或任何其他输出这一点非常有用。 自定义工具生成的代码文件的两个示例是在响应中的可视化设计器和使用 Web 服务描述语言 (WSDL) 生成的文件的更改生成代码。  
  
 当加载自定义工具，或保存该输入的文件时，项目系统会调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A>方法，并将传递到引用<xref:Microsoft.VisualStudio.Shell.Interop.IVsGeneratorProgress>回调接口，凭此工具可以向用户报告其进度。  
  
 自定义工具生成的输出文件添加到输入文件的依赖项目。 项目系统会自动确定的基于自定义工具的实现返回的字符串的输出文件名称<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A>。  
  
 必须实现一个自定义工具<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>接口。 （可选） 自定义工具支持<xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite>接口以从输入文件以外的源中检索信息。 在任何情况下，您可以使用自定义工具之前，必须注册它与系统中或在[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]本地注册表。 注册自定义工具的详细信息，请参阅[注册单个文件生成器](../../extensibility/internals/registering-single-file-generators.md)。  
  
## <a name="see-also"></a>请参阅  
 [确定项目的默认 Namespace](../../misc/determining-the-default-namespace-of-a-project.md)   
 [向可视化设计器公开类型](../../extensibility/internals/exposing-types-to-visual-designers.md)
