---
title: .VSCT XML 架构条件属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, conditional attributes
- conditional attributes (VSCT XML schema)
ms.assetid: 754d4f32-319b-44c9-915f-f7c60e53222e
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6294ee8027b61840149096561efc91b8a4a3c3ec
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62422144"
---
# <a name="vsct-xml-schema-conditional-attributes"></a>VSCT XML 架构条件属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

条件特性可应用于所有列表和项。 逻辑运算符和符号扩展表达式的计算结果为 true 或 false。 如果为 true，则在生成的输出中包含关联的列表或项。  
  
 可以针对其他令牌扩展或常量测试令牌扩展。 使用 ( # A1 定义的函数来测试是否定义了特定名称，即使该名称没有值也是如此。  
  
 将条件属性应用于列表时，该条件将应用于列表中的每个子元素。 如果子元素本身包含 Condition 属性，则通过 AND 运算将其条件与父表达式组合在一起。  
  
 值1、"1" 和 "true" 计算为 true，0、"0" 和 "false" 被计算为 false。  
  
## <a name="operators"></a>运算符  
 以下运算符可用于计算条件表达式。  
  
|操作员|定义|  
|--------------|----------------|  
|(,)|分组|  
|!|逻辑“非”|  
|\<, >, \<=, >=, ==, !=|关系式与等式|  
|和|布尔|  
|或|布尔|  
  
## <a name="examples"></a>示例  
  
```  
<Menu Condition="Defined(DEBUG)" …  
</Menu>  
  
<Menu Condition="%(SKU_MODE) = 'Demo'" …  
</Menu>  
  
<Menus Condition="Defined(DEBUG)">  
    <Menu …  
    </Menu>  
</Menus>  
  
<Menus Condition="Defined(DEMO_SKU)">  
    <Menus Condition="!Defined(DEBUG)">  
        <Menu …  
        </Menu>  
    </Menus>  
  
    <Menu …  
    </Menu>  
</Menus>  
  
<Menus Condition="(Defined(DEMO_SKU) or Defined(SAMPLE_SKU))   
and !Defined(DEBUG)">  
    <Menu …  
    </Menu>  
</Menus>  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
