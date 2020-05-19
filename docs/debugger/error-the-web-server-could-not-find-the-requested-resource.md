---
title: 错误：Web 服务器找不到请求的资源 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e5c9b428a03595f387c5ff6fb6f0b8ca35172752
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72737251"
---
# <a name="error-the-web-server-could-not-find-the-requested-resource"></a>错误：Web 服务器找不到所请求的资源
为了安全起见，IIS 已返回泛型错误。

一个可能的原因是服务器的安全配置。 IIS 6.0 和早期版本使用名为 URLScan 的外接程序来筛选出可疑请求和格式不正确的请求。 IIS 7.0 具有用于实现同一目的的内置请求筛选。 在这两种情况下，过度限制性请求筛选可防止 Visual Studio 调试服务器。

导致此错误的另一个可能原因是 IIS 的 W3SVC 服务未启动。 在“服务”窗口 (services.msc) 中检查此服务是否已启动（灰显）。

还有许多其他可能的原因会导致此错误。 一些最常见的原因包括 IIS 安装或配置、网站配置或文件系统权限的问题。 可尝试使用浏览器访问资源。 根据 IIS 的配置方式，可能必须使用服务器上的本地浏览器或检查 IIS 错误日志以获取详细的错误消息。

 有关 IIS 的疑难解答的详细信息，请参阅 [IIS 管理](/iis/manage/provisioning-and-managing-iis/iis-management-and-administration)。

## <a name="see-also"></a>请参阅
- [错误：Web 服务器已被锁定，并阻止 DEBUG 谓词](../debugger/error-the-web-server-has-been-locked-down-and-is-blocking-the-debug-verb.md)