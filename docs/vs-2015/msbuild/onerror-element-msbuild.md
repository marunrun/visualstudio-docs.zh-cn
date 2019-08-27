---
title: OnError 元素 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#OnError
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- OnError Element [MSBuild]
- <OnError Element [MSBuild]
ms.assetid: 765767d3-ecb7-4cd9-ba1e-d9468964dddc
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 46f6907bea5954cffae92b41398717a8247350e0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68195662"
---
# <a name="onerror-element-msbuild"></a>OnError 元素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

对于某失败的任务，如果 `ContinueOnError` 属性为 `false`，则会出现一个或多个要执行的目标。  
  
 \<Project>  
 \<Target>  
 \<OnError>  
  
## <a name="syntax"></a>语法  
  
```  
<OnError ExecuteTargets="TargetName"  
    Condition="'String A'=='String B'" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|说明|  
|---------------|-----------------|  
|`Condition`|可选特性。<br /><br /> 要计算的条件。 有关详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。|  
|`ExecuteTargets`|必需的特性。<br /><br /> 任务失败时要执行的目标。 用分号分隔多个目标。 以指定顺序执行多个目标。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[Target](../msbuild/target-element-msbuild.md)|[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 任务的容器元素。|  
  
## <a name="remarks"></a>备注  
 如果其中一个 `Target` 元素的任务失败并将 `ContinueOnError` 属性设置为 `ErrorAndStop`（或 `false`），则 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 执行 `OnError` 元素。 任务失败时，执行在 `ExecuteTargets` 属性中指定的目标。 如果目标中存在多个 `OnError` 元素，则在任务失败时将按顺序执行 `OnError` 元素。  
  
 有关 `ContinueOnError` 属性的详细信息，请参阅 [Task 元素 (MSBuild)](../msbuild/task-element-msbuild.md)。 有关目标的信息，请参阅[目标](../msbuild/msbuild-targets.md)。  
  
## <a name="example"></a>示例  
 以下代码执行 `TaskOne` 和 `TaskTwo` 任务。 如果 `TaskOne` 失败，[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 计算 `OnError` 元素并执行 `OtherTarget` 目标。  
  
```  
<Target Name="ThisTarget">  
    <TaskOne ContinueOnError="ErrorAndStop">  
    </TaskOne>  
    <TaskTwo>  
    </TaskTwo>  
    <OnError ExecuteTargets="OtherTarget" />  
</Target>  
```  
  
## <a name="see-also"></a>另请参阅  
 [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)   
 [目标](../msbuild/msbuild-targets.md)
