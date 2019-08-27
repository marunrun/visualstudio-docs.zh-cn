---
title: 如何：替换模板中的参数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- template parameters, substituting
- Visual Studio templates, using parameters
ms.assetid: a62924a7-4ba0-413d-b606-fdbe1fcf2807
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 3c0a710bc3ad504c6654528db33b9a6698f4f7ae
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435164"
---
# <a name="how-to-substitute-parameters-in-a-template"></a>如何：替换模板中的参数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

创建基于模板的文件时，可能会替换模板参数，比如类名称和命名空间。 有关模板参数的完整列表，请参阅[模板参数](../ide/template-parameters.md)。  
  
## <a name="procedure"></a>过程  
 每当创建基于模板的项目时，均可以替换模板的文件中的参数。 此过程说明使用模板创建新项目时，如何创建一个将命名空间名称替换为安全的项目名称的模板。  
  
#### <a name="to-use-a-parameter-to-replace-namespace-name-with-the-project-name"></a>使用参数将命名空间名称替换为项目名称  
  
1. 将参数插入模板中的一个或多个代码文件中。 例如：  
  
    ```  
    namespace $safeprojectname$  
    ```  
  
    > [!NOTE]
    > 模板参数是以 $参数$ 格式编写的。  
  
2. 在模板的 .vstemplate 文件中，找到包括此文件的 `ProjectItem` 元素。  
  
3. 将 `ProjectItem` 元素的 `ReplaceParameters` 特性设置为 `true`。 例如：  
  
    ```  
    <ProjectItem ReplaceParameters="true">Class1.cs</ProjectItem>  
    ```  
  
## <a name="see-also"></a>请参阅  
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)   
 [模板参数](../ide/template-parameters.md)   
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)   
 [ProjectItem 元素（Visual Studio 项模板）](../extensibility/projectitem-element-visual-studio-item-templates.md)
