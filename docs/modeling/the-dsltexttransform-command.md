---
title: DslTextTransform 命令
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, commands
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 32c01401eda8fb1bbe2bdcfc2950a51b968e98b7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "76114912"
---
# <a name="the-dsltexttransform-command"></a>DslTextTransform 命令
DslTextTransform 是一个脚本，它调用 TextTransform.exe 并使用常用选项运行它。 可以使用 DslTextTransformation 自动执行项目的夜间生成 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 。 有关详细信息，请参阅 [用 TextTransform 实用工具生成文件](../modeling/generating-files-with-the-texttransform-utility.md)。

 DslTextTransform 位于以下目录中：

 **\<Visual Studio SDK Installation Path>\VisualStudioIntegration\Tools\Bin**

 可以将以下参数指定为 DslTextTransform 的输入：

- 域模型项目的输出目录。

- 设计器定义项目的输出目录。

- 文本模板文件的位置。

  DslTextTransform 使用默认指令处理器和程序集处理指定的文本模板文件。 如果创建自定义指令处理器，则可以创建自己的批处理文件来调用 TextTransform.exe。 在此批处理文件中，可以指定程序集和关联的自定义指令处理器。
