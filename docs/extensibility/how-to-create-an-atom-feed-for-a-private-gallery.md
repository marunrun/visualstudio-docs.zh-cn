---
title: 如何：创建 Atom 馈送专用库 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Atom feed, VSIX private galleries
- VSIX private galleries, Atom feed
ms.assetid: 5897f538-9c41-486f-97d9-a1976d20d9fd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 027a7f70240695e64051ef6c16fd3e5469d75900
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66340889"
---
# <a name="how-to-create-an-atom-feed-for-a-private-gallery"></a>如何：创建 Atom 馈送专用库
您可以创建 Atom (RSS) 源到 intranet 位置包含扩展并添加到的源**扩展和更新**作为专用库。 有关详细信息，请参阅[专用库](../extensibility/private-galleries.md)。

## <a name="create-an-atom-feed"></a>创建 Atom 馈送
 若要创建 Atom 馈送作为专用库，则先收集你的扩展 ( *.vsix*文件) 的文件夹。 您可以将它们组织到子文件夹的前提。 您将需要以下资源：

- *Atom.xml*提供扩展作为专用库的文件。 有关如何连接信息*atom.xml*的文件**扩展和更新**，请参阅[专用库](../extensibility/private-galleries.md)。

- 包含已从扩展插件 （例如，屏幕截图） 中提取任何图像文件的文件夹。 *Atom.xml*文件，使他们能够在包含这些图像的相对链接**扩展和更新**。

  例如，假设您到文件夹收集了以下两个扩展：

- *Template_Wizard_239.vsix*，这是一个空的 VSIX 项目模板。

- *SelectionHighlight.vsix*，这是一个工具，可突出显示所选单词的所有实例。

  内容*atom.xml*文件将类似于下面的示例：

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

 请注意，这两个链接标记引用的映像的生成文件夹中的屏幕截图。

## <a name="see-also"></a>请参阅
- [专用库](../extensibility/private-galleries.md)
