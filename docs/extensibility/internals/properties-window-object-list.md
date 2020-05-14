---
title: 属性窗口对象列表 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, object list
ms.assetid: 6c159c9d-345d-4b23-8ddd-9839d338b62f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ffe11ae6ebb4e692686c884b663a4f93d1466535
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706153"
---
# <a name="properties-window-object-list"></a>属性窗口对象列表
**属性**窗口中的对象列表是一个下拉列表，允许您将所选内容更改为一个或多个选定窗口中可用的其他对象。 从此列表中选择其他对象将触发调用，以<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A>通知环境已选择新对象。 然后更改"**属性"** 窗口中显示的信息以显示与新选择的对象关联的属性。

## <a name="the-object-list"></a>对象列表
 对象列表由两个字段组成：对象名称（以粗体显示）和对象类型。

 使用`Name`<xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo>接口提供的属性从对象本身检索以粗体显示的对象类型左侧的对象名称。 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo.GetClassInfo%2A>，上<xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo>的唯一方法 返回<xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo>该接口的 coclass。 属性**窗口**用于<xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo>获取 coclass 的名称，该名称在下拉列表中显示为对象名称。

 如果对象没有`Name`属性，则名称不会显示在对象列表的"名称"区域中。 如果希望对象列表中显示的名称，则可以向对象添加 Name 属性。

 如果 COM 对象未实现<xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo>，**则属性**窗口将接口名称显示在列表左侧的对象名称中。

## <a name="see-also"></a>请参阅
- [扩展属性](../../extensibility/internals/extending-properties.md)
