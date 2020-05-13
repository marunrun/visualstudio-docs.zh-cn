---
title: IDebug属性2：：获取扩展信息 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetExtendedInfo
helpviewer_keywords:
- IDebugProperty2::GetExtendedInfo
ms.assetid: 0c9c0b2b-7540-4424-adb5-fce7aa37a026
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 34d6cd880ccae520bf000ad01b52223857f4f10f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721487"
---
# <a name="idebugproperty2getextendedinfo"></a>IDebugProperty2::GetExtendedInfo
获取属性的扩展信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetExtendedInfo ( 
   REFGUID* guidExtendedInfo,
   VARIANT* pExtendedInfo
);
```

```csharp
int GetExtendedInfo ( 
   ref Guid guidExtendedInfo,
   out object pExtendedInfo
);
```

## <a name="parameters"></a>参数
`guidExtendedInfo`\
[在]确定要检索的扩展信息的类型的 GUID。 有关详细信息，请参阅备注。

`pExtendedInfo`\
[出]返回可用于`VARIANT`检索扩展属性信息的 （C++） 或对象 （C#）。 例如，此参数可能会返回一个`IUnknown`接口，该接口可以查询[IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)接口。 有关详细信息，请参阅备注。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则返回错误代码。 如果没有`S_GETEXTENDEDINFO_NO_EXTENDEDINFO`要检索的扩展信息，则返回。

## <a name="remarks"></a>备注
 此方法的存在是为了检索无法通过调用[GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)方法检索的信息。

 此方法通常可识别以下 GUID（GUID 值指定为 C#，因为名称在任何程序集中不可用）。 可以创建其他 GUID 供内部使用。

|名称|GUID|描述|
|----------|----------|-----------------|
|吉德文件|[3f98de84-fee9-11d0-b47f-00a0244a1d2]|返回文档`IUnknown`的接口。 通常，可以从此`IUnknown`接口获取[IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)接口。|
|吉德代码上下文|[e2fc65e-56ce-11d1-b528-00ax004a8797]|返回文档`IUnknown`上下文的接口。 通常，可以从此`IUnknown`接口获取[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)接口。|
|吉德自定义查看器支持|[d9c9da31-ffbe-4eeb-9186-23121e3c088c]|返回包含自定义查看器的 CLSID 的字符串，通常由表达式赋值器实现。|
|吉德扩展信息槽|[6df235ad-82c6-4292-9c97-7389770bc42f]|如果此属性表示托管代码本地地址，则返回表示所需插槽号的 32 位数字。|
|吉德扩展信息签名|[b5fb6d46-f805-417f-96a3-8ba737073ffd]|返回一个字符串，其中包含与属性对象关联的变量的签名。|

## <a name="see-also"></a>请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
