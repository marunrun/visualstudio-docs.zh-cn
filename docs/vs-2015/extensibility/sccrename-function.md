---
title: SccRename 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccRename
helpviewer_keywords:
- SccRename function
ms.assetid: b467ade6-a1db-4c0b-b60f-7850ec4f79eb
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e78975acab0bf30f1f188cdd7b6454fd6e74ce6f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68143722"
---
# <a name="sccrename-function"></a>SccRename 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数重命名源代码管理系统中的文件。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
SCCRTN SccRename(  
   LPVOID pvContext,  
   HWND   hWnd,  
   LPCSTR lpFileName,  
   LPCSTR lpNewName  
);  
```  
  
#### <a name="parameters"></a>参数  
 pvContext  
 [in]源控制插件上下文结构。  
  
 hWnd  
 [in]它提供了任何对话框，父级可以使用源代码管理插件，则 IDE 窗口的句柄。  
  
 lpFileName  
 [in]要重命名该文件的完全限定的文件名。  
  
 lpNewName  
 [in]完全限定的新名称。 如果不同的目录路径，然后在文件已从一个子目录到另一个。  
  
## <a name="return-value"></a>返回值  
 此函数的源控制插件实现应返回以下值之一：  
  
|值|描述|  
|-----------|-----------------|  
|SCC_OK|重命名操作已成功完成。|  
|SCC_E_PROJNOTOPEN|不受源代码管理打开项目时。|  
|SCC_E_FILENOTCONTROLLED|文件不是源代码管理下。|  
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。|  
|SCC_E_NOTAUTHORIZED|未授权用户来完成此操作。|  
|SCC_E_COULDNOTCREATEPROJECT|重命名过程的一部分，无法创建项目。|  
|SCC_E_OPNOTPERFORMED|不执行此操作。|  
|SCC_E_NONSPECIFICERROR|未指定或常规时出错。|  
  
## <a name="remarks"></a>备注  
 此函数可用于重命名文件或它从一个位置移动到另一个源代码管理系统中。 源代码管理插件不应尝试访问磁盘上的文件。 它负责 IDE 的本地文件重命名。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
