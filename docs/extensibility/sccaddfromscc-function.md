---
title: Sccaddfromscc 功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccAddFromScc
helpviewer_keywords:
- SccAddFromScc function
ms.assetid: 902e764d-200e-46e1-8c42-4da7b037f9a0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1dd32e31330cdce958e463a40a4d92f88b09afb2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701250"
---
# <a name="sccaddfromscc-function"></a>Sccaddfromscc 功能
此功能允许用户浏览源代码管理系统中已有的文件，并随后使这些文件成为当前项目的一部分。 例如，此函数可以在不复制该文件的情况下将公共标头文件获取到当前项目中。 文件的`lplpFileNames`返回数组 包含用户要添加到 IDE 项目的文件列表。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccAddFromScc (
   LPVOID   pvContext,
   HWND     hWnd,
   LPLONG   lpnFiles,
   LPCSTR** lplpFileNames
);
```

### <a name="parameters"></a>参数
 pvContext

[在]源代码管理插件上下文结构。

 hwnd

[在]源控件插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 lpnFiles

[进出]要添加到的文件数的缓冲区。 （这是`NULL`如果指向的`lplpFileNames`内存要释放。 有关详细信息，请参阅备注。

 lplFile名称

[进出]指向所有文件名的指针数组，没有目录路径。 此数组由源代码管理插件分配和释放。 如果`lpnFiles`= `lplpFileNames` 1`NULL`和 不是 ，则指向`lplpFileNames`的数组中的第一个名称包含目标文件夹。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功找到文件并添加到项目中。|
|SCC_I_OPERATIONCANCELED|操作已取消，无效。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|

## <a name="remarks"></a>备注
 IDE 调用此函数。 如果源代码管理插件支持指定本地目标文件夹，则 IDE 将传递`lpnFiles`= 1 并将本地文件夹名称传递到`lplpFileNames`中。

 当`SccAddFromScc`对函数的调用返回时，插件已根据需要为`lpnFiles`和`lplpFileNames`分配了文件名数组的内存（请注意，此分配将替换 中的`lplpFileNames`指针。 源代码管理插件负责将所有文件放入用户的目录或指定的指定文件夹中。 然后，IDE 将文件添加到 IDE 项目中。

 最后，IDE 会第二次调用此函数，传入`NULL` `lpnFiles`。 这被解释为源代码管理插件的特殊信号，用于释放为文件名数组分配的内存。`lplpFileNames``.`

 `lplpFileNames`是指针`char ***`。 源代码管理插件放置指向指向文件名的指针数组的指针，从而以此 API 的标准方式传递列表。

> [!NOTE]
> VSSCI API 的初始版本没有提供指示所添加文件的目标项目的方法。 为了适应这种情况，参数的`lplpFIleNames`语义得到了增强，使其成为输入/输出参数，而不是输出参数。 如果只指定一个文件，即`lpnFiles`由 = 1 指向的值，则 的第`lplpFileNames`一个元素包含目标文件夹。 要使用这些新语义，IDE 将`SccSetOption`函数调用，`nOption`参数设置为`SCC_OPT_SHARESUBPROJ`。 如果源代码管理插件不支持语义，它将返回`SCC_E_OPTNOTSUPPORTED`。 这样做将禁用使用"**从源控制添加**"功能。 如果插件支持 **"从源代码管理添加**"功能 （），`SCC_CAP_ADDFROMSCC`则它必须支持新的语义并返回`SCC_I_SHARESUBPROJOK`。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [SccSetOption](../extensibility/sccsetoption-function.md)
