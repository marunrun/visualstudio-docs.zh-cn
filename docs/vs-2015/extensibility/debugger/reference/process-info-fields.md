---
title: PROCESS_INFO_FIELDS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- PROCESS_INFO_FIELDS
helpviewer_keywords:
- PROCESS_INFO_FIELDS enumeration
ms.assetid: 0d9cc345-3d3a-44d8-ae15-a67acb97a828
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7700670774dcb38b054cf28275f64c0c3046f741
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68205030"
---
# <a name="process_info_fields"></a>PROCESS_INFO_FIELDS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定要为进程检索的信息类型。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_PROCESS_INFO_FIELDS {   
   PIF_FILE_NAME             = 0x00000001,  
   PIF_BASE_NAME             = 0x00000002,  
   PIF_TITLE                 = 0x00000004,  
   PIF_PROCESS_ID            = 0x00000008,  
   PIF_SESSION_ID            = 0x00000010,  
   PIF_ATTACHED_SESSION_NAME = 0x00000020,  
   PIF_CREATION_TIME         = 0x00000040,  
   PIF_FLAGS                 = 0x00000080,  
   PIF_ALL                   = 0x000000ff  
};  
typedef DWORD PROCESS_INFO_FIELDS;  
```  
  
```csharp  
public enum enum_PROCESS_INFO_FIELDS {   
   PIF_FILE_NAME             = 0x00000001,  
   PIF_BASE_NAME             = 0x00000002,  
   PIF_TITLE                 = 0x00000004,  
   PIF_PROCESS_ID            = 0x00000008,  
   PIF_SESSION_ID            = 0x00000010,  
   PIF_ATTACHED_SESSION_NAME = 0x00000020,  
   PIF_CREATION_TIME         = 0x00000040,  
   PIF_FLAGS                 = 0x00000080,  
   PIF_ALL                   = 0x000000ff  
};  
```  
  
## <a name="members"></a>成员  
 PIF_FILE_NAME  
 初始化/使用 `bstrFileName` [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md) 结构的字段。  
  
 PIF_BASE_NAME  
 初始化/使用 `bstrBaseName` 结构的字段 `PROCESS_INFO` 。  
  
 PIF_TITLE  
 初始化/使用 `bstrTitle` 结构的字段 `PROCESS_INFO` 。  
  
 PIF_PROCESS_ID  
 初始化/使用 `ProcessId` 结构的字段 `PROCESS_INFO` 。  
  
 PIF_SESSION_ID  
 初始化/使用 `dwSessionId` 结构的字段 `PROCESS_INFO` 。  
  
 PIF_ATTACHED_SESSION_NAME  
 初始化/使用 `bstrAttachedSessionName` 结构的字段 `PROCESS_INFO` 。  
  
 PIF_CREATION_TIME  
 初始化/使用 `CreationTime` 结构的字段 `PROCESS_INFO` 。  
  
 PIF_FLAGS  
 初始化/使用 `Flags` 结构的字段 `PROCESS_INFO` 。  
  
 PIF_ALL  
 填写所有字段。  
  
## <a name="remarks"></a>备注  
 传递给 [GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md) 方法以指示要初始化 [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md) 结构的哪些字段。  
  
 还在结构的字段中用于 `Fields` `PROCESS_INFO` 指示哪些字段已使用并且有效。  
  
 这些标志可以与按位组合 `OR` 。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [计数](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
