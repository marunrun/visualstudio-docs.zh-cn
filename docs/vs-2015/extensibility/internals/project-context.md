---
title: 项目上下文 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], opening items
ms.assetid: d1803f4a-24eb-44b0-b5d2-cb40c15534be
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d4ee4da5fdea63cf1bdd33554c72f6dac30d0334
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62429933"
---
# <a name="project-context"></a>项目上下文
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

当用户添加或适用于项目和项目项时，IDE 将使用项目上下文的概念来确定应执行了各种操作。  
  
 通常情况下，文件是通过选择来显式创建用户的标准项目对象**新的项目**命令或通过选择，能够**打开项目**命令**文件**菜单。 在这些情况下，创建和打开项目的上下文中的文件和项目类型定义编辑文档的上下文。  
  
 某些项目提供非常丰富的上下文。 例如，项目管理的项目范围，以编程方式命名空间或数据绑定的项目范围的数据库连接。 用户可以经常打开的文件或数据库连接直接通过使用一个特定项目对象，例如在解决方案资源管理器中显示的项目项。  
  
 在其他情况下，项的项目上下文未显式指定。 例如，某项的上下文不可用时用户选择打开的文件**打开现有文件**命令**文件**时调试器的运行上一个文件，或当用户单击菜单**在文件中查找**命令，在**查找和替换**对话框。 若要处理这些情况下，IDE 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument>管理查找最佳的项目以打开的文档的过程。  
  
## <a name="see-also"></a>请参阅  
 [项目优先级](../../extensibility/internals/project-priority.md)   
 [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
