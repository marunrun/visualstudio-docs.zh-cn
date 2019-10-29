---
title: 如何：导入母版页或主题 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing items
- importing items [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2c5078d31e2dcb7f11e5c19e0f8cb228e2f75d50
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72984191"
---
# <a name="how-to-import-a-master-page-or-theme"></a>如何：导入母版页或主题
  您可以通过创建和使用母版页和主题，为您的 SharePoint 站点上的页面指定一致的外观。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 不提供这些元素的模板，但你可以在 SharePoint Designer 中创建模板，然后将其导入 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。 有关详细信息，请参阅 Microsoft 网站上的[构建基块：页面和用户界面](/previous-versions/office/developer/sharepoint-2010/ee539040(v=office.14))。

### <a name="to-import-a-master-page-or-theme"></a>导入母版页或主题

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中，创建或打开一个 SharePoint 项目。

     有关如何创建 SharePoint 项目的信息，请参阅[sharepoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

2. 在菜单栏上，依次选择“项目” > “添加新项”。

3. 在 "**添加新项**" 对话框中，展开 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

4. 在 SharePoint 模板列表中，选择 "**模块**" 模板，然后指定模块的名称。

     模块包含用于部署到你在 SharePoint 中指定的位置的文件（例如，母版页或主题文件）。

5. 在模块中，删除名为*test.txt*的默认文件。

6. 选择 "模块" 节点。

7. 在菜单栏上，选择 "**项目** > "**添加现有项**"，然后选择母版页或主题文件。

     母版页文件具有扩展名 .master，主题文件具有扩展名 thmx。

8. 如果已添加母版页，请在模块的属性中将其 "**部署冲突解决方法**" 设置更改为 "**自动**"。

    > [!NOTE]
    > 如果母版页名称与已标记为默认母版页或自定义母版页的现有母版页的名称相同，则会发生错误。 有关如何解决此问题的信息，请参阅[演练：使用图像导入自定义母版页和网站页面](../sharepoint/walkthrough-import-a-custom-master-page-and-site-page-with-an-image.md)。

9. 在模块中，打开 "*元素 .xml*"。

     必须更新*元素 .xml*文件，才能引用所添加的母版页或主题。

10. 对于母版页，请将现有的模块标记替换为以下标记。

    ```xml
    <Module Name="[Module Name]" Url="_catalogs/masterpage">
        <File Path="[Module Name]\[Master Page Name].master"
          Url="[Master Page Name].master" Type="GhostableInLibrary" />
    </Module>
    ```

     对于主题，请将现有的模块标记替换为以下标记。

    ```xml
    <Module Name="[Module Name]" Url="_catalogs/theme"
        <File Path="[Module Name]\[Theme Name].thmx" Url="[Theme
          Name].thmx" Type="GhostableInLibrary" />
    </Module>
    ```

     请确保将占位符值替换为模块和母版页或主题的实际名称。

     特性 `Type="GhostableInLibrary"` 指示项已添加到内容数据库，模块的 `Url` 特性指定在 SharePoint 内容数据库中存储文件的位置。

11. 若要更改母版页的部署范围，请在**解决方案资源管理器**中打开功能设计器中的功能文件，然后从 "**作用域**" 列表中选择新的部署范围。

     值为 " **Web** " 表示母版页仅适用于当前在项目中指定的网站。 "**站点**" 值表示母版页适用于当前网站集，其中包括所有子网站和根 web。 其他值不适用。

    > [!NOTE]
    > 因为主题仅适用于网站集级别，所以建议您不要将主题的作用域设置为**网站**以外的任何内容。 如果子站点中使用主题，则会发生错误。

12. 在菜单栏上，选择 "**生成** > **部署解决方案**"。

13. 若要验证是否已正确部署这些文件，请打开 SharePoint 站点，选择 "**站点操作**" 菜单，选择 "**站点设置**" 命令，然后选择 "**母版页**" 链接或 "**主题**" 链接。

     母版页或主题的列表随即显示，其中包含已导入的母版页或主题。

## <a name="see-also"></a>请参阅
- [母版页](/previous-versions/office/developer/sharepoint-2010/ms443795(v=office.14))
- [从现有 SharePoint 站点导入项](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [创建 SharePoint 页面](../sharepoint/creating-pages-for-sharepoint.md)
- [使用模块在解决方案中包括文件](../sharepoint/using-modules-to-include-files-in-the-solution.md)
