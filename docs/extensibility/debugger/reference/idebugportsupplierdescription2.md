---
title: IDebugPort供应商描述2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierDescription2 interface
ms.assetid: dd19b9d6-0703-44b3-9498-cedffa0ce5b7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 69853e34788a2f24afe183dfbb7070e48f14aa46
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724365"
---
# <a name="idebugportsupplierdescription2"></a>IDebugPortSupplierDescription2
使[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]UI 能够在 **"附加到流程"** 对话框的 **"传输信息**"部分内显示文本。

## <a name="syntax"></a>语法

```
IDebugPortSupplierDescription2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 此接口由端口供应商实现。

## <a name="methods"></a>方法
 下表显示了 的方法`IDebugPortSupplierDescription2`。

|方法|描述|
|------------|-----------------|
|[获取描述](../../../extensibility/debugger/reference/idebugportsupplierdescription2-getdescription.md)|检索端口供应商的说明和描述元数据。|

## <a name="requirements"></a>要求
 标题： Msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll
