---
title: ADDRESS_KIND | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- ADDRESS_KIND
helpviewer_keywords:
- ADDRESS_KIND enumeration
ms.assetid: 3a12fbec-7088-4cf9-8f6f-ad8ddec6009a
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6152ff5f493134812916f28e0b908bf98ecdbb35
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62561868"
---
# <a name="addresskind"></a>ADDRESS_KIND
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定地址的类型。  
  
## <a name="syntax"></a>语法  
  
```cpp  
enum enum_ADDRESS_KIND {  
   ADDRESS_KIND_NATIVE                  = 0x0001,  
   ADDRESS_KIND_UNMANAGED_THIS_RELATIVE = 0x0002,  
   ADDRESS_KIND_UNMANAGED_PHYSICAL      = 0x0005,  
   ADDRESS_KIND_METADATA_METHOD         = 0x0010,  
   ADDRESS_KIND_METADATA_FIELD          = 0x0011,  
   ADDRESS_KIND_METADATA_LOCAL          = 0x0012,  
   ADDRESS_KIND_METADATA_PARAM          = 0x0013,  
   ADDRESS_KIND_METADATA_ARRAYELEM      = 0x0014,  
   ADDRESS_KIND_METADATA_RETVAL         = 0x0015,  
};  
typedef DWORD ADDRESS_KIND;  
```  
  
```csharp  
public enum enum_ADDRESS_KIND {  
   ADDRESS_KIND_NATIVE                  = 0x0001,  
   ADDRESS_KIND_UNMANAGED_THIS_RELATIVE = 0x0002,  
   ADDRESS_KIND_UNMANAGED_PHYSICAL      = 0x0005,  
   ADDRESS_KIND_METADATA_METHOD         = 0x0010,  
   ADDRESS_KIND_METADATA_FIELD          = 0x0011,  
   ADDRESS_KIND_METADATA_LOCAL          = 0x0012,  
   ADDRESS_KIND_METADATA_PARAM          = 0x0013,  
   ADDRESS_KIND_METADATA_ARRAYELEM      = 0x0014,  
   ADDRESS_KIND_METADATA_RETVAL         = 0x0015,  
};  
```  
  
## <a name="terms"></a>术语  
 ADDRESS_KIND_NATIVE  
 表示本机地址[NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md)结构。  
  
 ADDRESS_KIND_UNMANAGED_THIS_RELATIVE  
 相对于非托管的地址`this`(`Me`在 Visual Basic 中) 指针并且由表示[UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md)结构。  
  
 ADDRESS_KIND_UNMANAGED_PHYSICAL  
 非托管的物理地址，由此[UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md)结构。  
  
 ADDRESS_KIND_METHOD  
 表示的类的方法[METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md)结构。  
  
 ADDRESS_KIND_FIELD  
 表示的类的字段[METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md)结构。  
  
 ADDRESS_KIND_LOCAL  
 地址是本地变量和为由[METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md)结构。  
  
 ADDRESS_KIND_PARAM  
 一个方法或函数的参数，表示[METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md)结构。  
  
 ADDRESS_KIND_ARRAYELEM  
 数组元素，表示[METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md)结构。  
  
 ADDRESS_KIND_RETVAL  
 返回值，表示[METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md)结构。  
  
## <a name="remarks"></a>备注  
 [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)方法将返回[DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)结构，其中包含的可能结构、 联合[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)结构。 `dwKind`字段`DEBUG_ADDRESS_UNION`结构保存`ADDRESS_KIND`值并介绍了如何解释联合字段。  
  
## <a name="requirements"></a>要求  
 标头： sh.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)   
 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)   
 [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
