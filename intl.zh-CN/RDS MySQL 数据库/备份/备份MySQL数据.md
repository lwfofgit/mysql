# 备份MySQL数据

备份数据用于应付数据丢失或损坏，您可以设置备份策略自动备份MySQL数据和日志，或者手动备份MySQL数据，对于本地SSD盘实例，还支持删除实例后继续保留备份。

其他引擎备份数据请参见：

-   [备份SQL Server数据](/intl.zh-CN/RDS SQL Server 数据库/备份/备份SQL Server数据.md)
-   [备份PostgreSQL数据](/intl.zh-CN/RDS PostgreSQL 数据库/备份/备份PostgreSQL数据.md)
-   [备份PPAS数据](/intl.zh-CN/RDS PPAS 数据库/备份/备份PPAS数据.md)
-   [自动备份MariaDB数据](/intl.zh-CN/RDS MariaDB TX 数据库/备份/自动备份MariaDB数据.md)

**说明：** 本文介绍的是默认的备份功能，备份文件存储于实例所在地域。您还可以将备份文件存储于另一个地域，详情请参见[跨地域备份数据](/intl.zh-CN/RDS MySQL 数据库/备份/跨地域备份数据.md)。

## 特色功能

-   RDS MySQL本地盘实例支持长期保留备份文件，并且可以设置删除实例后继续保留备份文件，避免了误操作导致的数据丢失。详情请参见[本地盘实例修改备份设置](#section_f33_lk4_ydb)。
-   RDS MySQL云盘实例支持分钟级快照，大幅增加快照频率。详情请参见[云盘实例修改备份设置](#section_hwp_vv2_lct)。

## 费用

每个RDS实例的备份空间都有一定量的免费额度，实例备份文件占用备份空间，空间使用量超出免费的额度将会产生额外的费用，请合理设计备份周期，以满足业务需求的同时，兼顾备份空间的合理利用。关于免费额度详情，请参见[查看备份空间免费额度](/intl.zh-CN/RDS MySQL 数据库/备份/查看备份空间免费额度.md)。

免费额度用完后，RDS MySQL的备份采用阶梯定价，730天内的备份（常规备份）价格请参见[RDS详细价格信息](https://www.alibabacloud.com/product/apsaradb-for-rds#pricing)，超过730天的备份（归档备份）价格请下载[国际站长期备份收费说明](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/141303/cn_zh/1582881893267/%E5%9B%BD%E9%99%85%E7%AB%99%E9%95%BF%E6%9C%9F%E5%A4%87%E4%BB%BD%E6%94%B6%E8%B4%B9%E8%AF%B4%E6%98%8E.xls)后查看。

## 注意事项

-   仅本地SSD盘实例支持归档备份。
-   备份期间不要执行DDL操作，避免锁表导致备份失败。
-   尽量选择业务低峰期进行备份。
-   若数据量较大，花费的时间可能较长，请耐心等待。
-   备份文件有保留时间，请及时下载需要保留的备份文件到本地。
-   表数量超过5万张将无法进行[单库单表恢复](/intl.zh-CN/RDS MySQL 数据库/恢复/MySQL单库单表恢复.md)，超过60万将无法进行备份。表数量过多时建议您进行分库处理。

## 备份说明

|数据备份|日志备份|
|----|----|
|数据库的数据文件备份，支持物理备份、逻辑备份和快照备份。可用于[恢复数据](/intl.zh-CN/RDS MySQL 数据库/恢复/恢复MySQL数据.md)。实例默认会自动进行物理备份或快照备份，支持情况如下： -   MySQL 5.5/5.6/5.7/8.0 本地SSD盘（含高可用版和三节点企业版）：
    -   自动备份支持全量物理备份。
    -   手动备份支持全量物理备份、全量逻辑备份和单库逻辑备份。
-   MySQL 5.7/8.0 ESSD云盘/SSD云盘（高可用版）：

仅支持快照备份，可恢复至新建实例，不支持下载。

-   MySQL 5.7/8.0 SSD云盘（基础版）：

仅支持快照备份，可恢复至新建实例，不支持下载。


|数据库的Binlog日志文件备份。可用于[按时间点恢复数据](/intl.zh-CN/RDS MySQL 数据库/恢复/恢复MySQL数据.md)。实例默认会自动进行日志备份。 **说明：**

-   Binlog文件会占用实例的磁盘容量。
-   Binlog大小超过500MB或写入超过6小时就会切换到新的Binlog文件继续写入，老的Binlog文件会异步上传。
-   您可以通过一键上传 Binlog功能将 Binlog 文件上传至 OSS，不影响实例的数据恢复功能，Binlog 也不再占用实例磁盘空间。
-   基础版暂不支持一键上传Binlog。
-   不支持访问Binlog文件所在的OSS存储空间。 |

## 本地盘实例修改备份设置

阿里云数据库会执行用户设定的备份策略，自动备份数据库。

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧导航栏中单击**备份恢复**。

5.  在**备份恢复**页面中选择**备份设置**页签，单击**编辑**。

6.  设置如下参数，然后单击**确定**。

    ![mysql备份设置](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7113729951/p86591.png)

    |参数|说明|
    |--|--|
    |**备份周期**|可以设置为一星期中的某几天。 **说明：** 为了您的数据安全，一周至少需要备份两次。 |
    |**备份时间**|可以设置为任意时段，以小时为单位，建议设置为业务低峰期时间。|
    |**保留时长**|填写具体保留天数，或勾选**实例释放前长期保留**。     -   超过保留天数的备份会被自动删除，勾选**实例释放前长期保留**则所有备份都不会被自动删除。如果需要实例删除后继续保留备份，请设置下方的**实例释放后备份文件是否保留**参数为**保留最后一个**或**全部保留**。
    -   保留天数在730天以内的备份，保留方式为常规备份。
    -   保留天数超过730天的备份会由常规备份自动转化为归档备份，您还需要选择归档备份的保留周期。例如选择每月2个，则会保留每个自然月最先产生的两个归档备份。

![归档周期](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7113729951/p86587.png) |
    |**日志备份**|日志备份的开关。 **说明：** 关闭日志备份会导致所有日志备份被清除，并且无法使用按时间点恢复数据的功能。 |
    |**日志备份保留**|    -   日志备份文件保留的天数，默认为7天。
    -   可以设置为7~730天，且必须小于等于数据备份天数。 |
    |**单库单表**|单库单表备份恢复功能。开通后会修改备份格式以支持该功能。默认为开启，无法关闭。 详情请参见[MySQL单库单表恢复](/intl.zh-CN/RDS MySQL 数据库/恢复/MySQL单库单表恢复.md)。|
    |**实例释放后备份文件是否保留**|实例删除后，数据备份的保留策略。可以选择**不保留**、**保留最后一个**或**全部保留**。 为防止忘记续费、误操作等情况导致实例数据丢失，建议选择**保留最后一个**或**全部保留**。

**说明：** 当前该备份是永久保留，暂不收取费用。 |


## 云盘实例修改备份设置

阿里云数据库会执行用户设定的备份策略，自动备份数据库。

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧导航栏中单击**备份恢复**。

5.  在**备份恢复**页面中选择**备份设置**页签，单击**编辑**。

6.  设置如下参数，然后单击**确定**。

    ![云盘备份设置](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7113729951/p134971.png)

    |参数|说明|
    |--|--|
    |**快照备份周期**|可以设置为一星期中的某几天。 **说明：** 为了您的数据安全，一周至少需要备份两次。 |
    |**快照备份开始时间**|可以设置为任意时段，以小时为单位，建议设置为业务低峰期时间。如果需要增加快照备份频率，请选中**增加快照频率**，并选择具体频率。 |
    |**快照备份保留天数**|填写具体保留天数。默认最大保留天数为730天，但是如果开启了**增加快照频率**，最大保留天数会相应减少。计算公式如下：最大保留天数 = ⌊900/每天备份次数/每周备份次数\*7⌋ （向下取整）

例如备份频率为30分钟，每周备份2次，则最大保留天数 = ⌊900/\( 24\*2 \)/2\*7⌋= 65天。 |
    |**日志备份**|日志备份的开关。 **说明：** 关闭日志备份会导致所有日志备份被清除，并且无法使用按时间点恢复数据的功能。 |
    |**日志备份保留**|    -   日志备份文件保留的天数，默认为7天。
    -   可以设置为7~730 天，且必须小于等于数据备份天数。
**说明：** MySQL 5.7 SSD云盘（基础版）的备份文件保存7天，不可修改。 |
    |**秒级备份**|开启后增加快照备份的备份速度，当前最多支持保留10个快照，超过10个时，备份会失败，建议**保留时间**不要超过10天。 **说明：** 仅MySQL ESSD云盘实例可以开启此功能。 |


## 手动备份MySQL数据

本例以MySQL 5.7 本地SSD盘（高可用版）单库逻辑备份为例。

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  单击页面右上角的**备份实例**，打开备份实例对话框。

5.  设置好备份方式、备份策略，单击**确定**。

    ![物理备份](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7113729951/p40345.png)

    **说明：** 如果选择**逻辑备份**后备份策略选择**单库备份**，请在左侧选择要备份的数据库，单击**\>**将要备份的数据库加入列表。若您还没有数据库，请先[创建数据库](/intl.zh-CN/RDS MySQL 数据库/快速入门/创建数据库和账号.md)。

    ![单库逻辑备份](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8113729951/p40344.png)

6.  在右上角**任务进度**列表查看任务进度，等待任务完成。

    ![查看任务进度](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2577559951/p66932.png)

    **说明：**

    -   备份完成后您可以在**备份恢复**页面下载备份文件。部分实例不支持下载备份，详情请参见[下载数据备份和日志备份](/intl.zh-CN/RDS MySQL 数据库/备份/下载数据备份和日志备份.md)。

        ![下载备份](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3577559951/p66935.png)

    -   手动备份的保留时间取决于备份设置中的**保留时间**。详情请参见[备份设置参数说明](#table_dn7_r06_h1k)。

## 常见问题

1.  RDS MySQL的数据备份是否可以关闭？

    答：不可以关闭。可以减少备份频率，一周至少2次。数据备份保留天数最少7天。

2.  RDS MySQL的日志备份是否可以关闭？

    答：可以关闭（基础版除外）。备份设置内关闭日志备份开关即可。

3.  为什么有时候备份任务会失败？

    答：备份过程中执行DDL操作，会导致锁表，进而导致备份失败。

4.  为什么数据很少，但是快照备份很大（例如数据只有几个G，快照备份几十G）？

    答：创建快照的过程中，系统通过消除空块的操作，使得单个快照容量小于磁盘容量。单个块的大小为2 M，如果写入时比较分散，就会导致大量的块没有写满，例如3 M的数据可能会占用2个块、3个块甚至4个块，在计算快照备份大小时，会计算所有非空块的大小，因此会出现快照备份占用空间远大于数据本身占用空间。

5.  删除实例后如果保留了备份文件，在哪里进行恢复呢？

    答：您可以在**已删除实例备份**页面下载备份文件，并恢复到本地数据库。

    ![已删除实例备份](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8113729951/p86993.png)


## 相关文档

-   [下载数据备份和日志备份](/intl.zh-CN/RDS MySQL 数据库/备份/下载数据备份和日志备份.md)
-   [恢复MySQL数据](/intl.zh-CN/RDS MySQL 数据库/恢复/恢复MySQL数据.md)

## 相关API

|API|描述|
|---|--|
|[创建备份](/intl.zh-CN/API 参考/备份/创建备份.md)|创建RDS备份。|
|[查看备份列表](/intl.zh-CN/API 参考/备份/查看备份列表.md)|查看RDS备份列表。|
|[查询备份设置](/intl.zh-CN/API 参考/备份/查询备份设置.md)|查看RDS实例备份设置。|
|[修改备份设置](/intl.zh-CN/API 参考/备份/修改备份设置.md)|修改RDS实例备份设置。|
|[删除数据备份](/intl.zh-CN/API 参考/备份/删除数据备份.md)|删除RDS实例数据备份文件。|
|[查询备份任务](/intl.zh-CN/API 参考/备份/查询备份任务.md)|查询RDS实例的备份任务列表。|
|[查询Binlog日志](/intl.zh-CN/API 参考/备份/查询Binlog日志.md)|查询RDS实例的Binlog文件。|

