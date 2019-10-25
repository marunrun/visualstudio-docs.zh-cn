---
title: "\"属性\" 窗口对象列表 |Microsoft Docs"
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, object list
ms.assetid: 6c159c9d-345d-4b23-8ddd-9839d338b62f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e50b3fe46edb8d14cad9a03a45bc8650cb9713ab
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72725189"
---
# <a name="properties-window-object-list"></a>属性窗口对象列表
"**属性**" 窗口中的对象列表是一个下拉列表，可用于将所选内容更改为在一个或多个选定窗口中可用的其他对象。 选择此列表中的不同对象将触发对 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A> 的调用，以通知环境已选择了新的对象。 然后，将更改在 "**属性**" 窗口中显示的信息，以显示与新选择的对象相关联的属性。

## <a name="the-object-list"></a>对象列表
 对象列表包括两个字段：对象名称（以粗体显示）和对象类型。

 使用 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> 接口提供的 `Name` 属性，可从对象本身检索以粗体显示的对象类型的对象名称。 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo.GetClassInfo%2A>，<xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> 上的唯一方法返回该接口的 coclass <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo>。 "**属性**" 窗口使用 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> 获取组件类的名称，该名称在下拉列表中显示为对象名称。

 如果该对象没有 `Name` 属性，则不会在对象列表的名称区域中显示名称。 如果希望在 "对象" 列表中显示名称，则可以将 "名称" 属性添加到对象。

 如果 COM 对象未实现 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo>，"**属性**" 窗口将显示接口名称，而不是列表左侧的对象名称。

## <a name="see-also"></a>请参阅
- [扩展属性](../../extensibility/internals/extending-properties.md)