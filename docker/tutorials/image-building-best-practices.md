---
title: Docker 教程-第8部分：图像分层
description: 如何检查和管理 Docker 映像中的映像层。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: eae21a729f30a0c77fa52e5774a2f5157286dab1
ms.sourcegitcommit: c4212f40df1a16baca1247cac2580ae699f97e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176671"
---
# <a name="image-layering"></a>图像分层

你是否知道可以查看构成映像的内容？ 使用 `docker image history` 命令，可以看到用于在映像中创建每个层的命令。

1. 使用 `docker image history` 命令查看在 `getting-started` 本教程前面创建的映像中的层。

    ```bash
    docker image history getting-started
    ```

    应会看到类似于下面 (日期/Id 可能不同) 的输出。

    ```plaintext
    IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
    a78a40cbf866        18 seconds ago      /bin/sh -c #(nop)  CMD ["node" "/app/src/ind…   0B                  
    f1d1808565d6        19 seconds ago      /bin/sh -c yarn install --production            85.4MB              
    a2c054d14948        36 seconds ago      /bin/sh -c #(nop) COPY dir:5dc710ad87c789593…   198kB               
    9577ae713121        37 seconds ago      /bin/sh -c #(nop) WORKDIR /app                  0B                  
    b95baba1cfdb        13 days ago         /bin/sh -c #(nop)  CMD ["node"]                 0B                  
    <missing>           13 days ago         /bin/sh -c #(nop)  ENTRYPOINT ["docker-entry…   0B                  
    <missing>           13 days ago         /bin/sh -c #(nop) COPY file:238737301d473041…   116B                
    <missing>           13 days ago         /bin/sh -c apk add --no-cache --virtual .bui…   5.35MB              
    <missing>           13 days ago         /bin/sh -c #(nop)  ENV YARN_VERSION=1.21.1      0B                  
    <missing>           13 days ago         /bin/sh -c addgroup -g 1000 node     && addu…   74.3MB              
    <missing>           13 days ago         /bin/sh -c #(nop)  ENV NODE_VERSION=12.14.1     0B                  
    <missing>           13 days ago         /bin/sh -c #(nop)  CMD ["/bin/sh"]              0B                  
    <missing>           13 days ago         /bin/sh -c #(nop) ADD file:e69d441d729412d24…   5.59MB   
    ```

    每行表示图像中的一个层。 此处显示的是底部显示最新层的底部。 使用此项，还可以快速查看每个层的大小，帮助诊断大型图像。

1. 你会注意到若干行已被截断。 如果添加该 `--no-trunc` 标志，则会获得完整输出 (是的，你可以使用截断的标志来获取未截断输出) 。

    ```bash
    docker image history --no-trunc getting-started
    ```

## <a name="layer-caching"></a>层缓存

现在，你已了解了操作中的分层，接下来将介绍一个重要的课程，帮助降低容器映像的生成时间。

> 层发生更改后，还必须重新创建所有下游层

让我们看一下你使用了多个时间的 Dockerfile .。。

```dockerfile
FROM node:12-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "/app/src/index.js"]
```

返回到映像历史记录输出，可以看到，Dockerfile 中的每个命令都成为该映像中的新层。 你可能会注意到，当你对映像进行更改时，必须重新安装 yarn 依赖项。 是否有解决此问题的方法？ 每次生成时都不会有这么多的依赖项，对吧？

若要解决此问题，你可以重新构建你的 Dockerfile，以帮助支持依赖项的缓存。 对于基于节点的应用程序，这些依赖项是在文件中定义的 `package.json` 。 那么，如果您首先复制了该文件，安装了依赖项， *然后再* 复制其他所有内容，该怎么办？ 如果发生更改，则只会重新创建 yarn 依赖项 `package.json` 。 有意义吗？

1. 更新要在第一个中复制的 Dockerfile `package.json` ，安装依赖项，然后复制中的其他所有内容。

    ```dockerfile hl_lines="3 4 5"
    FROM node:12-alpine
    WORKDIR /app
    COPY package.json yarn.lock ./
    RUN yarn install --production
    COPY . .
    CMD ["node", "/app/src/index.js"]
    ```

1. 使用生成新映像 `docker build` 。

    ```bash
    docker build -t getting-started .
    ```

    应会看到如下所示的输出：

    ```plaintext
    Sending build context to Docker daemon  219.1kB
    Step 1/6 : FROM node:12-alpine
    ---> b0dc3a5e5e9e
    Step 2/6 : WORKDIR /app
    ---> Using cache
    ---> 9577ae713121
    Step 3/6 : COPY package* yarn.lock ./
    ---> bd5306f49fc8
    Step 4/6 : RUN yarn install --production
    ---> Running in d53a06c9e4c2
    yarn install v1.17.3
    [1/4] Resolving packages...
    [2/4] Fetching packages...
    info fsevents@1.2.9: The platform "linux" is incompatible with this module.
    info "fsevents@1.2.9" is an optional dependency and failed compatibility check. Excluding it from installation.
    [3/4] Linking dependencies...
    [4/4] Building fresh packages...
    Done in 10.89s.
    Removing intermediate container d53a06c9e4c2
    ---> 4e68fbc2d704
    Step 5/6 : COPY . .
    ---> a239a11f68d8
    Step 6/6 : CMD ["node", "/app/src/index.js"]
    ---> Running in 49999f68df8f
    Removing intermediate container 49999f68df8f
    ---> e709c03bc597
    Successfully built e709c03bc597
    Successfully tagged getting-started:latest
    ```

    你将看到所有层都已重建。 很好，因为您已更改了 Dockerfile。

1. 现在，更改 `src/static/index.html` 文件 (例如，将更改为 "令人满意 `<title>` 的待办事项" ) 。

1. 立即使用来生成 Docker 映像 `docker build` 。 这次，您的输出看起来应该略有不同。

    ```plaintext hl_lines="5 8 11"
    Sending build context to Docker daemon  219.1kB
    Step 1/6 : FROM node:12-alpine
    ---> b0dc3a5e5e9e
    Step 2/6 : WORKDIR /app
    ---> Using cache
    ---> 9577ae713121
    Step 3/6 : COPY package* yarn.lock ./
    ---> Using cache
    ---> bd5306f49fc8
    Step 4/6 : RUN yarn install --production
    ---> Using cache
    ---> 4e68fbc2d704
    Step 5/6 : COPY . .
    ---> cccde25a3d9a
    Step 6/6 : CMD ["node", "/app/src/index.js"]
    ---> Running in 2be75662c150
    Removing intermediate container 2be75662c150
    ---> 458e5c6f080c
    Successfully built 458e5c6f080c
    Successfully tagged getting-started:latest
    ```

    首先，您应该注意到生成速度要快得多！ 而且，你会看到步骤1-4 都有 `Using cache` 。 那么，个万岁！ 你使用的是生成缓存。 将此映像和更新推送到其中会更快。 个万岁!

## <a name="multi-stage-builds"></a>多阶段生成

虽然我们不会在本教程中深入探讨这一点，但多阶段生成是一项极为强大的工具，可帮助使用多个阶段来创建映像。 它们有多个优点：

- 分离运行时依赖项的生成时依赖项
- *只*传送应用程序需要运行的内容来减少整体映像大小

### <a name="maventomcat-example"></a>Maven/Tomcat 示例

构建基于 Java 的应用程序时，需要使用 JDK 将源代码编译为 Java 字节码。 但是，在生产环境中不需要 JDK。 此外，还可以使用 Maven 或 Gradle 等工具来帮助生成应用。
最终映像中也不需要这些项。 多阶段生成帮助。

```dockerfile
FROM maven AS build
WORKDIR /app
COPY . .
RUN mvn package

FROM tomcat
COPY --from=build /app/target/file.war /usr/local/tomcat/webapps 
```

此示例使用一个名 `build` 为)  (阶段，通过 Maven 执行实际的 Java 生成。 第二个阶段 (`FROM tomcat` 从舞台) 的文件中复制 `build` 。 最终映像只是创建的最后一个阶段 (可以使用标志) 进行重写 `--target` 。

### <a name="react-example"></a>响应示例

在构建反应应用程序时，需要使用节点环境编译 JS 代码 (通常 JSX) 、SASS 样式表，以及更多的静态 HTML、JS 和 CSS。 如果未执行服务器端呈现，则无需为生产生成使用节点环境。 为什么不在静态 nginx 容器中运送静态资源？

```dockerfile
FROM node:12 AS build
WORKDIR /app
COPY package* yarn.lock ./
RUN yarn install
COPY public ./public
COPY src ./src
RUN yarn run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
```

在这里，你将使用 `node:12` 映像来执行生成 (最大化层缓存) 然后将输出复制到 nginx 容器中。 很酷吧？

## <a name="recap"></a>概括

通过深入了解如何对图像进行结构化，可以更快地生成图像并提供较少的更改。 多阶段生成还有助于减少总体映像大小，并通过将生成时依赖项与运行时依赖关系分离，提高最终容器安全性。

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [部署到云](deploy-to-cloud.md)