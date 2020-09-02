---
title: 隐藏具有子属性的属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- properties [Visual Studio SDK], hiding
- Properties window, hiding properties that have child properties
ms.assetid: 6003607e-fc19-4bf9-a299-9f6adf8e92eb
caps.latest.revision: 13
manager: jillfra
ms.openlocfilehash: 1d20b865c6f07d76320a7df8402810c82869ddfb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62822381"
---
# <a name="hiding-properties-that-have-child-properties"></a>隐藏具有子属性的属性
需要隐藏具有子属性的属性：  
  
- 如果嵌套项目的父项目以编程方式控制子项目的某些方面，则为。  
  
- 如果将控件用于专用设计器，并且不希望让开发人员对控件的所有属性都具有完全访问权限。  
  
- 如果你拥有对象的作用域所有权，并想要限制属性的视图。  
  
### <a name="to-hide-properties-that-have-child-properties"></a>隐藏具有子属性的属性  
  
1. 将 `pfDisplay` 参数设置 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.DisplayChildProperties%2A> 为 `FALSE` 。  
  
2. 将 `pfHide` 参数设置 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A> 为 `TRUE` 。  
  
## <a name="see-also"></a>另请参阅  
 [属性显示网格](../extensibility/internals/properties-display-grid.md)