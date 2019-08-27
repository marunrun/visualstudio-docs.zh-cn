---
title: 测试区域 8：插件切换 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], switching plug-ins
- source control plug-ins, switching
ms.assetid: 01370792-b5da-4e46-9ce2-7dd326587141
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 90650b8b3c3432fce05b03a25033977e68f60fca
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203124"
---
# <a name="test-area-8-plug-in-switching"></a>测试区域 8：插件切换
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]集成的开发环境 (IDE) 具有用户界面 (UI) 若要更改当前源代码管理插件。 此测试区域提供用于选择其要使用的解决方案源代码管理插件的过程的测试用例。  
  
## <a name="command-menu-access"></a>命令菜单访问  
 以下[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]测试用例中使用集成的开发环境菜单路径。  
  
- 当前源代码管理插件：**工具** -> **选项** -> **源代码管理** -> **插件选择**。  
  
- 更改源控制绑定：**文件** -> **源代码管理** -> **更改源代码管理**...  
  
## <a name="common-expected-behavior"></a>常见的预期的行为  
 更改源代码管理插件的一种解决方案是可能无需退出 Visual Studio 或重新加载解决方案。 此外，当前源代码管理插件自动更改为解决方案加载该解决方案时所使用的一个。  
  
## <a name="test-cases"></a>测试用例  
 以下是用于插件的切换测试区域的特定测试用例。  
  
### <a name="case-8a-automatic-change"></a>Case 8a:自动更改  
  
#### <a name="expected-behavior"></a>预期的行为  
 当用户加载源控件下的解决方案时，该解决方案会自动加载和相应的源代码管理插件选择的新。  
  
|操作|测试步骤|若要验证的预期的结果|  
|------------|----------------|--------------------------------|  
|自动进行源控制插件更改|1.选择插件下测试的新 (**工具** -> **选项** -> **源代码管理** -> **插件选择**。)<br />2.创建新项目。<br />3.将解决方案添加到源代码管理。<br />4.选择其他插件 (例如， [!INCLUDE[vsvss](../../includes/vsvss-md.md)])。<br />5.接受卸载解决方案提示。<br />6.重新打开该解决方案从磁盘。|打开解决方案。<br /><br /> 待测试插件是当前源代码管理插件。|  
  
### <a name="case-8b-solution-based-change"></a>Case 8b:基于解决方案的更改  
  
#### <a name="expected-behavior"></a>预期的行为  
 解决方案可以具有其关联的源代码管理插件已更改。  
  
|操作|测试步骤|若要验证的预期的结果|  
|------------|----------------|--------------------------------|  
|插件解决方案更改|1.选择插件下测试的新 (**工具** -> **选项** -> **源代码管理** -> **插件选择**)。<br />2.创建新项目和解决方案。<br />3.将解决方案添加到源代码管理。<br />4.取消绑定从源代码管理解决方案 (使用**更改源代码管理**对话框)。<br />5.选择其他插件 (例如， [!INCLUDE[vsvss](../../includes/vsvss-md.md)])。<br />6.如果已卸载，请重载从磁盘解决方案。<br />7.将解决方案添加到源代码管理。<br />8。取消绑定从源代码管理解决方案 (使用**更改源代码管理**对话框)。<br />9.选择待测试试插件。<br />10.如果已卸载，重新加载解决方案从磁盘。<br />11.将解决方案绑定到原始位置 (使用**更改源代码管理**对话框)。|通过使用所选解决方案添加到源代码管理插件。|  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件的测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
