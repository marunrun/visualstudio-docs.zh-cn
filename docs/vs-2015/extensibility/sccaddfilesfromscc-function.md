---
title: SccAddFilesFromSCC 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccAddFilesFromSCC
helpviewer_keywords:
- SccAddFilesFromSCC function
ms.assetid: f21a3500-ade8-4dd8-8647-10e2179be9c1
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d5af748c9180644cae928d1b6db3a3f880b6b286
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200908"
---
# <a name="sccaddfilesfromscc-function"></a>SccAddFilesFromSCC 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数将从源代码管理的文件的列表添加到当前打开的项目。  
  
## <a name="syntax"></a>语法  
  
```cpp  
SCCRTN SccAddFilesFromSCC(  
   LPVOID  pContext,  
   HWND    hWnd,  
   LPSTR   lpUser,  
   LPSTR   lpAuxProjPath,  
   LONG    cFiles,  
   LPCSTR* lpFilePaths,  
   LPCSTR  lpDestination,  
   LPCSTR  lpComment,  
   LPBOOL  pbResults  
);  
```  
  
#### <a name="parameters"></a>参数  
 pContext  
 [in]源控件插件上下文指针。  
  
 hWnd  
 [in]它提供了任何对话框，父级可以使用源代码管理插件，则 IDE 窗口的句柄。  
  
 lpUser  
 [in、 out]（最多 SCC_USER_SIZE，包括 null 终止符) 用户名。  
  
 lpAuxProjPath  
 [in、 out]标识项目的辅助字符串 (最多`SCC_PRJPATH_`大小，包括 null 终止符)。  
  
 cFiles  
 [in]通过给定的文件数`lpFilePaths`。  
  
 lpFilePaths  
 [in、 out]要添加到当前项目的文件名的数组。  
  
 lpDestination  
 [in]目标路径文件的要写入的位置。  
  
 lpComment  
 [in]要应用于每个要添加的文件的注释。  
  
 pbResults  
 [in、 out]不设置为指示 （非零值或 TRUE） 的成功或失败的标志的数组 （0 或 FALSE） 的每个文件 (数组的大小必须至少为`cFiles`长)。  
  
## <a name="return-value"></a>返回值  
 此函数的源控制插件实现应返回以下值之一：  
  
|值|描述|  
|-----------|-----------------|  
|SCC_E_PROJNOTOPEN|项目未打开。|  
|SCC_E_OPNOTPERFORMED|连接到与指定的相同的项目不是 `lpAuxProjPath.`|  
|SCC_E_NOTAUTHORIZED|未授权用户来更新数据库。|  
|SCC_E_NONSPECIFICERROR|未知的错误。|  
|SCC_I_RELOADFILE|需要重新加载文件或项目。|  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
