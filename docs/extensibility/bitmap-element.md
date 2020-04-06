---
title: 位图元素 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739994"
---
# <a name="bitmap-element"></a>位图元素
定义位图。 位图从资源或文件加载。

## <a name="syntax"></a>语法

```
<Bitmap guid="guidImages" href="images\MyImage.bmp" usedList="bmp1, bmp2, bmp3" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|guid|必需。 GUID/ID 命令标识符的 GUID。<br /><br /> 位图的 guid 属性不与任何 VSPackage 或其他命令组关联。  它应该是位图定义的唯一，不应用于任何其他目的。|
|渣 油|GUID/ID 命令标识符的 ID。 需要 resID 或 href属性。<br /><br /> resID 属性是一个整数资源 ID，用于确定在命令表合并期间要加载的位图条带。  加载命令表时，资源 ID 指定的位图将从同一模块的资源加载。|
|已使用列表|如果存在 resID 属性，则为必填项。 选择位图条中的可用图像。|
|href|位图的路径。 需要 resID 或 href属性。<br /><br /> 将搜索包含路径以查找指示的图像文件，该文件嵌入到生成的二进制文件中。  在命令表合并期间，将复制映像，无需其他资源查找或加载。  如果使用的 List 属性不存在，则条带中的所有图像都可用。 **注：** 图像可以以多种格式之一提供，包括 *.bmp、.png*和 *.png**.gif*。  早期版本的编译器不支持具有 Alpha 信息的 32 位位图图像，以便获得部分透明度。 这些版本的解决方法是使用 *.png*格式。|
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[位图元素](../extensibility/bitmaps-element.md)|对位图元素。|

## <a name="example"></a>示例

```
<Bitmap guid="guidWidgetIcons" href="WidgetToolbarIcons_32.bmp" />
<Bitmap guid="guidWidgetIcons2" resID="IDBMP_WIDGETICONS"
  usedList="1, 2, 3, 4"/>
```

## <a name="see-also"></a>请参阅
- [可视化工作室命令表 （.vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
