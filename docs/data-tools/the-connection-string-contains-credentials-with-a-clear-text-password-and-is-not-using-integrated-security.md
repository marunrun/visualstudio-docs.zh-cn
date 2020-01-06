---
title: 连接字符串包含的凭据具有明文密码并且未使用集成安全性
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 501d85af-92e0-4471-b280-8a59c0688575
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b9c807266182b419dc0967288715a187042f83b1
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586167"
---
# <a name="the-connection-string-contains-credentials-with-a-clear-text-password-and-is-not-using-integrated-security"></a>连接字符串包含的凭据具有明文密码并且未使用集成安全性

是否要将此敏感信息随连接字符串一起保存到当前 DBML 文件和应用程序配置文件中?  单击“否”可在保存连接字符串时不保存敏感信息。

在使用包含敏感信息（连接字符串中包含的密码）的数据连接时，可以选择将敏感信息随连接字符串一起保存到项目 DBML 文件和应用程序配置文件中，或者选择不保存敏感信息。

> [!WARNING]
> 将“连接”属性“应用程序设置”属性显式设置为“False”可将密码添加到 DBML 文件中。

## <a name="save-options"></a>保存选项

- 若要保存包含敏感信息的连接字符串，请选择 **"是"** 。

   连接字符串将存储为应用程序设置。 连接字符串以纯文本形式包含敏感信息。 DBML 文件不包含敏感信息。

- 若要保存不包含敏感信息的连接字符串，请选择 "**否**"。

   连接字符串将存储为应用程序设置，但不包含密码。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
