---
title: IDispatchEx：： GetNextDispID |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.GetNextDispID
apilocation:
- scrobj.dll
helpviewer_keywords:
- GetNextDispID method
ms.assetid: 8263d441-85ee-47f4-bdba-fbf2ad07e85f
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8811e828a6701769badf45ca7c37f9c53529150f
ms.sourcegitcommit: d281d2a04a5bc302650eebf369946d8f101e59dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88144424"
---
# <a name="idispatchexgetnextdispid"></a>IDispatchEx::GetNextDispID

枚举对象的成员。

## <a name="syntax"></a>语法

```cpp
HRESULT GetNextDispID(
   DWORD grfdex,
   DISPID id,
   DISPID *pid
);
```

## <a name="parameters"></a>参数

`grfdex`\
确定要枚举的项的集合。 这可以是以下值的组合：

|值|含义|
|-----------|-------------|
|fdexEnumDefault|请求对象枚举默认元素。 允许对象枚举任何元素集。|
|fdexEnumAll|请求对象枚举所有元素。 允许对象枚举任何元素集。|

`id`\
标识当前成员。 GetNextDispID 检索此项后的枚举中的项。 使用 GetDispID 或以前对 GetNextDispID 的调用来获取此标识符。 使用 DISPID_STARTENUM 值获取第一项的第一个标识符。

`pid`\
DISPID 变量的地址，该变量接收枚举中下一项的标识符。

如果成员由 `DeleteMemberByName` 或删除 `DeleteMemberByDispID` ，则需要对 `DISPID` 有效 `GetNextDispID` 。

## <a name="return-value"></a>返回值

返回以下值之一：

|值|含义|
|-|-|
|`S_OK`|成功。|
|`S_FALSE`|枚举已完成。|

## <a name="example"></a>示例

```cpp
   HRESULT hr;
   BSTR bstrName;
   DISPID dispid;
   IDispatchEx *pdex;

   // Assign to pdex
   hr = pdex->GetNextDispID(fdexEnumAll, DISPID_STARTENUM, &dispid);
   while (hr == NOERROR)
   {
      hr = pdex->GetMemberName(dispid, &bstrName);
      if (!wcscmp(bstrName, OLESTR("Bar")))
      {
         SysFreeString(bstrName);
         return TRUE;
      }
      SysFreeString(bstrName);
      hr = pdex->GetNextDispID(fdexEnumAll, dispid, &dispid);
   }
```

## <a name="see-also"></a>另请参阅

- [IDispatchEx 接口](../../winscript/reference/idispatchex-interface.md)
- [IDispatchEx::GetDispID](../../winscript/reference/idispatchex-getdispid.md)
- [IDispatchEx::DeleteMemberByName](../../winscript/reference/idispatchex-deletememberbyname.md)
- [IDispatchEx::DeleteMemberByDispID](../../winscript/reference/idispatchex-deletememberbydispid.md)