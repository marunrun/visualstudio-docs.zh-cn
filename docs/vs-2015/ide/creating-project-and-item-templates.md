---
title: 创建项目和项模板 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- templates [Visual Studio], projects
- item templates, about item templates
- templates [Visual Studio], item
- Visual Studio templates, item
- Visual Studio templates, about templates
- project templates [Visual Studio], about project templates
- Visual Studio templates, project
- templates [Visual Studio], about templates
ms.assetid: a6ce501a-699b-4e3e-ade8-c81895645c20
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: bfcfadf13074c3fc1dc82fce51f449453ca03b11
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201902"
---
# <a name="creating-project-and-item-templates"></a>创建项目和项模板
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目和项模板提供了可重用的存根，这些存根可为用户提供一些基本代码和结构以供其用于实现自己的目的。  
  
## <a name="visual-studio-templates"></a>Visual Studio 模板  
 安装 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 时将安装一系列的预定义项目和项模板。 项目模板的例子有 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 和 [!INCLUDE[csprcs](../includes/csprcs-md.md)] Windows 窗体应用程序和“新建项目”对话框中提供的类库模板  。 安装的项模板在“添加新项”对话框中可用，并包括代码文件、XML 文件、HTML 页和样式表等项  。  
  
 这些模板为用户提供一个开始创建项目或扩展当前项目的起点。 项目模板提供特定项目类型所需的文件，包括标准程序集引用，并设置默认项目属性和编译器选项。 项模板的复杂程度不一，从具有正确文件扩展名的单个空文件到包含具有存根代码的源代码文件、设计器信息文件和嵌入资源等的多文件项。  
  
 除了“新建项目”和“添加新项”对话框中的已安装模板，还可以创作自己的模板或下载并使用社区创建的模板   。 有关更多信息，请参见[如何：创建项目模板](../ide/how-to-create-project-templates.md)和[如何：创建项模板](../ide/how-to-create-item-templates.md)。  
  
## <a name="contents-of-a-template"></a>模板的内容  
 所有项目模板和项模板（无论是与 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 一起安装的还是由你创建的）均通过使用相同的原则工作并具有类似的内容。 所有模板均包含以下项：  
  
- 使用模板时要创建的文件。 包括源代码文件、嵌入资源、项目文件等。  
  
- 一个 vstemplate 文件。 该文件包含元数据，元数据提供在“新建项目”和“添加新项”对话框中显示模板以及从模板创建项目或项时所需的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 信息   。 有关 .vstemplate 文件的详细信息，请参阅[模板参数](../ide/template-parameters.md)。  
  
  当这些文件被压缩成一个 .zip 文件并放在正确的文件夹内时，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 将自动显示这些文件。 项目模板显示在“新建项目”对话框的“我的模板”部分，项模板显示在“添加新项”对话框    。 有关模板文件夹的详细信息，请参阅[如何：查找和组织模板](../ide/how-to-locate-and-organize-project-and-item-templates.md)。  
  
## <a name="starter-kits"></a>初学者工具包  
 初学者工具包是增强的模板，可与社区的其他成员共享。 初学者工具包包含可编译的代码示例、文档及其他资源，这些资源可帮助用户在生成有用的实际应用程序的同时学习新工具和编程技巧。 初学者工具包的基本内容和流程与模板的一样。 有关更多信息，请参见[如何：创建初学者工具包](../ide/how-to-create-starter-kits.md)。  
  
## <a name="see-also"></a>请参阅  
 [如何：创建项目模板](../ide/how-to-create-project-templates.md)   
 [如何：创建项模板](../ide/how-to-create-item-templates.md)   
 [模板参数](../ide/template-parameters.md)   
 [自定义模板](../ide/customizing-project-and-item-templates.md)   
 [如何：创建初学者工具包](../ide/how-to-create-starter-kits.md)
