---
title: ClickOnce 如何执行应用程序更新 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- updates, ClickOnce
- ClickOnce deployment, updates
- deploying applications [ClickOnce], application updates
ms.assetid: d54313c2-cf0c-420d-b151-99953a95f0bb
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9217558c68d47ef8f2bf34b10db16463ee76f857
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62900012"
---
# <a name="how-clickonce-performs-application-updates"></a>ClickOnce 如何执行应用程序更新
ClickOnce 使用应用程序的部署清单中指定的文件版本信息来决定是否要更新应用程序的文件。 在开始更新后，ClickOnce 使用一种称为*文件修补*以避免冗余的应用程序文件下载。

## <a name="file-patching"></a>文件修补
 当更新应用程序，ClickOnce 不会下载所有应用程序的新版本文件除非文件已更改。 相反，它将在当前应用程序中的新版本的清单签名的应用程序清单中指定的文件的哈希签名进行比较。 如果文件的签名不同，ClickOnce 会下载新版本。 如果签名匹配，该文件具有不更改从一个版本到下一步。 在这种情况下，ClickOnce 将现有文件复制并在新版本的应用程序中使用它。 这种方法使 ClickOnce 不必下载整个应用程序同样，即使只能将一个或两个文件已更改。

 将根据需要使用还文件修补适合下载的程序集<xref:System.Deployment.Application.ApplicationDeployment.DownloadFileGroup%2A>和<xref:System.Deployment.Application.ApplicationDeployment.DownloadFileGroupAsync%2A>方法。

 如果使用 Visual Studio 来编译你的应用程序，它将生成新的哈希签名的所有文件，只要重新生成整个项目。 在这种情况下，所有程序集将下载到客户端，尽管只有几个程序集可能已更改。

 修补文件不能用于标记为数据并存储在数据目录中的文件。 这些始终下载而不考虑文件的哈希签名。 数据目录的详细信息，请参阅[访问 ClickOnce 应用程序中的本地和远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)。

## <a name="see-also"></a>请参阅
- [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)
- [选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)