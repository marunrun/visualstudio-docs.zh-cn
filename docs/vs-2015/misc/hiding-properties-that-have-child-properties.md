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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62822381"
---
# <a name="hiding-properties-that-have-child-properties"></a>隐藏具有子属性的属性
你想要隐藏具有子属性的属性：  
  
- 如果具有嵌套的项目的父项目以编程方式控制子项目的某些方面。  
  
- 如果使用专门的设计器使用控件并且你不想要为开发人员的完全访问权限提供给控件的所有属性。  
  
- 如果你具有的一个对象的作用域所有权，并想要限制属性的视图。  
  
### <a name="to-hide-properties-that-have-child-properties"></a>若要隐藏具有子属性的属性  
  
1. 设置`pfDisplay`中的参数<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.DisplayChildProperties%2A>到`FALSE`。  
  
2. 设置`pfHide`中的参数<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A>到`TRUE`。  
  
## <a name="see-also"></a>请参阅  
 [属性显示网格](../extensibility/internals/properties-display-grid.md)