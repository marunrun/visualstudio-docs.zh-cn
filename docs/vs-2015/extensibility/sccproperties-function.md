---
title: SccProperties 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccProperties
helpviewer_keywords:
- SccProperties function
ms.assetid: 1bed38c9-73d2-4474-9717-f9dc26a89cbe
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f4e8452465873cb66883abd347406d17b469e90a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68199999"
---
# <a name="sccproperties-function"></a>SccProperties 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数显示文件或项目的源代码管理属性。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
SCCRTN SccProperties (  
   LPVOID pvContext,  
   HWND   hWnd,  
   LPCSTR lpFileName  
);  
```  
  
#### <a name="parameters"></a>参数  
 pvContext  
 中源代码管理插件上下文结构。  
  
 hWnd  
 中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。  
  
 lpFileName  
 中文件或项目的完全限定的路径名称。  
  
## <a name="return-value"></a>返回值  
 此函数的源代码管理插件实现应返回以下值之一：  
  
|值|说明|  
|-----------|-----------------|  
|SCC_OK|已成功显示属性。|  
|SCC_I_RELOADFILE|版本控制系统已修改文件属性，因此 IDE 应重新加载此文件。|  
|SCC_E_PROJNOTOPEN|未在源代码管理中打开指定的项目。|  
|SCC_E_NOTAUTHORIZED|用户无权查看此文件或项目的属性。|  
|SCC_E_FILENOTCONTROLLED|指定的文件或项目不受源代码管理。|  
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|出现未知错误或常规错误。|  
  
## <a name="remarks"></a>备注  
 源代码管理插件将属性显示在其自己的对话框中。  
  
 这些属性由源代码管理插件定义，并且可能不同于插件。 如果插件允许用户更改文件的源代码管理属性，则它应返回 `SCC_I_RELOAD` 通知 IDE 需要重新加载此文件或项目。  
  
## <a name="see-also"></a>另请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
