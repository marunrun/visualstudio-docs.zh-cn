---
title: m_stateObject 字段 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- m_stateObject field, Task class [.NET Framework debug engines]
ms.assetid: 68c54b22-3e1c-4031-b9c7-b972c519d8a0
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8e9cfc6f689504bef2a8366f90282641d1e9e105
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68149042"
---
# <a name="mstateobject-field"></a>m_stateObject 字段
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

一个对象，表示该操作将使用的数据。  
  
 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **程序集：** mscorlib （在 mscorlib.dll 中)  
  
 无法从.NET Framework 来访问此内部成员，因为以下语法提供通用中间语言 (CIL)。  
  
## <a name="syntax"></a>语法  
  
```  
.field assembly object m_stateObject  
```  
  
## <a name="remarks"></a>备注  
 这是`state`中的参数<xref:System.Threading.Tasks.Task.%23ctor%2A>构造函数。 它也是为支持字段<xref:System.Threading.Tasks.Task.AsyncState%2A?displayProperty=fullName>属性。  
  
## <a name="see-also"></a>请参阅  
 [Task 类](../../extensibility/debugger/task-class-internal-members.md)
