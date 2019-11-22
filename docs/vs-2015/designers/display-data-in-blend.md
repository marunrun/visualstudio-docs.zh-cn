---
title: 显示 Blend 中的数据 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 87d31b6c-4607-4121-bb7d-cfc80390ab93
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2ed51eaef8594695d4d594401ab9375563525b10
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74294582"
---
# <a name="display-data-in-blend"></a>显示 Blend 中的数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

自定义页面的布局时，可以在设计器中查看示例数据。 可以从头开始或使用现有类生成示例数据。 也可以连接到在连接到应用时出现在应用中的 *实时数据* 。

 **本主题内容：**

- [生成示例数据](#Scratch)

- [从类生成示例数据](#Existing)

- [在 WPF 应用程序中显示实时数据](#LiveWPF)

- [在应用商店或 Phone 应用中显示实时数据](#LiveStore)

## <a name="Scratch"></a> 生成示例数据
 若要生成示例数据，请打开 XAML 文档。 In the **Data** panel, choose the **Create sample data**![](../designers/media/30540d76-7256-43ce-b5d9-4b2edf3d339f.png "30540d76-7256-43ce-b5d9-4b2edf3d339f") button, and then choose **New Sample Data**.

 在“数据” 面板中定义数据的结构，然后将它绑定到任何页面上的 UI 元素。

 ![](../designers/media/496d7ebc-fe46-42f6-95a8-57b0e5be5d49.png "496d7ebc-fe46-42f6-95a8-57b0e5be5d49")

 If you want your sample data to appear in your pages when you run the app, choose **Data source options** ![](../designers/media/ae1fd260-4f84-420d-b196-45fde357d81d.png "ae1fd260-4f84-420d-b196-45fde357d81d"), and then choose **Enable When Running Application**.

 ![](../designers/media/05d5356d-91bb-4e6b-b3f7-29b76852c4b3.png "05d5356d-91bb-4e6b-b3f7-29b76852c4b3")

 **Watch a short video:** ![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Create sample data from scratch](https://www.bing.com/videos/search?q=blend%20data&qs=n&form=QBVR&pq=blend%20data&sc=8-7&sp=-1&sk=#view=detail&mid=F8F2449A76956D480FD2F8F2449A76956D480FD2).

 **Watch a short video:** ![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Mixing up some data binding with Blend](https://www.youtube.com/watch?v=LSwPB6CAvjg).

## <a name="Existing"></a> 从类生成示例数据
 如果已创建了描述数据结构的类，则可以从这些类生成示例数据。

 To generate sample data from a class, open a XAML document, and then in the **Data** panel, click the **Create sample data**![](../designers/media/30540d76-7256-43ce-b5d9-4b2edf3d339f.png "30540d76-7256-43ce-b5d9-4b2edf3d339f") button, and then click **Create Sample Data from Class**.

 **Watch a short video:** ![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Create sample data from a class](https://channel9.msdn.com/Shows/Inside+Windows+Phone/IWP54--Windows-Phone-Data-Binding-and-the-Magic-of-XAML).

 **Watch a short video:** ![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Mixing up some data binding with Blend](https://www.youtube.com/watch?v=LSwPB6CAvjg).

## <a name="LiveWPF"></a> 在 WPF 应用程序中显示实时数据
 **Watch a short video:** ![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Create an XML data source](https://www.youtube.com/watch?v=RjQueappjqk&feature=youtube_gdata).

## <a name="LiveStore"></a> 在应用商店或 Phone 应用中显示实时数据
 请参阅 [使用数据和文件 (XAML)](https://msdn.microsoft.com/library/windows/apps/xaml/br229562.aspx)。

## <a name="see-also"></a>请参阅
 [使用 Blend for Visual Studio 创建 UI](../designers/creating-a-ui-by-using-blend-for-visual-studio.md)
