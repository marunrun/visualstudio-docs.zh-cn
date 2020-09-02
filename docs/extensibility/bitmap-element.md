---
title: Bitmap 元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Bitmaps
- Bitmaps element (VSCT XML schema)
ms.assetid: edcd7891-f4e7-416d-809d-5e2eed9f17e4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2d663351aad7d381dd5bfe4cbaa0a263cc70b821
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739994"
---
# <a name="bitmap-element"></a>Bitmap 元素
定义位图。 位图是从资源或从文件加载的。

## <a name="syntax"></a>语法

```
<Bitmap guid="guidImages" href="images\MyImage.bmp" usedList="bmp1, bmp2, bmp3" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|说明|
|---------------|-----------------|
|guid|必需。 GUID/ID 命令标识符的 GUID。<br /><br /> 位图的 guid 属性不与任何 VSPackage 或其他命令组相关联。  它应该是位图定义的唯一，不能用于任何其他目的。|
|Resid 标识|GUID/ID 命令标识符的 ID。 Resid 标识或 href 属性是必需的。<br /><br /> Resid 标识属性是一个整数资源 ID，用于确定在命令表合并期间要加载的位图条带。  加载命令表时，将从同一个模块的资源加载资源 ID 指定的位图。|
|usedList|如果存在 Resid 标识属性，则为必需。 选择位图条带中的可用图像。|
|href|位图的路径。 Resid 标识或 href 属性是必需的。<br /><br /> 在包含路径中搜索指定的图像文件，该文件嵌入到生成的二进制文件中。  在命令表合并期间，会复制映像，无需进行额外的资源查找或加载。  如果 usedList 属性不存在，则带中的所有图像都可用。 **注意：**  可以采用多种格式之一（包括 *.bmp*、 *.png*和 *.gif*）提供图像。  早期版本的编译器不支持包含部分透明度的 alpha 信息的32位位图映像。 这些版本的解决方法是使用 *.png* 格式。|
|条件|可选。 请参阅 [条件特性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[位图元素](../extensibility/bitmaps-element.md)|组位图元素。|

## <a name="example"></a>示例

```
<Bitmap guid="guidWidgetIcons" href="WidgetToolbarIcons_32.bmp" />
<Bitmap guid="guidWidgetIcons2" resID="IDBMP_WIDGETICONS"
  usedList="1, 2, 3, 4"/>
```

## <a name="see-also"></a>另请参阅
- [Visual Studio 命令表 ( .vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
