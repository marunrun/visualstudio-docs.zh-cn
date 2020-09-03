---
title: IDebugCustomViewer：:D isplayValue |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
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
中父窗口

`dwID`\
中支持多种类型的自定义查看器的 ID。

`pHostServices`\
[in] 保留。 始终设置为 null。

`pDebugProperty`\
中可用于检索要显示的值的接口。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 显示是 "模式"，此方法将在返回到调用方之前创建所需的窗口、显示值、等待输入并关闭窗口。 这意味着该方法必须处理显示属性值的所有方面，从创建用于输出的窗口到等待用户输入来销毁窗口。

 若要支持更改给定 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) 对象上的值，可以使用 [SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md) 方法（如果值可以表示为字符串）。 否则，必须 `DisplayValue` 在实现接口的同一对象上创建自定义接口，该接口独占到实现此方法的表达式计算器 `IDebugProperty3` 。 此自定义接口将提供用于更改任意大小或复杂性的数据的方法。

## <a name="see-also"></a>另请参阅
- [IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)
