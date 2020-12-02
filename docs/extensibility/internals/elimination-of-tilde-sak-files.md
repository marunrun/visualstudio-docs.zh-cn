---
title: 消除 ~ SAK 文件 |Microsoft Docs
description: 了解源代码管理插件 API 1.2 消除 ~ SAK 的文件，以及如何将它们替换为功能标志和新函数。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- temporary files
- ~sak files
- source control plug-ins, ~SAK files
ms.assetid: 5277b5fa-073b-4bd1-8ba1-9dc913aa3c50
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8e846354b2d48b2f7866daa14987e757f41779c8
ms.sourcegitcommit: df6ba39a62eae387e29f89388be9e3ee5ceff69c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2020
ms.locfileid: "96480507"
---
# <a name="elimination-of-sak-files"></a>消除 ~ SAK 文件
在源代码管理插件 API 1.2 中， *~ SAK* 文件已替换为功能标志和新函数，这些函数可检测源代码管理插件是否支持 *mssccprj.scc* 文件和共享签出。

## <a name="sak-files"></a>~ SAK 文件
Visual Studio .NET 2003 创建了前缀为 *~ SAK* 的临时文件。 这些文件用于确定源代码管理插件是否支持：

- *Mssccprj.scc* 文件。

- 多 (共享) 签出。

对于支持源代码管理插件 API 1.2 中提供的高级函数的插件，IDE 可以检测这些功能，而无需通过使用新功能、标志和函数（将在以下部分中详细介绍）创建临时文件。

## <a name="new-capability-flags"></a>新功能标志
 `SCC_CAP_SCCFILE`

 `SCC_CAP_MULTICHECKOUT`

## <a name="new-functions"></a>新函数
- [SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md)

- [SccIsMultiCheckoutEnabled](../../extensibility/sccismulticheckoutenabled-function.md)

 如果源代码管理插件支持多个 (共享) 签出，则它将声明 `SCC_CAP_MULTICHECKOUT` 功能并实现 `SccIsMultiCheckOutEnabled` 函数。 只要在任何受源代码管理的项目上发生签出操作，就会调用此函数。

 如果源代码管理插件支持创建和使用 *mssccprj.scc* 文件，则它会声明 `SCC_CAP_SCCFILE` 功能并实现 [SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md)。 使用文件列表调用此函数。 此函数 `TRUE' or 'FALSE` 为每个文件返回，以指示 Visual Studio 是否应为其使用 *mssccprj.scc* 文件。 如果源代码管理插件选择不支持这些新功能和函数，则可以使用以下注册表项来禁用这些文件的创建：

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl]DoNotCreateTemporaryFilesInSourceControl**  =  *dword： 00000001*

> [!NOTE]
> 如果此注册表项设置为 *dword： 00000000*，则等效于不存在的键，并且 Visual Studio 仍将尝试创建临时文件。 但是，如果注册表项设置为 *dword： 00000001*，则 Visual Studio 不会尝试创建临时文件。 而是假定源代码管理插件不支持 *mssccprj.scc* 文件，并且不支持共享签出。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 版本1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
