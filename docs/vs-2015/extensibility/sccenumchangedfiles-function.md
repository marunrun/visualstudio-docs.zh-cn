---
title: SccEnumChangedFiles 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccEnumChangedFiles
helpviewer_keywords:
- SccEnumChangedFiles function
ms.assetid: 76cac510-107b-4c1a-ba60-9c39b6db2e71
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 00ef98c93f02aa8e8a1b4ea53f1998d0ab6713a9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200130"
---
# <a name="sccenumchangedfiles-function"></a>SccEnumChangedFiles 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

给定一个本地文件列表，此函数确定哪些文件与源代码管理数据库中对应的版本不同。  
  
## <a name="syntax"></a>语法  
  
```cpp  
SCCRTN SccEnumChangedFiles(  
   LPVOID  pContext,  
   HWND    hWnd,  
   LONG    cFiles,  
   LPCSTR* lpFileNames,  
   LONG*   plIsFileDifferent  
);  
```  
  
#### <a name="parameters"></a>参数  
 pContext  
 中源代码管理插件上下文指针。  
  
 hWnd  
 中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。  
  
 cFiles  
 中数组中指定的文件名 `lpFileNames` 。 还指定数组的大小 `plIsFileDifferent` 。  
  
 lpFileNames  
 中要检查的本地文件名的数组。  
  
 plIsFileDifferent  
 [in，out]值的数组，这些值指示每个文件 (数组的差异状态必须至少具有 `cFiles`) 条目。 非零表示文件不同。  
  
## <a name="return-value"></a>返回值  
 此函数的源代码管理插件实现应返回以下值之一：  
  
|值|说明|  
|-----------|-----------------|  
|SCC_OK|操作已成功完成。|  
|SCC_UNSPECIFIEDERROR|常规错误。|  
  
## <a name="see-also"></a>另请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
