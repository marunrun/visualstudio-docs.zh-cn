---
title: 如何：创建 BDC 模型 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], creating a model
- Business Data Connectivity service [SharePoint development in Visual Studio], creating a model
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9126a0d3bb552f525247cbfb2243504a1effaa92
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435469"
---
# <a name="how-to-create-a-bdc-model"></a>如何：创建 BDC 模型
  可以通过使用这种项的模板并将模型添加到任何 SharePoint 项目来创建业务数据连接 (BDC) 模型。 有关详细信息，请参阅[创建的业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。 有关如何设计模型的详细信息，请参阅[设计的业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

### <a name="to-create-a-bdc-project"></a>若要创建 BDC 项目

1. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

    > [!NOTE]
    > 如果您的 IDE 设置为使用 Visual Basic 开发设置，请选择**文件** > **新项目**。

     **“新建项目”** 对话框随即打开。

2. 下**Visual Basic**或**Visual C#**，选择**Office/SharePoint**， **SharePoint 解决方案**。

3. 在中**模板**窗格中，选择**SharePoint 2013-空项目**项，，然后选择**确定**按钮。

     **SharePoint 自定义向导**随即打开。

4. 上**指定用于调试的网站和安全级别**页上，指定本地计算机上的 SharePoint 站点的 URL，选择**部署为场解决方案**选项按钮，然后选择**完成**按钮。

     将测试指定的 SharePoint 站点上的模型。

    > [!IMPORTANT]
    > 因为 BDC 模型仅支持场解决方案，您必须将项目部署为场解决方案。

     创建一个空 SharePoint 项目。

5. 在菜单栏上，依次选择“项目” > “添加新项”。

6. 在中**添加新项**对话框框中，选择**Office/SharePoint**节点。

7. 在 SharePoint 模板列表中，选择**业务数据连接模型 （仅场解决方案）**。

8. 在中**名称**框中，指定 BDC 模型的名称，然后选择**添加**按钮。

     一个**业务数据连接模型**项添加到项目。 默认情况下，模型将显示在 BDC 设计器中。 有关详细信息，请参阅[创建的业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

## <a name="see-also"></a>请参阅
- [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)
- [如何：将现有 BDC 模型文件添加到 SharePoint 项目](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
- [如何：使用资源文件指定本地化的名称、 属性和权限](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
- [如何：在 BDC 功能中包含自定义程序集](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)
- [将业务数据集成到 SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)
