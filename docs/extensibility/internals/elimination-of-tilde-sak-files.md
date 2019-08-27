---
title: 消除了 ~ SAK 文件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- temporary files
- ~sak files
- source control plug-ins, ~SAK files
ms.assetid: 5277b5fa-073b-4bd1-8ba1-9dc913aa3c50
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e409a08ba295bb55eb1fcfcd2a048a9bdb5ea7c9
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66327539"
---
# <a name="elimination-of-sak-files"></a>消除了 ~ SAK 文件
在源控件插件 API 1.2 *~ SAK*功能标志已替换为文件和新的函数，检测是否将源控件插件支持*MSSCCPRJ*文件和共享方式签出。

## <a name="sak-files"></a>~SAK files
Visual Studio.NET 2003 中创建临时文件带有前缀 *~ SAK*。 这些文件用于确定是否支持源代码管理插件：

- *MSSCCPRJ.SCC*文件。

- （共享） 的多个签出。

插件的支持在源控件插件 API 1.2 中提供的高级的函数，IDE 可以检测这些功能，而无需创建临时文件通过使用新功能、 标志和函数，以下部分详细介绍。

## <a name="new-capability-flags"></a>新的功能标志
 `SCC_CAP_SCCFILE`

 `SCC_CAP_MULTICHECKOUT`

## <a name="new-functions"></a>新的函数
- [SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md)

- [SccIsMultiCheckoutEnabled](../../extensibility/sccismulticheckoutenabled-function.md)

 如果源代码管理插件支持多个 （共享） 签出，则它会声明`SCC_CAP_MULTICHECKOUT`功能和实现`SccIsMultiCheckOutEnabled`函数。 在任何受源代码管理项目发生签出操作时调用此函数。

 如果源代码管理插件支持创建和使用*MSSCCPRJ.SCC*文件，然后它会声明`SCC_CAP_SCCFILE`功能和实现[SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md)。 此函数调用的文件列表。 该函数将返回`TRUE' or 'FALSE`为每个文件，以指示是否应使用 Visual Studio *MSSCCPRJ.SCC*为它的文件。 如果选择不支持这些新功能和函数的源代码管理插件，它可以使用以下注册表项来禁用这些文件的创建：

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl]DoNotCreateTemporaryFilesInSourceControl** = *dword:00000001*

> [!NOTE]
> 如果此注册表项设置为*dword:00000000*，等效于键不存在，并且 Visual Studio 仍尝试创建临时文件。 但是，如果注册表项设置为*dword: 00000001*，Visual Studio 不会尝试创建临时文件。 而是假定的源代码管理插件不支持*MSSCCPRJ.SCC*文件，并不支持共享方式签出。

## <a name="see-also"></a>请参阅
- [什么是源控制插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)