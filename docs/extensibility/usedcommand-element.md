---
title: 已用命令元素 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- UsedCommands element (VSCT XML schema)
- VSCT XML schema elements, UsedCommands
ms.assetid: 99cd05d3-644a-42ff-b289-8458cd1b20c0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 65030c3fe24c3456b0c4c99a667362d2a4c67703
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698829"
---
# <a name="usedcommand-element"></a>UsedCommand 元素
使 VSPackage 能够访问在另一个 .vsct 文件中定义的命令。 例如，如果 VSPackage 使用由**Copy**[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]shell 定义的标准 Copy 命令，则可以将该命令添加到菜单或工具栏，而无需重新实现该命令。

## <a name="syntax"></a>语法

```
<UsedCommand guid="guidMyCommandGroup" id="MyCommand" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|guid|必需。 标识命令的 GUID ID 对的 GUID。|
|id|必需。 标识命令的 GUID ID 对的 ID。|
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|无||

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[UsedCommands 元素](../extensibility/usedcommands-element.md)|对"已使用命令"元素和其他"已使用命令"分组进行分组。|

## <a name="remarks"></a>备注
 通过将命令添加到元素，VS`<UsedCommands>`包通知[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]环境 VSPackage 需要该命令。 应为包要求`<UsedCommand>`的任何命令添加一个元素，该命令可能不包含在 Visual Studio 的所有版本和配置中。 例如，如果包调用特定于 Visual C++的命令，则该命令将不适用于 Visual Web 开发人员的用户，除非您包含该命令`<UsedCommand>`的元素。

## <a name="example"></a>示例

```
<UsedCommands>
  <UsedCommand guid="guidVSStd97" id="cmdidCut"/>
  <UsedCommand guid="guidVSStd97" id="cmdidCopy"/>
  <UsedCommand guid="guidVSStd97" id="cmdidPaste"/>
</UsedCommands>
```

## <a name="see-also"></a>请参阅
- [UsedCommands 元素](../extensibility/usedcommands-element.md)
- [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
