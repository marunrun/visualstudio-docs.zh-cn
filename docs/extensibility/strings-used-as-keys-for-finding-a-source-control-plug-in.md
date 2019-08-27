---
title: 字符串用作键用于查找源代码管理插件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, strings used for finding
ms.assetid: c1e31f76-42a1-4c3d-afb2-664044ef12fd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 31c2b30fb41976cdbbab13fa22d438c63bddbbef
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66331702"
---
# <a name="strings-used-as-keys-for-finding-a-source-control-plug-in"></a>作为用于查找源代码管理插件的密钥的字符串
以下字符串是用于访问注册表，以了解有关源代码管理插件的项。

 `STR_SCC_PROVIDER_REG_LOCATION``STR_PROVIDERREGKEY`， `STR_SCCPROVIDERPATH`，和`STR_SCCPROVIDERNAME`是注册表项或值用于将 DLL 注册为 Visual Studio 源代码管理插件。

 `SCC_PROJECTNAME_KEY``SCC_PROJECTAUX_KEY`， `SCC_KEY, SCC_FILE_SIGNATURE`，和`SCC_STATUS_FILE`用于描述 MSSCCPRJ 的格式。SCC 文件。

## <a name="string-keys-and-values"></a>字符串键和值

|键|值|
|---------|-----------|
|`STR_SCC_PROVIDER_REG_LOCATION`|Software\SourceCodeControlProvider|
|`STR_PROVIDERREGKEY`|ProviderRegKey|
|`STR_SCCPROVIDERPATH`|SCCServerPath|
|`STR_SCCPROVIDERNAME`|SCCServerName|
|`STR_SCC_INI_SECTION`|源代码管理|
|`STR_SCC_INI_KEY`|SourceCodeControlProvider|
|`SCC_PROJECTNAME_KEY`|SCC_Project_Name|
|`SCC_PROJECTAUX_KEY`|SCC_Aux_Path|
|`SCC_STATUS_FILE`|MSSCCPRJ.SCC|
|`SCC_KEY`|SCC|
|`SCC_FILE_SIGNATURE`|源代码控制文件|
|`SCC_NSE`|Namespace 扩展|
|`SCC_NSE_PREFIX`|协议前缀|
|`SCC_NSE_DisableOpenSCC`|DisableOpenFromSourceControl|
|`STR_SCCHELPCOLLECTION`|HelpCollection|
|`STR_UI_LANGUAGE`|UILanguage|
|`STR_SRCSAFE_ROOT_KEY`|Software\Microsoft\SourceSafe|

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [如何：安装源代码管理插件](../extensibility/internals/how-to-install-a-source-control-plug-in.md)
- [MSSCCPRJ.SCC 文件](../extensibility/mssccprj-scc-file.md)