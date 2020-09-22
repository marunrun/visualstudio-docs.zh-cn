---
title: SccAddFromScc 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccAddFromScc
helpviewer_keywords:
- SccAddFromScc function
ms.assetid: 902e764d-200e-46e1-8c42-4da7b037f9a0
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ccf3a25bda14cf98fdba4a58b0032444badc4c4a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840652"
---
# <a name="sccaddfromscc-function"></a>SccAddFromScc 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数允许用户浏览源控制系统中已存在的文件，并随后使这些文件成为当前项目的一部分。 例如，此函数可以在当前项目中获取公共标头文件，而不会复制该文件。 文件的返回数组 `lplpFileNames` 包含用户要添加到 IDE 项目中的文件的列表。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
SCCRTN SccAddFromScc (  
   LPVOID   pvContext,  
   HWND     hWnd,  
   LPLONG   lpnFiles,  
   LPCSTR** lplpFileNames  
);  
```  
  
#### <a name="parameters"></a>parameters  
 pvContext  
 中源代码管理插件上下文结构。  
  
 hWnd  
 中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。  
  
 lpnFiles  
 [in，out]要添加到中的文件数的缓冲区。  (`NULL` 如果要释放由指向的内存，则为 `lplpFileNames` 。 有关详细信息，请参阅备注。 )   
  
 lplpFileNames  
 [in，out]指向所有文件名称（不包含目录路径）的指针的数组。 此数组由源代码管理插件分配并释放。 如果 `lpnFiles` = 1 且 `lplpFileNames` 不为 `NULL` ，则由指向的数组中的第一个名称 `lplpFileNames` 包含目标文件夹。  
  
## <a name="return-value"></a>返回值  
 此函数的源代码管理插件实现应返回以下值之一：  
  
|值|说明|  
|-----------|-----------------|  
|SCC_OK|已成功找到并添加到项目中的文件。|  
|SCC_I_OPERATIONCANCELED|操作已取消，不起作用。|  
|SCC_I_RELOADFILE|需要重新加载文件或项目。|  
  
## <a name="remarks"></a>备注  
 IDE 调用此函数。 如果源代码管理插件支持指定本地目标文件夹，则 IDE 将传递 `lpnFiles` = 1 并将本地文件夹名称传递到中 `lplpFileNames` 。  
  
 当对函数的调用 `SccAddFromScc` 返回时，插件已将值分配给 `lpnFiles` 和，并 `lplpFileNames` 根据需要为文件名数组分配内存 (请注意，此分配将替换) 中的指针 `lplpFileNames` 。 源代码管理插件负责将所有文件放入用户的目录或指定的指定文件夹中。 然后，IDE 会将文件添加到 IDE 项目。  
  
 最后，IDE 将再次调用此函数，同时 `NULL` 为传入 `lpnFiles` 。 源代码管理插件将此方法解释为特殊信号，以释放为中的文件名称数组分配的内存。 `lplpFileNames``.`  
  
 `lplpFileNames` 为 `char ***` 指针。 源代码管理插件将指针放在指向文件名称的指针数组的后面，从而以标准方式为此 API 传递列表。  
  
> [!NOTE]
> VSSCI API 的初始版本未提供一种方法来指示所添加文件的目标项目。 为了满足这一问题， `lplpFIleNames` 已增强参数的语义，使其成为输入参数和输出参数，而不是输出参数。 如果只指定了一个文件（即，指向的值 `lpnFiles` = 1），则的第一个元素 `lplpFileNames` 包含目标文件夹。 若要使用这些新语义，IDE 将调用 `SccSetOption` 函数，并将 `nOption` 参数设置为 `SCC_OPT_SHARESUBPROJ` 。 如果源代码管理插件不支持语义，则返回 `SCC_E_OPTNOTSUPPORTED` 。 这样做会禁止使用 " **从源代码管理添加** " 功能。 如果插件支持 " **从源代码管理添加** " 功能 (`SCC_CAP_ADDFROMSCC`) ，则它必须支持新的语义并返回 `SCC_I_SHARESUBPROJOK` 。  
  
## <a name="see-also"></a>另请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)   
 [SccSetOption](../extensibility/sccsetoption-function.md)
