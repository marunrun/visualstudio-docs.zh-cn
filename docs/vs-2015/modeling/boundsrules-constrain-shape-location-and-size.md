---
title: BoundsRules 约束形状位置和大小 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, events
ms.assetid: 4d08e541-fc67-4e68-bf31-30d346aa2aa0
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7d660189ede0848216eb44d6ef49fe9c93a06ec8
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672730"
---
# <a name="boundsrules-constrain-shape-location-and-size"></a>BoundsRules 约束形状位置和大小
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*边界规则*是定义形状的大小和位置限制的类。 它提供一个方法，当用户拖动形状或形状的角部或边时，此方法会被重复调用。

 下面的示例将矩形形状约束为固定大小（水平或垂直）的条形。 当用户拖动角部或边时，大纲在高度和宽度的两个允许的配置之间翻转。

 边界规则是从 <xref:Microsoft.VisualStudio.Modeling.Diagrams.BoundsRules> 派生的类。 在形状中创建规则的实例：

```
using Microsoft.VisualStudio.Modeling.Diagrams; ...
public partial class BarShape
{
  /// <summary>
  /// Rule invoked when the user is resizing a shape.
  /// </summary>
  public override BoundsRules BoundsRules
  { get { return new BarBoundsRule(); } }
}
/// <summary>
/// Rule invoked when the user is changing a shape's outline.
/// Provides real-time mouse rubber-band feedback, so must work fast.
/// </summary>
public class BarBoundsRule: BoundsRules
{
  public override RectangleD GetCompliantBounds
     (ShapeElement shape, RectangleD proposedBounds)
  {
    double thickness = 0.1;
    if (proposedBounds.Height > proposedBounds.Width)
    {
      // There is a minimum width for a shape; the width
      // will actually be set to the lesser of
      // thickness and that minimum.
      return new RectangleD(proposedBounds.Location,
            new SizeD(thickness, proposedBounds.Height));
    }
    else
    {
      // There is a minimum height for a shape; the
      // height will actually be set to the lesser of
      // thickness and that minimum.
      return new RectangleD(proposedBounds.Location,
         new SizeD(proposedBounds.Width, thickness));
} } }
```

 请注意，如果需要，可以对位置和大小进行限制。

## <a name="see-also"></a>请参阅
 <xref:Microsoft.VisualStudio.Modeling.Diagrams.BoundsRules>[响应和传播更改](../modeling/responding-to-and-propagating-changes.md)
