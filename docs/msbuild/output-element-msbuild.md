---
title: Output 元素 (MSBuild) | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Output
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <Output> Element [MSBuild]
- Output Element [MSBuild]
ms.assetid: 34bc7cd1-efd3-4b57-b691-4584eeb6a0e9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cb8f7a02183fe34dcd882e23ee7bf8b90f9a2cc6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62963918"
---
# <a name="output-element-msbuild"></a>Output 元素 (MSBuild)
存储项和属性中的任务输出值。

 \<Project> \<Target> \<Task> \<Output>

## <a name="syntax"></a>语法

```xml
<Output TaskParameter="Parameter"
    PropertyName="PropertyName"
    Condition = "'String A' == 'String B'" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|说明|
|---------------|-----------------|
|`TaskParameter`|必需的特性。<br /><br /> 任务输出参数的名称。|
|`PropertyName`|`PropertyName` 或 `ItemName` 特性是必需的。<br /><br /> 接收任务输出参数值的属性。 然后，项目可引用具有 $(\<PropertyName>) 语法的属性。 此属性名称可以是新属性名称，也可以是项目中已定义的名称。<br /><br /> 在已使用 `ItemName` 的情况下，不能使用该特性。|
|`ItemName`|`PropertyName` 或 `ItemName` 特性是必需的。<br /><br /> 接收任务输出参数值的项。 然后，项目可引用具有 @(\<ItemName>) 语法的项。 项名称可以是新项名称，也可以是项目中已定义的名称。 当项名称是现有项时，将向该现有项添加输出参数值。 <br /><br /> 在已使用 `PropertyName` 的情况下，不能使用该特性。|
|`Condition`|可选特性。<br /><br /> 要计算的条件。 有关详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

| 元素 | 说明 |
| - | - |
| [Task](../msbuild/task-element-msbuild.md) | 创建并执行的 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 任务的实例。 |

## <a name="example"></a>示例
 以下代码示例演示在 `Target` 元素中执行的 `Csc` 任务。 传递给任务参数的项和属性在本示例外部声明。 来自输出参数 `OutputAssembly` 的值存储在 `FinalAssemblyName` 项中，来自输出参数 `BuildSucceeded` 的值存储在 `BuildWorked` 属性中。 有关详细信息，请参阅[任务](../msbuild/msbuild-tasks.md)。

```xml
<Target Name="Compile" DependsOnTargets="Resources">
    <Csc  Sources="@(CSFile)"
            TargetType="library"
            Resources="@(CompiledResources)"
            EmitDebugInformation="$(includeDebugInformation)"
            References="@(Reference)"
            DebugType="$(debuggingType)"
            OutputAssembly="$(builtdir)\$(MSBuildProjectName).dll" >
        <Output TaskParameter="OutputAssembly"
                  ItemName="FinalAssemblyName" />
        <Output TaskParameter="BuildSucceeded"
                  PropertyName="BuildWorked" />
    </Csc>
</Target>
```

## <a name="see-also"></a>请参阅
- [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
- [任务](../msbuild/msbuild-tasks.md)
