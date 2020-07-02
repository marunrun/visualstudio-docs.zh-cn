---
title: 拒绝访问 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 8a512060-d744-47af-a83e-4ba42ea2c5b2
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 874f7c0e5dcfaf4881c059a77f1c5e930d8c0578
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85814832"
---
# <a name="access-is-denied"></a>访问被拒绝
脚本尝试从当前页的主机以外的源访问数据。 后跟 Internet Explorer 及其他浏览器的同一初始策略允许脚本只从具备当前页 URL 的同一方案、主机和端口的源访问数据。  
  
 例如，如果当前页为 `https://employees.mycompany.com` ，则无法从以下 url 访问数据：  
  
- `http://data.contoso.com`，因为它使用 HTTP 而不是 HTTPS。  
  
- `https://somedatasource.com`，因为它是不同的域。  
  
- `https://employees.mycompany.com:8888`，因为它使用不同的端口。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 调查正尝试调用的 API 是支持 JSONP 还是 CORS，这是两种安全地允许跨源脚本的方法。  
  
- 如果正尝试调用 REST API，请将此调用重构到服务器端代码中，然后为客户端脚本公开新的 REST 终结点。  
  
     有关其他信息，请查找与同一初始策略、JSONP、CORS 相关的联机文档。
