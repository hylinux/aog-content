---
title: 不同订阅或者账号下网站如何进行备份还原
description: 不同订阅或者账号下网站如何进行备份还原(本文以国际版备份至中国版为例)
services: App Service
documentationCenter: ''
author: maysmiling
manager: ''
editor: ''
tags: 'Web Apps, Backup, Restore, Subscription'

ms.service: app-service-web
wacn.topic: aog
ms.topic: article
ms.author: v-tawe
ms.date: 07/17/2017
wacn.date: 07/17/2017
---

# 不同订阅或者账号下网站如何进行备份还原

## 问题描述

不同订阅或者账号下网站如何进行备份还原时，可能会遇到恢复时出现错误“还原操作未能通过存储 Blob 实现还原。错误详细信息:
 
```
Error occurred while downloading meta data from the storage account.”
```

## 解决方法

### 前提条件

备份及还原的操作要求网站为标准或高级模式才能使用。

### 操作步骤

此处我们以部署在美国东部的网站想要还原到中国北部为例：

> [!TIP]
> 中国版本的 Azure 虽然与国际版本的 Azure 在功能上类似，但是是属于两个不同的系统。不仅跨越了订阅和账号，还跨越了域。

1. 通过备份操作将部署在美国东部的网站备份到一个同订阅下的存储中。

    > [!TIP]
    > 此操作与中国区 Azure 的操作步骤一致。

    ![portal](./media/aog-web-apps-howto-backup-through-different-subscriptions/portal.png)

2. 下载备份好的文件。

    > [!NOTE]
    > 如果直接点击备份好的文件进行下载操作。则只会下载一个 zip 的压缩文件包。在还原时只有此文件是不够的。

    ![portal-2](./media/aog-web-apps-howto-backup-through-different-subscriptions/portal-2.png)

    我们到网站所关联的存储中查看我们的备份文件，发现每一次备份都会产生 3 个文件：log 文件、xml 文件、zip 文件。

    ![portal-3](./media/aog-web-apps-howto-backup-through-different-subscriptions/portal-3.png)
    
    将这 3 个文件下载到本地。

3. 打开中国区 Azure，将下载好的 3 个文件以 blob 的形式上传到已创建好的存储中。

    ![portal-4](./media/aog-web-apps-howto-backup-through-different-subscriptions/portal-4.png)

4. 在中国区 Azure 中打开已创建好的标准模式的网站，点击【备份】进行还原操作。

    选择刚才上传到存储中的 zip 文件。

    ![portal-5](./media/aog-web-apps-howto-backup-through-different-subscriptions/portal-5.png)

5. 还原成功以后即可进行访问。

    > [!NOTE]
    > 如果只有一个 zip 文件，在还原时就会遇到还原失败的错误，如下图：

    ![error](./media/aog-web-apps-howto-backup-through-different-subscriptions/error.png)

此场景同样适用于不同订阅或者不同账号之间网站的备份还原操作。