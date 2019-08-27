---
title: 如何：创建。从现有的 Vsct 文件。启动 Ctc 文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, creating based on a .ctc file
ms.assetid: 700e80a4-c1e1-4178-af53-45e86dd2c08b
caps.latest.revision: 9
manager: jillfra
ms.openlocfilehash: 7b963436e9d968dd5ba3829e97d0fd0c52e49641
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443010"
---
# <a name="how-to-create-a-vsct-file-from-an-existing-ctc-file"></a>如何：创建。从现有的 Vsct 文件。启动 Ctc 文件
可以从现有的命令表 .ctc 源文件创建一个基于 XML 的 .vsct 文件。 通过执行此操作，可以利用基于 XML 的新 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 命令表 (VSCT) 编译器格式。  
  
### <a name="to-create-a-vsct-file-from-a-ctc-file"></a>从 .ctc 文件创建 .vsct  文件  
  
1. 获取 Perl 语言的副本。  
  
2. 获取 Perl 脚本 ConvertCTCToVSCT.pl，通常位于一份 *\<Visual Studio SDK 安装路径 >* \VisualStudioIntegration\Tools\bin 文件夹。  
  
3. 获取要转换的 .ctc 源文件的副本。  
  
4. 将这些文件放在同一个目录中。  
  
5. 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 命令提示窗口中，导航到该目录。  
  
6. 类型  
  
    ```  
    perl.exe ConvertCTCtoVSCT.pl PkgCmd.ctc PkgCmd.vsct  
    ```  
  
     其中，PkgCmd.ctc 是 .ctc 文件的名称，PkgCmd.vsct 是要创建的 .vsct 文件的名称。  
  
     这将创建一个新的 .vsct XML 命令表源文件。 可以像其他任何 .vsct 文件一样，使用 VSCT 编译器 Vsct.exe 来编译此文件。  
  
    > [!NOTE]
    > 可以通过重新格式化 XML 注释来提高 .vsct 文件的可读性。  
  
## <a name="see-also"></a>请参阅  
 [如何：创建。Vsct 文件](../extensibility/internals/how-to-create-a-dot-vsct-file.md)   
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)