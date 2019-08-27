---
title: 如何：创建活动设计器库 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 5b62e092-63b3-462d-9d77-fb112482f45d
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a51b4cdb67590b908bc406b78c04ddf0c5aa3e2f
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65694557"
---
# <a name="how-to-create-an-activity-designer-library"></a>如何：创建活动设计器库
使用自定义活动设计器可为标准或自定义活动创建一个用户界面。 您可控制该用户界面的复杂度并且可为一个活动创建多个活动设计器。 此方案使您能创建适合多种受众的设计器。  
  
### <a name="to-create-an-activity-designer-library"></a>创建活动设计器库  
  
1. 启动 [!INCLUDE[vs2010](../includes/vs2010-md.md)]。  
  
2. 上**文件**菜单，依次指向**新建**，然后选择**项目...** 若要打开**新的项目**对话框。  
  
3. 在**项目类型**窗格中，选择**工作流**眖**Visual C#** 或者**Visual Basic**具体取决于你首选的分组语言。  
  
4. 在中**模板**窗格中，选择**活动设计器库**。  
  
5. 在中**名称**框中，输入您的项目以使其容易识别的描述性名称。  
  
6. 在中**位置**框中，输入想要保存你的项目，或者单击的目录**浏览**以导航到它。  
  
7. 在中**解决方案**框中，键入描述性名称为您的解决方案，然后单击**确定**。  
  
    > [!NOTE]
    > 如果你想要添加到现有解决方案工作流控制台应用程序，打开该解决方案[!INCLUDE[vs2010](../includes/vs2010-md.md)]，右键单击解决方案中**解决方案资源管理器**，然后选择**添加**，然后**新建项目...** 若要打开**新的项目**对话框。 按照此过程中的上述步骤继续操作。  
  
8. 该项目模板将在 XAML 中创建一个活动设计器定义并在源代码中创建代码隐藏实现文件。 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 将打开并显示活动设计器的画布。  
  
9. 拖动[!INCLUDE[avalon1](../includes/avalon1-md.md)]控件从**工具箱**至设计图面上，若要在自定义活动设计器中使用它们。  有关如何实现自定义活动设计器的示例，请参阅[如何：创建自定义活动设计器](https://msdn.microsoft.com/library/2f3aade6-facc-44ef-9657-a407ef8b9b31)。  
  
    > [!WARNING]
    > 自定义活动设计器可以用于自定义活动以及默认[!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)]活动。  
  
## <a name="see-also"></a>请参阅  
 [创建工作流项目](../workflow-designer/creating-a-workflow-project.md)