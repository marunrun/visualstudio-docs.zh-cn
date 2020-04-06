---
title: 测试区域 6： 删除 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], deleting items
- source control plug-ins, deleting items
ms.assetid: 6f2e872c-5ba2-4303-9f50-a90cef9a6225
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9902ab9d1cb9c28ddf67b83590a4cccd5f6562f2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704512"
---
# <a name="test-area-6-delete"></a>测试区域 6：删除
此源代码管理插件测试区域涵盖删除操作。

 源代码管理响应**解决方案资源管理器**中的删除操作。

 以下是可删除的项目列表：

- 文件

- Folders

- Project

  根据项目类型，您可以选择**删除**项目（将文件留在磁盘上 **）或删除项目**（删除磁盘上的文件）。 操作从**解决方案资源管理器**中删除项目或项。

## <a name="expected-behavior"></a>预期行为
 删除测试区域中测试用例的预期行为是：

- 已删除的项目在**解决方案资源管理器**中不再可见。

- 根据需要签出已删除项目或项目的父项（可能带有提示）。

- 删除签出或添加的项目后，它不会显示在 **"挂起签入"** 窗口中。

- 即使在删除之后，该项仍存在于源代码管理存储中，必须手动清除。

|操作|测试步骤|要验证的预期结果|
|------------|----------------|--------------------------------|
|删除客户端项目|1. 创建客户端项目。<br />2. 将解决方案添加到源代码管理。<br />3. 从解决方案中删除整个项目|常见预期行为。|
|删除空文件|1. 创建客户端项目。<br />2. 向项目添加零字节文件。<br />3. 将解决方案添加到源代码管理。<br />4. 选择文件，将其删除。|常见预期行为。|
|删除包含一个文件的文件夹|1. 创建单个项目解决方案。<br />2. 添加文件夹。<br />3. 将一个文件添加到文件夹中。<br />4. 将解决方案添加到源代码管理。<br />5. 查看项目以避免提示。<br />6. 删除文件夹。|常见预期行为。|
|删除文件系统 Web 项目|1. 创建文件系统 Web 项目（使用"浏览"按钮指定 UNC 路径）。<br />2. 将解决方案添加到源代码管理。<br />3. 从解决方案中删除整个项目。<br />4. 对本地 Web 项目重复步骤 1 到 3（通过代码执行不同的路径，但具有相同的外部接口和行为）。|常见预期行为。|
|从文件系统 Web 项目中删除文件|1. 创建文件系统 Web 项目。<br />2. 将解决方案添加到源代码管理。<br />3. 从项目中删除文件。<br />4. 对本地 Web 项目重复步骤 1 到 3（通过代码执行不同的路径，但具有相同的外部接口和行为）。|常见预期行为。|

## <a name="see-also"></a>请参阅
- [源代码管理插件的测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
