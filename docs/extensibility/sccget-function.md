---
title: SccGet 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGet
helpviewer_keywords:
- SccGet function
ms.assetid: 09a18bd2-b788-411a-9da6-067d806e46f6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4ad087af24723c6ccbf901280c7db748e2af461a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66332128"
---
# <a name="sccget-function"></a>SccGet 函数
此函数可检索一个或多个文件用于查看和编译但不能用于编辑的副本。 在大多数系统中，将文件标记为只读的。

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

[in]源代码管理插件上下文结构。

 hWnd

[in]它提供了任何对话框，父级可以使用源代码管理插件，则 IDE 窗口的句柄。

 nFiles

[in]中指定的文件数`lpFileNames`数组。

 lpFileNames

[in]要检索的文件的完全限定名称的数组。

 fOptions

[in]命令标志 (`SCC_GET_ALL`， `SCC_GET_RECURSIVE`)。

 pvOptions

[in]源代码管理插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源控制插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|获取操作的成功。|
|SCC_E_FILENOTCONTROLLED|文件不是源代码管理下。|
|SCC_E_OPNOTSUPPORTED|源代码管理系统不支持此操作。|
|SCC_E_FILEISCHECKEDOUT|无法获取当前用户已签出文件。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。 建议重试。|
|SCC_E_NOSPECIFIEDVERSION|指定的版本无效或日期/时间。|
|SCC_E_NONSPECIFICERROR|非特定故障;未同步文件。|
|SCC_I_OPERATIONCANCELED|在完成之前取消操作。|
|SCC_E_NOTAUTHORIZED|用户无权执行此操作。|

## <a name="remarks"></a>备注
 此函数调用计数、 要检索的文件的名称的数组。 如果 IDE 将标志传递`SCC_GET_ALL`，这意味着，中的项`lpFileNames`不是文件而是目录，并在给定目录中的源代码管理下的所有文件都都要检索。

 `SCC_GET_ALL`可以结合标志`SCC_GET_RECURSIVE`标志，用于检索在给定目录中的所有文件和所有子目录。

> [!NOTE]
> `SCC_GET_RECURSIVE` 应永远不会传递而无需`SCC_GET_ALL`。 此外，请注意，如果目录*C:\A*和*C:\A\B*两者上递归 get，传递*C:\A\B*和实际上将两次检索所有的子目录。 IDE 的负责 — 并不是源代码管理插件的 — 若要确保从数组的保持这种重复项。

 最后，即使在进行源代码管理插件指定`SCC_CAP_GET_NOUI`上初始化，表示它没有 Get 命令的用户界面，在 IDE 中检索文件可能仍调用此函数的标志。 该标志只是意味着 IDE 不会显示 Get 菜单项和，该插件不需要提供任何 UI。

## <a name="rename-files-and-sccget"></a>重命名文件和 SccGet
 情况： 在用户签出文件，例如， *a.txt*，并对其进行修改。 之前*a.txt*可以在第二个用户将重命名在中，选中*a.txt*到*b.txt*源代码管理数据库中签出*b.txt*，使某些修改文件，并检查该文件。 第一个用户想要使第一个用户将重命名他们的本地版本，第二个用户所做的更改*a.txt*的文件*b.txt*并获取对该文件。 但是，本地缓存，跟踪版本号仍然认为的第一个版本*a.txt*存储在本地，因此源代码管理无法解析的差异。

 有两种方法来解决这种情况下，源控制版本的本地缓存变得与源代码管理数据库不同步：

1. 不允许重命名当前已签出源代码管理数据库中的文件。

2. 执行操作"删除旧"后跟"添加新"的等效项。 下面的算法是一种方法来实现此目的。

    1. 调用[SccQueryChanges](../extensibility/sccquerychanges-function.md)函数，若要了解有关的重命名*a.txt*到*b.txt*源代码管理数据库中。

    2. 重命名本地*a.txt*到*b.txt*。

    3. 调用`SccGet`两个函数*a.txt*并*b.txt*。

    4. 因为*a.txt*不存在在源代码管理数据库中的本地版本缓存会清除缺失*a.txt*版本信息。

    5. *B.txt*签出文件合并在一起的本地内容*b.txt*文件。

    6. 已更新*b.txt*现在签入的文件。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [使用特定命令的位标志](../extensibility/bitflags-used-by-specific-commands.md)
