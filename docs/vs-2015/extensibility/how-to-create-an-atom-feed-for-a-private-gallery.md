---
title: 如何：创建专用库的 Atom 馈送 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204214"
---
# <a name="how-to-create-an-atom-feed-for-a-private-gallery"></a>如何：创建专用库的 Atom 源
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以创建 Atom (RSS) 源到包含扩展的 intranet 位置，并将源添加到作为专用库的 **扩展和更新** 。 有关详细信息，请参阅 [私有库](../extensibility/private-galleries.md)。  
  
## <a name="creating-an-atom-feed"></a>创建 Atom 馈送  
 若要创建作为专用库的 Atom 源，首先需要将扩展 ( .vsix 文件收集) 到文件夹中。 如果需要，可以将它们组织到子文件夹中。 还需要以下资源：  
  
- 一个 atom.xml 文件，该文件可将扩展作为专用库提供。 有关如何将 atom.xml 文件连接到 **扩展和更新**的信息，请参阅 [私有库](../extensibility/private-galleries.md)。  
  
- 一个文件夹，其中包含从扩展中提取的任何图像文件 (例如，屏幕截图) 。 atom.xml 文件包含指向这些映像的相对链接，以便它们可用于 **扩展和更新**。  
  
  例如，假设你已将以下两个扩展收集到一个文件夹中：  
  
- Template_Wizard_239 .vsix，它是一个空的 VSIX 项目模板。  
  
- SelectionHighlight，它是用于突出显示所选单词的所有实例的工具。  
  
  atom.xml 文件的内容将与以下示例类似：  
  
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
  
 请注意，这两个链接标记指的是生成的图像文件夹中的屏幕截图。  
  
## <a name="see-also"></a>另请参阅  
 [Private Galleries](../extensibility/private-galleries.md)
