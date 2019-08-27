---
title: TaskBody 元素 (MSBuild) | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- TaskBody element [MSBuild]
- <TaskBody> element [MSBuild]
ms.assetid: 49d8741b-f1ea-4470-94fd-a1ac27341a6a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8f788df1dd3cad2baddd6d2966b04195af01fe7d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62938956"
---
# <a name="taskbody-element-msbuild"></a>TaskBody 元素 (MSBuild)
包含传递给 `UsingTask` `TaskFactory` 的数据。 有关详细信息，请参阅 [UsingTask 元素 (MSBuild)](../msbuild/usingtask-element-msbuild.md)。

 \<Project> \<UsingTask> \<TaskBody>

## <a name="syntax"></a>语法

```xml
<TaskBody Evaluate="true/false" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|说明|
|---------------|-----------------|
|`Evaluate`|可选布尔属性。<br /><br /> 如果值为 `true`，任务实例化时，MSBuild 对所有内部元素求值，并在将信息传递到 `TaskFactory` 前扩展项和属性。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|数据|`TaskBody` 标记之间的文本一字不差地发送到 `TaskFactory`。|

### <a name="parent-elements"></a>父元素

| 元素 | 说明 |
| - | - |
| [UsingTask](../msbuild/usingtask-element-msbuild.md) | 提供在 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 中注册任务的方法。 项目中可能有零个或零个以上的 `UsingTask` 元素。 |

## <a name="example"></a>示例
 下面的示例演示如何将 `TaskBody` 元素和 `Evaluate` 属性结合使用。

```xml
<UsingTask TaskName="MyTask" AssemblyName="My.Assembly" TaskFactory="MyTaskFactory">
       <ParameterGroup>
              <Parameter1 ParameterType="System.String" Required="False" Output="False"/>
              <Parameter2 ParameterType="System.Int" Required="True" Output="False"/>
              ...
</ParameterGroup>
       <TaskBody Evaluate="true">
      ... Task factory-specific data ...
       </TaskBody>
</UsingTask>
```

## <a name="see-also"></a>请参阅
- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
- [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
