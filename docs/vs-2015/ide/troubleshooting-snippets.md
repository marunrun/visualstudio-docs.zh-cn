---
title: 疑难解答：代码片段 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: troubleshooting
helpviewer_keywords:
- IntelliSense Code Snippets, troubleshooting
- troubleshooting IntelliSense Code Snippets
- troubleshooting Visual Basic, IntelliSense Code Snippets
ms.assetid: 7b6dd40e-2f78-4b50-8e68-41fac1bcb81e
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 61f1a623d5ee5edee376819ad6c385aead5003f8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62429003"
---
# <a name="troubleshooting-snippets"></a>疑难解答：代码段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有关 IntelliSense 代码片段的问题通常由以下两个问题引起：代码片段文件损坏或代码片段文件中存在错误的内容。  
  
## <a name="common-problems"></a>常见问题  
  
### <a name="the-snippet-cannot-be-dragged-from-file-explorer-to-a-visual-studio-source-file"></a>代码片段不能从文件资源管理器拖动到 Visual Studio 源文件  
  
- 代码片段文件中的 XML 可能已损坏。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中的 XML 编辑器可找到 XML 结构中的问题。  
  
- 代码片段文件可能不符合代码片段架构。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中的 XML 编辑器可找到 XML 结构中的问题。  
  
### <a name="the-code-has-compiler-errors-that-are-not-highlighted"></a>代码具有未突出显示的编译器错误  
  
- 可能缺少项目引用。 检查有关代码片段的文档。 如果在计算机上找不到引用，则需要安装该引用。 插入代码片段时应在项目中添加所需的任何引用。 如果代码片段缺少引用信息，可将此情形作为一个错误报告给代码片段创建者。  
  
- 可能未定义变量。 代码片段中未定义的变量应突出显示。 如果未突出显示，则将此情形作为一个错误报告给代码片段创建者。  
  
## <a name="see-also"></a>请参阅  
 [代码片段](../ide/code-snippets.md)
