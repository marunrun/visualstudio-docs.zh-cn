---
title: 如何：使用设计器创建 SharePoint Web 部件 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], designer
- Web Parts [SharePoint development in Visual Studio], adding
- Web Parts [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 354fe62914a8708ac63acdde7d30060aca8d52fe
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62966817"
---
# <a name="how-to-create-a-sharepoint-web-part-by-using-a-designer"></a>如何：使用设计器创建 SharePoint Web 部件
  可以通过添加创建的 web 部件**可视 Web 部件**向任何 SharePoint 项目项。 这可以向 web 部件添加控件和代码的 Visual Studio 中打开的 Visual Web Developer 设计器。 可视 web 部件功能上相同 web 部件一样。 唯一的区别是您设计 Visual Web Developer 设计器中的可视 web 部件。

### <a name="to-create-a-project-for-visual-web-parts"></a>若要创建的 visual web 部件项目

1. 在菜单栏上，依次选择“文件” >“新建” > “项目”。

     **“新建项目”** 对话框随即打开。

2. 在**新的项目**对话框中的，在**Visual C#** 或**Visual Basic**，展开**Office/SharePoint**节点，然后选择**SharePoint 解决方案**类别。

3. 在项目模板列表中，选择**SharePoint 2013-可视 Web 部件**，然后选择**确定**按钮。

     **SharePoint 自定义向导**出现。

4. 上**指定用于调试的网站和安全级别**页上，指定是在本地计算机的 SharePoint 站点的 URL，然后选择**完成**按钮。

     在中**解决方案资源管理器**，显示 web 部件。 在设计时 Visual Web Developer 设计器中的 web 部件之后, 将测试它在你指定的站点上。

### <a name="to-add-a-visual-web-part-to-an-existing-sharepoint-project"></a>若要将可视 web 部件添加到现有的 SharePoint 项目

1. 在菜单栏上，依次选择“项目” > “添加新项”。

2. 在中**添加新项**对话框框中，选择**Office/SharePoint**节点。

3. 在项目模板列表中，选择**可视 Web 部件**，将其命名，，然后选择**添加**按钮。

     在中**解决方案资源管理器**，显示 web 部件。 在设计时 Visual Web Developer 设计器中的 web 部件之后, 将测试它在你指定的站点上。

## <a name="see-also"></a>请参阅
- [为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)
- [如何：创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)
- [演练：为 SharePoint 创建 web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
- [演练：使用设计器为 SharePoint 创建 web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)
