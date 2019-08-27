---
title: 一个解决方案中的多个 Dsl |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 7e668620-6217-4e87-aea7-e9036776c8e4
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: d70794dddc02605c76c1af330a49af4be917c0e3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68159016"
---
# <a name="multiple-dsls-in-one-solution"></a>一个解决方案中的多个 DSL
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可将多个 DSL 打包为单个解决方案的一部分，以便可同时安装它们。  
  
 可使用多种技术集成多个 DSL。 有关详细信息，请参阅[通过使用 Visual Studio Modelbus 集成模型](../modeling/integrating-models-by-using-visual-studio-modelbus.md)和[如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)并[自定义复制行为](../modeling/customizing-copy-behavior.md)。  
  
### <a name="to-build-more-than-one-dsl-in-the-same-solution"></a>在同一个解决方案中生成多个 DSL  
  
1. 创建两个或多个 DSL 解决方案和一个 VSIX 项目，并将所有项目添加到单个解决方案。  
  
   - 若要创建新的 VSIX 项目：在中**新的项目**对话框中，选择**Visual C#** ，**扩展性**， **VSIX 项目**。  
  
   - 在 VSIX 解决方案目录中创建两个或多个 DSL 解决方案。  
  
        对于每个 DSL，打开 Visual Studio 的新实例。 创建新 DSL，并指定与 VSIX 解决方案相同的解决方案目录。  
  
        确保使用不同的文件名扩展创建每个 DSL。  
  
   - 更改的名称**Dsl**并**DslPackage**项目，以便它们都不同。 例如：`Dsl1`、`DslPackage1`、`Dsl2`、`DslPackage2`。  
  
   - 在每个**DslPackage\*\source.extension.tt**，此行更新为正确的 Dsl 项目名称：  
  
        `string dslProjectName = "Dsl2";`  
  
   - 在 VSIX 解决方案中，添加 Dsl * 和 DslPackage\*项目。  
  
        你可能想要将每一对放在其自己的解决方案文件夹中。  
  
2. 合并 DSL 的 VSIX 清单：  
  
   1. 打开_YourVsixProject_ **\source.extension.manifest**。  
  
   2. 对于每个 DSL，选择**添加内容**和添加：  
  
       - `Dsl*` 项目用作**MEF 组件**  
  
       - `DslPackage*` 项目用作**MEF 组件**  
  
       - `DslPackage*` 项目用作**VS 包**  
  
3. 生成解决方案。  
  
   生成的 VSIX 将安装这两个 DSL。 可使用 F5，对其进行测试或部署_YourVsixProject_ **\bin\Debug\\\*.vsix**。  
  
## <a name="see-also"></a>请参阅  
 [使用 Visual Studio Modelbus 集成模型](../modeling/integrating-models-by-using-visual-studio-modelbus.md)   
 [如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)   
 [自定义复制行为](../modeling/customizing-copy-behavior.md)
