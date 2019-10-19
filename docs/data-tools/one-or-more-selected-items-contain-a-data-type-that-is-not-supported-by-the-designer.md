---
title: 一个或多个所选项包含设计器不支持的数据类型
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 71dcd4f9-2946-42c5-9ce4-99c819ea2785
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 036026d7640dc525538191d2acc347e9ba18b871
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72648264"
---
# <a name="one-or-more-selected-items-contain-a-data-type-that-is-not-supported-by-the-designer"></a>一个或多个所选项包含设计器不支持的数据类型

从**服务器资源管理器**或**数据库资源管理器**拖到**o/r 设计器**的一个或多个项包含**o/r 设计器**不支持的数据类型，例如， [CLR 用户定义类型](/dotnet/framework/data/adonet/sql/clr-user-defined-types)。

## <a name="to-correct-this-error"></a>更正此错误

1. 创建一个基于所需的表的视图，且其中不包括不支持的数据类型。

2. 将视图从**服务器资源管理器**或**数据库资源管理器**拖到设计器上。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)