---
title: 项定义 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- msbuild, item definitions
ms.assetid: 8e3dc223-f9e5-4974-aa0e-5dc7967419cb
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 18d6a2a30af4fb29a8d9e924c44c1570ff1efe29
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2020
ms.locfileid: "77633702"
---
# <a name="item-definitions"></a>项定义

MSBuild 2.0 版本可让你使用 [ItemGroup](../msbuild/itemgroup-element-msbuild.md) 元素在项目文件中实现项目的静态声明。 但是，只能在项级别添加元数据，即使所有项的元数据均相同，也是如此。 从 MSBuild 3.5 开始引入了一个名为 [ItemDefinitionGroup](../msbuild/itemdefinitiongroup-element-msbuild.md) 的项目元素，从而克服了这一限制。 使用 *ItemDefinitionGroup* 可以定义一组项定义，这些项定义将默认元数据值添加到命名项类型中的所有项中。

*ItemDefinitionGroup* 元素紧跟在项目文件的 [Project](../msbuild/project-element-msbuild.md) 元素之后。 项定义提供以下功能：

- 可为目标外部的项定义全局默认元数据。 也就是说，相同的元数据适用于指定类型的所有项。

- 项目类型可以有多个定义。 当其他元数据规范添加到该类型中时，最新的规范优先。 \(元数据遵循与属性相同的导入顺序。\)

- 元数据可具有累加性。 例如，根据要设置的属性，CDefines 值可以有条件地累积。 例如 `MT;STD_CALL;DEBUG;UNICODE`。

- 可删除元数据。

- 可使用条件来控制元数据的包含。

## <a name="item-metadata-default-values"></a>项元数据默认值

在 ItemDefinitionGroup 中定义的项元数据仅是默认元数据的声明。 除非定义一个使用 ItemGroup 包含元数据值的项，否则元数据不适用。

> [!NOTE]
> 在本主题的诸多示例中，尽管显示了 ItemDefinitionGroup 元素，但为清楚起见，省略了相应的 ItemGroup 定义。

ItemGroup 中显式定义的元数据优先于 ItemDefinitionGroup 中的元数据。 ItemDefinitionGroup 中的元数据仅应用于 ItemGroup 中未定义的元数据。 例如：

```xml
<ItemDefinitionGroup>
    <i>
        <m>m1</m>
        <n>n1</n>
    </i>
</ItemDefinitionGroup>
<ItemGroup>
    <i Include="a">
        <o>o1</o>
        <n>n2</n>
    </i>
</ItemGroup>
```

在本例中，默认元数据“m”应用于项“i”，这是由于项“i”没有显式定义元数据“m”。 但是，默认元数据“n”无法应用于项“i”，这是由于元数据“n”已经由项“i”定义。

> [!NOTE]
> XML 元素和参数名均区分大小写。 项元数据和项\/属性名均不区分大小写。 因此，应将名称中仅大小写不同的 ItemDefinitionGroup 项视作同一个 ItemGroup。

## <a name="value-sources"></a>值源

ItemDefinitionGroup 中定义的元数据的值可能来自许多不同的源，如下所示：

- PropertyGroup 属性

- ItemDefinitionGroup 中的项

- ItemDefinitionGroup 项上的项转换

- 环境变量

- 全局属性（来自 MSBuild.exe 命令行） 

- 保留属性

- ItemDefinitionGroup 中项上的常见元数据

- CDATA 节 \<\!\[CDATA\[此处的所有内容均未分析\]\]\>

> [!NOTE]
> ItemGroup 中的项元数据在 ItemDefinitionGroup 元数据声明中无用，这是因为已在 ItemGroup 元素之前处理 ItemDefinitionGroup 元素。

## <a name="additive-and-multiple-definitions"></a>累加性和多个定义

当添加定义或使用多个 ItemDefinitionGroup 时，请记住以下几点：

- 将其他元数据规范添加到此类型中。

- 最新规范优先。

当拥有多个 ItemDefinitionGroup 时，每个后续规范将其元数据添加至先前的定义。 例如：

```xml
<ItemDefinitionGroup>
    <i>
        <m>m1</m>
        <n>n1</n>
    </i>
</ItemDefinitionGroup>
<ItemDefinitionGroup>
    <i>
        <o>o1</o>
    </i>
</ItemDefinitionGroup>
```

在本例中，向“m”和“n”添加元数据“o”。

此外，还可以添加先前定义的元数据值。 例如：

```xml
<ItemDefinitionGroup>
    <i>
        <m>m1</m>
    </i>
</ItemDefinitionGroup>
<ItemDefinitionGroup>
    <i>
        <m>%(m);m2</m>
    </i>
</ItemDefinitionGroup>
```

在本例中，元数据“m”先前定义的值 \(m1\) 被添加至新值 \(m2\)，因此最终值为“m1;m2”。

> [!NOTE]
> 在相同的 ItemDefinitionGroup 中也可能出现这种情况。

当替代先前定义的元数据时，最新规范优先。 在下列示例中，元数据“m”的最终值从“m1”变为“m1a”。

```xml
<ItemDefinitionGroup>
    <i>
        <m>m1</m>
    </i>
</ItemDefinitionGroup>
<ItemDefinitionGroup>
    <i>
        <m>m1a</m>
    </i>
</ItemDefinitionGroup>
```

## <a name="use-conditions-in-an-itemdefinitiongroup"></a>在 ItemDefinitionGroup 中使用条件

可使用 ItemDefinitionGroup 中的条件来控制元数据的包含。 例如：

```xml
<ItemDefinitionGroup Condition="'$(Configuration)'=='Debug'">
    <i>
        <m>m1</m>
    </i>
</ItemDefinitionGroup>
```

在这种情况下，仅当“Configuration”属性的值为“Debug”时，才包括项“i”上的默认元数据“m1”。

> [!NOTE]
> 在条件中仅支持本地元数据引用。

对项（而非定义组）而言，在先前的 ItemDefinitionGroup 中定义的元数据的引用是本地的。 也就是说，引用的范围特定于项。 例如：

```xml
<ItemDefinitionGroup>
    <test>
        <yes>1</yes>
    </test>
    <i>
        <m>m0</m>
        <m Condition="'%(test.yes)'=='1'">m1</m>
    </i>
</ItemDefinitionGroup>

```

在上述示例中，项“i”在其条件中引用项“test”。 此种情况永远不会为 true，因为 MSBuild 将 ItemDefinitionGroup 中对另一个项的元数据的引用解释为空字符串。 因此，“m”将设置为“m0”。

```xml
  <ItemDefinitionGroup>
    <i>
      <m>m0</m>
      <yes>1</yes>
      <m Condition="'%(i.yes)'=='1'">m1</m>
    </i>
  </ItemDefinitionGroup>

```

在上述示例中，“m”将设置为值“m1”，作为项“yes”的条件引用项“i”的元数据值。

## <a name="override-and-delete-metadata"></a>替代和删除元数据

通过将元数据值设置为其他值，在 ItemDefinitionGroup 元素中定义的元数据可以在之后的 ItemDefinitionGroup 元素中被替代。 还可通过将元数据项设置为空值，高效删除元数据项。 例如：

```xml
<ItemDefinitionGroup>
    <i>
        <m>m1</m>
    </i>
</ItemDefinitionGroup>
<ItemDefinitionGroup>
    <i>
        <m></m>
    </i>
</ItemDefinitionGroup>
```

项“i”仍包含元数据“m”，但此时它的值为空。

## <a name="scope-of-metadata"></a>元数据范围

ItemDefinitionGroups 在定义的位置具有全局范围和全局属性。 ItemDefinitionGroup 中的默认元数据定义可自引用。 例如，以下示例使用了一个简单的元数据引用：

```xml
<ItemDefinitionGroup>
    <i>
        <m>m1</m>
        <m>%(m);m2</m>
    </i>
</ItemDefinitionGroup>
```

还可使用限定的元数据引用：

```xml
<ItemDefinitionGroup>
    <i>
        <m>m1</m>
        <m>%(i.m);m2</m>
    </i>
</ItemDefinitionGroup>
```

但是，以下项无效：

```xml
<ItemDefinitionGroup>
    <i>
        <m>m1</m>
        <m>@(x)</m>
    </i>
</ItemDefinitionGroup>
```

从 MSBuild 3.5 开始，ItemGroups 可以自引用。 例如：

```xml
<ItemGroup>
    <item Include="a">
        <m>m1</m>
        <m>%(m);m2</m>
    </item>
</ItemGroup>
```

## <a name="see-also"></a>请参阅

- [批处理](../msbuild/msbuild-batching.md)
