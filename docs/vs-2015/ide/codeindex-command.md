---
title: CodeIndex 命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- command-line tools [Team Foundation Server]
- TFSConfig
- CodeIndex command [Team Foundation Server]
ms.assetid: b79568d4-6a64-4ca9-a1ee-3e57f92a9c5c
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 070106dc4db0f5200c1346bbbf8c0b653aa104e5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72619681"
---
# <a name="codeindex-command"></a>CodeIndex 命令
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用 **CodeIndex** 命令管理 Team Foundation Server 中的代码索引。 例如，你可能希望重置该索引以修复 CodeLens 信息，或关闭索引以调查服务器性能问题。

 **所需权限**

 若要使用 **CodeIndex** 命令，必须是“Team Foundation Administrators”  安全组的成员。 请参阅 [Team Foundation Server 权限参考](https://msdn.microsoft.com/library/39997de5-b7fb-4777-b779-07de0543abe6)。

> [!NOTE]
> 即使你使用管理凭据进行登录，也必须使用提升权限打开命令提示符窗口以运行此命令。 你还必须从 Team Foundation 的应用层运行此命令。

## <a name="syntax"></a>语法

```
TFSConfig CodeIndex /indexingStatus | /setIndexing:[ on | off | keepupOnly ] | /ignoreList:[ add | remove | removeAll | view ] ServerPath | /listLargeFiles [/fileCount:FileCount] [/minSize:MinSize] | /reindexAll | /destroyCodeIndex [/noPrompt] | /temporaryDataSizeLimit:[ view | <SizeInGBs> | disable ] | /indexHistoryPeriod:[ view | all | <NumberOfMonths> ] [/collectionName:CollectionName | /collectionId:CollectionId]
```

#### <a name="parameters"></a>参数

|**参数**|**说明**|
|------------------|---------------------|
|`CollectionName`|指定团队项目集合的名称。 如果名称包含空格，则用引号将该名称引起来，例如“Fabrikam 网站”。|
|`CollectionId`|指定团队项目集合的标识号。|
|`ServerPath`|指定代码文件的路径。|

|**选项**|**说明**|
|----------------|---------------------|
|**/indexingStatus**|显示代码索引服务的状态和配置。|
|**/setIndexing:** [ on &#124; off &#124; keepupOnly ]|-   **on**：开始为所有变更集创建索引。<br />-   **off**：停止为所有变更集创建索引。<br />-   **keepupOnly**：停止为之前创建的变更集创建索引，开始仅为新的变更集创建索引。|
|**/ignoreList:** [ add &#124; remove &#124; removeAll &#124; view ] `ServerPath`<br /><br /> 可以在服务器路径的开头、末尾或两端使用通配符 (*)。|指定你不希望编制索引的代码文件的列表及其路径。<br /><br /> -   **add**：将不希望编制索引的文件添加到已忽略文件列表。<br />-   **remove**：从已忽略文件列表中移除希望编制索引的文件。<br />-   **removeAll**：清理忽略的文件列表，并开始为所有文件创建索引。<br />-   **view**：查看所有不要编制索引的文件。|
|**/listLargeFiles [/fileCount:** `FileCount` **/minSize:** `MinSize`]|显示超出指定大小（以 KB 为单位）的文件的指定数量。 然后可使用 **/ignoreList** 选项从编制索引中排除这些文件。|
|**/reindexAll**|清理以前的索引数据并重新开始创建索引。|
|**/destroyCodeIndex [/noPrompt]**|删除代码索引并移除所有索引的数据。 如果使用 **/noPrompt** 选项，则无需确认。|
|**/temporaryDataSizeLimit**:[ view &#124; <`SizeInGBs`> &#124; disable ]|控制处理变更集时 CodeLens 创建的临时数据量。 默认限制为 2 GB。<br /><br /> -   **view**：显示当前大小限制。<br />-   `SizeInGBs`：更改大小限制。<br />-   **disable**：删除大小限制。<br /><br /> 在检查过该限制后，CodeLens 才处理新的变更集。 如果临时数据超出此限制，CodeLens 将暂停处理过去的变更集，而不是新的变更集。 数据清理完毕并减少到此限制以下时，CodeLens 将重新开始处理。 清理会在每天自动运行一次。 这意味着临时数据可能超出此限制，直到清理开始运行。|
|**/indexHistoryPeriod**:[ view &#124; all &#124; <`NumberOfMonths`> ]|控制对更改历史记录编制索引的时间长度。 这会影响 CodeLens 向你显示的历史记录量。 默认限值为 12 个月。 这表示 CodeLens 仅显示过去 12 个月的更改历史记录。<br /><br /> -   **view**：显示当前月数。<br />-   **all**：对所有更改历史记录编制索引。<br />-   `NumberOfMonths`：更改用于对更改历史记录编制索引的月数。|
|**/collectionName:** `CollectionName`|指定运行 **CodeIndex** 命令的团队项目集合的名称。 如果不使用 **/CollectionId**，则为必需。|
|**/collectionId:** `CollectionId`|指定运行 **CodeIndex** 命令的团队项目集合的标识号。 如果不使用 **/CollectionName**，则为必需。|

## <a name="examples"></a>示例

> [!NOTE]
> 此处描述的示例公司、组织、产品、域名、电子邮件地址、徽标、人员、地点和事件均属虚构。  无意与任何真实的公司、组织、产品、域名、电子邮件地址、徽标、人物、地点或事件相关联，也不应进行这方面的推断。

 查看代码索引状态和配置：

```
TFSConfig CodeIndex /indexingStatus /collectionName:"Fabrikam Web Site"
```

 开始为所有变更集创建索引：

```
TFSConfig CodeIndex /setIndexing:on /collectionName:"Fabrikam Web Site"
```

 停止为之前创建的变更集创建索引，开始仅为新的变更集创建索引：

```
TFSConfig CodeIndex /setIndexing:keepupOnly /collectionName:"Fabrikam Web Site"
```

 查找最多 50 个大于 10 KB 的文件：

```
TFSConfig CodeIndex /listLargeFiles /fileCount:50 /minSize:10 /collectionName:"Fabrikam Web Site"
```

 从索引中排除特定的文件并将其添加到忽略的文件列表中：

```
TFSConfig CodeIndex /ignoreList:add "$/Fabrikam Web Site/Catalog.cs" /collectionName:"Fabrikam Web Site"
```

 查看所有未编制索引的文件：

```
TFSConfig CodeIndex /ignoreList:view
```

 清理以前的索引数据并重新开始创建索引：

```
TFSConfig CodeIndex /reindexAll /collectionName:"Fabrikam Web Site"
```

 若要保存所有变更集历史记录：

```
TFSConfig CodeIndex /indexHistoryPeriod:all /collectionName:"Fabrikam Web Site"
```

 若要删除对 CodeLens 临时数据的大小限制并不管临时数据大小继续索引：

```
TFSConfig CodeIndex /temporaryDataSizeLimit:disable /collectionName:"Fabrikam Web Site"
```

 删除代码索引并进行确认：

```
TFSConfig CodeIndex /destroyCodeIndex /collectionName:"Fabrikam Web Site"
```

## <a name="see-also"></a>另请参阅
 通过[适用于 TFS 的 TFSConfig 命令行工具](https://msdn.microsoft.com/be8c997a-b97b-4e59-97f5-04db0a601a6c)[管理服务器配置](https://msdn.microsoft.com/94424190-3b6b-4f33-a6b6-5807f4225b62)
