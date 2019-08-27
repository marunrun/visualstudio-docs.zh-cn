---
title: 如何：调试可执行文件不属于 Visual Studio 解决方案 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
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
- debugging [Visual Studio], executables
- executable files, importing
- executable files, debugging outside of projects
ms.assetid: 3ea176e8-1ce5-42c4-b7a2-abe3a2765033
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e33233fd313cd6a73013ce55333a860663ddb601
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65704524"
---
# <a name="how-to-debug-an-executable-not-part-of-a-visual-studio-solution"></a>如何：调试可执行文件不属于 Visual Studio 解决方案
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有时可能需要调试不属于 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目的可执行文件。 它可能是在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 外部创建的可执行文件，也可能是从其他用户处接收到的可执行文件。  
  
 解决此问题的常见方法是在 Visual Studio 外部启动可执行文件并使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 调试器附加到该文件。 有关详细信息，请参阅[将附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)。  
  
 附加到应用程序需要手动执行一些步骤，因此要花几秒钟的时间。 这一微小的延迟意味着如果尝试调试在启动过程中发生的问题，则这种附加将不会有帮助。 此外，如果调试的程序不等待用户输入而迅速完成，则可能没有时间附加到程序。 如果安装了 [!INCLUDE[vcprvc](../includes/vcprvc-md.md)]，则可以为此类程序创建 EXE 项目。  
  
### <a name="to-create-an-exe-project-for-an-existing-executable"></a>为现有的可执行文件创建 EXE 项目  
  
1. 上**文件**菜单上，单击**打开**，然后选择**项目**。  
  
2. 在**打开项目**对话框中，单击下拉列表列出到下的一步**文件名**，然后选择**所有项目文件**。  
  
3. 找到可执行文件，并单击**确定**。  
  
     这将创建一个包含该可执行文件的临时解决方案。  
  
### <a name="to-import-an-executable-into-a-visual-studio-solution"></a>将可执行文件导入到 Visual Studio 解决方案  
  
1. 上**文件**菜单，依次指向**添加项目**，然后单击**现有项目**。  
  
2. 在**添加现有项目**对话框中，单击下拉列表列出到下的一步**文件名**，然后选择**所有项目文件**。  
  
3. 找到并选择可执行文件。  
  
4. 单击 **“确定”**。  
  
5. 选择执行命令，如启动可执行文件**启动**，从**调试**菜单。  
  
    > [!NOTE]
    > 并非所有编程语言都支持 EXE 项目。 如果需要使用此功能，请安装 [!INCLUDE[vcprvc](../includes/vcprvc-md.md)]。  
  
     调试没有源代码的可执行文件时，可用的调试功能将受到限制，无论是附加到正在运行的可执行文件还是将可执行文件添加到 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 解决方案中。 如果可执行文件在生成时没有兼容格式的调试信息，则可用功能将进一步受到限制。 如果有源代码，则最佳方法是将源代码导入到 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中并在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中创建可执行文件的调试版本。  
  
## <a name="see-also"></a>请参阅  
 [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)   
 [调试器安全](../debugger/debugger-security.md)   
 [DBG 文件](https://msdn.microsoft.com/91e449e9-8b65-4123-960f-2107cd1f1cfd)
