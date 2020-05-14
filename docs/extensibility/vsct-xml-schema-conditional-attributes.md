---
title: VSCT XML 架构条件属性 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, conditional attributes
- conditional attributes (VSCT XML schema)
ms.assetid: 754d4f32-319b-44c9-915f-f7c60e53222e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f2b1fb3ee1b2cd396f25ec5591a585f8d87648d0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697946"
---
# <a name="vsct-xml-schema-conditional-attributes"></a>VSCT XML 架构条件属性
您可以将条件属性应用于所有列表和项。 逻辑运算符和符号扩展表达式计算为真或假。 如果为 true，则关联的列表或项包含在生成的输出中。

 您可以针对其他令牌扩展或常量测试令牌扩展。 函数`Defined()`测试是否定义了特定名称，即使它没有值。

 当条件属性应用于列表时，条件将应用于列表中的每个子元素。 如果子元素本身包含条件属性，则其条件将通过 AND 操作与父表达式组合。

 值 1、"1"和"true"被计算为 true，0、"0"和"false"被计算为 false。

## <a name="operators"></a>运算符
 使用以下运算符计算条件表达式。

|操作员|定义|
|--------------|----------------|
|(,)|分组|
|!|逻辑“非”|
|\<， >， \<*， >= ， * ， ！|关系式与等式|
|and|Boolean|
|或|Boolean|

## <a name="examples"></a>示例

```xml
<Menu Condition="Defined(DEBUG)" ...
</Menu>

<Menu Condition="%(SKU_MODE) = 'Demo'" ...
</Menu>

<Menus Condition="Defined(DEBUG)">
    <Menu ...
    </Menu>
</Menus>

<Menus Condition="Defined(DEMO_SKU)">
    <Menus Condition="!Defined(DEBUG)">
        <Menu ...
        </Menu>
    </Menus>

    <Menu ...
    </Menu>
</Menus>

<Menus Condition="(Defined(DEMO_SKU) or Defined(SAMPLE_SKU))
and !Defined(DEBUG)">
    <Menu ...
    </Menu>
</Menus>
```

## <a name="see-also"></a>请参阅
- [可视化工作室命令表 （.Vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
