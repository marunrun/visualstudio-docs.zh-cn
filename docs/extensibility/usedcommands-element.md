---
title: UsedCommands 元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- UsedCommands
helpviewer_keywords:
- UsedCommands element (VSCT XML schema)
- VSCT XML schema elements, UsedCommands
ms.assetid: 5e000ee0-a919-46e9-9277-2a0659f1eb78
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e43834517855f72dd32c024c222089cf42c7c3ac
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66316285"
---
# <a name="usedcommands-element"></a>UsedCommands 元素
UsedCommands 元素进行分组 UsedCommand 元素和其他 UsedCommands 分组。

 UsedCommands 元素是可选的。 如果未调用你的包的外部定义的命令，你无需在.vsct 文件中包含此部分。

## <a name="syntax"></a>语法

```
<UsedCommands condition="Defined(DEBUG)">
  <UsedCommand ... />
</UsedCommands>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[UsedCommand 元素](../extensibility/usedcommand-element.md)|由其他代码实现该命令。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义所有元素表示集成的开发环境 (IDE) 的 VSPackage 提供的命令 （例如，菜单项、 菜单、 工具栏和组合框）。|

## <a name="example"></a>示例

```
<UsedCommands>
  <UsedCommand guid="guidVSStd97" id="cmdidCut"/>
  <UsedCommand guid="guidVSStd97" id="cmdidCopy"/>
  <UsedCommand guid="guidVSStd97" id="cmdidPaste"/>
</UsedCommands>
```

## <a name="see-also"></a>请参阅
- [UsedCommand 元素](../extensibility/usedcommand-element.md)
- [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)