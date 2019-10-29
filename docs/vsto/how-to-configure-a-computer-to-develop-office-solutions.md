---
title: 如何：将计算机配置为开发 Office 解决方案
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- prerequisites [Office development in Visual Studio]
- Office development in Visual Studio, installing tools
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: eb29dc4151bc457eb60ce836986817bc1b0137c9
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985966"
---
# <a name="how-to-configure-a-computer-to-develop-office-solutions"></a>如何：将计算机配置为开发 Office 解决方案
  若要配置开发计算机以便可以使用 Visual Studio 中的 Microsoft Office 开发人员工具，请按照本主题中的说明进行操作。 必须在本地计算机上具有管理特权才能执行这些步骤。

### <a name="to-configure-the-development-computer"></a>配置开发计算机

1. 安装包括 Office 开发人员工具的 Visual Studio 版本。 默认安装 Office 开发人员工具。 如果通过选择要安装的功能来自定义 Visual Studio 安装，请确保在安装过程中选择**Microsoft Office 开发人员工具**。 有关包含 Office 开发人员工具的 Visual Studio 版本的详细信息，请参阅[配置计算机以开发 office 解决方案](../vsto/configuring-a-computer-to-develop-office-solutions.md)。

2. 安装 Visual Studio 中的 Office 开发人员工具支持的 Office 的版本。 有关详细信息，请参阅[配置计算机以开发 Office 解决方案](../vsto/configuring-a-computer-to-develop-office-solutions.md)。

     请确保也为安装的 Office 版本安装的 PIA。 默认情况下，PIA 随 Office 一起安装。 如果修改 Office 安装程序，请确保为你要以其为目标的应用程序选择 " **.Net 可编程性支持**" 功能。

3. 如果使用的是英文版的 Visual Studio，但使用非英语的 Windows 设置，则可以安装 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 语言包以与 Windows 相同的语言查看 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 消息。 Visual Studio 的非英语版本将自动安装该语言包。 可从[Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=54246)获取该语言包。

## <a name="see-also"></a>请参阅

- [Visual Studio &#40;中的 Office 开发入门&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [如何：安装 Visual Studio Tools for Office 运行时可再发行组件](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)
- [如何：安装 Office 主互操作程序集](../vsto/how-to-install-office-primary-interop-assemblies.md)
