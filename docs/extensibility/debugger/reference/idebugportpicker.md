---
title: IDebugPortPicker | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortPicker interface
ms.assetid: 8b7f6685-a3c5-4355-b706-c1b574f6ff84
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 991480886c2c43c330ce37561d383ffdc420e214
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66340369"
---
# <a name="idebugportpicker"></a>IDebugPortPicker
表示自定义的 UI 选择相应端口。

## <a name="syntax"></a>语法

```
IDebugPortPicker : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 此接口由端口提供程序实现。 端口提供程序定义其端口选取器通过将其公开为 CLSID 并指向`metricPortPickerCLSID`指标在公开的 CLSID。

## <a name="methods"></a>方法
 下表显示的方法`IDebugPortPicker`。

|方法|描述|
|------------|-----------------|
|[DisplayPortPicker](../../../extensibility/debugger/reference/idebugportpicker-displayportpicker.md)|显示指定的对话框，允许用户选择的端口。|
|[SetSite](../../../extensibility/debugger/reference/idebugportpicker-setsite.md)|设置服务提供程序。|

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll