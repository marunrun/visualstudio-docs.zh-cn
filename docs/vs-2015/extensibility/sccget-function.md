---
title: SccGet 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccGet
helpviewer_keywords:
- SccGet function
ms.assetid: 09a18bd2-b788-411a-9da6-067d806e46f6
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2a5d5065ca427f0319174aa59e6b87d356816d4c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432434"
---
# <a name="sccget-function"></a>SccGet 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数可检索一个或多个文件用于查看和编译但不能用于编辑的副本。 在大多数系统中，将文件标记为只读的。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
SCCRTN SccGet(  
   LPVOID    pvContext,  
   HWND      hWnd,  
   LONG      nFiles,  
   LPCSTR*   lpFileNames,  
   LONG      fOptions,  
   LPCMDOPTS pvOptions  
);  
```  
  
#### <a name="parameters"></a>参数  
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
  
|“值”|描述|  
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
> `SCC_GET_RECURSIVE` 应永远不会传递而无需`SCC_GET_ALL`。 另请注意，是否目录 C:\A 和 C:\A\B 传递递归 get，C:\A\B 及其所有的子目录将实际检索两次。 IDE 的负责 — 并不是源代码管理插件的 — 若要确保从数组的保持这种重复项。  
  
 最后，即使在进行源代码管理插件指定`SCC_CAP_GET_NOUI`上初始化，表示它没有 Get 命令的用户界面，在 IDE 中检索文件可能仍调用此函数的标志。 该标志只是意味着 IDE 不会显示 Get 菜单项和，该插件不需要提供任何 UI。  
  
## <a name="renaming-and-sccget"></a>重命名和 SccGet  
 情况： 用户签出文件，例如，a.txt，并对其进行修改。 A.txt 可以签入之前，第二个用户将 a.txt 重命名为 b.txt 源代码管理数据库中签出 b.txt、 使对该文件，某些修改，签入该文件。 第一个用户想要使第一个用户将其本地版本的 a.txt 文件重命名为 b.txt 并获取对该文件，第二个用户所做的更改。 但是，本地缓存，跟踪版本号仍然认为 a.txt 的第一个版本存储在本地，并且因此源代码管理无法解决的差异。  
  
 有两种方法来解决这种情况下，源控制版本的本地缓存变得与源代码管理数据库不同步：  
  
1. 不允许重命名当前已签出源代码管理数据库中的文件。  
  
2. 执行操作"删除旧"后跟"添加新"的等效项。 下面的算法是一种方法来实现此目的。  
  
    1. 调用[SccQueryChanges](../extensibility/sccquerychanges-function.md)若要了解如何重命名为 b.txt 源代码管理数据库中的 a.txt 的函数。  
  
    2. 将本地 a.txt 重命名为 b.txt。  
  
    3. 调用`SccGet`a.txt 和 b.txt 函数。  
  
    4. 源代码管理数据库中不存在 a.txt，因为本地版本缓存会清除缺失 a.txt 版本信息。  
  
    5. 正在签出的 b.txt 文件与本地 b.txt 文件的内容合并。  
  
    6. 现在可以检查更新的 b.txt 文件。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)   
 [特定命令使用的位标志](../extensibility/bitflags-used-by-specific-commands.md)
