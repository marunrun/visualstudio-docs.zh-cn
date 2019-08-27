---
title: “选项”对话框 ->“项目和解决方案” | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Projects and Solutions Options dialog box
- Options dialog box, Projects and Solutions
ms.assetid: 2801f24e-a138-488a-ae3c-e1f99a678ac0
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 2bdcfc2f6a4b7655a6f4f2e335310e938e5acfed
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65701983"
---
# <a name="projects-and-solutions-options-dialog-box"></a>“选项”对话框 ->“项目和解决方案”
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

设置 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 项目文件夹的默认路径，并在开发和生成项目时确定“输出”窗口、“任务列表”和“解决方案资源管理器”的默认行为。 若要访问此对话框，请单击“工具/选项”，展开“项目和解决方案”，然后单击“常规”。  
  
> [!NOTE]
> 对话框中的可用选项以及显示的菜单命令的名称和位置可能与“帮助”中的描述不同，具体取决于您的当前设置或版本。 此帮助页是根据“常规开发设置”而编写的。 若要查看或更改设置，请在“工具”菜单上选择“导入和导出设置”。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## <a name="settings"></a>设置  
 **项目位置**  
 设置在其中创建新的项目和解决方案文件夹以及目录的默认位置。 几个对话框还使用此选项中为文件夹起始点设置的位置。 例如，“打开项目”对话框将此位置用于“我的项目”的快捷方式。  
  
 **用户项目模板位置**  
 设置“新建项目”对话框中使用的默认位置来创建“我的模板”的列表。 有关详细信息，请参阅[如何：查找和组织模板](../../ide/how-to-locate-and-organize-project-and-item-templates.md)。  
  
 **用户项模板位置**  
 设置“添加新项”对话框中使用的默认位置来创建“我的模板”的列表。 有关详细信息，请参阅[如何：查找和组织模板](../../ide/how-to-locate-and-organize-project-and-item-templates.md)。  
  
 **如果生成完成时出现错误，则始终显示错误列表**  
 仅当项目无法生成时，在完成生成时将打开“错误列表”窗口。 将显示在生成过程中发生的错误。 如果清除此选项，则仍将发生错误，但在完成生成时窗口将不会打开。 默认情况下会启用此选项。  
  
 **跟踪解决方案资源管理器中的活动项**  
 当选中时，“解决方案资源管理器”将自动打开，活动项处于选中状态。 选定的项根据您在项目或解决方案中使用的不同文件或设计器中的不同组件而不同。 清除此选项后，“解决方案资源管理器”中的所选内容不会自动更改。 默认情况下会启用此选项。  
  
 **显示高级生成配置**  
 当选中时，生成配置选项显示在“项目属性页”对话框和“解决方案属性页”对话框中。 如果未选中，对于包含一个配置或两个配置调试和发布的 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 和 [!INCLUDE[csprcs](../../includes/csprcs-md.md)] 项目，生成配置选项将不显示在“项目属性页”对话框和“解决方案属性页”对话框中。 如果一个项目具有用户定义的配置，则会显示生成的配置选项。  
  
 未选中时，“生成”菜单上的命令（如“生成解决方案”、“重新生成解决方案”和“清理解决方案”）将在发布配置上执行，“调试”菜单上的命令（如“启动调试”和“启动但不调试”）将在调试配置上执行。  
  
 **总是显示解决方案**  
 如果选中，该解决方案和解决方案中执行的所有命令将始终显示在 IDE 中。 未选中时，如果该解决方案只包含一个项目，所有项目将作为独立项目创建，您不会看到在解决方案资源管理器中的解决方案或 IDE 中解决方案的执行命令。  
  
 **创建时保存新项目**  
 当选中时，你可以在“新建项目”对话框中为你的项目指定位置。 如果未选中，所有新项目将创建为临时项目。 当您正在使用临时项目时，您可以创建和试验项目，无需指定磁盘位置。  
  
 **当项目位置不受信任时警告用户**  
 如果您尝试在不完全信任的位置（例如，在 UNC 路径或 HTTP 路径）创建一个新项目或打开现有项目，将显示一条消息。 使用此选项以指定每次在不完全受信任的位置尝试创建或打开一个项目时是否显示该消息。  
  
 **在生成开始时显示输出窗口**  
 在解决方案生成一开始就在 IDE 中自动显示输出窗口。 有关详细信息，请参阅[如何：控制输出窗口](https://msdn.microsoft.com/library/91aebd15-8854-4a7a-9f7d-57376fb4e858)。 默认情况下会启用此选项。  
  
 **在重命名文件时提示重命名符号**  
 选定后，将显示一个消息框，询问是否[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]还应该将项目中的所有引用重命名为代码元素。  
  
## <a name="see-also"></a>请参阅  
 [“选项”对话框 ->“项目和解决方案”->“生成和运行”](../../ide/reference/options-dialog-box-projects-and-solutions-build-and-run.md)
