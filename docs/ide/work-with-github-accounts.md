---
title: 在 Visual Studio 中使用 GitHub 帐户
ms.date: 11/16/2020
ms.custom: ''
ms.topic: conceptual
description: 了解如何在 Visual Studio 中使用 GitHub 帐户。
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
monikerRange: '>=vs-2019'
ms.openlocfilehash: 845b663a3a0828806766fa0609e45efafabec50a
ms.sourcegitcommit: e8a13978131f257d91ce37c5a2e0d153a4c400ef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2020
ms.locfileid: "94704012"
---
# <a name="work-with-github-accounts-in-visual-studio"></a>在 Visual Studio 中使用 GitHub 帐户

如果你有公共 GitHub 或 GitHub Enterprise 帐户，可以将它添加到 Visual Studio 密钥链中。 添加帐户后，你就可以通过直接在 Visual Studio 中访问和创建 GitHub 存储库来利用平台集成。

## <a name="adding-public-github-accounts"></a>添加公共 GitHub 帐户

如果你已使用 Microsoft 帐户或工作或学校帐户登录 Visual Studio，则可以添加公共 GitHub 帐户。

1. 在 Visual Studio 环境的右上角，选择包含首字母的图标。 然后，选择“帐户设置...”来管理帐户。 也可以通过依次转到“文件” > “帐户设置”来打开“帐户设置”对话框。

    :::image type="content" source="../ide/media/account-picker.png" alt-text="帐户设置":::

2. 在“所有帐户”子菜单下，选择加号来添加帐户，然后选择“GitHub”。

    :::image type="content" source="../ide/media/sign-in-add-github.png" alt-text="选择添加 GitHub 帐户":::

3. 此时，你被重定向到可以在其中使用 GitHub 凭据进行登录的浏览器。 登录后，你将在浏览器中看到“成功”窗口，然后可以返回到 Visual Studio。

    :::image type="content" source="../ide/media/github-success-signin.png" alt-text="浏览器中的“成功”窗口":::

4. 此时，这两个帐户同时出现在“所有帐户”子菜单下。

    :::image type="content" source="../ide/media/show-both-accounts.png" alt-text="两个帐户同时显示":::

如果你还没有使用其他帐户登录 Visual Studio，请选择 Visual Studio 环境右上角的“登录”链接。 也可以通过依次转到“文件” > “帐户设置”来打开“帐户设置”对话框。 然后，按照上面的说明操作来添加 GitHub 帐户。

![不是已登录用户](../ide/media/vs2019_usernotsignedin.png)

## <a name="adding-github-enterprise-accounts"></a>添加 GitHub Enterprise 帐户

默认情况下，Visual Studio 只启用了公共 GitHub 帐户。

1. 若要启用 GitHub Enterprise 帐户，请依次转到“工具” > “选项”，然后搜索“帐户”选项。

    :::image type="content" source="../ide/media/accounts-options.png" alt-text="“帐户”选项菜单":::

2. 然后，选中“包括 GitHub Enterprise Server 帐户”复选框。 当你下次转到“帐户设置”并尝试添加 GitHub 帐户时，就会同时看到 GitHub 和 GitHub Enterprise 对应的选项。

    :::image type="content" source="../ide/media/github-enterprise-endpoint-signin.png" alt-text="使用 GitHub Enterprise 登录":::

3. 在输入 GitHub Enterprise 服务器地址后，选择“使用浏览器登录”。 在浏览器中，可以使用 GitHub Enterprise 凭据登录。

## <a name="see-also"></a>另请参阅

- [使用多个用户帐户](work-with-multiple-user-accounts.md)
- [登录 Visual Studio](signing-in-to-visual-studio.md)
