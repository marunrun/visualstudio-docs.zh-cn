---
title: IDebugField::GetExtendedInfo | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugField::GetExtendedInfo
helpviewer_keywords:
- IDebugField::GetExtendedInfo method
ms.assetid: 46c0dd4d-4fd5-4efd-a908-71e4248e8e8d
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3de21bc984a36db87f8ce1567f4ff7d97212c40e
ms.sourcegitcommit: 0cd282a7584b9bfd4df7882f8fdf3ad8a270e219
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2019
ms.locfileid: "62547554"
---
# <a name="idebugfieldgetextendedinfo"></a>IDebugField::GetExtendedInfo
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法获取扩展字段的信息。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetExtendedInfo(   
   REFGUID guidExtendedInfo,  
   BYTE**  prgBuffer,  
   DWORD*  pdwLen  
);  
```  
  
```csharp  
int GetExtendedInfo(  
   ref Guid guidExtendedInfo,   
   IntPtr[] prgBuffer,   
   ref uint pdwLen  
);  
```  
  
#### <a name="parameters"></a>参数  
 `guidExtendedInfo`  
 [in]选择要返回的信息。 有效值为：  
  
|值|描述|  
|-----------|-----------------|  
|`guidConstantValue`|作为一个字节序列的值。|  
|`guidConstantType`|类型签名形式的类型。|  
  
 `prgBuffer`  
 [out]返回扩展的信息。  
  
 `pdwLen`  
 [in、 out]以字节为单位返回大小的扩展信息。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 目前，此方法返回类型或常量的值。 调用方必须释放中返回的缓冲区`prgBuffer`通过调用 COM 的`CoTaskMemFree`函数 (C++) 或<xref:System.Runtime.InteropServices.Marshal.FreeCoTaskMem%2A>(C#)。  
  
## <a name="see-also"></a>请参阅  
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
