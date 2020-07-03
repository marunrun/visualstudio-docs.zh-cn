---
title: 如何：创建专用库的 Atom 馈送 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Atom feed, VSIX private galleries
- VSIX private galleries, Atom feed
ms.assetid: 5897f538-9c41-486f-97d9-a1976d20d9fd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 269161e831fdb176dbfea844e951597efb467312
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905853"
---
# <a name="how-to-create-an-atom-feed-for-a-private-gallery"></a>如何：创建专用库的 Atom 馈送
你可以创建包含扩展的 intranet 位置的 Atom （RSS）源，并将源添加到作为专用库的**扩展和更新**中。 有关详细信息，请参阅[专用库](../extensibility/private-galleries.md)。

## <a name="create-an-atom-feed"></a>创建 Atom 馈送
 若要创建作为专用库的 Atom 源，首先需要将扩展（*.vsix*文件）收集到一个文件夹中。 如果需要，可以将它们组织到子文件夹中。 还需要以下资源：

- 一个*atom.xml*文件，该文件可将扩展作为专用库提供。 有关如何将*atom.xml*文件连接到**扩展和更新**的信息，请参阅[私有库](../extensibility/private-galleries.md)。

- 一个文件夹，其中包含从扩展中提取的任何图像文件（例如，屏幕截图）。 *atom.xml*文件包含指向这些映像的相对链接，以便它们可用于**扩展和更新**。

  例如，假设你已将以下两个扩展收集到一个文件夹中：

- *Template_Wizard_239 .vsix*，它是一个空的 vsix 项目模板。

- *SelectionHighlight*，它是用于突出显示所选单词的所有实例的工具。

  *atom.xml*文件的内容将与以下示例类似：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<feed xmlns="http://www.w3.org/2005/Atom">
  <title type="text" />
  <id>uuid:bcecded5-97c8-4d24-96f1-7d9e16652433;id=1</id>
  <updated>2011-04-14T21:25:48Z</updated>
  <entry>
    <id>SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa</id>
    <title type="text">Highlight all occurrences of selected word</title>
    <summary type="text">This extends the editor to highlight ....</summary>
    <published>2011-04-14T14:24:51-07:00</published>
    <updated>2011-04-14T14:24:22-07:00</updated>
    <author>
      <name>Microsoft</name>
    </author>
    <link rel="icon" href="VSIXImages/SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa_Icon_SelectionHighlightIcon.jpg" />
    <link rel="previewimage" href="VSIXImages/SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa_PreviewImage_SelectionHighlight.jpg" />
    <content type="application/octet-stream" src="SelectionHighlight.vsix" />
    <Vsix xmlns="http://schemas.microsoft.com/developer/vsx-syndication-schema/2010" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Id>SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa</Id>
      <Version>1.31</Version>
      <References />
      <Rating xsi:nil="true" />
      <RatingCount xsi:nil="true" />
      <DownloadCount xsi:nil="true" />
    </Vsix>
  </entry>
  <entry>
    <id>Template_Wizard_239.Microsoft.3b38a7e3-5cbc-4389-a92a-d82tyc2ed592</id>
    ...
  </entry>
</feed>
```

 请注意，这两个链接标记指的是生成的图像文件夹中的屏幕截图。

## <a name="see-also"></a>另请参阅
- [专用库](../extensibility/private-galleries.md)
