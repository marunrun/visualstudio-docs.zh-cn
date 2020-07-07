---
title: 如何：在 BDC 功能中包含自定义程序集 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 772cdbaca67cc82fc6b7eb2c5ef5adb6508df34a
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015253"
---
# <a name="how-to-include-a-custom-assembly-in-a-bdc-feature"></a>如何：在 BDC 功能中包含自定义程序集
  你的项目可以引用同一解决方案中其他项目的程序集。 但是，必须使用 "**将引用的程序集分配到 lobsystem** " 对话框将这些程序集添加到项目的功能文件中。

### <a name="to-include-a-custom-assembly-in-a-business-data-connectivity-bdc-feature"></a>在业务数据连接（BDC）功能中包含自定义程序集

1. 在**解决方案资源管理器**中，选择包含 BDC 模型的文件夹。

2. 在 **“视图”** 菜单上，单击 **“属性窗口”**。

3. 在 "**属性**" 窗口中，选择 "**程序集**" 属性，然后选择省略号按钮（![ASP.NET Mobile 设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")）。

     此时将显示 "**将引用的程序集分配给 lobsystem** " 对话框。

4. 在 "**选择程序集**" 列表中，选择自定义程序集。

    > [!NOTE]
    > 如果已将引用添加到包含程序集的项目中，则程序集仅出现在 "**将引用的程序集分配给 lobsystem** " 对话框中。 有关详细信息，请参阅[如何：使用 "添加引用" 对话框添加或删除引用](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)。

5. 在 "**引用属性**" 组中，打开为 " **LobSystem 范围**" 属性显示的列表，选择使用自定义程序集的方法的 LOB 系统，然后选择 **"确定"** 按钮。

    > [!NOTE]
    > 若要调试自定义程序集中的代码，则必须将程序集添加到解决方案包。 有关详细信息，请参阅[如何：添加和移除附加程序集](../sharepoint/how-to-add-and-remove-additional-assemblies.md)。

## <a name="see-also"></a>另请参阅
- [如何：使用资源文件指定本地化名称、属性和权限](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
- [如何：向 SharePoint 项目添加现有 BDC 模型文件](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
- [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)
- [如何：创建 BDC 模型](../sharepoint/how-to-create-a-bdc-model.md)
- [将业务数据 Integragte 到 SharePoint 中](../sharepoint/integrating-business-data-into-sharepoint.md)
