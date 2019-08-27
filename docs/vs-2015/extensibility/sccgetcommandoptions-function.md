---
title: SccGetCommandOptions 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccGetCommandOptions
helpviewer_keywords:
- SccGetCommandOptions function
ms.assetid: bbe4aa4e-b4b0-403e-b7a0-5dd6eb24e5a9
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 55d4d2cae73dd77fc601ca85ab45d969fc0e4de8
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432410"
---
# <a name="sccgetcommandoptions-function"></a>SccGetCommandOptions 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数会提示用户提供有关给定命令的高级选项。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
SCCRTN SccGetCommandOptions(  
   LPVOID pvContext,  
   HWND hWnd,  
   enum SCCCOMMAND iCommand,  
   LPCMDOPTS* ppvOptions  
);  
```  
  
#### <a name="parameters"></a>参数  
 pvContext  
 [in]源控制插件上下文结构。  
  
 hWnd  
 [in]它提供了任何对话框，父级可以使用源代码管理插件，则 IDE 窗口的句柄。  
  
 iCommand  
 [in]为其请求高级的选项的命令 (请参阅[命令代码](../extensibility/command-code-enumerator.md)有关可能的值)。  
  
 ppvOptions  
 [in]选项的结构 (也可以是`NULL`)。  
  
## <a name="return-value"></a>返回值  
 此函数的源控制插件实现应返回以下值之一：  
  
|“值”|描述|  
|-----------|-----------------|  
|SCC_OK|成功。|  
|SCC_I_ADV_SUPPORT|源代码管理插件支持命令的高级的选项。|  
|SCC_I_OPERATIONCANCELED|用户取消了源控制即插即用的项的**选项**对话框。|  
|SCC_E_OPTNOTSUPPORTED|源代码管理插件不支持此操作。|  
|SCC_E_ISCHECKEDOUT|无法执行此操作对当前已签出文件。|  
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。 建议重试。|  
|SCC_E_NONSPECIFICERROR|非特定故障。|  
  
## <a name="remarks"></a>备注  
 IDE 将调用此函数与第一次`ppvOptions` = `NULL`来确定源代码管理插件是否支持指定命令的高级的选项功能。 如果插件支持该功能针对该命令，在 IDE 此函数会再次调用时的用户请求的高级的选项 (通常作为实现**高级**在对话框中的按钮) 并提供的非NULL指针`ppvOptions` ，它指向`NULL`指针。 该插件将存储在专用结构中用户指定的任何高级的选项并向该结构中返回的指针`ppvOptions`。 然后，此结构传递到需要了解的信息，包括对后续调用的所有其他源控制插件 API 函数`SccGetCommandOptions`函数。  
  
 一个例子来帮助阐明这种情况。  
  
 用户选择**获取**命令，IDE 将显示**获取**对话框。 IDE 调用`SccGetCommandOptions`函数与`iCommand`设置为`SCC_COMMAND_GET`并`ppvOptions`设置为`NULL`。 这由源代码管理插件作为问题解释，"您有此命令的任何高级的选项？" 如果该插件返回`SCC_I_ADV_SUPPORT`，则 IDE 将显示**高级**按钮在其**获取**对话框。  
  
 第一次用户单击**高级**按钮，IDE 再次调用`SccGetCommandOptions`函数，这与非一次`NULL``ppvOptions`指向`NULL`指针。 插件显示其自身**获取选项**对话框中，会提示用户输入的信息，将放到其自己的结构，该信息并向该结构中返回的指针`ppvOptions`。  
  
 如果用户单击**高级**再次在同一对话框中，在 IDE 调用`SccGetCommandOptions`再次而无需更改函数`ppvOptions`，以便该结构传递到该插件。 这样，要重新初始化其对话框，以便用户以前设置的值的插件。 该插件修改返回之前的位置中的结构。  
  
 最后，当用户单击**确定**在 IDE 中**获取**对话框中，IDE 调用[SccGet](../extensibility/sccget-function.md)，并传入此结构中返回`ppvOptions`，其中包含高级的选项。  
  
> [!NOTE]
> 该命令`SCC_COMMAND_OPTIONS`则 IDE 将显示时，将使用**选项**对话框中，使用户能够设置控制集成的工作方式的首选项。 如果源代码管理插件想要提供其自己的首选项对话框中，它可以显示它从**高级**IDE 的首选项对话框中的按钮。 在插件处于全权负责获取和保存此信息;IDE 不会使用它或对其进行修改。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)   
 [命令代码](../extensibility/command-code-enumerator.md)
