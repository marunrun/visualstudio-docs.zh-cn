---
title: 如何：添加资源文件 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- resource files [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, resource files
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e7b8394d0c21ed5a45639e4dad5fe3695aaccc27
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440013"
---
# <a name="how-to-add-a-resource-file"></a>如何：添加资源文件
  解决方案节点并在解决方案资源管理器功能节点的快捷菜单上是用于将资源文件添加的命令。 有关详细信息，请参阅[本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)。

### <a name="to-add-a-global-resource-file-to-a-sharepoint-solution"></a>若要将全局资源文件添加到 SharePoint 解决方案

1. 在[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，打开 SharePoint 解决方案。

2. 在中**解决方案资源管理器**，选择 SharePoint 项目节点，，然后，在菜单栏上选择**项目** > **添加新项**。

3. 在中**添加新项**对话框框中，选择**全局资源文件**模板，然后选择**添加**按钮。

   > [!NOTE]
   > 仅当选择 SharePoint 项目项时，将出现全局资源文件项目项模板。

4. 在中**添加资源**对话框框中，选择资源文件，例如英语 （美国） 区域性。

    此步骤将全局资源文件添加到你的解决方案中的格式，Resource_x_**。**<em>区域性</em><strong>。</strong>resx，如*Resource1.en US.resx*。

5. 当**资源编辑器**中打开[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，将资源添加到资源文件。

### <a name="to-add-a-feature-resource-file-to-a-sharepoint-feature"></a>若要将功能资源文件添加到 SharePoint 功能

1. 如果尚未在中打开 SharePoint 解决方案[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，打开解决方案。

2. 在中**解决方案资源管理器**，打开下的功能的名称的快捷菜单**功能**节点，然后选择**添加功能资源**。

     此步骤将资源文件添加到格式中的功能_ResourceFileName_**。**_区域性_**.resx**，如*Feature1.en US.resx*。

3. 当**资源编辑器**中打开[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，将资源添加到资源文件。

## <a name="see-also"></a>请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
