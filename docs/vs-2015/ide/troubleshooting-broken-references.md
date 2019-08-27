---
title: 有关已损坏引用的疑难解答 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: troubleshooting
helpviewer_keywords:
- Visual C# projects, references
- Visual Basic projects, references
- troubleshooting references
- referencing files from projects
- referencing components, troubleshooting
ms.assetid: 00a9ade9-652e-40de-8ada-85f63cd183ee
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a436ffa96e6ca86479bdb5b4f91e30c386acc1a6
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65689298"
---
# <a name="troubleshooting-broken-references"></a>Troubleshooting Broken References
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果应用程序尝试使用损坏的引用，则会生成异常错误。 无法找到引用的组件是造成此错误的主要起因，但有几种情况可以将引用视为损坏。 下表中列出了这些情况：  
  
- 项目的引用路径不正确或不完整。  
  
- 已删除引用的文件。  
  
- 已重命名引用的文件。  
  
- 网络连接或身份验证失败。  
  
- 引用指向计算机上没有安装的 COM 组件。  
  
  下面列出了这些问题的补救措施。  
  
> [!NOTE]
> 使用项目文件的绝对路径引用程序集中的文件。 因此，在多开发人员环境下工作的用户可能会在其本地环境中缺少引用的程序集。 为了避免这些错误，在这些情况下最好添加项目到项目的引用。 有关详细信息，请参阅 [NIB 如何：使用“添加引用”对话框添加或删除引用](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)和[使用程序集编程](https://msdn.microsoft.com/library/25918b15-701d-42c7-95fc-c290d08648d6)。  
  
## <a name="reference-path-is-incorrect"></a>引用路径不正确  
 如果在不同计算机上共享项目，当组件位于每台计算机上的不同目录中时可能找不到某些引用。 引用存储时采用组件文件的名称（例如，MyComponent）。 向项目添加引用时，组件文件的文件夹位置（例如 C:\MyComponents\\）追加到 **ReferencePath** 项目属性。  
  
 打开项目时，它会尝试通过查找引用路径上的目录找到这些引用的组件文件。 如果在组件存储于其他目录（例如 D:\MyComponents\\）的计算机上打开项目，则无法找到该引用，并且任务列表中会出现错误。  
  
 若要解决此问题，可以删除损坏的引用，然后使用“添加引用”对话框替换引用。 另一种解决方案是使用项目的属性页中的“引用路径”项，并修改列表中的文件夹，以指向正确位置。 为每台计算机上的每位用户保留“引用路径”属性。 因此，修改引用路径不会影响项目中的其他用户。  
  
> [!TIP]
> 项目到项目的引用不存在这些问题。 因此，如果可以，请使用项目到项目的引用，而不是文件引用。  
  
#### <a name="to-fix-a-broken-project-reference-by-correcting-the-reference-path"></a>通过纠正引用路径修复损坏的项目引用  
  
1. 在“解决方案资源管理器”中，右键单击项目节点，然后单击“属性”。  
  
2. 随即显示“项目设计器”。  
  
3. 如果使用 Visual Basic，请选择“引用”页，并单击“引用路径”按钮。 在“引用路径”对话框中，键入包含要在“文件夹”字段中引用的项的文件夹路径，然后单击”添加文件夹”按钮。  
  
     或  
  
     如果使用 Visual C#，请选择“引用路径”页。 在“文件夹”字段中，键入包含要引用项的文件夹路径，然后单击”添加文件夹”按钮。  
  
## <a name="referenced-file-has-been-deleted"></a>引用的文件已删除  
 引用的文件可能已删除，并且不再存在于驱动器上。  
  
#### <a name="to-fix-a-broken-project-reference-for-a-file-that-no-longer-exists-on-your-drive"></a>针对不再存在于驱动器上的文件修复损坏的项目引用  
  
- 删除引用。  
  
- 如果引用位于计算机上的另一个位置，请从该位置读取它。  
  
- 有关详细信息，请参阅 [NIB 如何：使用“添加引用”对话框添加或删除引用](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)。  
  
## <a name="referenced-file-has-been-renamed"></a>引用的文件已重命名  
 引用的文件可能已重命名。  
  
#### <a name="to-fix-a-broken-reference-for-a-file-that-has-been-renamed"></a>针对已重命名的文件修复损坏的引用  
  
- 删除该引用，然后添加对重命名文件的引用。  
  
- 如果引用位于计算机上的另一个位置，则必须从该位置读取它。 有关详细信息，请参阅 [NIB 如何：使用“添加引用”对话框添加或删除引用](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)。  
  
## <a name="network-connection-or-authentication-has-failed"></a>网络连接或身份验证失败  
 可能有许多原因导致文件无法访问：例如，网络连接失败或身份验证失败。 每种原因可能有不同的解决方法；例如，可能需要联系本地管理员才能访问所需资源。 但是，删除引用和修复使用该引用的代码是一种始终可供选择的方法。 有关详细信息，请参阅 [NIB 如何：使用“添加引用”对话框添加或删除引用](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)。  
  
## <a name="com-component-is-not-installed-on-computer"></a>计算机上未安装 COM 组件  
 如果一个用户已添加对 COM 组件的引用，而第二个用户尝试在未安装此组件的计算机上运行代码，则第二个用户将收到引用已损坏的错误。 在第二台计算机上安装组件可更正此错误。 有关如何在项目中使用对 COM 组件的引用，请参阅 [.NET Framework 应用程序中的 COM 互操作性](https://msdn.microsoft.com/library/f5a72143-c268-4dff-a019-974ad940e17d)。  
  
## <a name="see-also"></a>请参阅  
 [项目设计器简介](https://msdn.microsoft.com/898dd854-c98d-430c-ba1b-a913ce3c73d7)   
 [项目设计器 ->“引用”页 (Visual Basic)](../ide/reference/references-page-project-designer-visual-basic.md)   
 [NIB 如何：使用“添加引用”对话框添加或删除引用](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)
