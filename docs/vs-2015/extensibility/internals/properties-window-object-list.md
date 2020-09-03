---
title: "\"属性\" 窗口对象列表 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Properties window, object list
ms.assetid: 6c159c9d-345d-4b23-8ddd-9839d338b62f
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 95ef509491e05daf575e211ae479c815994eb3d0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148327"
---
# <a name="properties-window-object-list"></a>属性窗口对象列表
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

" **属性** " 窗口中的对象列表是一个下拉列表，可用于将所选内容更改为在一个或多个选定窗口中可用的其他对象。 选择此列表中的不同对象将触发对的调用 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A> ，以通知环境已选择了新的对象。 然后，将更改在 " **属性** " 窗口中显示的信息，以显示与新选择的对象相关联的属性。  
  
## <a name="the-object-list"></a>对象列表  
 对象列表包括两个字段：对象名称以粗体显示 () 和对象类型。  
  
 以粗体显示的对象类型的对象名称是从对象本身使用接口提供的属性来检索的 `Name` <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> 。 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo.GetClassInfo%2A>仅上的方法 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo> 为该接口的 coclass 返回。 " **属性** " 窗口使用 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> 来获取组件类的名称，该名称在下拉列表中显示为对象名称。  
  
 如果该对象没有 `Name` 属性，则不会在对象列表的名称区域中显示名称。 如果希望在 "对象" 列表中显示名称，则可以将 "名称" 属性添加到对象。  
  
 如果 COM 对象未实现 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> ，" **属性** " 窗口将显示接口名称，而不是列表左侧的对象名称。  
  
## <a name="see-also"></a>另请参阅  
 [扩展属性](../../extensibility/internals/extending-properties.md)
