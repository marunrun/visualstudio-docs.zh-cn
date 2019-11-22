---
title: 使用 LINQ to XML 进行 WPF 数据绑定概述 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 3bf80845-891b-41de-a71b-4080b5bd3ea6
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 751840960288f46c0a1ca09ebe80a2b8e7603359
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299524"
---
# <a name="wpf-data-binding-with-linq-to-xml-overview"></a>使用 LINQ to XML 进行 WPF 数据绑定概述
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题介绍 <xref:System.Xml.Linq> 命名空间中的动态数据绑定功能。 这些功能可用作 Windows Presentation Foundation (WPF) 中用户界面 (UI) 元素的数据源。

## <a name="xaml-and-linq-to-xml"></a>XAML 和 LINQ to XML
 可扩展应用程序标记语言 (XAML) 是由 Microsoft 创建的 XML 方言，支持 .NET Framework 3.0 技术。 它在 WPF 中用于表示用户界面元素和相关功能，如事件和数据绑定。 在 Windows Workflow Foundation 中，XAML 用于表示程序结构，如程序控制（工作流）。 XAML 使技术的声明性方面与相关的过程性代码分离，从而可定义更具个性化的程序行为。

 XAML 和 LINQ to XML 的交互有两种主要方式：

- 由于 XAML 文件是格式良好的 XML，因此可以通过 XML 技术（如 LINQ to XML）查询和操作。

- 由于 LINQ to XML 查询表示数据的源，因此这些查询可用作 WPF UI 元素数据绑定的数据源。

  本文档说明第二种情况。

## <a name="data-binding-in-the-windows-presentation-foundation"></a>Windows Presentation Foundation 中的数据绑定
 WPF 数据绑定可使 UI 元素将其一个属性与一个数据源相关联。 这种情况的一个简单示例是 <xref:System.Windows.Controls.Label>，其文本表示用户定义对象中一个公共属性的值。 WPF 数据绑定依赖于下列组件：

|组件|描述|
|---------------|-----------------|
|绑定目标|要与数据源关联的 UI 元素。 WPF 中的可视元素是从 <xref:System.Windows.UIElement> 类派生的。|
|目标属性|绑定目标的依赖项属性，反映数据绑定源的值。 从中派生 <xref:System.Windows.DependencyObject> 的 <xref:System.Windows.UIElement> 类直接支持依赖项属性。|
|绑定源|提供给 UI 元素以便进行显示的一个或多个值的源对象。 WPF 自动支持以下类型作为绑定源：CLR 对象、ADO.NET 数据对象、XML 数据（来自 XPath 或 LINQ to XML 查询）或其他 <xref:System.Windows.DependencyObject>。|
|源路径|绑定源的属性，可解析为要绑定的一个或一组值。|

 依赖项属性是特定于 WPF 的概念，它表示 UI 元素的动态计算的属性。 例如，依赖项属性通常具有默认值或具有由父元素提供的值。 <xref:System.Windows.DependencyProperty> 类的实例（而不是支持标准属性的字段）支持这些特殊属性。 有关详细信息，请参阅[依赖项属性概述](https://msdn.microsoft.com/library/d119d00c-3afb-48d6-87a0-c4da4f83dee5)。

### <a name="dynamic-data-binding-in-wpf"></a>WPF 中的动态数据绑定
 默认情况下，仅在初始化目标 UI 元素时，才会发生数据绑定。 这称为“一次性”绑定。 这不能满足多数用途的需要；通常，数据绑定解决方案要求使用以下方式之一在运行时动态传播更改：

- 单向绑定，这种方式会自动传播对一侧所做的更改。 最常见的情况是对源所做的更改会反映在目标中，但有时需要相反的情况。

- 双向绑定，在这种方式中，对源所做的更改会自动传播到目标，而且对目标的更改也会自动传播到源。

  为了进行单向或双向绑定，源必须实现一种更改通知机制，例如通过实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口或通过对支持的每个属性使用 PropertyNameChanged 模式。

  有关 WPF 中数据绑定的详细信息，请参阅[数据绑定 (WPF)](https://msdn.microsoft.com/library/90f79b97-17e7-40d1-abf0-3ba600ad1d7e)。

## <a name="dynamic-properties-in-linq-to-xml-classes"></a>LINQ to XML 类中的动态属性
 大多数 LINQ to XML 类都不适合作为适当的 WPF 动态数据源：一些最有用的信息只能通过方法（而不是属性）提供，并且这些类中的属性不实现更改通知。 为了支持 WPF 数据绑定，LINQ to XML 公开了一组动态属性。

 这些动态属性是特殊的运行时属性，它们重复 <xref:System.Xml.Linq.XAttribute> 和 <xref:System.Xml.Linq.XElement> 类中现有方法和属性的功能。 将这些属性添加到这些类中只是为了使这些类能够充当 WPF 的动态数据源。 为了满足这一要求，所有这些动态属性都要实现更改通知。 下一节 [LINQ to XML 动态属性](../designers/linq-to-xml-dynamic-properties.md)中提供有关这些动态属性的详细参考。

> [!NOTE]
> <xref:System.Xml.Linq> 命名空间的各个类中的很多标准公共属性都可用于一次性数据绑定。 但请记住，在这种方案下，源和目标都不会动态更新。

### <a name="accessing-dynamic-properties"></a>访问动态属性
 不能像访问标准属性那样访问 <xref:System.Xml.Linq.XAttribute> 和 <xref:System.Xml.Linq.XElement> 类中的动态属性。 例如，在符合 CLR 的语言（如 C#）中，动态属性不能：

- 在编译时直接访问。 动态属性对于编译器和 Visual Studio IntelliSense 是不可见的。

- 在运行时使用 .NET 反射来发现或访问。 即使在运行时，它们也不是基本 CLR 意义上的属性。

  在 C# 中，动态属性只能在运行时通过 <xref:System.ComponentModel> 命名空间提供的功能进行访问。

  但相比之下，在 XML 源中，可以通过下面形式的简洁表示法访问动态属性：

```
<object>.<dynamic-property>
```

 这两个类的动态属性或者解析为可以直接使用的值，或者解析为必须与索引一起提供的索引器，以便获取结果值或值的集合。 后一种语法采用的格式为：

```
<object>.<dynamic-property>[<index-value>]
```

 有关详细信息，请参阅 [LINQ to XML 动态属性](../designers/linq-to-xml-dynamic-properties.md)。

 为了实现 WPF 动态绑定，需要与 <xref:System.Windows.Data> 命名空间提供的功能（特别是 <xref:System.Windows.Data.Binding> 类）一起使用动态属性。

## <a name="see-also"></a>请参阅
 [WPF Data Binding with LINQ to XML](../designers/wpf-data-binding-with-linq-to-xml.md) [LINQ to XML Dynamic Properties](../designers/linq-to-xml-dynamic-properties.md) [XAML in WPF](https://msdn.microsoft.com/library/5d858575-a83b-42df-ad3f-047ed2d6e3c8) [Data Binding (WPF)](https://msdn.microsoft.com/library/90f79b97-17e7-40d1-abf0-3ba600ad1d7e) [Using Workflow Markup](https://go.microsoft.com/fwlink/?LinkId=98685)
