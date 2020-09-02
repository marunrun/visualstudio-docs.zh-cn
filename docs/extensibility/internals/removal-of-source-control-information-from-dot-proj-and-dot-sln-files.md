---
title: 从 proj 和 .sln 文件中删除源代码管理信息
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, .sln and .proj files
ms.assetid: 7b06883f-35de-41e2-9a9e-d3edba236f17
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ba3085a7806bfb0556613d1fca1b94953dcdb0b2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80705587"
---
# <a name="removal-of-source-control-information-from-proj-and-sln-files"></a>删除 .Proj 和 .Sln 文件中的源代码管理信息
源代码管理插件 API 版本1.2 中的 SCC 信息存储在 MSSCCPRJ.SCC 中。SCC 文件。 MSSCCPRJ.SCC 的优点。SCC 文件是 SCC 信息不受源代码管理，就像它位于 proj 和 .sln 文件中一样。

## <a name="version-12-changes"></a>版本1.2 更改
 在基于源代码管理插件 API 版本1.1 的源代码管理插件中，有关源代码管理的信息存储在项目 () 和解决方案 ( .sln) 文件中。 源代码管理信息的数据库位置由 AuxPath 指定，并且数据库中的特定位置由 ProjName 指定。 此行为可能会导致分支、分叉或复制操作出现问题，因为在这些操作中，ProjName 通常会无效。

 在源代码管理插件 API 版本1.1 中，IDE 使用 ~ SAK 文件来检测插件是否支持 MSSCCPRJ.SCC。存储源代码管理信息的 SCC 方法。 源代码管理插件 API 版本1.2 提供一项新功能来检测对 MSSCCPRJ.SCC 的支持。SCC 文件，而无需使用 ~ SAK 文件。 有关详细信息，请参阅 [清除 ~ SAK 文件](../../extensibility/internals/elimination-of-tilde-sak-files.md)。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
