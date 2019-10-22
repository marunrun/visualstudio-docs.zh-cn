---
title: 如何：创建活动设计器库 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 5b62e092-63b3-462d-9d77-fb112482f45d
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 63404d3d81c44ac4b8308d949cdb87df419f2e04
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662869"
---
# <a name="how-to-create-an-activity-designer-library"></a>如何：创建活动设计器库
使用自定义活动设计器可为标准或自定义活动创建一个用户界面。 您可控制该用户界面的复杂度并且可为一个活动创建多个活动设计器。 此方案使您能创建适合多种受众的设计器。

### <a name="to-create-an-activity-designer-library"></a>创建活动设计器库

1. 启动 [!INCLUDE[vs2010](../includes/vs2010-md.md)]。

2. 在 "**文件**" 菜单上，指向 "**新建**"，然后选择 "**项目 ...** " 打开 "**新建项目**" 对话框。

3. 在 "**项目类型**" 窗格中，根据您的首选语言从**视觉对象C#** 或**Visual Basic**分组中选择 "**工作流**"。

4. 在 "**模板**" 窗格中，选择 "**活动设计器库**"。

5. 在 "**名称**" 框中，输入项目的描述性名称以便于识别。

6. 在 "**位置**" 框中，输入要保存项目的目录，或者单击 "**浏览**" 导航到该目录。

7. 在 "**解决方案**" 框中，键入解决方案的描述性名称，然后单击 **"确定"** 。

    > [!NOTE]
    > 如果要向现有解决方案添加工作流控制台应用程序，请在 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 中打开该解决方案，右键单击**解决方案资源管理器**中的解决方案，然后依次选择 "**添加**"、"**新建项目 ...** " 打开 "**新建项目**" 对话框。 按照此过程中的上述步骤继续操作。

8. 该项目模板将在 XAML 中创建一个活动设计器定义并在源代码中创建代码隐藏实现文件。 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 将打开并显示活动设计器的画布。

9. 将 [!INCLUDE[avalon1](../includes/avalon1-md.md)] 控件从**工具箱**拖到设计图面以在您的自定义活动设计器中使用它们。  有关如何实现自定义活动设计器的示例，请参阅[如何：创建自定义活动设计器](https://msdn.microsoft.com/library/2f3aade6-facc-44ef-9657-a407ef8b9b31)。

    > [!WARNING]
    > 自定义活动设计器可用于自定义活动以及默认 [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)]activities。

## <a name="see-also"></a>请参阅
 [创建工作流项目](../workflow-designer/creating-a-workflow-project.md)