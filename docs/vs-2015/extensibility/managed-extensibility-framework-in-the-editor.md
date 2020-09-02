---
title: 在编辑器中 Managed Extensibility Framework |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - using MEF for extensions
ms.assetid: 3f59a285-6c33-4ae3-a4fb-ec1f5aa21bd1
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f19b71c86d972b59a9d46f379bf7ec93f63aeb9a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65679957"
---
# <a name="managed-extensibility-framework-in-the-editor"></a>编辑器中的 Managed Extensibility Framework
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

编辑器是通过使用 Managed Extensibility Framework (MEF) 组件生成的。 您可以构建自己的 MEF 组件来扩展编辑器，代码还可以使用编辑器组件。  
  
## <a name="overview-of-the-managed-extensibility-framework"></a>Managed Extensibility Framework 概述  
 MEF 是一个 .NET 库，可让你添加和修改遵循 MEF 编程模型的应用程序或组件的功能。 Visual Studio 编辑器可以提供和使用 MEF 组件部件。  
  
 MEF 包含在 .NET Framework 版本 4 System.ComponentModel.Composition.dll 程序集中。  
  
 有关 MEF 的详细信息，请参阅 [ (MEF) Managed Extensibility Framework ](https://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde)。  
  
### <a name="component-parts-and-composition-containers"></a>组件部件和组合容器  
 组件部分是类或类的成员，它可以执行一项 (或同时执行以下操作) ：  
  
- 使用另一个组件  
  
- 被另一个组件使用  
  
  例如，假设有一个订单输入组件，它依赖仓库库存组件提供的产品可用性数据。 在 MEF 术语中，库存部件可以 *导出* 产品可用性数据，订单输入部分可以 *导入* 数据。 订单录入部分和库存部件不必彼此了解，宿主应用程序 (提供的 *组合容器*) 负责维护导出集，以及解析导出和导入。  
  
  组合容器 <xref:System.ComponentModel.Composition.Hosting.CompositionContainer> 通常由主机拥有。 组合容器维护导出组件部件的 *目录* 。  
  
### <a name="exporting-and-importing-component-parts"></a>导出和导入组件部件  
 可以导出任何功能，只要它作为公共类或类的公共成员实现 (属性或方法) 。 你不必从派生组件部分 <xref:System.ComponentModel.Composition.Primitives.ComposablePart> 。 相反，您必须将 <xref:System.ComponentModel.Composition.ExportAttribute> 特性添加到要导出的类或类成员。 此属性指定其他组件部件可用于导入功能的 *协定* 。  
  
### <a name="the-export-contract"></a>导出协定  
 <xref:System.ComponentModel.Composition.ExportAttribute>定义要导出的实体 (类、接口或结构) 。 通常，导出属性采用指定导出类型的参数。  
  
```  
[Export(typeof(ContentTypeDefinition))]  
class TestContentTypeDefinition : ContentTypeDefinition {   }  
```  
  
 默认情况下， <xref:System.ComponentModel.Composition.ExportAttribute> 属性定义一个协定，该协定是导出类的类型。  
  
```  
[Export]  
[Name("Structure")]  
[Order(After = "Selection", Before = "Text")]  
class TestAdornmentLayerDefinition : AdornmentLayerDefinition {   }  
```  
  
 在此示例中，默认 `[Export]` 属性等效于 `[Export(typeof(TestAdornmentLayerDefinition))]` 。  
  
 您还可以导出属性或方法，如以下示例中所示。  
  
```  
[Export]  
[Name("Scarlet")]  
[Order(After = "Selection", Before = "Text")]  
public AdornmentLayerDefinition scarletLayerDefinition;  
```  
  
### <a name="importing-a-mef-export"></a>导入 MEF 导出  
 如果要使用 MEF 导出，则必须知道协定 (通常是导出它的类型) ，然后添加具有该值的 <xref:System.ComponentModel.Composition.ImportAttribute> 特性。 默认情况下，import 特性采用一个参数，该参数是它修改的类的类型。 以下代码行将导入该 <xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService> 类型。  
  
```  
[Import]  
internal IClassificationTypeRegistryService ClassificationRegistry;  
```  
  
## <a name="getting-editor-functionality-from-a-mef-component-part"></a>从 MEF 组件部分获取编辑器功能  
 如果现有代码是 MEF 组件部件，则可以使用 MEF 元数据来使用编辑器组件部件。  
  
#### <a name="to-consume-editor-functionality-from-a-mef-component-part"></a>从 MEF 组件部分使用编辑器功能  
  
1. 向全局程序集缓存中添加对 System.Composition.ComponentModel.dll 的引用，该程序集位于全局程序集缓存 (GAC) 和编辑器程序集。  
  
2. 添加相关的 using 语句。  
  
    ```  
    using System.ComponentModel.Composition;  
    using Microsoft.VisualStudio.Text;  
    ```  
  
3. 将 `[Import]` 属性添加到服务接口，如下所示。  
  
    ```  
    [Import]  
    ITextBufferFactoryService textBufferService;  
    ```  
  
4. 获取服务后，可以使用它的任何一个组件。  
  
5. 编译程序集后，将其放在中。Visual Studio 安装的 \Common7\IDE\Components\ 文件夹。  
  
## <a name="see-also"></a>另请参阅  
 [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
