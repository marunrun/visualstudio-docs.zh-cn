---
title: 如何：创建 Atom 馈送专用库 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Atom feed, VSIX private galleries
- VSIX private galleries, Atom feed
ms.assetid: 5897f538-9c41-486f-97d9-a1976d20d9fd
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f6d4ba78028774e8fbf8e281afa2855781dab43a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204214"
---
# <a name="how-to-create-an-atom-feed-for-a-private-gallery"></a>如何：为专用库创建 Atom 馈送
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以创建 Atom (RSS) 源到 intranet 位置包含扩展并添加到的源**扩展和更新**作为专用库。 有关详细信息，请参阅[专用库](../extensibility/private-galleries.md)。  
  
## <a name="creating-an-atom-feed"></a>创建 Atom 馈送  
 若要创建 Atom 馈送作为专用库，你首先收集有关你的扩展 （.vsix 文件） 到一个文件夹。 您可以将它们组织到子文件夹的前提。 您将需要以下资源：  
  
- 提供扩展作为专用库 atom.xml 文件。 有关如何连接到 atom.xml 文件信息**扩展和更新**，请参阅[专用库](../extensibility/private-galleries.md)。  
  
- 包含已从扩展插件 （例如，屏幕截图） 中提取任何图像文件的文件夹。 Atom.xml 文件，使他们能够在包含这些图像的相对链接**扩展和更新**。  
  
  例如，假设您到文件夹收集了以下两个扩展：  
  
- Template_Wizard_239.vsix，这是一个空的 VSIX 项目模板。  
  
- SelectionHighlight.vsix，这是一个工具，可突出显示所选单词的所有实例。  
  
  Atom.xml 文件的内容将类似于下面的示例：  
  
```  
  <?xml version="1.0" encoding="utf-8" ?>   
- <feed xmlns="http://www.w3.org/2005/Atom">  
  <title type="text" />   
  <id>uuid:bcecded5-97c8-4d24-96f1-7d9e16652433;id=1</id>   
  <updated>2011-04-14T21:25:48Z</updated>   
- <entry>  
  <id>SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa</id>   
  <title type="text">Highlight all occurrences of selected word</title>   
  <summary type="text">This extends the editor to highlight ….</summary>   
  <published>2011-04-14T14:24:51-07:00</published>   
  <updated>2011-04-14T14:24:22-07:00</updated>   
- <author>  
  <name>Microsoft</name>   
  </author>  
  <link rel="icon" href="VSIXImages/SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa_Icon_SelectionHighlightIcon.jpg" />   
  <link rel="previewimage" href="VSIXImages/SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa_PreviewImage_SelectionHighlight.jpg" />   
  <content type="application/octet-stream" src="SelectionHighlight.vsix" />   
- <Vsix xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/developer/vsx-syndication-schema/2010">  
  <Id>SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa</Id>   
  <Version>1.31</Version>   
  <References />   
  <Rating xsi:nil="true" />   
  <RatingCount xsi:nil="true" />   
  <DownloadCount xsi:nil="true" />   
  </Vsix>  
  </entry>  
- <entry>  
  <id>Template_Wizard_239.Microsoft.3b38a7e3-5cbc-4389-a92a-d82tyc2ed592</id>   
  …  
  </entry>  
  </feed>  
  
```  
  
 请注意，这两个链接标记引用的映像的生成文件夹中的屏幕截图。  
  
## <a name="see-also"></a>请参阅  
 [专用库](../extensibility/private-galleries.md)
