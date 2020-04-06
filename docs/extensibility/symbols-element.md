---
title: 符号元素 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Symbols element (VSCT XML schema)
- VSCT XML schema elements, Symbols
ms.assetid: 1cda43d8-42a5-4b1b-a3c8-cf0401c3202f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5c24c3f84df23a07b6b16272b66b29e32ad7b911
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699353"
---
# <a name="symbols-element"></a>Symbols 元素
定义其他 VSCT 元素使用的 GUID 和 I。 对于非托管代码，此信息通常来自[Extern 元素](../extensibility/extern-element.md)指定的标头文件。 托管代码使用 Symbols 元素的子元素来定义此信息。

 如果从现有的 .cto 文件创建 .vsct 文件，则符号将作为 Symbol 元素的子级生成。 有关详细信息，请参阅[如何：创建 。来自现有 的 Vct 文件。Cto 文件](../extensibility/internals/how-to-create-a-dot-vsct-file.md#how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file)。

 符号元素不应与[定义元素](../extensibility/define-element.md)混淆，该元素定义名称值对供预处理器使用。

## <a name="syntax"></a>语法

```
<Symbols>
  <GuidSymbol>... </GuidSymbol>
  <GuidSymbol>... </GuidSymbol>
</Symbols>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|说明|
|---------------|-----------------|
|无||

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|吉德符号|定义 GUID 符号。 GuidSymbol 有两个必需的属性：名称和值。 名称是符号的名称，该值是 GUID 作为字符串的值。<br /><br /> 例如：GuidSymbol\<名称="guidV 包装1Pkg"值="{c5f54698-101a-4846-84d3-dc748f9cd848}"/>|
|ID符号|定义符号。 IDSymbol 具有两个必需的属性：名称和值。 名称是符号的名称，值是符号作为字符串的值。<br /><br /> 例如：IDSymbol\<名称="MyMenuGroup"值="0x1020"/>|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|.vsct 文件的根元素。|

## <a name="example"></a>示例

```
<Symbols>
  <GuidSymbol name="guidVsPackage1Pkg" value="{c5f54698-101a-4846-84d3-dc748f9cd848}" />
  <GuidSymbol name="guidVsPackage1CmdSet" value="{cb9dfd7f-2fcc-4a3e-aae8-f7fe30b1cfac}">
    <IDSymbol name="MyMenuGroup" value="0x1020" />
    <IDSymbol name="cmdidMyCommand" value="0x0100" />
    <IDSymbol name="cmdidMyTool" value="0x0101" />
  </GuidSymbol>
</Symbols>
```

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
