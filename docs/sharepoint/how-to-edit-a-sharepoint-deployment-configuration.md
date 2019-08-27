---
title: 如何：编辑 SharePoint 部署配置 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.DeploymentConfig
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ffa7923bbe7e8a7b44fec280a5528ab023feed37
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444703"
---
# <a name="how-to-edit-a-sharepoint-deployment-configuration"></a>如何：编辑 SharePoint 部署配置
  您可以创建部署配置或修改现有的部署配置。 例如，无法运行单步执行或更改的部署过程中的步骤顺序。 您可能想要创建或修改部署配置，因为不能更改的内置和以编程方式添加了配置。

## <a name="create-a-sharepoint-deployment-configuration"></a>创建 SharePoint 部署配置

#### <a name="to-create-a-sharepoint-deployment-configuration"></a>若要创建的 SharePoint 部署配置

1. 在中**解决方案资源管理器**，选择 SharePoint 项目，，然后，在菜单栏上选择**项目**， _ProjectName_**属性**。

2. 上**SharePoint**选项卡上，选择**新建**按钮。

     **添加新的部署配置**对话框随即出现。

3. 在中**名称**文字框中，输入部署配置的名称。

4. 在**可用的部署步骤**窗格中，选择你想要添加到部署配置，请选择的步骤 (**>**) 按钮，，然后选择**确定**按钮。

    > [!NOTE]
    > 如果已配置预先部署命令或后期部署命令，这些步骤将运行仅当将它们添加到自定义的部署配置。

## <a name="change-the-active-deployment-configuration"></a>更改活动部署配置

#### <a name="to-change-the-active-deployment-configuration"></a>若要更改活动部署配置

1. 在中**解决方案资源管理器**，选择 SharePoint 项目，，然后，在菜单栏上选择**项目** > **\<*ProjectName*> 属性**。

2. 选择**SharePoint**选项卡。

3. 在中**活动部署配置**列表框中，选择你想要使用的部署配置的名称。

## <a name="see-also"></a>请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
