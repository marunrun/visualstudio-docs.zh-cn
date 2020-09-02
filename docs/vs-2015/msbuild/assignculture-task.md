---
title: AssignCulture 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#AssignCulture
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, AssignCulture task
- AssignCulture task [MSBuild]
ms.assetid: 8f8314cc-82a6-4f16-a62d-b9f0d1d5e274
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 23b991efaa32e2c1886e6e0cd64bb9d6181190d0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68187043"
---
# <a name="assignculture-task"></a>AssignCulture 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此任务接受文件名中可能包含有效 .NET 区域性标识符字符串的项的列表，并且生成包含相应的区域性标识符且名为 `Culture` 的元数据的项。 例如，文件名 Form1.fr-fr.resx 具有嵌入的区域性标识符“fr-fr”，因此该任务会生成具有相同文件名的项，其中元数据 `Culture` 为 `fr-fr`。 该任务还会生成文件名中删除了区域性的文件名列表。  
  
## <a name="task-parameters"></a>任务参数  
 下表描述了 `AssignCulture` 任务的参数。  
  
|参数|说明|  
|---------------|-----------------|  
|`AssignedFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含 `Files` 参数收到的项列表，同时向每个项添加 `Culture` 元数据条目。<br /><br /> 如果来自 `Files` 参数的传入项已包含 `Culture` 元数据条目，则使用原始的元数据条目。<br /><br /> 如果文件名包含有效的区域性标识符，则该任务仅分配 `Culture` 元数据条目。 区域性标识符必须位于文件名中最后两个点之间。|  
|`AssignedFilesWithCulture`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含 `AssignedFiles` 参数中具有 `Culture` 元数据条目的项的子集。|  
|`AssignedFilesWithNoCulture`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含 `AssignedFiles` 参数中不具有 `Culture` 元数据条目的项的子集。|  
|`CultureNeutralAssignedFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含 `AssignedFiles` 参数中生成的同一项列表，但区域性已从文件名中删除。<br /><br /> 如果文件名是有效的区域性标识符，该任务仅从文件名删除区域性。|  
|`Files`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定要为其分配区域性并且嵌入了区域性名称的文件的列表。|  
  
## <a name="remarks"></a>备注  
 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数及其说明的列表，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。  
  
## <a name="example"></a>示例  
 以下示例使用 `ResourceFiles` 项集合执行 `AssignCulture` 任务。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <ResourceFiles Include="MyResource1.fr.resx"/>  
        <ResourceFiles Include="MyResource2.XX.resx"/>  
    </ItemGroup>  
  
    <Target Name="Culture">  
        <AssignCulture  
            Files="@(ResourceFiles)"  
            <Output TaskParameter="AssignedFiles"  
                ItemName="OutAssignedFiles"/>  
            <Output TaskParameter="AssignedFilesWithCulture"  
                ItemName="OutAssignedFilesWithCulture"/>  
            <Output TaskParameter="AssignedFilesWithNoCulture"  
                ItemName="OutAssignedFilesWithNoCulture"/>  
            <Output TaskParameter="CultureNeutralAssignedFiles"  
                ItemName="OutCultureNeutralAssignedFiles"/>  
        </AssignCulture>  
    </Target>  
</Project>  
```  
  
 下表对任务执行后输出项的值进行了描述。 项元数据显示在项后的括号中。  
  
|项集合|内容|  
|---------------------|--------------|  
|`OutAssignedFiles`|`MyResource1.fr.resx (Culture="fr")`<br /><br /> `MyResource2.XX.resx`（无其他元数据）|  
|`OutAssignedFilesWithCulture`|`MyResource1.fr.resx (Culture="fr")`|  
|`OutAssignedFilesWithNoCulture`|`MyResource2.XX.resx`（无其他元数据）|  
|`OutCultureNeutralAssignedFiles`|`MyResource1.resx (Culture="fr")`<br /><br /> `MyResource2.XX.resx (`无其他元数据）|  
  
## <a name="see-also"></a>另请参阅  
 [操作](../msbuild/msbuild-tasks.md)   
 [任务引用](../msbuild/msbuild-task-reference.md)
