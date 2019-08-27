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
ms.openlocfilehash: 6cac959fb4f9c52849e6e121943fd847deb923d0
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63427403"
---
# <a name="how-to-import-a-master-page-or-theme"></a>如何：导入母版页或主题
  您可以为页在 SharePoint 站点上一致的外观通过创建和使用母版页和主题。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 不提供模板，这些元素，但可以在 SharePoint Designer 中创建它们，然后将它们导入[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。 有关详细信息，请参阅[构建基块：页面和用户界面](http://go.microsoft.com/fwlink/?LinkID=182095)Microsoft 网站上。

### <a name="to-import-a-master-page-or-theme"></a>若要导入母版页或主题

1. 在[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]、 创建或打开一个 SharePoint 项目。

     有关如何创建一个 SharePoint 项目的信息，请参阅[SharePoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

2. 在菜单栏上，依次选择“项目” > “添加新项”。

3. 在中**添加新项**对话框框中，展开**SharePoint**节点，然后选择**2010年**节点。

4. 在 SharePoint 模板列表中，选择**模块**模板，然后指定该模块的名称。

     模块包含文件 （例如，母版页或主题文件） 以部署到 SharePoint 中指定的位置。

5. 在模块中，删除默认文件中，名为*Sample.txt*。

6. 选择在模块节点。

7. 在菜单栏上依次选择**项目** > **添加现有项**，然后选择主页面或主题文件。

     母版页文件扩展名为.master，并且主题文件带有.thmx 扩展名。

8. 如果添加了母版页，更改其**部署冲突解决方法**将设置为**自动**中模块的属性。

    > [!NOTE]
    > 如果主页面的名称与现有的主页面标记为默认母版页或自定义母版页的名称相同，则可能发生错误。 有关如何解决此问题的信息，请参阅[演练：导入自定义母版页和包含图像的站点页面](../sharepoint/walkthrough-import-a-custom-master-page-and-site-page-with-an-image.md)。

9. 在模块中，打开*Elements.xml*。

     必须更新*Elements.xml*要引用的母版页或主题添加文件。

10. 对于主页面中，使用以下标记替换现有模块标记。

    ```xml
    <Module Name="[Module Name]" Url="_catalogs/masterpage">
        <File Path="[Module Name]\[Master Page Name].master"
          Url="[Master Page Name].master" Type="GhostableInLibrary" />
    </Module>
    ```

     对于主题，将以下标记替换为现有模块标记。

    ```xml
    <Module Name="[Module Name]" Url="_catalogs/theme"
        <File Path="[Module Name]\[Theme Name].thmx" Url="[Theme
          Name].thmx" Type="GhostableInLibrary" />
    </Module>
    ```

     请确保将占位符值替换该模块的母版页或主题的实际名称。

     该属性`Type="GhostableInLibrary"`指示该项添加到内容数据库和`Url`模块的属性指定在 SharePoint 内容数据库中存储文件的位置。

11. 若要更改在母版页上的部署范围内**解决方案资源管理器**，打开功能设计器中中的功能文件，然后选择从新的部署范围**作用域**列表。

     值为**Web**母版页仅适用于当前项目中指定的网站的方式。 值为**站点**意味着对当前站点集合，其中包括所有子站点和根 web 应用主页面。 其他值不会应用。

    > [!NOTE]
    > 由于仅对网站集级别应用主题，我们建议，您不设置主题的作用域为任何内容而不**站点**。 如果在子站点中使用了主题，则可能发生错误。

12. 在菜单栏上依次选择**构建** > **部署解决方案**。

13. 若要验证是否已正确部署的文件，打开 SharePoint 站点中，选择**站点操作**菜单中，选择**站点设置**命令，然后再选择**母版页**链接或**主题**链接。

     母版页或主题的列表，其中包含主页面或已导入的主题。

## <a name="see-also"></a>请参阅
- [母版页](http://go.microsoft.com/fwlink/?LinkId=184955)
- [从现有的 SharePoint 网站导入项](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [为 SharePoint 创建页](../sharepoint/creating-pages-for-sharepoint.md)
- [使用模块包括解决方案中的文件](../sharepoint/using-modules-to-include-files-in-the-solution.md)
