---
title: 如何：调试 Code Center Premium 源代码 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Code Center Premium
- debugging [Visual Studio], Code Center Premium
ms.assetid: 18b4769d-b007-4428-9dae-9e72c283ff0d
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: db9a3e08e14e7fadca6df9e32361c0b042f565e9
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438333"
---
# <a name="how-to-debug-with-code-center-premium-source"></a>如何：调试 Code Center Premium 源代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] 调试器可以调试来自 Microsoft MSDN Code Center Premium 的安全共享源。  
  
 本主题介绍如何在 Visual Studio 中设置和调试 Code Center Premium 源代码。  
  
### <a name="to-prepare-for-debugging-with-code-center-premium"></a>准备调试 Code Center Premium  
  
1. 连接您的智能卡读卡器，并插入您从共享源计划所取得的智能卡。  
  
2. 启动 Visual Studio。  
  
3. 在 **“工具”** 菜单上，单击 **“选项”**。  
  
4. 在中**选项**对话框中，打开**调试**节点，然后单击**常规**。  
  
5. 清除**启用仅我的代码 （仅限托管）** 复选框。  
  
6. 选择**启用源服务器支持**。  
  
7. 清除**要求源文件与完全匹配的原始版本**。  
  
8. 下**调试**节点中，单击**符号**。  
  
9. 在中**符号文件 (.pdb) 位置**框中，清除**Microsoft 服务器符号**复选框，并添加以下位置：  
  
     `https://codepremium.msdn.microsoft.com/symbols`  
  
     `src=https://codepremium.msdn.microsoft.com/source/Visual%20Studio%202010/SP1/`  
  
   > [!NOTE]
   > 请务必包括尾部反斜杠<strong>/</strong> 路径的末尾。  
  
     将这些位置移至列表顶端以确保首先加载这些符号。  
  
   > [!NOTE]
   > 必须先列出这些 Code Center Premium 位置，以使它们成为首先加载的位置。 在 Visual Studio 2010 中，不能将上述任何服务器移**Microsoft 符号服务器**条目，这就是原因必须清除该复选框。  
   > 
   >  若要在调试会话期间从 Microsoft 符号加载符号，请执行下列操作：  
   > 
   > 1. 上**调试**菜单中，选择**Windows** ，然后选择**模块**。  
   >    2.  选择需要其符号的模块，然后打开快捷菜单。 选择**负载从符号**，然后选择**Microsoft 符号服务器**。  
  
10. 在**缓存在此目录中的符号服务器中的符号**框中，输入一个位置，例如`C:\symbols`Code Center Premium 可以在其中缓存符号。 缓存符号可以大大提升调试期间的性能。  
  
     若在完成此过程之后使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 调试源代码遇到困难，请检查缓存位置以确认是否有之前缓存过的过时符号文件。 删除过时的符号文件。  
  
11. 单击 **“确定”**。  
  
12. 重新启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 以确保各项设置得以保留。  
  
### <a name="to-debug-your-source-code-using-attach-to-process"></a>使用“附加到进程”调试源代码  
  
1. 连接您的智能卡读卡器，并插入您从共享源计划所取得的智能卡。  
  
2. 启动 Visual Studio。  
  
3. 打开 Visual Studio 项目。  
  
4. 上**工具**菜单上，单击**附加到进程**。  
  
5. 在中**附加到进程**对话框中，单击**选择**。  
  
6. 在中**选择代码类型**对话框中的**检测以下代码类型**，选择**本机**，**托管**，和**托管 （v4.0)**。  
  
7. 单击**确定**以关闭**选择代码类型**对话框。  
  
8. 在中**可用进程**框中，选择你想要调试的进程。  
  
9. 单击 **“附加”**。  
  
10. 当系统提示确认你的证书时，单击**确定**。 然后输入您的 PIN。 如有相应提示，请接受 Code Center Premium 的使用条款。  
  
     根据网络速度，下载符号可能会占用大量时间。 所有符号下载成功之后，状态栏会有相应提示。  
  
11. 为解决方案中的所有托管项目重复执行附加步骤。  
  
### <a name="to-debug-source-code-from-an-existing-solution"></a>从现有解决方案调试源代码  
  
1. 在中**解决方案资源管理器**，打开解决方案的快捷菜单，然后选择**属性**。  
  
2. 在解决方案属性页对话框中，选择**调试源文件**中**通用属性**节点。  
  
3. 添加到以下位置**包含源文件的目录**列表：  
  
    `https://codepremium.msdn.microsoft.com/source/Visual%20Studio%202010/SP1/`  
  
   > [!NOTE]
   > 请务必包括尾部反斜杠<strong>/</strong> 路径的末尾。  
  
4. 对于解决方案中的每个托管项目，请执行下列操作  
  
   1. 在解决方案资源管理器，打开项目的快捷菜单，然后选择**属性**。  
  
   2. 选择**调试**，然后选择**启用非托管代码调试**。  
  
### <a name="to-debug-your-solution-with-code-center-premium-source"></a>调试解决方案的 Code Center Premium 源代码  
  
1. 在 `Package` 类中，在包构造函数上设置一个断点。  
  
2. 在中`Debug`菜单上，单击**启动调试**。  
  
3. 当命中包构造函数中的断点时，请转到**调用堆栈**窗口中，右键单击你想要加载的程序集的堆栈帧符号，然后单击**加载符号**。  
  
     双击调用帧以加载源代码。  
  
### <a name="to-browse-source-code-on-code-center-premium"></a>浏览 Code Center Premium 上的源代码  
  
1. 连接您的智能卡读卡器，并插入您从共享源计划所取得的智能卡。  
  
2. 启动 Internet Explorer 输入下列 URL：`https://codepremium.msdn.microsoft.com`  
  
3. 浏览找到所需的源代码。  
  
## <a name="see-also"></a>请参阅  
 [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)   
 [调试器安全](../debugger/debugger-security.md)   
 [Code Center Premium](https://www.microsoft.com/en-us/sharedsource/code-center-premium.aspx)
