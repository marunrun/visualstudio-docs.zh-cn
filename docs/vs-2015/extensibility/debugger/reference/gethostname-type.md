---
title: GETHOSTNAME_TYPE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- GETHOSTNAME_TYPE
helpviewer_keywords:
- GETHOSTNAME_TYPE enumeration
ms.assetid: 2be92bea-8133-412b-9015-1833baf16e1b
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b3f7d09e29489dac0598b9558df595aedd0c5d61
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203060"
---
# <a name="gethostname_type"></a>GETHOSTNAME_TYPE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定主机名的类型。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_GETHOSTNAME_TYPE {   
   GHN_FRIENDLY_NAME = 0,  
   GHN_FILE_NAME     = 1  
};  
typedef DWORD GETHOSTNAME_TYPE;  
```  
  
```csharp  
public enum enum_GETHOSTNAME_TYPE {   
   GHN_FRIENDLY_NAME = 0,  
   GHN_FILE_NAME     = 1  
};  
```  
  
## <a name="members"></a>成员  
 GHN_FRIENDLY_NAME  
 指定主机的友好名称。  
  
 GHN_FILE_NAME  
 指定主机的文件名。  
  
## <a name="remarks"></a>备注  
 这些值作为参数传递给 [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md) 方法以检索不同格式的主机名。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [计数](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)
