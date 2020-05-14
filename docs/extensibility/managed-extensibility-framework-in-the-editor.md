---
title: 编辑器中的托管扩展性框架 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - using MEF for extensions
ms.assetid: 3f59a285-6c33-4ae3-a4fb-ec1f5aa21bd1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 888c5206b87079cf9fa91cb68e9801cb3c4f8c1a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702870"
---
# <a name="managed-extensibility-framework-in-the-editor"></a>编辑器中的托管扩展性框架
编辑器是通过使用托管扩展框架 （MEF） 组件构建的。 您可以构建自己的 MEF 组件来扩展编辑器，并且代码也可以使用编辑器组件。

## <a name="overview-of-the-managed-extensibility-framework"></a>托管扩展性框架概述
 MEF 是一个 .NET 库，允许您添加和修改遵循 MEF 编程模型的应用程序或组件的功能。 Visual Studio 编辑器既可以提供也可以使用 MEF 组件部件。

 MEF 包含在 .NET 框架版本 4*系统.组件模型.合成.dll*程序集中。

 有关 MEF 的详细信息，请参阅[托管扩展性框架 （MEF）。](/dotnet/framework/mef/index)

### <a name="component-parts-and-composition-containers"></a>部件零件和合成容器
 组件部件是类或类的成员，可以执行以下一项（或两者）：：

- 使用另一个组件

- 由其他组件使用

  例如，考虑一个购物应用程序，该应用程序具有依赖于仓库库存组件提供的产品可用性数据的订单输入组件。 在 MEF 术语中，库存部件可以*导出*产品可用性数据，订单输入部分可以*导入*数据。 订单输入部分和库存部分不必相互了解;*组合容器*（由宿主应用程序提供）负责维护导出集和解决导出和导入问题。

  组合容器<xref:System.ComponentModel.Composition.Hosting.CompositionContainer>通常由主机拥有。 组合容器维护导出的零部件的*目录*。

### <a name="export-and-import-component-parts"></a>进出口零部件
 只要它是作为公共类或类（属性或方法）的公共成员实现的，就可以导出任何功能。 不必从<xref:System.ComponentModel.Composition.Primitives.ComposablePart>派生组件部件。 相反，您必须向要导出<xref:System.ComponentModel.Composition.ExportAttribute>的类或类成员添加属性。 此属性指定其他组件部件可以导入功能*的协定*。

### <a name="the-export-contract"></a>出口合同
 定义<xref:System.ComponentModel.Composition.ExportAttribute>要导出的实体（类、接口或结构）。 通常，导出属性采用指定导出类型的参数。

```
[Export(typeof(ContentTypeDefinition))]
class TestContentTypeDefinition : ContentTypeDefinition {   }
```

 默认情况下，该<xref:System.ComponentModel.Composition.ExportAttribute>属性定义作为导出类类型的协定。

```
[Export]
[Name("Structure")]
[Order(After = "Selection", Before = "Text")]
class TestAdornmentLayerDefinition : AdornmentLayerDefinition {   }
```

 在此示例中，默认`[Export]`属性等效于`[Export(typeof(TestAdornmentLayerDefinition))]`。

 您还可以导出属性或方法，如以下示例所示。

```
[Export]
[Name("Scarlet")]
[Order(After = "Selection", Before = "Text")]
public AdornmentLayerDefinition scarletLayerDefinition;
```

### <a name="import-a-mef-export"></a>导入 MEF 导出
 当您想要使用 MEF 导出时，必须知道导出它的协定（通常是类型），并添加具有该值<xref:System.ComponentModel.Composition.ImportAttribute>的属性。 默认情况下，导入属性采用一个参数，这是它修改的类的类型。 以下代码行导入类型<xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService>。

```
[Import]
internal IClassificationTypeRegistryService ClassificationRegistry;
```

## <a name="get-editor-functionality-from-a-mef-component-part"></a>从 MEF 组件部件获取编辑器功能
 如果现有代码是 MEF 组件部件，则可以使用 MEF 元数据使用编辑器组件部件。

#### <a name="to-consume-editor-functionality-from-a-mef-component-part"></a>使用 MEF 组件部件的编辑器功能

1. 添加对位于全局程序集缓存 （GAC） 和编辑器程序集的*引用*。

2. 添加相关的使用指令。

    ```
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text;
    ```

3. 将`[Import]`属性添加到服务接口，如下所示。

    ```
    [Import]
    ITextBufferFactoryService textBufferService;
    ```

4. 获得服务后，可以使用其任一组件。

5. 编译程序集后，将其放入 *中。[公共7_IDE_组件\*文件夹的可视化工作室安装。

## <a name="see-also"></a>请参阅
- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
