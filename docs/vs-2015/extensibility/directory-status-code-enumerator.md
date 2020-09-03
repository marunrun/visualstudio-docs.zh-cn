---
title: 目录状态代码枚举器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- directory status code enumerator
- source control plug-ins, directory status enumeration
ms.assetid: 616026b5-f529-40ef-90c1-1836e116d797
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e082a691a389d5cb9a8fa307a627b11911e0db78
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68185251"
---
# <a name="directory-status-code-enumerator"></a>目录状态代码枚举器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`SccDirStatus`枚举器包含指定源代码管理系统中目录状态的命名常量值。 此枚举由 [SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)使用。 源代码管理插件 API 版本1.2 中引入了此项。  
  
## <a name="syntax"></a>语法  
  
```  
enum SccDirStatus {  
   SCC_DIRSTATUS_INVALID       = -1L,  
   SCC_DIRSTATUS_NOTCONTROLLED = 0x0000L,  
   SCC_DIRSTATUS_CONTROLLED    = 0x0001L,  
   SCC_DIRSTATUS_EMPTYPROJ     = 0x0002L  
};  
```  
  
## <a name="members"></a>成员  
 SCC_DIRSTATUS_INVALID  
 无法获取状态;不要依赖于它。  
  
 SCC_DIRSTATUS_NOTCONTROLLED  
 目录不受源代码管理。  
  
 SCC_DIRSTATUS_CONTROLLED  
 目录受源代码管理。  
  
 SCC_DIRSTATUS_EMPTYPROJ  
 与此目录相对应的项目为空。  
  
## <a name="see-also"></a>另请参阅  
 [源代码管理插件](../extensibility/source-control-plug-ins.md)   
 [SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)
