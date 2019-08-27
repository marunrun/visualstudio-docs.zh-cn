---
title: 包含元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- Include
helpviewer_keywords:
- Include element (VSCT XML schema)
- VSCT XML schema elements, Include
ms.assetid: c923dfe6-084a-4105-aec1-f0a3f8399c54
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7287f4e8b611f55ea28e648aec3f95d1407bf07e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350097"
---
# <a name="include-element"></a>包含元素
Include 元素指定的文件，可以找到对提供包括插入到当前文件的路径。  所有符号和定义的类型将都成为已编译的结果的一部分。

## <a name="syntax"></a>语法

```csharp
<Include href="stdidcmd.h" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|href|必需。 标头文件的路径：<br /><br /> href="stdidcmd.h"|
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|无。|无。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示命令的元素的所有 — 也就是说，菜单项、 菜单、 工具栏和组合框 — VSPackage 提供到 IDE。|

## <a name="example"></a>示例

```
<Include href="PackagePlacements.vsct"/>
```

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表格 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)