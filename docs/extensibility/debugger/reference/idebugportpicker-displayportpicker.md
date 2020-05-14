---
title: IDebugPortPicker：:D播放波特皮克 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- DisplayPortPicker
- IDebugPortPicker::DisplayPortPicker
ms.assetid: 08511ef5-be64-4069-b169-a569cc94bc64
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e0a02169b37bba804034990ed5d972f973244769
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724889"
---
# <a name="idebugportpickerdisplayportpicker"></a>IDebugPortPicker::DisplayPortPicker
显示允许用户选择端口的指定对话框。

## <a name="syntax"></a>语法

```cpp
HRESULT DisplayPortPicker(
   HWND hwndParentDialog,
   BSTR* pbstrPortId
);
```

```csharp
public int DisplayPortPicker(
   int hwndParentDialog,
   out string pbstrPortId
);
```

## <a name="parameters"></a>参数
`hwndParentDialog`\
[在]父对话框的句柄。

`pbstrPortId`\
[出]端口标识符字符串。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。 返回`S_FALSE`值 （或 与`S_OK``BSTR`设置为`NULL`的 返回值 ） 表示用户单击 **"取消**"。

## <a name="see-also"></a>请参阅
- [IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md)
