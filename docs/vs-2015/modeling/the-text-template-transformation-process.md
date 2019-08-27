---
title: 文本模板转换过程 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, transformation process
ms.assetid: 80b3f0e0-49e7-4865-a1ac-dba068abe96b
caps.latest.revision: 32
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 0f92b4053006aa5da3c28d9330b372466f84d0fd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68199954"
---
# <a name="the-text-template-transformation-process"></a>文本模板转换过程
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

文本模板转换过程将文本模板文件作为输入并生成一个新的文本文件作为输出。 例如，可以使用文本模板来生成 Visual Basic 或 C# 代码，或可以生成一份 HTML 报告。  
  
 三个组件参与此过程： 引擎、 主机和指令处理器。 引擎控制该过程;它与宿主和指令处理器生成输出文件进行交互。 主机提供与环境中，如定位文件和程序集进行任何交互。 指令处理器添加功能，例如，在从 XML 文件或数据库读取数据。  
  
 文本模板转换过程中两个步骤执行。 首先，引擎就会创建一个临时的类，这被称为生成的转换类。 此类包含生成的指令和控制块的代码。 在此之后，该引擎编译并执行生成的转换类生成输出文件。  
  
## <a name="components"></a>组件  
  
|组件|描述|可自定义 （是/否）|  
|---------------|-----------------|------------------------------|  
|引擎|引擎组件控制文本模板转换过程|不是。|  
|Host|该主机是引擎和用户环境之间的接口。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 是一个主机的文本转换过程。|可以。 您可以编写自定义主机。|  
|指令处理器|指令处理器是处理指令文本模板中的类。 指令可用于从输入源向文本模板提供的数据。|可以。 您可以编写自定义指令处理器|  
  
## <a name="the-engine"></a>引擎  
 引擎接收该模板作为主机，用于处理在转换过程中使用的所有文件中的字符串。 引擎然后会要求主机以查找任何自定义指令处理器和环境的其他方面。 然后，该引擎编译并运行生成的转换类。 引擎返回到主机，通常将文本保存到一个文件生成的文本。  
  
## <a name="the-host"></a>主机  
 主机负责向外转换过程，其中包括环境相关的任何内容：  
  
- 定位文本和二进制文件请求的引擎或指令处理器。 宿主可以搜索目录和全局程序集缓存，以查找程序集。 主机可以找到该引擎的自定义指令处理器代码。 主机还可以查找和读取文本文件并返回其内容作为字符串。  
  
- 提供标准的程序集和该引擎用于创建生成的转换类的命名空间的列表。  
  
- 提供当引擎编译并执行生成的转换类时使用的应用程序域。 主机应用程序免受模板代码中的错误将使用单独的应用程序域。  
  
- 写入生成的输出文件。  
  
- 设置适用于生成的输出文件的默认扩展。  
  
- 处理文本模板转换错误。 例如，主机可以在用户界面中显示的错误或将其写入到文件。 (在[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，错误消息窗口中显示错误。)  
  
- 如果用户已调用指令，而无需提供一个值，请提供所需的参数值。 指令处理器可指定的指令，并使用参数名称，并要求宿主提供的默认值，如果有的话。  
  
## <a name="directives-and-directive-processors"></a>指令和指令处理器  
 指令是在文本模板中的命令。 它提供了生成过程的参数。 通常，指令定义的源和类型的模型或其他输入和输出文件的文件扩展名。  
  
 指令处理器可以处理一个或多个指令。 在转换模板时，你必须安装指令处理器来处理在模板中的指令。  
  
 指令通过将代码添加生成的转换类中的工作。 创建生成的转换类时，可以从文本模板和引擎进程的所有指令调用调用指令。 已成功调用指令后，在文本模板中编写的代码的其余部分可以依赖于该指令提供的功能。 例如，您可以进行以下调用到`import`指令在模板中：  
  
 `<#@ import namespace="System.Text" #>`  
  
 标准的指令处理器将转换为`using`生成的转换类中的语句。 然后，可以使用`StringBuilder`类中的模板代码，而不用其限定为 rest `System.Text.StringBuilder`。
