---
title: SccRemove 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccRemove
helpviewer_keywords:
- SccRemove function
ms.assetid: 20830fdc-c0e9-4a5f-bf60-33f28874442f
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 62974f585fe164c7ccf7ea21a19d22939d806d73
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68199973"
---
# <a name="sccremove-function"></a>SccRemove 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数从源代码管理系统中删除文件。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
SCCRTN SccRemove(  
   LPVOID    pvContext,  
   HWND      hWnd,  
   LONG      nFiles,  
   LPCSTR*   lpFileNames,  
   LPCSTR    lpComment,  
   LONG      fOptions,  
   LPCMDOPTS pvOptions  
);  
```  
  
#### <a name="parameters"></a>参数  
 pvContext  
 [in]源控制插件上下文结构。  
  
 hWnd  
 [in]它提供了任何对话框，父级可以使用源代码管理插件，则 IDE 窗口的句柄。  
  
 nFiles  
 [in]中指定的文件数`lpFileNames`数组。  
  
 lpFileNames  
 [in]要删除的文件的完全限定的本地路径名称的数组。  
  
 lpComment  
 [in]要应用于每个文件被删除的注释。  
  
 fOptions  
 [in]命令标志 （未使用）。  
  
 pvOptions  
 [in]源代码管理插件特定选项。  
  
## <a name="return-value"></a>返回值  
 此函数的源控制插件实现应返回以下值之一：  
  
|值|描述|  
|-----------|-----------------|  
|SCC_OK|删除成功。|  
|SCC_E_FILENOTCONTROLLED|所选的文件不受源代码管理中。|  
|SCC_E_OPNOTSUPPORTED|源代码管理系统不支持此操作。|  
|SCC_E_ISCHECKEDOUT|无法删除文件，因为用户当前已将其签。|  
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。|  
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|  
|SCC_E_NONSPECIFICERROR|非特定故障;不删除文件。|  
|SCC_I_OPERATIONCANCELED|在完成之前已取消操作。|  
  
## <a name="remarks"></a>备注  
 此函数从源代码管理系统中删除文件，但不会从用户的本地硬盘删除它们。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
