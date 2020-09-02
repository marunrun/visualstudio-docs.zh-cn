---
title: UsedCommand 元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- UsedCommands element (VSCT XML schema)
- VSCT XML schema elements, UsedCommands
ms.assetid: 99cd05d3-644a-42ff-b289-8458cd1b20c0
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 91929038d77bcf14c6997f9b60551ed8c9c3b820
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68186369"
---
# <a name="usedcommand-element"></a>UsedCommand 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

允许 VSPackage 访问在 .vsct 文件中定义的命令。 例如，如果你的 VSPackage 使用由 shell 定义的标准 **复制** 命令， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 则可以将命令添加到菜单或工具栏，而无需重新实现它。  
  
## <a name="syntax"></a>语法  
  
```  
<UsedCommand guid="guidMyCommandGroup" id="MyCommand" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|说明|  
|---------------|-----------------|  
|guid|必需。 标识命令的 GUID ID 对的 GUID。|  
|id|必需。 标识命令的 GUID ID 对的 ID。|  
|条件|可选。 请参阅 [条件特性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|说明|  
|-------------|-----------------|  
|无||  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[UsedCommands 元素](../extensibility/usedcommands-element.md)|将 UsedCommand 元素和其他 UsedCommands 分组分组。|  
  
## <a name="remarks"></a>备注  
 通过将命令添加到 `<UsedCommands>` 元素，VSPackage 向 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 环境通知 VSPackage 需要该命令。 应 `<UsedCommand>` 为包所需的任何命令添加一个元素，Visual Studio 的所有版本和配置中可能不包含此元素。 例如，如果你的包调用特定于 Visual C++ 的命令，则 Visual Web Developer 的用户将不能使用该命令，除非你 `<UsedCommand>` 为该命令包含一个元素。  
  
## <a name="example"></a>示例  
  
```  
<UsedCommands>  
  <UsedCommand guid="guidVSStd97" id="cmdidCut"/>  
  <UsedCommand guid="guidVSStd97" id="cmdidCopy"/>  
  <UsedCommand guid="guidVSStd97" id="cmdidPaste"/>  
</UsedCommands>  
```  
  
## <a name="see-also"></a>另请参阅  
 [UsedCommands 元素](../extensibility/usedcommands-element.md)   
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
