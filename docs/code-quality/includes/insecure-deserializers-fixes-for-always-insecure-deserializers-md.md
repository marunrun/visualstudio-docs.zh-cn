---
author: dotpaul
ms.author: paulming
ms.date: 05/01/2019
ms.topic: include
ms.openlocfilehash: bc423f10cfbae0b7a0cdaedb72f6891a0e12d228
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68147115"
---
- 如果可能，而是使用安全的序列化程序和**不允许攻击者能够指定任意类型进行反序列化**。 一些更安全的序列化程序包括：
  - <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>
  - <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType>
  - <xref:System.Web.Script.Serialization.JavaScriptSerializer?displayProperty=nameWithType> -永远不会使用<xref:System.Web.Script.Serialization.SimpleTypeResolver?displayProperty=nameWithType>。 如果必须使用类型解析程序，到预期的列表限制反序列化的类型。
  - <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>
  - Newtonsoft Json.NET-使用 TypeNameHandling.None。 如果必须为 TypeNameHandling 使用另一个值，限制对具有自定义 ISerializationBinder 预期列表反序列化的类型。
  - 协议缓冲区
- 使序列化的数据篡改。 在序列化之后, 密码学角度上登录序列化的数据。 在反序列化之前验证的加密签名。 保护从公布的加密密钥和密钥轮换的设计。