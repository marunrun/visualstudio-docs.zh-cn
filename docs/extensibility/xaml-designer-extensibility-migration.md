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
ms.openlocfilehash: 4485e9a11cb4770477374deed651fbff2df6df52
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67890318"
---
# <a name="xaml-designer-extensibility-migration"></a>XAML 设计器扩展性迁移

在 Visual Studio 2019，XAML 设计器支持两个不同的体系结构： 设计器隔离体系结构和较新的图面上隔离体系结构。 在.NET Framework 进程中支持不能在托管的目标运行时需要此体系结构转换。 第三方可扩展性模型迁移到图面上隔离体系结构引入重大更改。 本文概述了这些更改可在 Visual Studio 2019 16.2 预览通道中。

**设计器隔离**由.NET Framework 为目标的项目的 WPF 设计器，并支持 *。 design.dll*扩展。 在外部进程中加载用户代码、 控件库和第三方扩展 (*XDesProc.exe*) 以及实际的设计器代码和设计器面板。

**图面隔离**UWP 设计器使用。 它也是面向.NET Core 的项目使用 WPF 设计器。 在图面上隔离中，唯一的用户代码和控件库单独的进程中时加载 Visual Studio 进程中加载在设计器和其面板 (*DevEnv.exe*)。 用于执行用户代码和控件库运行时使用的.NET Framework 为实际的设计器和第三方扩展代码不同。

![extensibility-migration-architecture](media/xaml-designer-extensibility-migration-architecture.png)

由于此体系结构转换，第三方扩展不能再加载到与第三方控件库相同的进程中。 扩展无法再对控件库的直接依赖项或直接访问运行时对象。 以前编写的设计器隔离体系结构使用的扩展*Microsoft.Windows.Extensibility.dll* API 必须迁移到新的工作图面上隔离的体系结构方法。 在实践中，将需要针对新的可扩展性 API 程序集编译现有扩展插件。 访问运行时控件类型通过[typeof](/dotnet/csharp/language-reference/keywords/typeof)或必须替换或删除，因为控件库现在已加载的不同进程中运行时实例。

## <a name="new-extensibility-api-assemblies"></a>新扩展性 API 程序集

新扩展性 API 程序集是类似于现有的可扩展性 API 程序集，但遵循不同的命名方案，以区分它们。 同样，命名空间名称已更改以反映新的程序集名称。

| 设计器隔离 API 程序集            | API 图面上隔离程序集                       |
|:------------------------------------------ |:---------------------------------------------------- |
| Microsoft.Windows.Design.Extensibility.dll | Microsoft.VisualStudio.DesignTools.Extensibility.dll |
| Microsoft.Windows.Design.Interaction.dll   | Microsoft.VisualStudio.DesignTools.Interaction.dll   |

## <a name="new-file-extension-and-discovery"></a>新的文件扩展名和发现

而不是使用 *。 design.dll*文件扩展名，将使用发现扩展的新面 *。 designtools.dll*文件扩展名。 *。 design.dll*并 *。 designtools.dll*扩展可以位于同一*设计*子文件夹。

尽管第三方控件库针对实际目标运行时 （.NET Core 或 UWP） 编译 *。 designtools.dll*扩展应始终编译为.NET Framework 程序集。

## <a name="decouple-attribute-tables-from-runtime-types"></a>将从运行时类型的属性表中分离出来

图面上隔离可扩展性模型不允许扩展依赖于实际控件库，因此，扩展不能从控件库引用类型。 例如， *MyLibrary.designtools.dll*不应依赖于*MyLibrary.dll*。

注册通过属性表的类型的元数据时，此类依赖项是最常见。 通过直接引用控件库的扩展插件代码类型[typeof](/dotnet/csharp/language-reference/keywords/typeof)或[GetType](/dotnet/visual-basic/language-reference/operators/gettype-operator)中新的 Api 使用基于字符串的类型名称将替换：

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

功能提供程序将在扩展程序集中实现，并在 Visual Studio 进程中加载。 `FeatureAttribute` 将继续引用直接使用的功能提供程序类型[typeof](/dotnet/csharp/language-reference/keywords/typeof)。

目前，支持以下功能提供程序：

* `DefaultInitializer`
* `AdornerProvider`
* `ContextMenuProvider`
* `ParentAdapter`
* `PlacementAdapter`

功能提供程序现在已在实际运行时代码和控件库不同的进程中加载的因为它们将不再能够直接访问运行时对象。 相反，必须将所有此类交互转换为使用相应的基于模型的 Api。 模型 API 进行了更新，以及访问<xref:System.Type>或<xref:System.Object>是不再可用或已替换`TypeIdentifier`和`TypeDefinition`。

`TypeIdentifier` 表示没有标识一种类型的程序集名称的字符串。 一个`TypeIdenfifier`可被解析为`TypeDefinition`来查询有关类型的其他信息。 `TypeDefinition` 不能在扩展代码中缓存实例。

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

从该图面上隔离可扩展性 API 集中移除 Api:

* `ModelFactory.CreateItem(EditingContext context, object item)`
* `ViewItem.PlatformObject`
* `ModelProperty.DefaultValue`

使用的 Api`TypeIdentifier`而不是<xref:System.Type>:

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

使用的 Api`TypeIdentifier`而不是<xref:System.Type>及不再支持构造函数自变量：

* `ModelFactory.CreateItem(EditingContext context, TypeIdentifier typeIdentifier, params object[] arguments)`
* `ModelFactory.CreateItem(EditingContext context, TypeIdentifier typeIdentifier, CreateOptions options, params object[] arguments)`

使用的 Api`TypeDefinition`而不是<xref:System.Type>:

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

使用的 Api`ModelItem`而不是<xref:System.Object>:

* `ModelItemCollection.Insert(int index, object value)`
* `ModelItemCollection.Remove(object value)`
* `ModelItemDictionary.Add(object key, object value)`
* `ModelItemDictionary.ContainsKey(object key)`
* `ModelItemDictionary.Remove(object key)`
* `ModelItemDictionary.TryGetValue(object key, out ModelItem value)`

等基元类型的已知`Int32`， `String`，或`Thickness`可以作为.NET Framework 实例传递给模型 API，并将转换为目标运行时进程中的相应对象。 例如:

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

更多代码示例位于[xaml 设计器扩展性示例](https://github.com/microsoft/xaml-designer-extensibility-samples)存储库。

## <a name="limited-support-for-designdll-extensions"></a>对有限的支持。 design.dll 扩展

如果有的话 *。 designtools.dll*控件库发现扩展、 加载第一个和发现 *。 design.dll*扩展会跳过。

如果没有 *。 designtools.dll*扩展是否存在，但 *。 design.dll*找到扩展、 XAML 语言服务将尝试加载此程序集以提取属性表信息，以支持基本编辑器和属性检查器方案。 此机制在范围内的限制。 它不允许执行功能提供程序的设计器隔离扩展的加载，但可能会提供基本支持现有 WPF 控件库。
