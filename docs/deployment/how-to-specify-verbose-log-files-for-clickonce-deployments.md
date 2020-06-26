---
title: 如何指定 ClickOnce 部署的详细日志文件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- logs, ClickOnce deployment
- ClickOnce deployment, logging
ms.assetid: 0807a28d-2e40-4a51-ab10-308d808ded6b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1e1d2ca7c58d7da85ad67e56eae7713e517a1d2c
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85381764"
---
# <a name="how-to-specify-verbose-log-files-for-clickonce-deployments"></a>如何：指定 ClickOnce 部署的详细日志文件
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]维护所有部署的活动日志文件。 这些日志记录有关安装、初始化、更新和卸载部署的详细信息 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 若要增加 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 写入这些日志文件的详细信息，请使用注册表编辑器（*regedit.exe*）指定详细级别。

> [!CAUTION]
> 如果不正确地使用注册表编辑器，可能会导致严重问题，可能需要重新安装操作系统。 请慎用注册表编辑器，风险自负。

 下面的过程描述如何为 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 当前用户指定日志文件的详细级别。 若要降低详细级别，请删除此注册表值。

### <a name="to-specify-verbose-log-files"></a>指定详细日志文件

1. 打开 *Regedit.exe*。

2. 导航到**HKEY_CURRENT_USER \software\classes\software\microsoft\windows\currentversion\deployment**的节点。

3. 如有必要，请创建一个名为的新字符串值 `LogVerbosityLevel` 。

4. 将 `LogVerbosityLevel` 值设置为 `1` 。

## <a name="see-also"></a>请参阅
- [ClickOnce 部署疑难解答](../deployment/troubleshooting-clickonce-deployments.md)