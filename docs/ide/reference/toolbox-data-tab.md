---
title: 工具箱，“数据”选项卡
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Toolbox, Data tab
- Data tab, Toolbox
- data [Visual Studio], Toolbox
ms.assetid: 2ae38b2a-29d2-461c-a67d-29dad274bf45
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e79b80890925bdf4d6d191db759516b5545fc403
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590249"
---
# <a name="toolbox-data-tab"></a>工具箱，“数据”选项卡

显示可添加到窗体和组件的数据对象。 创建具有关联设计器的项目时，将会显示“工具箱”的“数据”选项卡   。 默认情况下，“工具箱”将出现在 Visual Studio 集成开发环境中；如果需要显示“工具箱”，请从“视图”菜单中选择“工具箱”     。

> [!TIP]
> 运行“数据源配置向导”将自动创建和配置大部分数据项。 有关详细信息，请参阅[添加新数据源](../../data-tools/add-new-data-sources.md)。

## <a name="ui-element-list"></a>UI 元素列表

要直接转到某个组件的 .NET 引用页，请针对“工具箱”中的项或设计器栏中的组件项按 F1   。

|“属性”|描述|
|----------|-----------------|
|<xref:System.Data.DataSet>|向窗体或组件中添加类型化或非类型化数据集的实例。 将此对象拖到设计器上后，它将显示一个对话框，可在其中选择一个现有的类型化数据集类或指定希望创建新的非类型化空数据集。 **注意：** 不要使用“工具箱”上的 <xref:System.Data.DataSet> 对象创建新的类型化数据集架构和类  。 有关详细信息，请参阅[创建和配置数据集](../../data-tools/create-and-configure-datasets-in-visual-studio.md)。|
|<xref:System.Windows.Forms.DataGridView>|提供一种以表格格式显示数据的功能强大且灵活的方法。|
|<xref:System.Windows.Forms.BindingSource>|简化将控件绑定到基础数据源的过程。|
|<xref:System.Windows.Forms.BindingNavigator>|表示窗体上绑定到数据的控件的导航和操作用户界面 (UI)。|

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中访问数据](../../data-tools/accessing-data-in-visual-studio.md)
- [适用于 NET 的 Visual Studio Data Tools](../../data-tools/visual-studio-data-tools-for-dotnet.md)
- [Visual Studio 中的数据集工具](../../data-tools/dataset-tools-in-visual-studio.md)
- [在 Visual Studio 中将控件绑定到数据](../../data-tools/bind-controls-to-data-in-visual-studio.md)
- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [编辑数据集中的数据](../../data-tools/edit-data-in-datasets.md)
- [验证数据集中的数据](../../data-tools/validate-data-in-datasets.md)
