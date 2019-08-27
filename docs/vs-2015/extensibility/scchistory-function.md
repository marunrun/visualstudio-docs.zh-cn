---
title: SccHistory 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccHistory
helpviewer_keywords:
- SccHistory function
ms.assetid: a636d9d3-47c1-4b48-ac6b-bcfde19d6cf9
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8df85c03201e46768c43fb64cc41b7fa081eb91a
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63446829"
---
# <a name="scchistory-function"></a>SccHistory 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数可显示指定的文件的历史记录。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
SCCRTN SccHistory(  
   LPVOID    pvContext,  
   HWND      hWnd,  
   LONG      nFiles,  
   LPCSTR*   lpFileNames,  
   LONG      fOptions,  
   LPCMDOPTS pvOptions  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pvContext`  
 [in]源控制插件上下文结构。  
  
 `hWnd`  
 [in]它提供了任何对话框，父级可以使用源代码管理插件，则 IDE 窗口的句柄。  
  
 `nFiles`  
 [in]中指定的文件数`lpFileName`数组。  
  
 `lpFileName`  
 [in]文件的完全限定名称的数组。  
  
 `fOptions`  
 [in]（目前未使用） 的命令标志。  
  
 `pvOptions`  
 [in]源代码管理插件特定选项。  
  
## <a name="return-value"></a>返回值  
 此函数的源控制插件实现应返回以下值之一：  
  
|“值”|描述|  
|-----------|-----------------|  
|SCC_OK|成功地获取版本历史记录。|  
|SCC_I_RELOADFILE|源代码管理系统实际上在情况下修改磁盘上的文件提取历史记录 （例如，通过获取的旧版本），因此 IDE 应重新加载此文件。|  
|SCC_E_FILENOTCONTROLLED|文件不是源代码管理下。|  
|SCC_E_OPNOTSUPPORTED|源代码管理系统不支持此操作。|  
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|  
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。 建议重试。|  
|SCC_E_PROJNOTOPEN|项目未打开。|  
|SCC_E_NONSPECIFICERROR|非特定故障。 无法获取文件历史记录。|  
  
## <a name="remarks"></a>备注  
 源代码管理插件可以显示其自己的对话框来显示每个文件的历史记录使用`hWnd`作为父窗口。 或者，可选的文本输出回调函数提供给[SccOpenProject](../extensibility/sccopenproject-function.md)可以使用，如果它受支持。  
  
 请注意，在某些情况下，此调用的执行期间可能会更改要检查的文件。 例如， [!INCLUDE[vsvss](../includes/vsvss-md.md)] history 命令使用户有机会以获取文件的旧版本。 在这种情况下，源代码管理插件返回`SCC_I_RELOAD`来警告 IDE，它需要重新加载该文件。  
  
> [!NOTE]
> 如果源代码管理插件不支持此函数的文件的数组，可以显示仅的第一个文件文件历史记录。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)   
 [SccOpenProject](../extensibility/sccopenproject-function.md)
