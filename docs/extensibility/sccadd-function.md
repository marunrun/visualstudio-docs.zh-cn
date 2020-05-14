---
title: SccAdd 功能 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701316"
---
# <a name="sccadd-function"></a>SccAdd 函数
此功能向源代码管理系统添加新文件。

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

[在]源代码管理插件上下文结构。

 hwnd

[在]源控件插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 n文件

[在]选择添加到当前项目中的文件数（如数组中给出的`lpFileNames`）。

 lpFile名称

[在]要添加的文件完全限定的本地名称的数组。

 lpComment

[在]要应用于要添加到的所有文件的注释。

 pfOptions

[在]命令标志数组，按文件提供。

 pvOptions

[在]源代码管理插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|添加操作成功。|
|SCC_E_FILEALREADYEXISTS|所选文件已在源代码管理中。|
|SCC_E_TYPENOTSUPPORTED|源代码管理系统不支持文件的类型（例如二进制文件）。|
|SCC_E_OPNOTSUPPORTED|源代码管理系统不支持此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题。 建议重试。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_NONSPECIFICERROR|非特异性故障;未执行添加。|
|SCC_I_OPERATIONCANCELED|操作在完成之前已取消。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|
|SCC_E_FILENOTEXIST|未找到本地文件。|

## <a name="remarks"></a>备注
 通常`fOptions`在此处替换为数组，`pfOptions`每个文件有一个选项`LONG`规范。 这是因为文件类型可能因文件而异。

> [!NOTE]
> 为同一文件指定和`SCC_FILETYPE_TEXT``SCC_FILETYPE_BINARY`选项是无效的，但同时指定这两个文件都无效。 设置两者与 设置`SCC_FILETYPE_AUTO`相同，在这种情况下，源代码管理插件自动检测文件类型。

 下面是`pfOptions`数组中使用的标志列表：

|选项|值|含义|
|------------|-----------|-------------|
|SCC_FILETYPE_AUTO|0x00|源代码管理插件应检测文件类型。|
|SCC_FILETYPE_TEXT|0x01|指示 ASCII 文本文件。|
|SCC_FILETYPE_BINARY|0x02|指示 ASCII 文本以外的文件类型。|
|SCC_ADD_STORELATEST|0x04|只存储文件的最新副本，没有增量。|
|SCC_FILETYPE_TEXT_ANSI|0x08|将文件视为 ANSI 文本。|
|SCC_FILETYPE_UTF8|0x10|以 UTF8 格式将文件视为 Unicode 文本。|
|SCC_FILETYPE_UTF16LE|0x20|将文件视为 UTF16 小 Endian 格式的 Unicode 文本。|
|SCC_FILETYPE_UTF16BE|0x40|将文件视为 UTF16 大 Endian 格式的 Unicode 文本。|

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
