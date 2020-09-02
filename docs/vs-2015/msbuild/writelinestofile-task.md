---
title: WriteLinesToFile 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#WriteLinesToFile
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- WriteLinesToFile task [MSBuild]
- MSBuild, WriteLinesToFile task
ms.assetid: 9c8862ac-8da5-4437-9430-ecc30421f1c9
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f530648c7dd772fb60148f4d755d4a4ffb420cbb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62419954"
---
# <a name="writelinestofile-task"></a>WriteLinesToFile 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

将指定项的路径写入指定的文本文件。  
  
## <a name="task-parameters"></a>任务参数  
 下表描述了 `WriteLinestoFile` 任务的参数。  
  
|参数|描述|  
|---------------|-----------------|  
|`File`|必选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定要将项写入到的文件。|  
|`Lines`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定要写入到文件的项。|  
|`Overwrite`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，该任务覆盖文件中的任何现有内容。|  
|`Encoding`|可选 `String` 参数。<br /><br /> 选择字符编码，例如“Unicode”。  另请参阅 <xref:System.Text.Encoding>。|  
  
## <a name="remarks"></a>备注  
 如果 `Overwrite` 为 `true`，创建一个新文件，向其中写入内容，然后关闭文件。 如果目标文件已存在，则覆盖该文件。 如果 `Overwrite` 为 `false`会将内容追加到文件中，如果目标文件还不存在则创建该文件。  
  
 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数及其说明的列表，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。  
  
## <a name="example"></a>示例  
 以下示例使用 `WriteLinesToFile` 任务，将 `MyItems` 项集合中项的路径写入到 `MyTextFile` 项集合指定的文件中。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <MyTextFile Include="Items.txt"/>  
        <MyItems Include="*.cs"/>  
    </ItemGroup>  
  
    <Target Name="WriteToFile">  
        <WriteLinesToFile  
            File="@(MyTextFile)"  
            Lines="@(MyItems)"  
            Overwrite="true"  
            Encoding="Unicode"/>  
    </Target>  
  
</Project>  
```  
  
## <a name="see-also"></a>另请参阅  
 [操作](../msbuild/msbuild-tasks.md)   
 [任务引用](../msbuild/msbuild-task-reference.md)
