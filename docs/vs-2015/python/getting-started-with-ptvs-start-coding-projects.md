---
title: PTVS 入门：开始编码（项目）| Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-python
ms.topic: conceptual
ms.assetid: 14b85e70-b9a8-415c-a307-8c8c316a0495
caps.latest.revision: 7
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: 28622f290d82f86bf3d18cc4f40cfcfc8e953dad
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62537138"
---
# <a name="getting-started-with-ptvs-start-coding-projects"></a>PTVS 入门：开始编码（项目）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Python Tools for Visual Studio (PTVS) 可帮助你管理代码。 
 
 你可以在很短的 [youtube 视频](https://www.youtube.com/watch?v=KHPoVpL7zHg&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=2)中观看这些说明。 
 
 如果之前用过 Python，则可知你的项目由文件在磁盘上的布局方式定义。 这非常适用于纯 Python 项目，但有更多文件（使用 JavaScript 的网页、单元测试和生成脚本）时，文件系统可能开始会有所限制。 Visual Studio 使用项目来实现三项任务。 
 
- 识别关键文件。 重要的文件是签入到版本控制系统（源文件、资源等）中的文件，而不是作为生成输出生成的文件。 重要文件也是复制到另一台计算机上以便其他人能够使用你的应用的文件。 
 
- 指定应如何使用文件。 你可能会有只要发生更改，工具就需对其进行处理的文件。 Visual Studio 项目可以捕获此信息 
 
- 定义组件的边界。 如果应用中有多个组件，可将每个组件放在一个单独的项目中。 这些组件可能最终会被部署到不同的服务器，以不同的版本或调试设置生成，或甚至可以通过使用另一种 Visual Studio 支持的语言（如 C++ 或 Node.js）进行编写 
 
  有几个项目模板，可以帮助你入门。 如果已有需处理的 Python 代码，“从现有代码”向导将帮助你创建包含你所有文件的项目。 对于一些常用框架存在多个 Web 项目。 PTVS 示例包中提供了更多模板。 存在可使提供的 Web 模板用于其他框架的选项。 Python 应用程序模板是一个干净的空项目。 有一个模块，可以帮助你入门。 
 
  Visual Studio 在“解决方案资源管理器”窗口中显示打开的项目，包括所有文件、搜索路径和 Python 环境。 若要添加新项，请选择你的项目文件夹，并从上下文菜单（按右指针按钮）中依次选择“添加”和“新项”。 可在对话框中选择任何项、自定义项的名称以及将项添加到项目中。 
 
  可以拖放到“解决方案资源管理器”中。 如果已经将文件复制到项目的目录结构中，则可以选择“解决方案资源管理器”顶部的“显示所有文件”。 然后可以选择要添加的项，并从上下文菜单中选择“包括在项目中”。 
 
  你可以在很短的 [youtube 视频](https://www.youtube.com/watch?v=KHPoVpL7zHg&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=2)中观看这些说明。 
 
## <a name="see-also"></a>另请参阅 
 [Wiki 文档](https://github.com/Microsoft/PTVS/wiki/Projects) [PTVS 入门和深入了解视频](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)
