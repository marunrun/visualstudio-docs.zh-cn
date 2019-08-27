---
title: 什么&#39;中的源控制插件 API 版本 1.3 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, what's new in API v1.3
- what's new [Visual Studio SDK], source control plug-ins
ms.assetid: 7dfb2227-6e1d-4028-bce9-f8967456a993
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4d5333a5b44e9c990843e66da357578e4a90d210
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200919"
---
# <a name="what39s-new-in-the-source-control-plug-in-api-version-13"></a>什么&#39;中的源控制插件 API 版本 1.3
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

源控件插件 API 版本 1.3 引入了以下新函数，以提供更高级的控制。  
  
## <a name="changes"></a>Changes  
 以下函数不熟悉源控制插件 API 版本 1.3:  
  
|函数|概述|  
|--------------|--------------|  
|[SccGetExtendedCapabilities](../../extensibility/sccgetextendedcapabilities-function.md)|允许其他功能位报告|  
|[SccEnumChangedFiles](../../extensibility/sccenumchangedfiles-function.md)|允许对文件中的本地磁盘上的版本控制数据库比具有较新版本的检查|  
|[SccQueryChanges](../../extensibility/sccquerychanges-function.md)|指定的文件，以允许对的名称更改 （重命名、 添加和删除操作） 的状态检查|  
|[SccPopulateDirList](../../extensibility/sccpopulatedirlist-function.md)|允许对目录和文件的版本控制数据库中的检查|  
|[SccAddFilesFromSCC](../../extensibility/sccaddfilesfromscc-function.md)|将指定的文件列表从版本控制数据库添加到当前项目|  
|[SccBackgroundGet](../../extensibility/sccbackgroundget-function.md)|执行无提示"获取"指定的文件 （没有用户界面显示）|  
|[SccGetUserOption](../../extensibility/sccgetuseroption-function.md)|允许访问特定于用户的选项|  
  
## <a name="see-also"></a>请参阅  
 [入门](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)   
 [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
