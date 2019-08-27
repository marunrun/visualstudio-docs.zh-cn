---
title: 如何：忽略任务中的错误 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, ignoring errors
- ContinueOnError attribute [MSBuild]
ms.assetid: e2f1ca4f-787b-44bd-bc64-81a036025e96
caps.latest.revision: 21
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5025cc3e9dc0e13c3ae4658d129f5d0ac94f6fd6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68156589"
---
# <a name="how-to-ignore-errors-in-tasks"></a>如何：忽略任务中的错误
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有时你希望生成能够容忍某些任务中的错误。 如果这些非关键任务失败，你希望生成能够继续进行，因为它仍然可以产生所需的输出。 例如，如果一个项目在每个组件生成之后都使用 `SendMail` 任务发送电子邮件消息，那么即使邮件服务器变得不可用而导致状态邮件无法发送，但依然让生成继续完成，这一情况或许便是可以接受的。 或者，如果在生成过程中，中间文件通常会被删除，但即使无法删除这些文件，那么让生成继续完成也是可以接受的。  
  
## <a name="using-the-continueonerror-attribute"></a>使用 ContinueOnError 属性  
 `Task` 元素的 `ContinueOnError` 属性控制在发生任务失败时，是停止还是继续生成。 此属性还可以控制在生成继续操作时，错误被视为错误还是警告。  
  
 `ContinueOnError` 属性可以包含下列值之一：  
  
- **WarnAndContinue** 或 **true**。 当任务失败时，[Target](../msbuild/target-element-msbuild.md) 元素中的后续任务和生成将继续执行，并且来自该任务的所有错误都被视为警告。  
  
- **ErrorAndContinue**。 当任务失败时，`Target` 元素中的后续任务和生成将继续执行，并且来自该任务的所有错误都被视为错误。  
  
- **ErrorAndStop** 或 **false**（默认值）。 当任务失败时，将不会执行 `Target` 元素中的剩余任务和生成，并且整个 `Target` 元素和生成都被视为已失败。  
  
  4\.5 之前的 .NET Framework 版本仅支持 `true` 和 `false` 值。  
  
  `ContinueOnError` 的默认值为 `ErrorAndStop`。 如果你将属性设置为 `ErrorAndStop`，则会使此行为对读取项目文件的任何人都显式可见。  
  
#### <a name="to-ignore-an-error-in-a-task"></a>忽略任务中的错误  
  
- 使用任务的 `ContinueOnError` 属性。 例如:  
  
     `<Delete Files="@(Files)" ContinueOnError="WarnAndContinue"/>`  
  
## <a name="example"></a>示例  
 以下代码示例阐释即使 `Delete` 任务失败，`Build` 目标仍将运行并且生成将被视为成功。  
  
```  
<Project DefaultTargets="FakeBuild"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <Files Include="*.obj"/>  
    </ItemGroup>  
    <Target Name="Clean">  
        <Delete Files="@(Files)" ContinueOnError="WarnAndContinue"/>  
    </Target>  
  
    <Target Name="FakeBuild" DependsOnTargets="Clean">  
        <Message Text="Building after cleaning..."/>  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>另请参阅
[MSBuild](msbuild.md)  
 [任务参考](../msbuild/msbuild-task-reference.md)   
 [任务](../msbuild/msbuild-tasks.md)
