---
title: 测试区域 6：删除 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], deleting items
- source control plug-ins, deleting items
ms.assetid: 6f2e872c-5ba2-4303-9f50-a90cef9a6225
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 935c735009d83274cc1a8ae126d46f8ee9dbe1ae
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66327992"
---
# <a name="test-area-6-delete"></a>测试区域 6：删除
此源代码管理插件的测试部分覆盖了删除操作。

 源控件删除中的操作的响应**解决方案资源管理器**。

 下面是要删除的项的列表：

- 文件

- 文件夹

- 项目

  可能会根据项目类型中，可以选择**删除**项目 （留在磁盘上的文件） 或**删除**（删除磁盘上的文件） 的项目。 以上任一操作中删除项目或项从**解决方案资源管理器**。

## <a name="expected-behavior"></a>预期的行为
 删除测试区域中的测试用例预期的行为是：

- 已删除的项将不再显示在**解决方案资源管理器**。

- 已删除的项目或项的父签出，根据需要 （也许加上提示。）

- 删除签入或添加的项后，它不会出现在**挂起的签入**窗口。

- 项仍然后删除，在源代码管理存储区中，存在，并且必须手动清除。

|操作|测试步骤|若要验证的预期的结果|
|------------|----------------|--------------------------------|
|删除客户端项目|1.创建客户端项目。<br />2.将解决方案添加到源代码管理。<br />3.从解决方案中删除整个项目|常见的预期的行为。|
|删除空文件|1.创建客户端项目。<br />2.将零字节文件添加到项目。<br />3.将解决方案添加到源代码管理。<br />4.选择此文件，将其删除。|常见的预期的行为。|
|使用一个文件中删除文件夹|1.创建单个项目的解决方案。<br />2.添加的文件夹。<br />3.将一个文件添加到的文件夹。<br />4.将解决方案添加到源代码管理。<br />5.签出该项目，以避免出现提示。<br />6.删除文件夹。|常见的预期的行为。|
|删除文件系统 Web 项目|1.创建文件系统 Web 项目 （使用浏览按钮来指定 UNC 路径）。<br />2.将解决方案添加到源代码管理。<br />3.从解决方案中删除整个项目。<br />4.对本地的 Web 项目重复步骤 1 到 3 （练习通过代码的不同路径但具有相同的外部接口和行为）。|常见的预期的行为。|
|从文件系统 Web 项目中删除文件|1.创建文件系统 Web 项目。<br />2.将解决方案添加到源代码管理。<br />3.从项目中删除一个文件。<br />4.对本地的 Web 项目重复步骤 1 到 3 （练习通过代码的不同路径但具有相同的外部接口和行为）。|常见的预期的行为。|

## <a name="see-also"></a>请参阅
- [源代码管理插件的测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)