---
title: 如何：使用资源文件指定本地化名称、属性和权限 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], localize strings
- BDC [SharePoint development in Visual Studio], localize strings
- BDC [SharePoint development in Visual Studio], resource file
- Business Data Connectivity service [SharePoint development in Visual Studio], resource strings
- BDC [SharePoint development in Visual Studio], properties
- Business Data Connectivity service [SharePoint development in Visual Studio], properties
- Business Data Connectivity service [SharePoint development in Visual Studio], resource file
- BDC [SharePoint development in Visual Studio], resource strings
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a87cc8a3eb8f98ea19a87e93c37aae5303151ecf
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015399"
---
# <a name="how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions"></a>如何：使用资源文件指定本地化名称、属性和权限
  通过使用资源文件，您可以对在业务数据连接 (BDC) 模型中定义的对象提供本地化名称、定义属性和应用权限。 若要指定此信息，请将**业务数据连接资源**项添加到包含**业务数据连接模型**项的项目。 然后通过编辑资源文件的 XML 来指定名称、属性和权限。

### <a name="to-add-a-bdc-resource-file-to-a-sharepoint-project"></a>向 SharePoint 项目添加 BDC 资源文件

1. 在**解决方案资源管理器**中，展开 SharePoint 项目的文件夹，然后选择包含 BDC 模型的文件夹。

2. 在菜单栏上，选择 "**项目**" "  >  **添加新项**"。

3. 展开 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

4. 在 "**添加新项**" 对话框中，选择 "**业务数据连接资源项**"。

5. 在 "**名称**" 框中，指定资源文件的名称，然后选择 "**添加**" 按钮。

     扩展名为 .bdcr 的资源文件将添加到项目中并打开以进行编辑。

6. 添加 XML 以定义要应用 BDC 模型的本地化名称、属性和权限。

     有关如何定义这些元素的详细信息，请参阅[模型和资源文件](/previous-versions/office/developer/sharepoint-2010/aa674515(v=office.14))。

## <a name="see-also"></a>另请参阅
- [如何：向 SharePoint 项目添加现有 BDC 模型文件](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
- [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)
- [如何：创建 BDC 模型](../sharepoint/how-to-create-a-bdc-model.md)
- [如何：在 BDC 功能中包含自定义程序集](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)
- [将业务数据集成到 SharePoint 中](../sharepoint/integrating-business-data-into-sharepoint.md)
