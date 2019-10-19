---
title: 在编辑器中 Managed Extensibility Framework |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - using MEF for extensions
ms.assetid: 3f59a285-6c33-4ae3-a4fb-ec1f5aa21bd1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f376a43b6d59ba494db2ad4e5ef26b260d91f6ad
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72632610"
---
# <a name="managed-extensibility-framework-in-the-editor"></a>编辑器中的 Managed Extensibility Framework
编辑器是使用 Managed Extensibility Framework （MEF）组件生成的。 您可以构建自己的 MEF 组件来扩展编辑器，代码还可以使用编辑器组件。

## <a name="overview-of-the-managed-extensibility-framework"></a>Managed Extensibility Framework 概述
 MEF 是一个 .NET 库，可让你添加和修改遵循 MEF 编程模型的应用程序或组件的功能。 Visual Studio 编辑器可以提供和使用 MEF 组件部件。

 MEF 包含在 .NET Framework 版本 4 *system.componentmodel*程序集中。

 有关 MEF 的详细信息，请参阅[Managed Extensibility Framework （MEF）](/dotnet/framework/mef/index)。

### <a name="component-parts-and-composition-containers"></a>组件部件和组合容器
 组件部分是类或类的成员，它可以执行以下一项操作（或同时执行这两种操作）：

- 使用另一个组件

- 被另一个组件使用

  例如，假设有一个订单输入组件，它依赖仓库库存组件提供的产品可用性数据。 在 MEF 术语中，库存部件可以*导出*产品可用性数据，订单输入部分可以*导入*数据。 订单录入部分和库存部件不必彼此了解，*组合容器*（由主机应用程序提供）负责维护导出集，以及解析导出和导入。

  组合容器 <xref:System.ComponentModel.Composition.Hosting.CompositionContainer> 通常由主机拥有。 组合容器维护导出组件部件的*目录*。

### <a name="export-and-import-component-parts"></a>导出和导入组件部件
 您可以导出任何功能，只要它作为公共类或类（属性或方法）的公共成员实现。 不必从 <xref:System.ComponentModel.Composition.Primitives.ComposablePart> 派生组件部分。 相反，您必须将 <xref:System.ComponentModel.Composition.ExportAttribute> 特性添加到要导出的类或类成员。 此属性指定其他组件部件可用于导入功能的*协定*。

### <a name="the-export-contract"></a>导出协定
 @No__t_0 定义要导出的实体（类、接口或结构）。 通常，导出属性采用指定导出类型的参数。

```
[Export(typeof(ContentTypeDefinition))]
class TestContentTypeDefinition : ContentTypeDefinition {   }
```

 默认情况下，<xref:System.ComponentModel.Composition.ExportAttribute> 属性定义一个协定，该协定是导出类的类型。

```
[Export]
[Name("Structure")]
[Order(After = "Selection", Before = "Text")]
class TestAdornmentLayerDefinition : AdornmentLayerDefinition {   }
```

 在此示例中，默认 `[Export]` 特性等效于 `[Export(typeof(TestAdornmentLayerDefinition))]`。

 您还可以导出属性或方法，如以下示例中所示。

```
[Export]
[Name("Scarlet")]
[Order(After = "Selection", Before = "Text")]
public AdornmentLayerDefinition scarletLayerDefinition;
```

### <a name="import-a-mef-export"></a>导入 MEF 导出
 当你想要使用 MEF 导出时，你必须知道其导出的协定（通常为类型），并添加具有该值的 <xref:System.ComponentModel.Composition.ImportAttribute> 特性。 默认情况下，import 特性采用一个参数，该参数是它修改的类的类型。 以下代码行将导入 <xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService> 类型。

```
[Import]
internal IClassificationTypeRegistryService ClassificationRegistry;
```

## <a name="get-editor-functionality-from-a-mef-component-part"></a>从 MEF 组件部分获取编辑器功能
 如果现有代码是 MEF 组件部件，则可以使用 MEF 元数据来使用编辑器组件部件。

#### <a name="to-consume-editor-functionality-from-a-mef-component-part"></a>从 MEF 组件部分使用编辑器功能

1. 将对*system.componentmodel*的引用添加到全局程序集缓存（GAC）中，并添加到编辑器程序集。

2. 添加相关的 using 指令。

    ```
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text;
    ```

3. 将 `[Import]` 特性添加到服务接口，如下所示。

    ```
    [Import]
    ITextBufferFactoryService textBufferService;
    ```

4. 获取服务后，可以使用它的任何一个组件。

5. 编译程序集后，将其放入 *.。\Common7\IDE\Components \* Visual Studio 安装的文件夹。

## <a name="see-also"></a>请参阅
- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
