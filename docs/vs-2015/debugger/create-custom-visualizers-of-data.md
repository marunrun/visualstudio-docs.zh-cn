---
title: 创建数据的自定义可视化工具 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.visualizer.troubleshoot
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, visualizers
- visualizers
ms.assetid: c24c006f-f2ac-429f-89db-677fc0c6e1ea
caps.latest.revision: 31
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 50df868f0e01d49d4c49bccae32d743d5291a066
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840684"
---
# <a name="create-custom-visualizers-of-data"></a>创建数据的自定义可视化工具
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可视化工具是 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 调试器用户界面的组件。 *可视化工具*创建一个对话框或其他界面，以根据其数据类型的方式来显示变量或对象。 例如，HTML 可视化工具解释 HTML 字符串，并按照该字符串出现在浏览器窗口中时的样子显示结果；位图可视化工具解释位图结构并显示该位图结构表示的图形。 某些可视化工具允许您修改数据，还允许您查看数据。  
  
 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 调试器包括六个标准可视化工具。 它们分别是文本可视化工具、HTML 可视化工具、XML 可视化工具 和 JSON 可视化工具、WPF 树可视化工具以及数据集可视化工具，前四种均用于字符串对象，第五种用于显示 WPF 对象可视化树的属性，最后一种用于 DataSet、DataView 和 DataTable 对象。 将来可以从 Microsoft Corporation 以及第三方和社区下载更多的可视化工具。 此外，你可以编写自己的可视化工具，并将它们安装在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 调试器中。  
  
> [!NOTE]
> 在应用 **商店** 应用中，仅支持标准文本、HTML、XML 和 JSON 可视化工具。 不支持自定义（用户创建的）可视化工具。  
  
 可视化工具在调试器中用放大镜图标表示。 在 **数据提示**中，在调试器变量窗口或 " **快速监视** " 对话框中看到放大镜图标时，可以单击放大镜来选择适合相应对象的数据类型的可视化工具。  
  
 Compact Framework 上不支持可视化工具。  
  
> [!NOTE]
> 调试器可视化工具要求比部分信任的应用程序允许的特权更大的特权。 因此，在部分信任的代码中停止时，可视化工具不会加载。 若要使用可视化工具进行调试，必须运行完全信任的代码。  
  
## <a name="in-this-section"></a>本节内容  
 [如何：编写可视化工具](../debugger/how-to-write-a-visualizer.md)  
  
 [演练：用 C# 编写可视化工具](../debugger/walkthrough-writing-a-visualizer-in-csharp.md)  
  
 [如何：安装可视化工具](../debugger/how-to-install-a-visualizer.md)  
  
 [如何：测试和调试可视化工具](../debugger/how-to-test-and-debug-a-visualizer.md)  
  
 [可视化工具 API 参考](../debugger/visualizer-api-reference.md)  
  
## <a name="related-sections"></a>相关章节  
 [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)
