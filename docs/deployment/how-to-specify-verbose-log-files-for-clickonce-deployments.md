---
title: 如何：指定 ClickOnce 部署的详细日志文件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: d57c9aa618ec3df91b130cb2f870d88b01c323c2
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63406692"
---
# <a name="how-to-specify-verbose-log-files-for-clickonce-deployments"></a>如何：指定 ClickOnce 部署的详细日志文件
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 维护所有部署的活动日志文件。 这些日志记录与安装、 初始化、 更新和卸载相关的详细信息[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]部署。 若要增加详细信息，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]写入这些日志文件，使用注册表编辑器 (*regedit.exe*) 来指定详细级别。

> [!CAUTION]
> 如果注册表编辑器使用不当可能会导致严重的问题，可能需要重新安装操作系统。 使用注册表编辑器的风险由用户自行承担。

 以下过程描述如何指定的详细级别[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]当前用户的日志文件。 若要减少的详细级别，请删除此注册表值。

### <a name="to-specify-verbose-log-files"></a>若要指定详细日志文件

1. 打开*Regedit.exe*。

2. 导航到的节点**HKEY_CURRENT_USER\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment**。

3. 如有必要，创建一个名为的新字符串值`LogVerbosityLevel`。

4. 设置`LogVerbosityLevel`值设为`1`。

## <a name="see-also"></a>请参阅
- [ClickOnce 部署疑难解答](../deployment/troubleshooting-clickonce-deployments.md)