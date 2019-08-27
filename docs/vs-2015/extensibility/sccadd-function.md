---
title: SccAdd 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccAdd
helpviewer_keywords:
- SccAdd function
ms.assetid: 545268f3-8e83-446a-a398-1a9db9e866e8
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: daac15bbb7829d510db17ba02057a2dc86c55990
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432512"
---
# <a name="sccadd-function"></a>SccAdd 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数将新文件添加到源代码管理系统。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
SCCRTN SccAdd(  
   LPVOID    pvContext,  
   HWND      hWnd,  
   LONG      nFiles,  
   LPCSTR*   lpFileNames,  
   LPCSTR    lpComment,  
   LONG*     pfOptions,  
   LPCMDOPTS pvOptions  
);  
```  
  
#### <a name="parameters"></a>参数  
 pvContext  
 [in]源控制插件上下文结构。  
  
 hWnd  
 [in]它提供了任何对话框，父级可以使用源代码管理插件，则 IDE 窗口的句柄。  
  
 nFiles  
 [in]选择要添加到当前项目中给出的文件数`lpFileNames`数组。  
  
 lpFileNames  
 [in]要添加的文件的完全限定的本地名称的数组。  
  
 lpComment  
 [in]要应用于所有要添加的文件的注释。  
  
 pfOptions  
 [in]命令标志，在每个文件的基础上提供的数组。  
  
 pvOptions  
 [in]源代码管理插件特定选项。  
  
## <a name="return-value"></a>返回值  
 此函数的源控制插件实现应返回以下值之一：  
  
|“值”|描述|  
|-----------|-----------------|  
|SCC_OK|添加操作已成功。|  
|SCC_E_FILEALREADYEXISTS|所选的文件已在源代码管理下。|  
|SCC_E_TYPENOTSUPPORTED|（例如二进制） 文件的类型不受源代码管理系统。|  
|SCC_E_OPNOTSUPPORTED|源代码管理系统不支持此操作。|  
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。 建议重试。|  
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|  
|SCC_E_NONSPECIFICERROR|非特定故障;添加不执行。|  
|SCC_I_OPERATIONCANCELED|在完成之前已取消操作。|  
|SCC_I_RELOADFILE|需要重新加载文件或项目。|  
|SCC_E_FILENOTEXIST|找不到本地文件。|  
  
## <a name="remarks"></a>备注  
 常用`fOptions`由一个数组，此处替换`pfOptions`，其中一个`LONG`选项每个文件规范。 这是因为文件类型可能会有所不同文件文件。  
  
> [!NOTE]
> 它是无效的同时指定`SCC_FILETYPE_TEXT`和`SCC_FILETYPE_BINARY`是未指定有效的同一文件中，但它的选项。 设置既不是设置相同`SCC_FILETYPE_AUTO`，在这种情况下进行源代码管理插件自动检测文件类型。  
  
 下面是列表中使用标志`pfOptions`数组：  
  
|选项|“值”|含义|  
|------------|-----------|-------------|  
|SCC_FILETYPE_AUTO|0x00|源代码管理插件应检测到的文件类型。|  
|SCC_FILETYPE_TEXT|0x01|指示一个 ASCII 文本文件。|  
|SCC_FILETYPE_BINARY|0x02|指示之外 ASCII 文本的文件类型。|  
|SCC_ADD_STORELATEST|0x04|存储仅该文件，没有增量数据的最新副本。|  
|SCC_FILETYPE_TEXT_ANSI|0x08|将该文件视为 ANSI 文本。|  
|SCC_FILETYPE_UTF8|0x10|将该文件视为 UTF8 格式的 Unicode 文本。|  
|SCC_FILETYPE_UTF16LE|0x20|将该文件视为 Unicode 文本中 UTF16 Little Endian 格式。|  
|SCC_FILETYPE_UTF16BE|0x40|将作为 Unicode 文本 UTF16 Big Endian 文件格式。|  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
