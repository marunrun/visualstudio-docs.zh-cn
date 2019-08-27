---
title: 如何：创建和删除项目依赖项 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- VS.ProjectDependenciesDlg
helpviewer_keywords:
- vs.build.projectdependencies
- project dependencies
- builds [Visual Studio], setting up
- project build configurations, dependencies
- dependencies, project
- projects [Visual Studio], dependencies
ms.assetid: e2a0a8ff-dae7-40a8-b774-b88aa5235183
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: e4b039f514c7d43e768becca8532a05fb14785b3
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65680367"
---
# <a name="how-to-create-and-remove-project-dependencies"></a>如何：创建和移除项目依赖项
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

生成包含多个项目的解决方案时，可能需要首先生成某些项目，然后才能生成由其他项目使用的代码。 当一个项目使用另一个项目生成的可执行代码时，生成代码的项目则称为使用代码的项目的项目依赖项。 可在“项目依赖项”对话框中定义此类依赖关系。  
  
### <a name="to-assign-dependencies-to-projects"></a>将依赖项分配给项目  
  
1. 在“解决方案资源管理器”中，选择一个项目。  
  
2. 在“项目”菜单上，选择“项目依赖项”。  
  
    “项目依赖项”对话框随即打开。  
  
   > [!NOTE]
   > “项目依赖项”选项仅可在具有多个项目的解决方案中使用。  
  
3. 从“依赖项”选项卡上的“项目”下拉菜单中选择一个项目。  
  
4. 在“依赖对象”字段中，选中必须在此项目生成前生成的任何其他项目的复选框。  
  
   解决方案必须包含多个项目才能创建项目依赖项。  
  
### <a name="to-remove-dependencies-from-projects"></a>删除项目中的依赖项  
  
1. 在“解决方案资源管理器”中，选择一个项目。  
  
2. 在“项目”菜单上，选择“项目依赖项”。  
  
     “项目依赖项”对话框随即打开。  
  
    > [!NOTE]
    > “项目依赖项”选项仅可在具有多个项目的解决方案中使用。  
  
3. 从“依赖项”选项卡上的“项目”下拉菜单中选择一个项目。  
  
4. 在“依赖对象”字段中，清除不再属于此项目依赖项的任何其他项目的复选框。  
  
## <a name="see-also"></a>请参阅  
 [在 Visual Studio 中生成和清理项目和解决方案](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)   
 [编译和生成](../ide/compiling-and-building-in-visual-studio.md)   
 [了解生成配置](../ide/understanding-build-configurations.md)   
 [NIB 如何：修改项目属性和配置设置](https://msdn.microsoft.com/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)
