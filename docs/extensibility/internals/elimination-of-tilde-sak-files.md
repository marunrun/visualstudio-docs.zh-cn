---
title: 消除 [SAK 文件]微软文档
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
ms.openlocfilehash: 0294198bb1560f8df6f17170013f88d4fe11e5cf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708503"
---
# <a name="elimination-of-sak-files"></a>消除 _SAK 文件
在源代码管理插件 API 1.2 中 *，\SAK*文件已被功能标志和新功能所取代，这些功能检测源代码管理插件是否支持*MSSCCPRJ*文件和共享签出。

## <a name="sak-files"></a>*SAK文件
Visual Studio .NET 2003 创建了临时文件，预缀了 *@SAK*。 这些文件用于确定源代码管理插件是否支持：

- *MSSCCPRJ.SCC*文件。

- 多个（共享）签出。

对于支持源代码管理插件 API 1.2 中提供的高级功能的插件，IDE 无需使用以下各节中详述的新功能、标志和函数来检测这些功能，而无需创建临时文件。

## <a name="new-capability-flags"></a>新功能标志
 `SCC_CAP_SCCFILE`

 `SCC_CAP_MULTICHECKOUT`

## <a name="new-functions"></a>新函数
- [SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md)

- [SccIsMultiCheckoutEnabled](../../extensibility/sccismulticheckoutenabled-function.md)

 如果源代码管理插件支持多个（共享）签出，则它声明该`SCC_CAP_MULTICHECKOUT`功能并实现该`SccIsMultiCheckOutEnabled`功能。 每当对任何源控制的项目执行签出操作时，都会调用此功能。

 如果源代码管理插件支持创建和使用*MSSCCPRJ.SCC*文件，则它声明`SCC_CAP_SCCFILE`该功能并实现[SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md)。 使用文件列表调用此功能。 该函数将`TRUE' or 'FALSE`为每个文件返回，以指示 Visual Studio 是否应为其使用*MSSCCPRJ.SCC*文件。 如果源代码管理插件选择不支持这些新功能和功能，它可以使用以下注册表项来禁用这些文件的创建：

 **[HKEY_CURRENT_USER_软件\微软[VisualStudio]8.0\源控制]不创建临时文件在源代码管理** = *dword：0000001*

> [!NOTE]
> 如果此注册表项设置为*dword：00000000，* 则等效于不存在的密钥，Visual Studio 仍尝试创建临时文件。 但是，如果注册表项设置为*dword：00000001，Visual*Studio 不会尝试创建临时文件。 相反，它假定源代码管理插件不支持*MSSCCPRJ.SCC*文件，并且不支持共享签出。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
