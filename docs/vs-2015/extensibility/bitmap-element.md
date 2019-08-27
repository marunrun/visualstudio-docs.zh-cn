---
title: Bitmap 元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Bitmaps
- Bitmaps element (VSCT XML schema)
ms.assetid: edcd7891-f4e7-416d-809d-5e2eed9f17e4
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fc1fb57c7ec43421b211b29cfd6ab97b24a1864c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68184745"
---
# <a name="bitmap-element"></a>Bitmap 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

定义位图。 从资源或从文件加载位图。  
  
## <a name="syntax"></a>语法  
  
```  
<Bitmap guid="guidImages" href="images\MyImage.bmp" usedList="bmp1, bmp2, bmp3" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|guid|必需。 GUID ID 的命令标识符的 GUID。<br /><br /> 位图的 guid 属性不与任何 VSPackage 或其他命令组相关联。  它应是唯一的位图定义并不用于任何其他用途。|  
|resID|GUID ID 的命令标识符的 ID。 ResID 或 href 属性是必需的。<br /><br /> ResID 属性是一个整数资源 ID，用于确定是要在命令表合并期间加载的位图条。  加载的命令表时，将从相同模块的资源加载指定的资源 ID 的位图。|  
|usedList|所需 resID 属性是否存在。 位图条中选择可用的映像。|  
|href|位图的路径。 ResID 或 href 属性是必需的。<br /><br /> 包含路径中搜索所指示的图像文件，生成的二进制文件中嵌入的。  在命令表合并，映像将复制并没有查找其他资源或负载是必需的。  如果 usedList 属性不存在，则该带中的所有映像。 **注意：** 中包括.bmp、.png 和.gif 的几种格式之一，可能会提供映像。  早期版本的编译器不支持部分透明 alpha 信息的 32 位位图图像。 这些版本的解决方法是使用.png 格式。|  
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[Bitmaps 元素](../extensibility/bitmaps-element.md)|位图元素进行分组。|  
  
## <a name="example"></a>示例  
  
```  
<Bitmap guid="guidWidgetIcons" href="WidgetToolbarIcons_32.bmp" />  
<Bitmap guid="guidWidgetIcons2" resID="IDBMP_WIDGETICONS"  
  usedList="1, 2, 3, 4"/>  
```  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
