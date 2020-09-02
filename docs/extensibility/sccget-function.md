---
title: SccGet 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGet
helpviewer_keywords:
- SccGet function
ms.assetid: 09a18bd2-b788-411a-9da6-067d806e46f6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c2d69308d2f569fc2e0d72dcf64c762687955d4d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700891"
---
# <a name="sccget-function"></a>SccGet 函数
此函数检索一个或多个文件的副本，以便进行查看和编译，但不能进行编辑。 在大多数系统中，文件被标记为只读。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccGet(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>参数
 pvContext

中源代码管理插件的上下文结构。

 hWnd

中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。

 n

中数组中指定的文件数 `lpFileNames` 。

 lpFileNames

中要检索的文件的完全限定的名称数组。

 用于

中命令标志 (`SCC_GET_ALL` ， `SCC_GET_RECURSIVE`) 。

 pvOptions

中源代码管理插件特定的选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|获取操作成功。|
|SCC_E_FILENOTCONTROLLED|此文件不受源代码管理。|
|SCC_E_OPNOTSUPPORTED|源代码管理系统不支持此操作。|
|SCC_E_FILEISCHECKEDOUT|无法获取用户当前已签出的文件。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。 建议重试。|
|SCC_E_NOSPECIFIEDVERSION|指定了无效的版本或日期/时间。|
|SCC_E_NONSPECIFICERROR|模糊失败;文件未同步。|
|SCC_I_OPERATIONCANCELED|操作在完成之前已取消。|
|SCC_E_NOTAUTHORIZED|用户无权执行此操作。|

## <a name="remarks"></a>备注
 将调用此函数，其中包含要检索的文件的计数和名称数组。 如果 IDE 传递了标志 `SCC_GET_ALL` ，这意味着中的项 `lpFileNames` 不是文件，而是目录，并且会检索给定目录中的所有受源代码管理的文件。

 `SCC_GET_ALL`标志可与 `SCC_GET_RECURSIVE` 标志结合，以检索给定目录和所有子目录中的所有文件。

> [!NOTE]
> `SCC_GET_RECURSIVE` 不应在没有的情况下传递 `SCC_GET_ALL` 。 另请注意，如果在递归 get 上传递目录 *C:\A* 和 *C:\A\B* ，则将实际检索到 *C:\A\B* 及其所有子目录。 这是 IDE 的责任（而不是源代码管理插件），以确保将此类重复项（如此项）保留在数组之外。

 最后，即使源代码管理插件在初始化时指定了 `SCC_CAP_GET_NOUI` 标志，指示它没有 Get 命令的用户界面，IDE 仍可调用此函数来检索文件。 该标志只是表示 IDE 不显示 Get 菜单项，并且该插件不应提供任何 UI。

## <a name="rename-files-and-sccget"></a>重命名文件和 SccGet
 情况：用户签出文件（例如 *a.txt*），并对其进行修改。 在签入 *a.txt* 之前，第二个用户会将 *a.txt* 重命名为在源代码管理数据库中 *b.txt* ，并签出 *b.txt*，对文件进行一些修改，并检查中的文件。 第一个用户需要第二个用户所做的更改，以便第一个用户将 *a.txt* 文件的本地版本重命名为 *b.txt* ，并对该文件执行 get 操作。 但是，跟踪版本号的本地缓存仍会认为第一个版本的 *a.txt* 存储在本地，因此源代码管理无法解决这些差异。

 可以通过两种方法来解决这种情况：源代码管理版本的本地缓存与源代码管理数据库不同步：

1. 不允许重命名当前签出的源代码管理数据库中的文件。

2. 等效于 "删除旧项"，然后执行 "添加新项"。 以下算法是实现此目的的一种方法。

    1. 调用[SccQueryChanges](../extensibility/sccquerychanges-function.md)函数可了解如何重命名源代码管理数据库中*b.txt*的*a.txt* 。

    2. 将本地 *a.txt* 重命名为 *b.txt*。

    3. `SccGet`为*a.txt*和*b.txt*调用函数。

    4. 由于源代码管理数据库中不存在 *a.txt* ，因此会清除缺少的 *a.txt* 版本信息的本地版本缓存。

    5. 要签出的 *b.txt* 文件与本地 *b.txt* 文件的内容合并。

    6. 现在可以签入更新后的 *b.txt* 文件。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [特定命令使用的 Bitflags](../extensibility/bitflags-used-by-specific-commands.md)
