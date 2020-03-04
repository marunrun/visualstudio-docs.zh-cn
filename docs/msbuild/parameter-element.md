---
title: Parameter 元素 | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
- xml
helpviewer_keywords:
- Parameter element [MSBuild]
- <Parameter> element [MSBuild]
ms.assetid: b273afff-b500-4e97-8cfd-31f39fa64a51
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dbf0c25967d84e930ee97a84709c808d3541e733
ms.sourcegitcommit: 3ed59ce39692124fe61c484df4348c0b9abee9b9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2020
ms.locfileid: "78263083"
---
# <a name="parameter-element"></a>Parameter 元素

包含某个任务的特定参数信息，该任务可通过使用 `UsingTask` `TaskFactory` 生成。  元素的名称就是该参数的名称。  有关详细信息，请参阅 [UsingTask 元素 (MSBuild)](../msbuild/usingtask-element-msbuild.md)。

 \<Project> \<UsingTask> \<ParameterGroup> \<Parameter>

## <a name="syntax"></a>语法

```xml
<ParameterGroup ParameterType="SystemType"
    Output="true/false"
    Required="true/false" />
```

## <a name="attributes-and-elements"></a>特性和元素

 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|`ParameterType`|可选特性。<br /><br /> 参数的 .NET 类型，例如，`System.String`。|
|`Output`|可选布尔属性。<br /><br /> 如果值为 `true`，该参数是任务的输出参数。 默认情况下，该值为 `false`。|
|`Required`|可选布尔属性。<br /><br /> 如果值为 `true`，该参数是任务的必需参数。 默认情况下，该值为 `false`。|

### <a name="child-elements"></a>子元素

 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[ParameterGroup](../msbuild/parametergroup-element.md)|包含一系列可选参数，这些参数将显示在通过使用 `UsingTask` `TaskFactory` 生成的任务上。|

## <a name="example"></a>示例

 下面的示例演示如何使用 `Parameter` 元素。

```xml
<UsingTask TaskName="MyTask" AssemblyName="My.Assembly" TaskFactory="MyTaskFactory">
       <ParameterGroup>
              <Parameter1 ParameterType="System.String" Required="False" Output="False"/>
              <Parameter2 ParameterType="System.Int" Required="True" Output="False"/>
             ...
</ParameterGroup>
       <Task Evaluate="true">
       ... Task factory-specific data ...
       </Task>
</UsingTask>
```

## <a name="see-also"></a>请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
- [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
