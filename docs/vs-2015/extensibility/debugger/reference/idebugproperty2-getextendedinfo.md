---
title: IDebugProperty2::GetExtendedInfo |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetExtendedInfo
helpviewer_keywords:
- IDebugProperty2::GetExtendedInfo
ms.assetid: 0c9c0b2b-7540-4424-adb5-fce7aa37a026
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 74810aab2f47a36c716891fd45b7424eb737b142
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68164978"
---
# <a name="idebugproperty2getextendedinfo"></a>IDebugProperty2::GetExtendedInfo
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取扩展的属性信息。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
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
  
#### <a name="parameters"></a>Parameters  
 `guidExtendedInfo`  
 [in]确定要检索的扩展信息的类型的 GUID。 有关详细信息，请参阅备注。  
  
 `pExtendedInfo`  
 [out]返回`VARIANT`(C++) 或对象 (C#) 可用于检索的扩展的属性信息。 例如，此参数可能会返回`IUnknown`接口，可用于查询[IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)接口。 有关详细信息，请参阅备注。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则返回错误代码。 返回`S_GETEXTENDEDINFO_NO_EXTENDEDINFO`如果没有要检索的扩展的信息。  
  
## <a name="remarks"></a>备注  
 此方法以便检索不会将自身添加到由调用检索的信息存在[GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)方法。  
  
 以下 Guid 通常所识别的 （GUID 值指定为 C# 因为名称不能在任何程序集中） 此方法。 供内部使用，可以创建其他 Guid。  
  
|名称|GUID|描述|  
|----------|----------|-----------------|  
|guidDocument|{3f98de84-fee9-11d0-b47f-00a0244a1dd2}|返回`IUnknown`到文档的接口。 通常情况下， [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)接口可以获取从此`IUnknown`接口。|  
|guidCodeContext|{e2fc65e-56ce-11d1-b528-00aax004a8797}|返回`IUnknown`文档上下文的接口。 通常情况下， [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)接口可以获取从此`IUnknown`接口。|  
|guidCustomViewerSupported|{d9c9da31-ffbe-4eeb-9186-23121e3c088c}|返回一个包含自定义查看器通常由表达式计算器实现的 CLSID 的字符串。|  
|guidExtendedInfoSlot|{6df235ad-82c6-4292-9c97-7389770bc42f}|返回表示所需的槽数，如果此属性表示托管的代码的本地地址的 32 位数字。|  
|guidExtendedInfoSignature|{b5fb6d46-f805-417f-96a3-8ba737073ffd}|返回一个包含与属性对象关联的变量的签名字符串。|  
  
## <a name="see-also"></a>请参阅  
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)   
 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
