---
title: DslTextTransform 命令
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, commands
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a303fc3ddb880402e3f998b2360122f6f056b757
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72605930"
---
# <a name="the-dsltexttransform-command"></a>DslTextTransform 命令
DslTextTransform 是一个脚本，它调用 TextTransform 并使用常用选项运行它。 你可以使用 DslTextTransformation 自动执行 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 项目的夜间生成。 有关详细信息，请参阅[用 TextTransform 实用工具生成文件](../modeling/generating-files-with-the-texttransform-utility.md)。

 DslTextTransform 位于以下目录中：

 **\<Visual Studio SDK 安装路径 > \VisualStudioIntegration\Tools\Bin**

 可以将以下参数指定为 DslTextTransform 的输入：

- 域模型项目的输出目录。

- 设计器定义项目的输出目录。

- 文本模板文件的位置。

  DslTextTransform 使用默认指令处理器和程序集处理指定的文本模板文件。 如果创建自定义指令处理器，则可以创建自己的批处理文件来调用 TextTransform。 在此批处理文件中，可以指定程序集和关联的自定义指令处理器。