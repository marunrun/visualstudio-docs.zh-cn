---
title: IDebugCustom查看器：:D播放价值 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomViewer::DisplayValue
helpviewer_keywords:
- IDebugCustomViewer::DisplayValue
ms.assetid: 7a538248-5ced-450e-97cd-13fabe35fb1c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 32e444d0d6a30484f708d3001b95e7a71856edd5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732450"
---
# <a name="idebugcustomviewerdisplayvalue"></a>IDebugCustomViewer::DisplayValue
调用此方法以显示指定的值。

## <a name="syntax"></a>语法

```cpp
HRESULT DisplayValue(
   HWND             hwnd,
   DWORD            dwID,
   IUnknown *       pHostServices,
   IDebugProperty3* pDebugProperty);
);
```

```csharp
int DisplayValue(
   IntPtr          hwnd,
   uint            dwID,
   object          pHostServices,
   IDebugProperty3 pDebugProperty
);
```

## <a name="parameters"></a>参数
`hwnd`\
[在]父窗口

`dwID`\
[在]支持多种类型的自定义查看器的 ID。

`pHostServices`\
[in] 保留。 始终设置为 null。

`pDebugProperty`\
[在]可用于检索要显示的值的接口。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则返回错误代码。

## <a name="remarks"></a>备注
 显示是"模态的"，因为此方法将创建必要的窗口、显示值、等待输入并关闭窗口，所有这些都在返回到调用方之前。 这意味着该方法必须处理显示属性值的所有方面，从为输出创建窗口，到等待用户输入，到销毁窗口。

 要支持更改给定[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)对象上的值，可以使用[SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)方法 —如果该值可以表示为字符串。 否则，有必要在实现`DisplayValue``IDebugProperty3`接口的同一对象上创建自定义接口（独占表达式赋值器实现此方法）。 此自定义接口将提供用于更改任意大小或复杂性的数据的方法。

## <a name="see-also"></a>请参阅
- [IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)
