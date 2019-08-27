---
title: SccDirQueryInfo 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccDirQueryInfo
helpviewer_keywords:
- SccDirQueryInfo function
ms.assetid: 459e2d99-573d-47c4-b834-6d82c5e14162
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7334ddd1ce6c7f9feac63253246e55b65121e18b
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432442"
---
# <a name="sccdirqueryinfo-function"></a>SccDirQueryInfo 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数将检查以了解其当前状态的完全限定目录的列表。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
SCCRTN SccDirQueryInfo(  
LPVOID  pContext,  
LONG    nDirs,  
LPCSTR* lpDirNames,  
LPLONG  lpStatus  
);  
```  
  
#### <a name="parameters"></a>参数  
 pContext  
 [in]源控制插件上下文结构。  
  
 nDirs  
 [in]选择要查询的目录数。  
  
 lpDirNames  
 [in]要查询的目录的完全限定路径的数组。  
  
 lpStatus  
 [in、 out]源代码管理插件返回的状态标志的数组结构 (请参阅[目录状态代码](../extensibility/directory-status-code-enumerator.md)有关详细信息)。  
  
## <a name="return-value"></a>返回值  
 此函数的源控制插件实现应返回以下值之一：  
  
|“值”|描述|  
|-----------|-----------------|  
|SCC_OK|查询已成功。|  
|SCC_E_OPNOTSUPPORTED|源代码控制系统不支持此操作。|  
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。 建议重试。|  
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特定故障。|  
  
## <a name="remarks"></a>备注  
 该函数将填充返回数组中的位的位掩码`SCC_DIRSTATUS`系列 (请参阅[目录状态代码](../extensibility/directory-status-code-enumerator.md))，提供每个目录的一个条目。 由调用方分配状态数组。  
  
 IDE 使用此函数之前目录已重命名，以检查是否该目录位于源控件下通过查询其是否具有相应的项目。 如果目录不受源代码管理中，IDE 可以向用户提供正确的警告。  
  
> [!NOTE]
> 如果源代码管理插件选择实现一个或多个状态的值，则未实现的位应设置为零。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)   
 [目录状态代码](../extensibility/directory-status-code-enumerator.md)
