---
title: 不支持的数据类型
description: 一个或多个所选项包含设计器不支持的数据类型
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 71dcd4f9-2946-42c5-9ce4-99c819ea2785
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b393798ea3abd89b79bb47e4449d33272a3324f8
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2020
ms.locfileid: "89741850"
---
# <a name="one-or-more-selected-items-contain-a-data-type-that-is-not-supported-by-the-designer"></a>一个或多个所选项包含设计器不支持的数据类型

从 **服务器资源管理器** 或 **数据库资源管理器** 拖到 **o/r 设计器** 的一个或多个项包含 **o/r 设计器**不支持的数据类型，例如， [CLR 用户定义类型](/dotnet/framework/data/adonet/sql/clr-user-defined-types)。

## <a name="to-correct-this-error"></a>更正此错误

1. 创建一个基于所需的表的视图，且其中不包括不支持的数据类型。

2. 将视图从 **服务器资源管理器** 或 **数据库资源管理器** 拖到设计器上。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
