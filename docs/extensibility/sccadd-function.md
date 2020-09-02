---
title: SccAdd 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccAdd
helpviewer_keywords:
- SccAdd function
ms.assetid: 545268f3-8e83-446a-a398-1a9db9e866e8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 23a6226b0d3cc2441a509c16b2e4672a766f3329
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80701316"
---
# <a name="sccadd-function"></a>SccAdd 函数
此函数将新文件添加到源代码管理系统。

## <a name="syntax"></a>语法

```cpp
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

### <a name="parameters"></a>参数
 pvContext

中源代码管理插件上下文结构。

 hWnd

中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。

 n

中选定要添加到当前项目中的、在数组中所指定的文件数 `lpFileNames` 。

 lpFileNames

中要添加的文件的完全限定本地名称数组。

 lpComment

中要应用到要添加的所有文件的注释。

 pfOptions

中命令标志的数组，在每个文件的基础上提供。

 pvOptions

中源代码管理插件特定的选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|添加操作成功。|
|SCC_E_FILEALREADYEXISTS|所选文件已受源代码管理。|
|SCC_E_TYPENOTSUPPORTED|文件类型 (例如，二进制) 不受源代码管理系统支持。|
|SCC_E_OPNOTSUPPORTED|源代码管理系统不支持此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。 建议重试。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_NONSPECIFICERROR|模糊失败;添加未执行。|
|SCC_I_OPERATIONCANCELED|操作在完成前被取消。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|
|SCC_E_FILENOTEXIST|找不到本地文件。|

## <a name="remarks"></a>备注
 在此，通常会将其 `fOptions` 替换为 `pfOptions` 一个数组， `LONG` 每个文件有一个选项规范。 这是因为文件类型在文件中可能会有所不同。

> [!NOTE]
> 为 `SCC_FILETYPE_TEXT` 同一个文件同时指定和选项是无效的 `SCC_FILETYPE_BINARY` ，但同时指定两者都是有效的。 设置都不与设置相同 `SCC_FILETYPE_AUTO` ，在这种情况下，源代码管理插件自动检测 dll 文件类型。

 下面是数组中使用的标志列表 `pfOptions` ：

|选项|值|含义|
|------------|-----------|-------------|
|SCC_FILETYPE_AUTO|0x00|源代码管理插件应检测文件类型。|
|SCC_FILETYPE_TEXT|0x01|指示 ASCII 文本文件。|
|SCC_FILETYPE_BINARY|0x02|指示 ASCII 文本以外的文件类型。|
|SCC_ADD_STORELATEST|0x04|仅存储文件的最新副本，无增量。|
|SCC_FILETYPE_TEXT_ANSI|0x08|将文件视为 ANSI 文本。|
|SCC_FILETYPE_UTF8|0x10|以 UTF8 格式将文件视为 Unicode 文本。|
|SCC_FILETYPE_UTF16LE|0x20|以 UTF16 小 Endian 格式将文件视为 Unicode 文本。|
|SCC_FILETYPE_UTF16BE|0x40|将文件视为 UTF16 大 Endian 格式的 Unicode 文本。|

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
