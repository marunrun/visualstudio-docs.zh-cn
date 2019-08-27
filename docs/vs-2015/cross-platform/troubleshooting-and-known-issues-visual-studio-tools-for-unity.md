---
title: 疑难解答和已知问题 (Visual Studio Tools for Unity) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-unity-tools
ms.topic: troubleshooting
ms.assetid: 8f5db192-8d78-4627-bd07-dbbc803ac554
caps.latest.revision: 7
author: conceptdev
ms.author: crdun
manager: jillfra
ms.openlocfilehash: 6e1b34cbc2497bd70f65021c83db4f59480519f1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62573201"
---
# <a name="troubleshooting-and-known-issues-visual-studio-tools-for-unity"></a>疑难解答和已知问题 (Visual Studio Tools for Unity)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本部分将介绍 Visual Studio Tools for Unity 常见问题的解决方案、已知问题的说明并了解如何通过报告错误来帮助改进 Visual Studio Tools for Unity。  
  
## <a name="troubleshooting"></a>疑难解答  
 若要解决 Visual Studio Tools for Unity 的一些常见问题，请参阅以下各部分。  
  
### <a name="migrating-from-unityvs-to-visual-studio-tools-for-unity"></a>从 UnityVS 迁移到 Visual Studio Tools for Unity  
 如果从 UnityVS 迁移到 Visual Studio Tools for Unity，将需要为你的 Unity 项目生成新的 Visual Studio 解决方案。  
  
##### <a name="to-migrate-your-unity-project-from-unityvs-18-to-visual-studio-tools-for-unity-19"></a>若要将 Unity 项目从 UnityVS 1.8 迁移到 Visual Studio Tools for Unity 1.9  
  
1. 从 Unity 项目中将旧的解决方案和项目文件删除。 在 Unity 项目的根目录中，找到 Visual Studio .sln 和 .*proj 文件并将其全部删除。  
  
2. 将 Visual Studio Tools for Unity 包导入 Unity 项目中。 有关如何导入 VSTU 包的信息，请参阅 [入门](../cross-platform/getting-started-with-visual-studio-tools-for-unity.md) 页面上的“配置 Visual Studio Tools for Unity”。  
  
3. 生成新的解决方案和项目文件。 如果想要立即生成它们，则在 Unity 编辑器中的主菜单上，选择“Visual Studio Tools” 、“生成项目文件” 。 或者如果愿意，可以跳过此步骤；当选择“Visual Studio Tools” 、“在 Visual Studio 中打开” 时，Visual Studio Tools for Unity 会自动生成新的文件。  
  
### <a name="visual-studio-wont-load-the-solution-that-visual-studio-tools-for-unity-created"></a>Visual Studio 不会加载 Visual Studio Tools for Unity 创建的解决方案  
 有关详细信息，请参阅 [此 stackoverflow 问题的答案](http://stackoverflow.com/a/24035907/36702)。  
  
### <a name="on-windows-8-visual-studio-asks-to-download-the-unity-target-framework"></a>在 Windows 8 上，Visual Studio 会要求下载 Unity 目标框架  
 UnityVS 要求安装默认情况下 Windows 8 上未安装的 .net framework 3.5。 若要解决此问题，请按照说明下载并安装 .net framework 3.5。  
  
## <a name="known-issues"></a>已知问题  
 在 Visual Studio Tools for Unity 中存在一些已知问题，是由调试器与 Unity 的旧版本的 C# 编译器的交互方式导致的。 我们正设法帮助解决这些问题，但在此期间，你可能会遇到以下问题。  
  
- 在调试时，Unity 有时会崩溃。  
  
- 在调试时，Unity 有时会冻结。  
  
- 有时单步执行和跳出方法的方式不正确，尤其是在迭代器中或在 switch 语句内。  
  
## <a name="reporting-errors"></a>报告错误  
 请在遇到崩溃、冻结或其他错误时发送错误报告以帮助我们改进 Visual Studio Tools for Unity 的质量。 这可以帮助我们调查并修复 Visual Studio Tools for Unity 中的问题。 谢谢！  
  
### <a name="how-to-report-an-error-when-visual-studio-freezes"></a>如何在 Visual Studio 冻结时报告错误  
 有报告表明使用 Visual Studio Tools for Unity 进行调试时 Visual Studio 有时会冻结，但我们需要更多的数据来了解这个问题。 你可以通过执行下面的步骤来帮助我们调查。  
  
##### <a name="to-report-that-visual-studio-freezes-while-debugging-with-visual-studio-tools-for-unity"></a>报告使用 Visual Studio Tools for Unity 进行调试时 Visual Studio 会冻结  
  
1. 打开 Visual Studio 的新实例。  
  
2. 打开“附加到进程”对话框。 在 Visual Studio 的新实例中的主菜单上，选择“调试” 、“附加到进程” 。  
  
3. 将调试器附加到 Visual Studio 的已冻结的实例。 在“附加到进程”  对话框中，从“可用进程”  表中选择 Visual Studio 的已冻结实例，然后选择“附加”  按钮。  
  
4. 暂停调试器。 在 Visual Studio 的新实例中的主菜单上，选择“调试” 、“全部中断”  或仅按 **“Ctrl + Alt + Break”**。  
  
5. 创建线程转储。 在命令窗口中，输入以下命令并按“Enter” 。  
  
   ```powershell  
   Debug.ListCallStack /AllThreads /ShowExternalCode  
   ```  
  
    你可能首先需要使“命令”  窗口可见。 在 Visual Studio 中的主菜单上，选择“视图” 、“其他窗口” 、“命令窗口” 。  
  
6. 最后，将线程转储以及 Visual Studio 冻结时你正在执行的操作的说明一起发送到 [vstusp@microsoft.com](mailto:vstusp@microsoft.com)。
