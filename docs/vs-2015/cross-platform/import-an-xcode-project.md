---
title: 导入 XCode 项目 | Microsoft Docs
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: aa4b8161-d98f-4a1a-9db3-520133bfc82f
caps.latest.revision: 10
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: 4faa2ecae7f53d29e6aad92723ca6d12e50e2812
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150902"
---
# <a name="import-an-xcode-project"></a>导入 XCode 项目
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在适用于跨平台移动开发的 Microsoft Visual C++ 中，支持将 XCode 项目移动到 Visual Studio，可在此处创建跨平台库并与其他项目共享代码。 通过“从 XCode 导入”向导，可更轻松地导入项目和拆分 XCode 目标中的 C++ 代码，使其用作静态库或共享代码项目。 可在 Visual Studio 中管理特定于 iOS 的代码，还可继续使用 XCode 处理情节提要和生成操作。 若要了解如何轻松地在 Visual Studio 和 XCode 之间来回移动代码，请参阅“在 XCode 和 Visual Studio 间移动更改”。  
  
## <a name="using-the-import-from-xcode-wizard"></a>使用“从 XCode 导入”向导  
 本主题介绍了如何将 XCode 项目移动到 Visual Studio 中以利用代码共享和跨平台解决方案。 但首先必须将 Mac 与 Visual Studio 进行配对，以便可导入、导出和构建项目。 有关如何设置配对的说明，请参阅 [安装和配置工具以使用 iOS 进行生成](../cross-platform/install-and-configure-tools-to-build-using-ios.md)。 还必须通过网络共享 XCode 项目或将其移动到 Visual Studio 计算机，才可使用“从 XCode 导入”向导。  
  
#### <a name="import-from-xcode"></a>从 XCode 导入  
  
1. 在“文件”**** 菜单上，依次选择“新建”****、“导入”**** 和“从 XCode 导入”****。 这将启动“从 XCode 导入”**** 向导对话框。  
  
    ![选择要导入的 XCode 目标项目](../cross-platform/media/cppmdd-u2-importxcode-choose.PNG "CPPMDD_U2_ImportXCode_Choose")  
  
2. 在“选择项目”窗格中，选择“浏览”按钮以选择 XCode .pbxproj 文件****。 导航到“选择 XCode 项目文件”**** 对话框中的项目文件，然后选择“打开”****。  
  
    ![在“选择 Xcode 项目文件”对话框中选择一个项目文件](../cross-platform/media/cppmdd-u2-importxcode-browse.PNG "CPPMDD_U2_ImportXCode_Browse")  
  
    在“从 XCode 导入”向导中，选择“下一步”****。  
  
3. 在“多目标”**** 窗格中，选择要导入到 Visual Studio 项目的 XCode 项目目标。 XCode 目标与 Visual Studio 项目类似；大多数是生成二进制项的代码和资源的集合。 “从 XCode 导入”向导只允许导入生成二进制项（而非静态库）的目标作为多目标。 下一步将讨论 XCode 静态库目标。  
  
    !["从 XCode 导入" 向导目标窗格](../cross-platform/media/cppmdd-u2-importxcode-destination.jpg "CPPMDD_U2_ImportXCode_Destination")  
  
    对于在“要导入的目标”**** 中选择的每个目标，向导会自动检测可拆分为单独静态库项目的 C++ 代码文件，并将它们置于“C++ 项目项”**** 部分中。 其他代码和资源保留在“XCode 项目项”**** 部分中。 向导完成导入过程时，它们将成为 Visual Studio 中的单独静态库和应用程序项目。 默认情况下，单元测试和框架目标不会被向导拆分为单独的项目。  
  
    若要更改每个项目中要包含的文件，请使用向上和向下按钮。 若对每个项目中的文件均感到满意，请选择“下一步”**** 继续操作。  
  
4. 在“库目标”**** 窗格中，选择要导入到 Visual Studio 项目的 XCode 项目静态库目标。 在此窗格中，可选择要放在共享代码项目中的文件和要放在静态库项目中的文件。 在“要导入的目标”**** 列表下的每个目标中，可通过向上和向下按钮控制要放入“共享代码项目项”**** 和“静态库项目项”**** 的文件。  
  
    !["从 XCode 库导入" 目标窗格](../cross-platform/media/cppmdd-u2-importxcode-library.jpg "CPPMDD_U2_ImportXCode_Library")  
  
    共享代码项目是一种在 Visual Studio 的项目间共享一组源代码文件的方式。 代码随附其所在的项目一并生成，而不是作为自己的项目生成。 由于包含共享代码的项目可能具有不同的体系结构和配置，因此最好采用此方法提供包含可针对多种平台构建的代码的单个项目。  
  
    若对每个项目中的文件均感到满意，请选择“下一步”**** 继续操作。  
  
5. “全局属性”**** 窗格可用于为 Visual Studio 中的所有 iOS 项目设置框架搜索路径和 include 标头搜索路径。 Visual Studio 将这些路径用于源代码浏览和 IntelliSense。 创建使用一组通用标头和框架的 iOS 项目时，这些全局路径很有用。  
  
    !["从 XCode 导入" 全局属性窗格](../cross-platform/media/cppmdd-u2-importxcode-global.jpg "CPPMDD_U2_ImportXCode_Global")  
  
    还可在 Visual Studio 的“选项”**** 对话框中设置这些全局路径。 可在“工具”**** 菜单上选择“选项”**** 进行查找。 在“选项”**** 对话框中，展开“跨平台”****、“C++”****、“iOS”**** 和“全局属性”****。  
  
    选择“下一步”  继续。  
  
6. “框架”**** 窗格可用于配置 Visual Studio 进行浏览和 IntelliSense 处理项目时所用的路径。 对于 XCode 项目引用的每个框架，这些路径必须可供 Visual Studio 访问。 向导会检查 XCode 项目中的框架引用，并显示 Visual Studio 能否找到框架。 Visual Studio 应可发现“全局属性”中设置的所有路径。 框架列表中列出了异常。 对于标有 X 的每个框架，请提供一个电脑可访问的路径，便于 Visual Studio 查找框架。 您可以使用 "浏览" 按钮（"..."）来查找**Select Folder**路径。 框架路径可以是本地副本，或者是 Mac 上可通过网络访问的共享。  
  
    !["从 XCode 框架导入" 窗格](../cross-platform/media/cppmdd-u2-importxcode-frameworks.jpg "CPPMDD_U2_ImportXCode_Frameworks")  
  
    选择“下一步”  继续。  
  
7. “项目设置”**** 窗格可用于针对向导创建的每个项目更改框架和 include 标头搜索路径。 可使用此窗格设置与全局设置不同的项目特定路径。  
  
    若要为特定项目设置路径，请在“目标项目”**** 下拉列表中选择项目文件，然后在“框架搜索路径”**** 和“Include 标头搜索路径”**** 控件中设置值。 你可以使用每个控件旁边的浏览按钮 [...] 来使用 " **选择文件夹** " 对话框查找路径。  
  
    !["从 XCode 项目导入" 窗格](../cross-platform/media/cppmdd-u2-importxcode-projects.jpg "CPPMDD_U2_ImportXCode_Projects")  
  
    如果 Visual Studio 中没有与此电脑配对的远程 Mac，则会显示“配置远程计算机”链接。 有关如何设置配对的说明，请参阅 [安装和配置工具以使用 iOS 进行生成](../cross-platform/install-and-configure-tools-to-build-using-ios.md)。  
  
    若要使用向导设置导入 XCode 项目，请选择“导入”****。  
  
   “从 XCode 导入”向导会在 Visual Studio 中创建与所选 XCode 项目目标对应的项目。 可与其他 C++ 项目共享的代码会拆分为单独的共享代码和静态库项目。 剩下的代码将放置在可由 Visual Studio 远程生成的 iOS 库和应用程序项目中。 有关在 Visual Studio 和 XCode 之间移动代码的详细信息，请参阅 [在 XCode 和 Visual Studio 之间同步更改](../cross-platform/sync-changes-between-xcode-and-visual-studio.md)。
