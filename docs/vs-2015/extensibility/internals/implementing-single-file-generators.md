---
title: 实现单文件生成器 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192699"
---
# <a name="implementing-single-file-generators"></a>实现单个文件生成器
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

自定义工具（有时称为单个文件生成器）可用于 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] 在中扩展和项目系统 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 自定义工具是实现接口的 COM 组件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> 。 使用此接口，自定义工具将单个输入文件转换为一个输出文件。 转换的结果可以是源代码，也可以是任何有用的输出。 自定义工具生成的代码文件的两个示例是生成的代码，以响应可视化设计器中的更改和使用 Web 服务描述语言 (WSDL) 生成的文件。  
  
 加载自定义工具或保存输入文件时，项目系统会调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A> 方法，并传递对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsGeneratorProgress> 回调接口的引用，由此工具可向用户报告其进度。  
  
 自定义工具生成的输出文件将添加到项目中，并对输入文件产生依赖关系。 项目系统根据自定义工具的实现返回的字符串，自动确定输出文件的名称 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A> 。  
  
 自定义工具必须实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> 接口。 自定义工具还支持 <xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite> 从输入文件以外的源中检索信息的接口。 在任何情况下，你都必须将其注册到系统或本地注册表中，然后才能使用自定义工具 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 有关注册自定义工具的详细信息，请参阅 [注册单个文件生成器](../../extensibility/internals/registering-single-file-generators.md)。  
  
## <a name="see-also"></a>另请参阅  
 [确定项目的默认命名空间](../../misc/determining-the-default-namespace-of-a-project.md)   
 [向可视化设计器公开类型](../../extensibility/internals/exposing-types-to-visual-designers.md)
