---
title: 如何：在 BDC 功能中包含自定义程序集 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.BDC.Add_Assemblies_Dialog
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], add reference
- Business Data Connectivity service [SharePoint development in Visual Studio], custom assembly
- BDC [SharePoint development in Visual Studio], custom assembly
- BDC [SharePoint development in Visual Studio], add reference
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6de3313dad06c009244a8b784e81bf7d2a768c3b
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443119"
---
# <a name="how-to-include-a-custom-assembly-in-a-bdc-feature"></a>如何：在 BDC 功能中包含自定义程序集
  你的项目可以从同一解决方案中的其他项目引用程序集。 但是，您必须添加这些程序集到项目的功能文件通过使用**分配引用的程序集 Lobsystem 到**对话框。

### <a name="to-include-a-custom-assembly-in-a-business-data-connectivity-bdc-feature"></a>若要自定义程序集包含业务数据连接 (BDC) 功能

1. 在中**解决方案资源管理器**，选择包含 BDC 模型的文件夹。

2. 在 **“视图”** 菜单上，单击 **“属性窗口”**。

3. 在中**属性**窗口中，选择**程序集**属性，然后单击省略号按钮 (![ASP.NET 移动设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器椭圆"))。

     **分配引用的程序集 Lobsystem 到**对话框随即出现。

4. 在中**选择的程序集**列表中，选择自定义程序集。

    > [!NOTE]
    > 程序集只能出现在**分配引用的程序集 Lobsystem 到**对话框中，如果你已添加对包含程序集的项目的引用。 有关详细信息，请参阅[如何：添加或删除引用通过使用添加引用对话框中](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)。

5. 在**引用属性**组中，打开为显示列表**LobSystem 范围**属性中，选择的方法，使用自定义程序集，然后选择 LOB 系统**确定**按钮。

    > [!NOTE]
    > 若要调试自定义程序集中的代码，必须将程序集添加到解决方案包中。 有关详细信息，请参阅[如何：添加和删除其他程序集](../sharepoint/how-to-add-and-remove-additional-assemblies.md)。

## <a name="see-also"></a>请参阅
- [如何：使用资源文件指定本地化的名称、 属性和权限](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
- [如何：将现有 BDC 模型文件添加到 SharePoint 项目](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
- [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)
- [如何：创建 BDC 模型](../sharepoint/how-to-create-a-bdc-model.md)
- [在 SharePoint 中 Integragte 业务数据](../sharepoint/integrating-business-data-into-sharepoint.md)
