---
title: 如何：为专用库创建 Atom 源 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Atom feed, VSIX private galleries
- VSIX private galleries, Atom feed
ms.assetid: 5897f538-9c41-486f-97d9-a1976d20d9fd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c72fbf2d3973ffd84de1cf6f33788c43511c3ce4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711012"
---
# <a name="how-to-create-an-atom-feed-for-a-private-gallery"></a>如何：为专用库创建 Atom 源
您可以创建 Atom （RSS） 源到包含扩展的 Intranet 位置，并将源作为专用库添加到**扩展和更新**。 有关详细信息，请参阅[专用库](../extensibility/private-galleries.md)。

## <a name="create-an-atom-feed"></a>创建原子源
 要将 Atom 源创建为专用库，请首先将扩展名 *（.vsix*文件）收集到文件夹中。 如果需要，可以将它们组织到子文件夹中。 您还需要以下资源：

- 使扩展作为专用库可用的*atom.xml*文件。 有关如何将*Atom.xml*文件连接到**扩展和更新**的信息，请参阅[专用库](../extensibility/private-galleries.md)。

- 包含从扩展名中提取的任何图像文件的文件夹（例如，屏幕截图）。 *Atom.xml*文件包含指向这些图像的相对链接，以便它们在**扩展和更新**中可用。

  例如，假设您已将以下两个扩展收集到一个文件夹中：

- *Template_Wizard_239.vsix*，这是一个空的 VSIX 项目模板。

- *选择高亮显示.vsix*， 这是一个突出显示选定单词的所有实例的工具。

  *atom.xml*文件的内容类似于以下示例：

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

 请注意，两个链接标记是指生成的图像文件夹中的屏幕截图。

## <a name="see-also"></a>请参阅
- [私人画廊](../extensibility/private-galleries.md)
