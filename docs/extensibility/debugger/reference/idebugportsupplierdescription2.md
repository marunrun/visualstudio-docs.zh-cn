---
title: IDebugPortSupplierDescription2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierDescription2 interface
ms.assetid: dd19b9d6-0703-44b3-9498-cedffa0ce5b7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ae6491628888f682d61c94ae618bfad72837c845
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66339883"
---
# <a name="idebugportsupplierdescription2"></a>IDebugPortSupplierDescription2
使[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]UI 来显示内的文本**传输信息**一部分**附加到进程**对话框。

## <a name="syntax"></a>语法

```
IDebugPortSupplierDescription2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 此接口由端口提供程序实现。

## <a name="methods"></a>方法
 下表显示的方法`IDebugPortSupplierDescription2`。

|方法|描述|
|------------|-----------------|
|[GetDescription](../../../extensibility/debugger/reference/idebugportsupplierdescription2-getdescription.md)|检索端口提供程序的说明和描述性元数据。|

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll