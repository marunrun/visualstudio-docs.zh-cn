---
title: 自定义工具 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, custom tools
- tools [Visual Studio], custom
- custom tools
ms.assetid: d669f154-9b23-48b6-b9f6-7419c8dd61a6
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 594d564cf4a18eb0b673abd9b45b7d70e20381b1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196921"
---
# <a name="custom-tools"></a>自定义工具
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

*自定义工具*可将工具与项目中的项相关联，并运行该工具，每次保存该文件。 某些自定义工具，有时称为*单个文件生成器*，通常用于实现转换器生成代码中的数据，反之亦然。 例如，单个文件生成器创建[!INCLUDE[csprcs](../../includes/csprcs-md.md)]和[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]带.settings 和.resx 文件的源代码。 生成的源代码提供强类型化访问.settings 和.resx 文件中的数据。 [!INCLUDE[csprcs](../../includes/csprcs-md.md)]和[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]项目类型支持自定义工具;[!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]项目类型不这样做。 你自己的项目类型还可以支持自定义工具。  
  
 自定义工具是实现的已注册的组件`IVsSingleFileGenerator`接口。  
  
 与之关联的自定义工具`ProjectItem`接口对象，并如下所示设计器和编辑器。 自定义工具将表示的文件`ProjectItem`作为输入，并将其文件名称提供的一个新文件写入`DefaultExtension`方法。  
  
## <a name="in-this-section"></a>本节内容  
 [实现单个文件生成器](../../extensibility/internals/implementing-single-file-generators.md)  
 介绍如何使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>接口实现一个自定义工具。  
  
 [确定项目的默认命名空间](../../misc/determining-the-default-namespace-of-a-project.md)  
 介绍如何确定正确的命名空间基于所用的语言。  
  
 [注册单个文件生成器](../../extensibility/internals/registering-single-file-generators.md)  
 介绍了自定义工具的所有注册表项。  
  
 [向可视化设计器公开类型](../../extensibility/internals/exposing-types-to-visual-designers.md)  
 介绍了如何项目系统支持对访问生成类和类型的可视化设计器通过提供临时可移植可执行文件 (PE) 文件。  
  
 [保留项目项的属性](../../extensibility/persisting-the-property-of-a-project-item.md)  
 演示如何持久保存项目项属性，例如源代码文件，在项目文件中的作者。  
  
## <a name="reference"></a>参考  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>  
 详细介绍<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>，其中将一个输入的文件转换为可以编译或添加到项目中的单个输出文件。  
  
 <xref:EnvDTE.ProjectItem>  
 介绍了`ProjectItem`接口，它表示项目中的项。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A>  
 详细介绍`DefaultExtension`方法，检索提供给输出文件的名称的文件扩展名。  
  
## <a name="related-sections"></a>相关章节  
 [扩展项目](../../extensibility/extending-projects.md)  
 介绍如何使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 项目和解决方案来组织代码文件和资源文件，以及如何实现源代码管理。
