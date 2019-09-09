---
title: XAML 设计器扩展性迁移
ms.date: 07/09/2019
ms.topic: conceptual
author: lutzroeder
ms.author: lutzr
manager: jillfra
dev_langs:
- csharp
- vb
monikerRange: vs-2019
ms.openlocfilehash: 6ffa8888529586e23d6f9762c3ec5b724c708ca5
ms.sourcegitcommit: ab2c49ce72ccf44b27b5c8852466d15a910453a6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69024548"
---
# <a name="xaml-designer-extensibility-migration"></a>XAML 设计器扩展性迁移

在 Visual Studio 2019 中，XAML 设计器支持两种不同的体系结构：设计器隔离体系结构和最新的 surface 隔离体系结构。 需要使用此体系结构转换支持无法在 .NET Framework 进程中承载的目标运行时。 移动到 surface 隔离体系结构会引入对第三方扩展性模型的重大更改。 本文概述了这些更改，这些更改在 Visual Studio 2019 （从版本16.3 开始）中可用。

**设计器隔离**由 WPF 设计器用于面向 .NET Framework 的项目，并支持 *. 设计 .dll*扩展。 用户代码、控件库和第三方扩展将与实际的设计器代码和设计器面板一起加载到外部进程（*xdesproc.exe*）。

UWP 设计器使用**表面隔离**。 WPF 设计器还可将其用于面向 .NET Core 的项目。 在表面隔离中，仅将用户代码和控件库加载到单独的进程中，而设计器及其面板会加载到 Visual Studio 进程（*DevEnv*）中。 用于执行用户代码和控件库的运行时与 .NET Framework 用于实际设计器和第三方扩展性代码的运行时不同。

![extensibility-migration-architecture](media/xaml-designer-extensibility-migration-architecture.png)

由于此体系结构转换，第三方扩展不再加载到与第三方控件库相同的进程中。 扩展不能再直接依赖控件库，也不能直接访问运行时对象。 以前使用*Microsoft.* node.js API 为设计器隔离体系结构编写的扩展必须迁移到一种新的方法，以使用 surface 隔离体系结构。 在实践中，将需要针对新的扩展性 API 程序集编译现有扩展。 必须[替换或删除](/dotnet/csharp/language-reference/keywords/typeof)对运行时控件类型的访问，因为控件库现在是在另一个进程中加载的。

## <a name="new-extensibility-api-assemblies"></a>新的扩展性 API 程序集

新的扩展性 API 程序集类似于现有的扩展性 API 程序集，但采用不同的命名方案来区分它们。 同样，命名空间名称已更改，以反映新的程序集名称。

| 设计器隔离 API 程序集            | Surface 隔离 API 程序集                       |
|:------------------------------------------ |:---------------------------------------------------- |
| Microsoft.Windows.Design.Extensibility.dll | Microsoft.VisualStudio.DesignTools.Extensibility.dll |
| Microsoft.Windows.Design.Interaction.dll   | Microsoft.VisualStudio.DesignTools.Interaction.dll   |

## <a name="new-file-extension-and-discovery"></a>新的文件扩展名和发现

将使用*designtools*文件扩展名来发现新的 surface extensions，而不是使用*design .dll*文件扩展名。 *designtools*扩展可以存在于同一个*设计*子文件夹中。

虽然为实际目标运行时（.NET Core 或 UWP）编译第三方控件库，但应始终将*designtools*扩展名编译为 .NET Framework 的程序集。

## <a name="decouple-attribute-tables-from-runtime-types"></a>分离运行时类型的属性表

Surface 隔离扩展性模型不允许扩展依赖于实际的控件库，因此，扩展无法引用控件库中的类型。 例如， *mylibrary.dll*不应在*mylibrary.dll*上具有依赖关系。

当通过属性表为类型注册元数据时，这种依赖关系最为常见。 通过使用基于字符串的类型名称，在新的 Api 中替换直接通过[typeof](/dotnet/csharp/language-reference/keywords/typeof)或[GetType](/dotnet/visual-basic/language-reference/operators/gettype-operator)引用控件库类型的扩展代码：

```csharp
using Microsoft.VisualStudio.DesignTools.Extensibility.Metadata;
using Microsoft.VisualStudio.DesignTools.Extensibility.Features;
using Microsoft.VisualStudio.DesignTools.Extensibility.Model;

[assembly: ProvideMetadata(typeof(AttributeTableProvider))]

public class AttributeTableProvider : IProvideAttributeTable
{
  public AttributeTable AttributeTable
  {
    get
    {
      var builder = new AttributeTableBuilder();
      builder.AddCustomAttributes("MyLibrary.MyControl", new DescriptionAttribute(Strings.MyControlDescription);
      builder.AddCustomAttributes("MyLibrary.MyControl", new FeatureAttribute(typeof(MyControlDefaultInitializer));
      return builder.CreateTable();
    }
  }
}
```

```vb
Imports Microsoft.VisualStudio.DesignTools.Extensibility.Metadata
Imports Microsoft.VisualStudio.DesignTools.Extensibility.Features
Imports Microsoft.VisualStudio.DesignTools.Extensibility.Model

<Assembly: ProvideMetadata(GetType(AttributeTableProvider))>

Public Class AttributeTableProvider
    Implements IProvideAttributeTable

    Public ReadOnly Property AttributeTable As AttributeTable Implements IProvideAttributeTable.AttributeTable
        Get
            Dim builder As New AttributeTableBuilder
            builder.AddCustomAttributes("MyLibrary.MyControl", New DescriptionAttribute(Strings.MyControlDescription))
            builder.AddCustomAttributes("MyLibrary.MyControl", New FeatureAttribute(GetType(MyControlDefaultInitializer)))
            Return builder.CreateTable()
        End Get
    End Property
End Class
```

## <a name="feature-providers-and-model-api"></a>功能提供程序和模型 API

功能提供程序在扩展程序集中实现，并在 Visual Studio 进程中加载。 `FeatureAttribute`将继续使用[typeof](/dotnet/csharp/language-reference/keywords/typeof)直接引用功能提供程序类型。

目前支持以下功能提供程序：

* `DefaultInitializer`
* `AdornerProvider`
* `ContextMenuProvider`
* `ParentAdapter`
* `PlacementAdapter`

由于功能提供程序现已加载到不同于实际运行时代码和控件库的进程中，因此它们将不再能够直接访问运行时对象。 相反，必须将所有此类交互转换为使用相应的基于模型的 Api。 模型<xref:System.Type> API 已更新，或者对或<xref:System.Object>的访问不再可用`TypeIdentifier`或已替换为和`TypeDefinition`。

`TypeIdentifier`表示一个字符串，该字符串没有标识类型的程序集名称。 可解析为，以查询有关类型的其他信息。 `TypeDefinition` `TypeIdenfifier` `TypeDefinition`无法在扩展代码中缓存实例。

```csharp
TypeDefinition type = ModelFactory.ResolveType(
    item.Context, new TypeIdentifier("MyLibrary.MyControl"));
TypeDefinition buttonType = ModelFactory.ResolveType(
    item.Context, new TypeIdentifier("System.Windows.Controls.Button"));
if (type?.IsSubclassOf(buttonType) == true)
{
}
```

```vb
Dim type As TypeDefinition = ModelFactory.ResolveType(
    item.Context, New TypeIdentifier("MyLibrary.MyControl"))
Dim buttonType As TypeDefinition = ModelFactory.ResolveType(
    item.Context, New TypeIdentifier("System.Windows.Controls.Button"))
If type?.IsSubclassOf(buttonType) Then

End If
```

从 surface 隔离扩展性 API 集中删除的 Api：

* `ModelFactory.CreateItem(EditingContext context, object item)`
* `ViewItem.PlatformObject`
* `ModelProperty.DefaultValue`

使用`TypeIdentifier` 的<xref:System.Type>api，而不是：

* `ModelFactory.CreateItem(EditingContext context, Type itemType, params object[] arguments)`
* `ModelFactory.CreateItem(EditingContext context, Type itemType, CreateOptions options, params object[] arguments)`
* `ModelFactory.CreateStaticMemberItem(EditingContext context, Type type, string memberName)`
* `ViewItem.ItemType`
* `ModelEvent.EventType`
* `ModelEvent.IsEventOfType(Type type)`
* `ModeItem.IsItemOfType(Type type)`
* `ModelParent.CanParent(EditingContext context, ModelItem parent, Type childType)`
* `ModelParent.FindParent(EditingContext context, Type childType, ModelItem startingItem)`
* `ModelParent.FindParent(Type childType, GestureData gestureData)`
* `ModelProperty.IsPropertyOfType(Type type)`
* `ParentAdpater.CanParent(ModelItem parent, Type childType)`
* `ParentAdapter.RedirectParent(ModelItem parent, Type childType)`

使用而不`TypeIdentifier`是和<xref:System.Type>的 api 将不再支持构造函数参数：

* `ModelFactory.CreateItem(EditingContext context, TypeIdentifier typeIdentifier, params object[] arguments)`
* `ModelFactory.CreateItem(EditingContext context, TypeIdentifier typeIdentifier, CreateOptions options, params object[] arguments)`

使用`TypeDefinition` 的<xref:System.Type>api，而不是：

* `ModelFactory.ResolveType(EditingContext context, TypeIdentifier typeIdentifier)`
* `ValueTranslationService.GetProperties(Type itemType)`
* `ValueTranslationService.HasValueTranslation(Type itemType, PropertyIdentifier identifier)`
* `ValueTranslationService.TranslatePropertyValue(Type itemType, ModelItem item, PropertyIdentifier identifier, object value)`
* `ModelService.Find(ModelItem startingItem, Type type)`
* `ModelService.Find(ModelItem startingItem, Predicate<Type> match)`
* `ModelItem.ItemType`
* `ModelProperty.AttachedOwnerType`
* `ModelProperty.PropertyType`
* `FeatureManager.CreateFeatureProviders(Type featureProviderType, Type type)`
* `FeatureManager.CreateFeatureProviders(Type featureProviderType, Type type, Predicate<Type> match)`
* `FeatureManager.InitializeFeatures(Type type)`
* `FeatureManager.GetCustomAttributes(Type type, Type attributeType)`
* `AdapterService.GetAdapter<TAdapterType>(Type itemType)`
* `AdapterService.GetAdapter(Type adapterType, Type itemType)`

使用`ModelItem` 的<xref:System.Object>api，而不是：

* `ModelItemCollection.Insert(int index, object value)`
* `ModelItemCollection.Remove(object value)`
* `ModelItemDictionary.Add(object key, object value)`
* `ModelItemDictionary.ContainsKey(object key)`
* `ModelItemDictionary.Remove(object key)`
* `ModelItemDictionary.TryGetValue(object key, out ModelItem value)`

而且， `ModelItem`类似`SetValue`的 api 只支持基元类型的实例或可为目标运行时转换的内置 .NET Framework 类型。 当前支持这些类型：

* 基元 .NET Framework 类型： `Boolean`、 `Byte`、 `Char` `DateTime` 、、`Double`、 、`Enum` 、、`SByte` 、、 、`Nullable` `Guid` `Int16` `Int32` `Int64`, `Single`, `String`, `Type`, `UInt16`, `UInt32`, `UInt64`,`Uri`
* 已知 WPF .NET Framework 类型（和派生类型）： `Brush`、 `Color` `EasingFunctionBase` `CompositeTransform` `Duration` `CornerRadius` 、、`FontFamily`、 `EasingMode` `EllipseGeometry`、、、、、 、`GeneralTransform` `Geometry`, `GradientStopCollection`, `GradientStop`, `GridLength`, `ImageSource`, `InlineCollection`, `Inline`, `KeySpline`, `Material`, `Matrix`, `PathFigureCollection`, `PathFigure`, `PathSegmentCollection`, `PathSegment`, `Path`, `PointCollection`, `Point`, `PropertyPath`, `Rect`, `RepeatBehavior`, `Setter`, `Size`, `StaticResource`, `TextAlignment`, `TextDecorationCollection`, `ThemeResourceExtension`, `Thickness`, `TimeSpan`, `Transform3D`,`TransformCollection`

例如：

```csharp
using Microsoft.VisualStudio.DesignTools.Extensibility.Features;
using Microsoft.VisualStudio.DesignTools.Extensibility.Model;

public class MyControlDefaultInitializer : DefaultInitializer
{
  public override void InitializeDefaults(ModelItem item)
  {
    item.Properties["Width"].SetValue(800d);
    base.InitializeDefaults(item);
  }
}
```

```vb
Imports Microsoft.VisualStudio.DesignTools.Extensibility.Features
Imports Microsoft.VisualStudio.DesignTools.Extensibility.Model

Public Class MyControlDefaultInitializer
    Inherits DefaultInitializer

    Public Overrides Sub InitializeDefaults(item As ModelItem)
        item.Properties!Width.SetValue(800.0)
        MyBase.InitializeDefaults(item)
    End Sub
End Class
```

[Xaml 设计器扩展性-示例](https://github.com/microsoft/xaml-designer-extensibility-samples)存储库中提供了更多代码示例。

## <a name="limited-support-for-designdll-extensions"></a>对. design 扩展名的有限支持

如果为控件库发现了*designtools*扩展名，将先加载该控件库，然后再对其进行发现。将跳过*设计 .dll*扩展。

如果不存在*designtools*扩展名但找到了 *. design .dll*扩展名，则 XAML 语言服务将尝试加载此程序集以提取属性表信息，以支持基本编辑器和属性检查器方案。 此机制限制在范围内。 它不允许加载设计器隔离扩展来执行功能提供程序，但可能为现有 WPF 控件库提供基本支持。
