---
title: 如何：为 ClickOnce 部署错误设置一个自定义日志文件位置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- troubleshooting ClickOnce deployments
- ClickOnce deployment, troubleshooting
- ClickOnce deployment, error logging
ms.assetid: 77424414-7f0e-4b99-94bb-ea130de92d09
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7a1b7c93e4b30bbfd373a5fad9d7001452d4f587
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63403547"
---
# <a name="how-to-set-a-custom-log-file-location-for-clickonce-deployment-errors"></a>如何：为 ClickOnce 部署错误设置自定义日志文件位置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 维护所有部署的激活日志文件。 这些日志记录与安装和初始化相关的任何错误[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署。 默认情况下，[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]创建一个日志文件的每个部署激活。 它会将这些日志文件存储在临时 Internet 文件文件夹中。 发生了激活失败，并在用户单击时，向用户显示的日志文件的部署**详细信息**中出现的错误对话框。  
  
 可以为特定的客户端更改此行为，使用注册表编辑器 (**regedit.exe**) 设置自定义日志文件路径。 在这种情况下，[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]单个文件中记录激活成功和失败的所有部署。  
  
> [!CAUTION]
> 如果注册表编辑器使用不当可能会导致严重的问题，可能需要重新安装操作系统。 使用注册表编辑器的风险由用户自行承担。  
  
> [!NOTE]
> 你将需要截断或删除日志文件，有时可用于阻止其增长得过大。  
  
 以下过程介绍如何为单个客户端设置自定义日志文件位置。  
  
### <a name="to-set-a-custom-log-file-location"></a>若要设置自定义日志文件位置  
  
1. 打开**Regedit.exe**。  
  
2. 导航到的节点`HKCU\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment`。  
  
3. 将字符串值`LogFilePath`到的完整路径和文件名你首选的自定义日志的位置。  
  
     此位置必须是用户对其具有写访问权限的目录中。 例如，在 Windows Vista 中，创建以下文件夹结构并设置`LogFilePath`到 C:\Users\\< 用户名\>\Documents\Logs\ClickOnce\installation.log。  
  
## <a name="see-also"></a>请参阅  
 [ClickOnce 部署疑难解答](../deployment/troubleshooting-clickonce-deployments.md)
