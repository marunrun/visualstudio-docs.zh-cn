---
title: 托管在编辑器中的可扩展性框架 |Microsoft Docs
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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65679957"
---
# <a name="managed-extensibility-framework-in-the-editor"></a>编辑器中的 Managed Extensibility Framework
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用 Managed Extensibility Framework (MEF) 组件生成编辑器。 您可以构建您自己的 MEF 组件来扩展编辑器中，和你的代码可以使用编辑器的组件。  
  
## <a name="overview-of-the-managed-extensibility-framework"></a>Managed 的 Extensibility Framework 概述  
 MEF 是一个.NET 库，可以添加和修改应用程序或组件遵循 MEF 编程模型的功能。 在 Visual Studio 编辑器可以同时提供和使用 MEF 组件部分。  
  
 MEF 被包含在.NET Framework 版本 4 System.ComponentModel.Composition.dll 程序集。  
  
 有关 MEF 的详细信息，请参阅[Managed Extensibility Framework (MEF)](https://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde)。  
  
### <a name="component-parts-and-composition-containers"></a>组件的各部分和撰写容器  
 某一组件部分是类还是可以执行一个 （或两者） 的以下类的成员：  
  
- 使用另一个组件  
  
- 可供另一个组件  
  
  例如，考虑具有取决于产品可用性数据仓库清单组件提供一个订单项组件的购物应用程序。 在 MEF 术语中，清单一部分可以*导出*产品可用性数据，并且订单条目一部分可以*导入*数据。 订单项部分和清单部分不需要知道有关彼此;*撰写容器*（由主机应用程序提供） 是负责维护的导出，集和解析导出和导入。  
  
  撰写容器<xref:System.ComponentModel.Composition.Hosting.CompositionContainer>，通常拥有的主机。 撰写容器维护*目录*导出的组件构成。  
  
### <a name="exporting-and-importing-component-parts"></a>导出和导入组件的各部分  
 只要它作为公共类或类 （属性或方法） 的公共成员，您可以导出任何功能。 无需派生来自您组件部件<xref:System.ComponentModel.Composition.Primitives.ComposablePart>。 相反，必须添加<xref:System.ComponentModel.Composition.ExportAttribute>类或类成员，你想要导出的属性。 此属性指定*协定*通过的另一个组件部分可以导入您的功能。  
  
### <a name="the-export-contract"></a>导出协定  
 <xref:System.ComponentModel.Composition.ExportAttribute>定义正在导出的实体 （类、 接口或结构）。 通常情况下，export 特性采用一个参数以指定的导出类型。  
  
```  
[Export(typeof(ContentTypeDefinition))]  
class TestContentTypeDefinition : ContentTypeDefinition {   }  
```  
  
 默认情况下，<xref:System.ComponentModel.Composition.ExportAttribute>属性定义协定的导出类的类型。  
  
```  
[Export]  
[Name("Structure")]  
[Order(After = "Selection", Before = "Text")]  
class TestAdornmentLayerDefinition : AdornmentLayerDefinition {   }  
```  
  
 在示例中，默认值`[Export]`属性等同于`[Export(typeof(TestAdornmentLayerDefinition))]`。  
  
 此外可以导出的属性或方法，如下面的示例中所示。  
  
```  
[Export]  
[Name("Scarlet")]  
[Order(After = "Selection", Before = "Text")]  
public AdornmentLayerDefinition scarletLayerDefinition;  
```  
  
### <a name="importing-a-mef-export"></a>导入的 MEF 导出  
 当你想要使用的 MEF 导出结果时，您必须知道的协定 （通常类型） 依据其导出，并添加<xref:System.ComponentModel.Composition.ImportAttribute>具有该值的属性。 默认情况下，导入属性采用一个参数，这是它会修改类的类型。 以下几行代码导入<xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService>类型。  
  
```  
[Import]  
internal IClassificationTypeRegistryService ClassificationRegistry;  
```  
  
## <a name="getting-editor-functionality-from-a-mef-component-part"></a>从 MEF 组件部分获取编辑器的功能  
 如果您的现有代码是 MEF 组件部分，可以使用 MEF 元数据来使用编辑器组件部分。  
  
#### <a name="to-consume-editor-functionality-from-a-mef-component-part"></a>若要使用 MEF 组件部分中的编辑器功能  
  
1. 将引用添加到 System.Composition.ComponentModel.dll，全局程序集缓存 (GAC) 中，则和编辑器程序集。  
  
2. 添加相关 using 语句。  
  
    ```  
    using System.ComponentModel.Composition;  
    using Microsoft.VisualStudio.Text;  
    ```  
  
3. 添加`[Import]`属性到你的服务接口，如下所示。  
  
    ```  
    [Import]  
    ITextBufferFactoryService textBufferService;  
    ```  
  
4. 时获取该服务后，可以使用其组件之一。  
  
5. 编译您的程序集，将其放入时...在 Visual Studio 安装 \Common7\IDE\Components\ 文件夹。  
  
## <a name="see-also"></a>请参阅  
 [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
