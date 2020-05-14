---
title: 可视化 XAML UI 中的示例数据
titleSuffix: Blend for Visual Studio
ms.date: 03/06/2018
ms.topic: conceptual
ms.assetid: 87d31b6c-4607-4121-bb7d-cfc80390ab93
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0614552bbbadd9a472e0780db6f277d423446966
ms.sourcegitcommit: aa302af53de342e75793bd05b10325939dc69b53
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2020
ms.locfileid: "82921231"
---
# <a name="display-data-in-blend-for-visual-studio"></a>在 Blend for Visual Studio 中显示数据

自定义页面的布局时，可以在设计器中查看示例数据。 可以从头开始或使用现有类生成示例数据。 也可以连接到在连接到应用时出现在应用中的实时数据**。

> [!NOTE]
> Blend 中的**数据**面板仅支持面向 .NET Framework 的项目。 对于以 .NET Core 为目标的 UWP 项目或项目，不支持此方法。 

## <a name="generate-sample-data"></a>生成示例数据

若要生成示例数据，请打开 XAML 文档。 在 "**数据**" 面板中，选择 "**创建示例数据** ![" "](../designers/media/30540d76-7256-43ce-b5d9-4b2edf3d339f.png)创建示例数据" 图标按钮，然后选择 "**新建示例数据**"。

在“数据” **** 面板中定义数据的结构，然后将它绑定到任何页面上的 UI 元素。

![数据面板](../designers/media/496d7ebc-fe46-42f6-95a8-57b0e5be5d49.png)

如果希望示例数据在运行应用程序时出现在页面中，请选择 "**数据源选项** ![" "数据源选项](../designers/media/ae1fd260-4f84-420d-b196-45fde357d81d.png)" 图标，然后选择 "**运行应用程序时启用**"。

![“在运行应用程序时启用”菜单项](../designers/media/05d5356d-91bb-4e6b-b3f7-29b76852c4b3.png)

**观看简短视频：** ![播放图标](../designers/media/bldadminconsoleinitialconfigicon.PNG) [从头开始创建示例数据](https://www.bing.com/videos/search?q=blend%20data&qs=n&form=QBVR&pq=blend%20data&sc=8-7&sp=-1&sk=#view=detail&mid=F8F2449A76956D480FD2F8F2449A76956D480FD2)。

## <a name="generate-sample-data-from-a-class"></a>从类生成示例数据

如果已创建了描述数据结构的类，则可以从这些类生成示例数据。

若要从类生成示例数据，请打开 XAML 文档，然后在 "**数据**" 面板中，单击 **"创建示例数据** ![" "创建](../designers/media/30540d76-7256-43ce-b5d9-4b2edf3d339f.png)示例数据" 图标按钮，然后单击 "**从类创建示例数据**"。

**观看简短视频：** ![播放图标](../designers/media/bldadminconsoleinitialconfigicon.PNG) [通过 Blend 混合数据绑定](https://www.youtube.com/watch?v=LSwPB6CAvjg)。

## <a name="see-also"></a>另请参阅

- [使用 Blend for Visual Studio 创建 UI](../xaml-tools/creating-a-ui-by-using-blend-for-visual-studio.md)
