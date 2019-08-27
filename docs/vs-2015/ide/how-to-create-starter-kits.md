---
title: 如何：创建初学者工具包 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Starter Kits, creating
ms.assetid: ed7d1844-7c01-424a-a831-5003efe0f7bc
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: fb7b601c04c73cd1f617e42c848edaf7dc65bde8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62429323"
---
# <a name="how-to-create-starter-kits"></a>如何：创建初学者工具包
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

初学者工具包包含一个完整应用程序的代码以及有关如何修改或扩展该应用程序的文档。 创建初学者工具包与创建常规项目模板基本相同，唯一的区别是初学者工具包包括创建基于初学者工具包的项目时设置为打开的文档文件。  
  
## <a name="designing-and-developing-a-starter-kit"></a>设计和开发初学者工具包  
 首先，必须标识想要开发和定义目标受众的初学者工具包类型。 然后，设计项目和文档，使其符合你的目标。  
  
 如果要创建示例应用程序或插件：  
  
- 创建一个在生成时未发生错误的项目。  
  
- 添加模板代码以实现其他任务（可选）。  
  
- 准备文档。  
  
  如果要创建学习工具：  
  
- 创建一个在生成时未发生错误的项目。  
  
- 组织资源，例如代码片段和项模板。  
  
- 准备文档。  
  
## <a name="creating-a-template"></a>创建模板  
 完成项目和文档的步骤后，即可准备创建初学者工具包的项目模板。 此过程与项目模板的创建完全相同。  
  
 以下主题包含有关创建模板的信息。  
  
 [如何：创建项目模板](../ide/how-to-create-project-templates.md)  
 说明如何使用“导出模板”向导创建模板。  
  
 [如何：更新现有模板](../ide/how-to-update-existing-templates.md)  
 描述如何编辑已导出的模板。 使用此过程修改 .vstemplate 文件以自定义你的初学者工具包。  
  
## <a name="see-also"></a>请参阅  
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)   
 [自定义模板](../ide/customizing-project-and-item-templates.md)   
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
