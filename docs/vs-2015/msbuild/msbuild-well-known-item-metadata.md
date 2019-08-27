---
title: MSBuild 常见的项元数据 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, item metadata
- MSBuild, well-known item metadata
ms.assetid: b5e791b5-c68f-4978-ad8a-9247d03bb6c0
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1bb2e53102221194dc829df162c44bbf04378b28
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154087"
---
# <a name="msbuild-well-known-item-metadata"></a>MSBuild 常见的项元数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

下表描述了创建每个项时分配给该项的元数据。 在每个示例中，以下项声明用于将文件 `C:\MyProject\Source\Program.cs` 包含在项目中。  
  
```  
<ItemGroup>  
    <MyItem Include="Source\Program.cs" />  
</ItemGroup>  
```  
  
|项元数据|描述|  
|-------------------|-----------------|  
|%(FullPath)|包含项的完整路径。 例如:<br /><br /> `C:\MyProject\Source\Program.cs`|  
|%(RootDir)|包含项的根目录。 例如:<br /><br /> `C:\`|  
|%(Filename)|包含项的文件名，但不包含扩展名。 例如：<br /><br /> `Program`|  
|%(Extension)|包含项的文件扩展名。 例如:<br /><br /> `.cs`|  
|%(RelativeDir)|包含 `Include` 属性中指定的路径，直到最后的反斜杠 (\\)。 例如:<br /><br /> `Source\`|  
|%(Directory)|包含项的目录，但不包含根目录。 例如:<br /><br /> `MyProject\Source\`|  
|%(RecursiveDir)|如果 `Include` 属性包含通配符 \*\*，则此元数据将指定代替通配符的路径的一部分。 有关通配符的详细信息，请参阅[如何：选择生成的文件](../msbuild/how-to-select-the-files-to-build.md)。<br /><br /> 如果文件夹 C:\MySolution\MyProject\Source\\ 包含文件 Program.cs，并且该项目文件包含此项： <br /><br /> `<ItemGroup>`<br /><br /> `<MyItem Include="C:\**\Program.cs" />`<br /><br /> `</ItemGroup>`<br /><br /> `%(MyItem.RecursiveDir)` 的值为 MySolution\MyProject\Source\\  。|  
|%(Identity)|`Include` 属性中指定的项。 例如：<br /><br /> `Source\Program.cs`|  
|%(ModifiedTime)|包含上一次修改项的时间戳。 例如:<br /><br /> `2004-07-01 00:21:31.5073316`|  
|%(CreatedTime)|包含创建项的时间戳。 例如:<br /><br /> `2004-06-25 09:26:45.8237425`|  
|%(AccessedTime)|包含上一次访问项的时间戳。<br /><br /> `2004-08-14 16:52:36.3168743`|  
  
## <a name="see-also"></a>请参阅  
 [项](../msbuild/msbuild-items.md)   
 [批处理](../msbuild/msbuild-batching.md)   
 [MSBuild 参考](../msbuild/msbuild-reference.md)
