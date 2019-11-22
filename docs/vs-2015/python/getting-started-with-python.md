---
title: Getting Started with Python | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-python
ms.topic: conceptual
ms.assetid: 33f4f6fb-0ae4-4234-9df2-531f2d3af17f
caps.latest.revision: 13
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: 21e724e585f2a5bf0e1fe2a6b70f89c1bd5f5eec
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298188"
---
# <a name="getting-started-with-python"></a>Python 入门
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

The Python Tools for Visual Studio (PTVS), is a free, [open-source](https://github.com/Microsoft/ptvs) plug-in for Visual Studio that a powerful Python development experience.  
  
## <a name="python-the-language"></a>Python 语言
  
Python is a popular programming language that is used by many universities, scientists, app scripters, casual developers, and professional developers, working on applications, web sites, and cloud services.

As a programming language, Python is:
  
- 可靠。
- Generally useful for scripting quick programs, app scripting, desktop apps, web servers, web services, and scientific computing.
- 易于学习，设计良好，能帮助提高编码质量（许多大学都将它用于编程入门课程）。
- Flexible, supporting imperative, functional, and object-oriented programming styles.
- 免费且开源。
- Runs well on all major operating systems.  
- Supported by many free, useful, and well-designed libraries.  
- Supported by lots of documentation, samples, and a strong developer community.  

To learn more about the language, start with [Python for Beginners](https://www.python.org/about/gettingstarted/) on python.org.

To install Python itself, visit [https://www.python.org/download/](https://www.python.org/download/).

## <a name="python-tools-for-visual-studio"></a>Visual Studio 的 Python 工具
  
The Python Tools for Visual Studio, which you can install from [visualstudio.com](https://www.visualstudio.com/explore/python-vs), provide the following features:  
  
- 支持多种解释器：各种版本的 CPython、IronPython 以及 IPython  
- 项目系统可隐式选取 Python 代码的文件夹结构，也允许显式控制，以便标识应用代码、测试代码、网页、JavaScript、生成脚本等等。  
- 用于控制台、Web、Azure、数据科学和其他类型项目的项目模板。    
- The Azure SDK for Python (see below)    
- 丰富的编辑和代码理解功能，包括语法着色、跨所有代码和库的自动完成功能、签名帮助、类视图、转到定义、查找所有引用、重构等等。    
- 交互式 (REPL) 窗口
- 使用数据可视化功能的 IPython。
- 支持 IronPython 和 .NET/WPF。    
- 丰富的无需 Visual Studio 项目的调试功能，包括可对现有可执行文件进行调试、混合模式调试、对 Windows/Linux/Mac 进行远程调试，以及在交互式窗口中进行调试。   
- 分析工具。  
- 测试工具。  
  
下列资源可帮你入门：

- [安装指南](https://github.com/Microsoft/PTVS/wiki/PTVS-Installation)    
- [入门和深入了解短片](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)  
- Installation and features demo (27 min)](https://www.youtube.com/watch?v=JNNAOypc6Ek)  
- [文档](https://github.com/Microsoft/PTVS/wiki)  

Note that Visual Studio does not at present provide the means to create a stand-alone executable using Python, which essentially means a program with an embedded Python interpreter. 但是，如 [StackOverflow](https://stackoverflow.com/questions/5458048/how-to-make-a-python-script-standalone-executable-to-run-without-any-dependency) 所述，Python 社区中有多种方法可以实现此功能。 如博客文章 [Using CPython's Embeddable Zip File](https://devblogs.microsoft.com/python/cpython-embeddable-zip-file/)（使用 CPython 可嵌入 zip 文件）中所述，CPython 还支持嵌入到本机应用程序中。
  
## <a name="building-ui-with-python"></a>Building UI with Python  

The main offering for building a UI with Python is the [Qt Project](https://www.qt.io/qt-for-application-development/), with bindings for Python known as [PySide (the official binding)](https://wiki.qt.io/PySide) (also see [PySide downloads](https://download.qt.io/official_releases/pyside/.))and [PyQt](https://wiki.python.org/moin/PyQt). 目前，Visual Studio 中的 Python 支持不包括用于 UI 开发的任何特定工具。

## <a name="azure-sdk-for-python"></a>Azure SDK for Python
  
Azure SDK for Python 支持 Windows、Mac 和 Linux，使得使用和管理 Microsoft Azure 服务更加方便。 请参阅下列资源了解详细信息： 

- 若要安装 SDK，请使用 [Python 软件包索引](https://pypi.python.org/pypi/azure)或者按照 Azure 文档中的[安装 Python 和 SDK](https://docs.microsoft.com/azure/python/python-sdk-azure-install) 的说明进行操作。 
- [Azure SDK for Python 开发人员中心](https://azure.microsoft.com/develop/python/)通过教程提供许多从安装到文档的帮助。  以下为一些要点：  
- 操作指南：
  - [存储 Blob](https://azure.microsoft.com/develop/python/how-to-guides/blob-service/)  
  - [存储队列](https://azure.microsoft.com/develop/python/how-to-guides/queue-service/)  
  - [存储表](https://azure.microsoft.com/develop/python/how-to-guides/table-service/)  
  - [服务总线队列](https://azure.microsoft.com/develop/python/how-to-guides/service-bus-queues/)
  - [服务总线主题/订阅](https://azure.microsoft.com/develop/python/how-to-guides/service-bus-topics/) 
  - [服务管理](https://azure.microsoft.com/develop/python/how-to-guides/service-management/)  

## <a name="scientific-computing"></a>科学计算

除所有 Python 数据科学家库以外，Python Tools for Visual Studio 也支持 IPython 和 IPython 笔记本（可以在 Azure 中托管）。

我们建议从[加利福尼亚大学欧文分校](https://www.lfd.uci.edu/~gohlke/pythonlibs/#scipy-stack)获取 IPython 和科学计算库（matplotlib、scipy、numpy 等）。  
  
## <a name="see-also"></a>请参阅  

[PTVS 入门：设置 Visual Studio](../python/getting-started-with-ptvs-setting-up-visual-studio.md)
[PTVS 入门：开始编码（项目）](../python/getting-started-with-ptvs-start-coding-projects.md)
[PTVS 入门：编辑代码](../python/getting-started-with-ptvs-editing-code.md)
[PTVS 入门：调试](../python/getting-started-with-ptvs-debugging.md)
[PTVS 入门：交互式 Python](../python/getting-started-with-ptvs-interactive-python.md)
[PTVS 入门：在 Azure 中构建网站](../python/getting-started-with-ptvs-building-a-website-in-azure.md)
