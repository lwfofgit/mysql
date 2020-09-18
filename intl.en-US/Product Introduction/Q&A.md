# Q&A

This topic provides answers to some commonly asked questions about ApsaraDB for RDS.

-   Basic concepts
    -   [What is a database instance?](#section_ffn_rnj_6re)
    -   [What are primary and secondary RDS instances?](#section_cjg_u2w_f3j)
    -   [What are read-only RDS instances?](#section_f1r_e8w_hat)
-   Billing and purchase
    -   [Why am I charged additional fees for my subscription-billed RDS instance?](#section_ok7_0wt_4zq)
    -   [After I create an RDS instance, why does the ApsaraDB for RDS console not respond and why am I unable to find the RDS instance that I created?](#section_5e4_m6z_1aq)
    -   [Will I be charged for my pay-as-you-go-billed RDS instance that I am not using?](#section_2bj_use_4pb)
    -   [Can I switch between subscription billing and pay-as-you-go billing?](#section_ojs_eo0_brc)
    -   [How much do I need to pay if I change the specifications of my subscription-billed RDS instance?](#section_wdv_jkm_e65)
    -   [What will happen if my subscription-billed RDS instance expires or its payment is overdue?](#section_vr8_ewz_pso)
    -   [Is the inbound and outbound Internet traffic that is consumed for my pay-as-you-go- and subscription-billed RDS instances free of charge?](#section_qn5_9eq_3xh)
    -   [Do I need to pay when I apply for a public endpoint?](#section_n8a_lv5_mqc)
    -   [When the same CPU and memory specifications are used, an entry-level RDS instance supports a larger maximum number of connections and delivers higher input/output operations per second \(IOPS\) than an enterprise-level RDS instance. Why?](#section_z4r_eqe_ui8)
-   Instance management
    -   [How do I authorize a RAM user to manage my RDS instance?](#section_a01_3be_76g)
    -   [How do I change the storage type of my RDS instance among local SSD, standard SSD, and enhanced SSD?](#section_fee_nog_yo5)
    -   [How much time is required to expand the storage capacity of my RDS instance?](#section_kew_v07_i2i)
    -   [When I upgrade my primary RDS instance, will ApsaraDB for RDS automatically upgrade its read-only RDS instances?](#section_k18_jdc_lxy)
    -   [When I change the specifications of my RDS instance, will my online workloads be interrupted?](#section_ch3_nzp_v6n)
    -   [After I change the specifications of my RDS instance, will its endpoints change?](#section_76z_1fv_qb1)
    -   [How do I change the VPC of my RDS instance?](#section_cli_kcd_v6p)
    -   [Can I access my secondary RDS instance?](#section_1ha_ug8_hg0)
    -   [If my RDS instance resides in a VPC, how many private IP addresses does it occupy?](#section_75r_gs0_260)
-   Security
    -   [After I configure an IP address whitelist for my RDS instance, is the IP address whitelist immediately applied?](#section_d5m_4qb_mhg)
    -   [Why do I find IP address whitelists that I did not create?](#section_93e_g99_sk5)
    -   [If I disable Internet access and enable only internal network access, will my RDS instance be exposed to security risks?](#section_rm7_kcn_rpy)
    -   [If I do not update the expired SSL certificate, will my RDS instance malfunction or its data security deteriorate?](#section_29n_w8a_esi)
-   Audit

    [How do I obtain the size of SQL logs that are generated by the SQL Explorer feature?](#section_ycn_97y_thi)

-   Connection
    -   [What do I do if I cannot connect an ECS instance to an ApsaraDB for RDS instance?](/intl.en-US/FAQs/Connections and Networks/What do I do if I cannot connect an ECS instance to an ApsaraDB for RDS instance?.md)
    -   [If my application resides outside the VPC of my RDS instance, can it communicate with my RDS instance?](#section_4u1_mdw_fn5)
    -   [Does a primary/secondary switchover trigger changes to the endpoints and port numbers of my RDS instance?](#section_fll_r2e_ox9)
-   Database and account management
    -   [Can I manage accounts on my RDS instance at more granular levels, such as the source IP address and table levels?](#section_op9_gkr_rel)
    -   [Which specific permissions do privileged and standard accounts have?](#section_eep_5jp_tiw)
    -   [Does ApsaraDB for RDS provide accounts that are equivalent to root or super users?](#section_x6k_n67_z67)
    -   [Can I manage the accounts created on my primary RDS instance from its read-only RDS instances?](#section_va9_n55_v73)
-   Read-only instance and read/write splitting
    -   [When I upgrade my primary RDS instance, will ApsaraDB for RDS automatically upgrade its read-only RDS instances?](#section_gyf_7a2_b01)
    -   [After I set the read weight of a read-only instance to 0, can I still connect to the read-only RDS instance?](#section_4jv_8uf_52j)
    -   [If I release a read-only RDS instance, will my workloads be interrupted?](#section_6jn_1pu_iy2)
    -   [What can I do if read/write splitting becomes abnormal?](#section_aph_ldz_afl)
-   Backup and restoration
    -   [Can I disable the data backup function of my ApsaraDB RDS for MySQL instance?](#section_bbb_307_bll)
    -   [Can I disable the log backup function of my ApsaraDB RDS for MySQL instance?](#section_qj5_nuz_bsy)
    -   [Why does a backup fail?](#section_hzn_nb6_bxe)
    -   [Why do I find two log backup files with the same name on the Log Backup tab?](#section_zea_7jn_0sz)
    -   [What can I do with the data and log backup files that I downloaded?](#section_zgt_8ui_0ce)
    -   [Why does my RDS instance have a small volume of data but the size of the generated snapshot is large?](#section_8eq_hkf_l5b)

## What is a database instance?

A database instance is a database server on which you can create one or more databases. Each database can house one or more tables.

## What are primary and secondary RDS instances?

In the RDS High-availability, Cluster, or Enterprise Edition, your database system consists of one primary RDS instance and one or two secondary RDS instances. The primary RDS instance is used to communicate with your application. In addition, the primary RDS instance synchronizes data to its secondary RDS instance in real time.

If the primary RDS instance is working as normal, its secondary RDS instance serves as a backup and does not provide database services. If the primary RDS instance becomes abnormal, your database system fails over to its secondary RDS instance. In this case, the primary RDS instance is demoted as a secondary RDS instance, and its secondary RDS instance is promoted as the primary RDS instance. During the failover, your database service remains available. However, a transient connection error may occur.

For more information about the primary and secondary RDS instances in each RDS edition, see [Overview of ApsaraDB for RDS editions](/intl.en-US/Product Introduction/Product editions/Overview of ApsaraDB for RDS editions.md).

## What are read-only RDS instances?

Read-only RDS instances are provided to scale the read capability of your database system. If a large number of read requests overwhelm the primary RDS instance, your workloads may be interrupted. In this case, you can create one or more read-only RDS instances to offload read requests from the primary RDS instance. This ensures the stability of your database system and increases the throughput of your application.

For more information, see [Overview of ApsaraDB RDS for MySQL read-only instances](/intl.en-US/RDS MySQL Database/Read-only instances/Overview of ApsaraDB RDS for MySQL read-only instances.md).

## Why am I charged additional fees for my subscription-billed RDS instance?

The fee that you pay when you purchase your subscription-billed RDS instance covers only the instance and its storage capacity. If you create read-only RDS instances, enable the SQL Explorer or performance monitoring feature, or use more storage than that is allowed by the free quota for backup storage, you must pay the required additional fees. For more information, see [Pricing, billable items, and billing methods](/intl.en-US/Purchase Guide/Pricing, billable items, and billing methods.md).

## After I create an RDS instance, why does the ApsaraDB for RDS console not respond and why am I unable to find the RDS instance that I created?

This issue may occur due to the following two reasons:

-   The RDS instance that you created does not reside in the selected region.

    In the top navigation bar, select the region where the RDS instance resides. Then, you can find the RDS instance that you created.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

-   The selected zone cannot provide sufficient resources.

    Resources in zones are dynamically allocated. After you submit your purchase order, the selected zone may be unable to provide sufficient resources. As a result, the RDS instance cannot be created. In this case, we recommend that you select another zone and try again. If the RDS instance cannot be created, you can go to [the Orders page](https://billing.console.aliyun.com/?#/order/list/) in the Billing Management console to view the refunded fees.


## Will I be charged for my pay-as-you-go-billed RDS instance that I am not using?

Yes, you are still charged an hourly fee for your pay-as-you-go-billed instance that you are not using. This is because a pay-as-you-go-billed RDS instance consumes computing and storage resources even if it is not used. If you do not intend to use your pay-as-you-go-billed RDS instance for a long period of time, we recommend that you save the required data and then release the instance.

## Can I switch between subscription billing and pay-as-you-go billing?

Yes, you can switch between subscription billing and pay-as-you-go billing. For more information, see [Switch the billing method from pay-as-you-go to subscription](/intl.en-US/RDS MySQL Database/Instance Change/Switch the billing method from pay-as-you-go to subscription.md) and [Switch the billing method from subscription to pay-as-you-go](/intl.en-US/RDS MySQL Database/Instance Change/Switch the billing method from subscription to pay-as-you-go.md).

## How much do I need to pay if I change the specifications of my subscription-billed RDS instance?

For more information, see [Specification change fees](/intl.en-US/Purchase Guide/Specification change fees.md).

## What will happen if my subscription-billed RDS instance expires or its payment is overdue?

For more information, see [Unlock an instance that expires or is overdue](/intl.en-US/Purchase Guide/Unlock an instance that expires or is overdue.md).

## Is the inbound and outbound Internet traffic that is consumed for my pay-as-you-go- and subscription-billed RDS instances free of charge?

Yes, all of the inbound and outbound Internet traffic that is consumed for your pay-as-you-go- and subscription-billed RDS instances is free of charge.

## Do I need to pay when I apply for a public endpoint?

No, you are not charged when you apply for a public endpoint.

## When the same CPU and memory specifications are used, an entry-level RDS instance supports a larger maximum number of connections and delivers higher input/output operations per second \(IOPS\) than an enterprise-level RDS instance. Why?

An entry-level RDS instance belongs to the shared or general-purpose instance family, whereas an enterprise-level RDS instance belongs to the dedicated instance family. The shared and general-purpose instance families support the reuse of CPU resources. This allows an entry-level RDS instance to support a larger maximum number of connections and deliver higher IOPS. However, the dedicated instance family supports the exclusive allocations of CPU and memory resources. This allows an enterprise-level RDS instance to run more stably. For more information, see [Instance families](/intl.en-US/Product Introduction/Product specifications/Instance families.md).

## How do I authorize a RAM user to manage my RDS instance?

For more information, see [Use RAM to manage ApsaraDB for RDS permissions](https://www.alibabacloud.com/help/zh/doc-detail/58932.htm).

## How do I change the storage type of my RDS instance among local SSD, standard SSD, and enhanced SSD?

For more information, see [How to change a cloud disk to a local disk](/intl.en-US/FAQs/Purchases and Payments/How do I change an SSD to a local SSD?.md)

## How much time is required to expand the storage capacity of my RDS instance?

The required time varies based on whether the physical host that houses your RDS instance can provide sufficient remaining storage capacity for your expansion plan. If the remaining storage capacity is sufficient, you do not need to migrate the data of your RDS instance and therefore the required time is short. If the remaining storage capacity is insufficient, you must migrate the data of your RDS instance to another qualified physical host before you start the expansion. This is complex and time-consuming.

## When I upgrade my primary RDS instance, will ApsaraDB for RDS automatically upgrade its read-only RDS instances?

No, after you upgrade your primary RDS instance, you must manually upgrade its read-only RDS instances.

## When I change the specifications of my RDS instance, will my online workloads be interrupted?

No, when you change the specifications of your RDS instance, your online workloads will not be interrupted. However, a transient connection error of about 30 seconds may occur during the subsequent switchover.

## After I change the specifications of my RDS instance, will its endpoints change?

After you change the specifications of your RDS instance, its internal, public, and read/write splitting endpoints remain unchanged. However, the IP addresses that are associated with the endpoints may change. For more information, see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance.md) and [Enable the read/write splitting function in the shared proxy of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Shared proxy (phased-out)/Enable the read/write splitting function in the shared proxy of an ApsaraDB RDS for MySQL instance.md). We recommend that you use the internal, public, or read/write splitting endpoint of your RDS instance to establish a connection from your application.

## How do I change the VPC of my RDS instance?

-   If your RDS instance supports VPC and VSwitch changes, you can directly perform these changes. For more information, see [Switch to a new VPC and VSwitch for an RDS MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/Switch to a new VPC and VSwitch for an RDS MySQL instance.md).
-   If your RDS instance supports network type changes, perform the following operations:
    1.  Change the network type from VPC to classic network.
    2.  Change the network type from classic network to VPC with the required VPC selected.
-   If your RDS instance does not support network type changes, perform the following operations:

    Purchase a new RDS instance that resides in the required VPC, and then migrate the data of your RDS instance to the new RDS instance. For more information, see [Migrate data between ApsaraDB for RDS instances](/intl.en-US/RDS MySQL Database/Data Migration/Migrate data between ApsaraDB for RDS instances.md).


## Can I access my secondary RDS instance?

No, you cannot access your secondary RDS instance. You can access only your primary RDS instance. Your secondary RDS instance serves only as a backup and does not provide services.

## If my RDS instance resides in a VPC, how many private IP addresses does it occupy?

The number of private IP addresses that your RDS instance occupies varies based on the selected database engine and RDS edition.

-   MySQL 5.5, 5.6, 5.7, and 8.0 on RDS High-availability Edition \(with local SSDs\): 1
-   MySQL 5.6, 5.7, and 8.0 on RDS Enterprise Edition \(with local SSDs\): 1
-   MySQL 5.7 on RDS Basic Edition \(with standard SSDs\): 1
-   MySQL 8.0 on RDS Basic Edition \(with standard SSDs\): 2
-   MySQL 5.7 and 8.0 on RDS High-availability Edition \(with standard or enhanced SSDs\): 3
-   MySQL 5.7 and 8.0 on RDS Enterprise Edition \(with standard or enhanced SSDs\): 1

## After I configure an IP address whitelist for my RDS instance, is the IP address whitelist immediately applied?

No, after you configure an IP address whitelist for your RDS instance, the IP address whitelist requires about 1 minute to be applied.

## Why do I find IP address whitelists that I did not create?

If the IP address whitelists consist of private IP addresses, these IP address whitelists are probably created by other Alibaba Cloud services, such as Data Management \(DMS\) and Database Autonomy Service \(DAS\). These IP address whitelists do not affect your data and can be ignored.

![IP address whitelist created by HDM](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5450359951/p68936.png)

## If I disable Internet access and enable only internal network access, will my RDS instance be exposed to security risks?

We recommend that you change the network type of your RDS instance to VPC. In this case, only an ECS instance in the same VPC can access your RDS instance after the required IP address is added to an IP address whitelist of your RDS instance. For more information, see [Change the network type of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/Change the network type of an ApsaraDB RDS for MySQL instance.md).

## If I do not update the expired SSL certificate, will my RDS instance malfunction or its data security deteriorate?

If you do not update the expired SSL certificate, your RDS instance can still run and its data security does not deteriorate. However, your application that uses encrypted connections to communicate with your RDS instance is disconnected.

## How do I obtain the size of SQL logs that are generated by the SQL Explorer feature?

Log on to the ApsaraDB for RDS console, find your RDS instance, and go to the **Basic Information** page. In the **Usage Statistics** section of the page, you can view the size of SQL logs that are generated by the SQL Explorer feature.

![Log Size](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2540359951/p67321.png)

## If my application resides outside the VPC of my RDS instance, can it communicate with my RDS instance?

If the IP address of your application is added to an IP address whitelist of your RDS instance, your application can communicate with your RDS instance over the Internet. This applies regardless of whether your application resides in a VPC or the classic network. For more information, see [Control access to an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Control access to an ApsaraDB RDS for MySQL instance.md).

## Does a primary/secondary switchover trigger changes to the endpoints and port numbers of my RDS instance?

No, a primary/secondary switchover does not trigger changes to the endpoints or port numbers of your RDS instance. Only the IP addresses that are associated with the endpoints change. Your application can still connect to your RDS instance by using the endpoints.

## Can I manage accounts on my RDS instance at more granular levels, such as the source IP address and table levels?

Yes, you can log on to your RDS instance and then use commands to grant permissions to accounts at more granular levels. For more information, see [Connect to an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Connect to an ApsaraDB RDS for MySQL instance.md).

## Which specific permissions do privileged and standard accounts have?

For more information, see [Create accounts and databases for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create accounts and databases for an ApsaraDB RDS for MySQL instance.md).

## Does ApsaraDB for RDS provide accounts that are equivalent to root or super users?

No, ApsaraDB for RDS does not provide accounts that are equivalent to root or super users. This allows you to protect your RDS instance from data losses and leaks caused by unintentional operations.

## Can I manage the accounts created on my primary RDS instance from its read-only RDS instances?

No, although the accounts created on your primary RDS instance are synchronized to its read-only RDS instances, you cannot manage the accounts on the read-only RDS instances. The accounts only have the read permissions on the read-only RDS instances.

## When I upgrade my primary RDS instance, will ApsaraDB for RDS automatically upgrade its read-only RDS instances?

No, after you upgrade your primary RDS instance, you must manually upgrade its read-only RDS instances. For more information, see [Change the specifications of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the specifications of an ApsaraDB RDS for MySQL instance.md).

## After I set the read weight of a read-only instance to 0, can I still connect to the read-only RDS instance?

Yes, after you set the read weight of a read-only RDS instance to 0, you can connect to the read-only RDS instance by using its internal or public endpoint. However, you cannot connect to the read-only RDS instance by using its read/write splitting endpoint. For more information, see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance.md). This function is provided for you to configure a read-only RDS instance to process only specific workloads.

## If I release a read-only RDS instance, will my workloads be interrupted?

Yes, if you release a read-only RDS instance, your workloads will be interrupted. Before you release a read-only RDS instance, we recommend that you set its read weight to 0. For more information, see [Modify the latency threshold and read weights of ApsaraDB RDS for MySQL instances](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Shared proxy (phased-out)/Modify the latency threshold and read weights of ApsaraDB RDS for MySQL instances.md). However, the cached connection with your database system remains valid on the released read-only RDS instance. You must close the connection and establish a new one.

## What can I do if read/write splitting becomes abnormal?

For more information, see [FAQ on read/write splitting](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Shared proxy (phased-out)/FAQ on read/write splitting.md).

## Can I disable the data backup function of my ApsaraDB RDS for MySQL instance?

No, you cannot disable the data backup function of your ApsaraDB RDS for MySQL instance. However, you can reduce the backup frequency to as low as twice a week. The data backup retention period must span at least seven days.

## Can I disable the log backup function of my ApsaraDB RDS for MySQL instance?

Yes, if your ApsaraDB RDS for MySQL instance does not run the RDS Basic Edition, you can disable the log backup function in the ApsaraDB for RDS console.

## Why does a backup fail?

Data definition language \(DDL\) statements trigger locks on tables. If you execute DDL statements during a backup, the backup may fail as a result of the table locks.

## Why do I find two log backup files with the same name on the Log Backup tab?

In the RDS High-availability Edition, your database system consists of a primary RDS instance and a secondary RDS instance. Both instances generate log backup files. Each log backup file is identified by an **Instance ID** on the Log Backup tab. The instance IDs allow you to distinguish the log backup files that are generated by the primary RDS instance from those that are generated by the secondary RDS instance. On the Service Availability page, you can view the IDs of the primary and secondary RDS instances based on the Primary Instance No. and Secondary Instance No. fields.

![Primary Instance No. and Secondary Instance No.](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3530359951/p38570.png)

## What can I do with the data and log backup files that I downloaded?

You can use the downloaded data and log backup files to restore data at any time. For more information, see [Use a physical backup file to restore an ApsaraDB RDS for MySQL instance to a user-created MySQL database](/intl.en-US/RDS MySQL Database/Restoration/Use a physical backup file to restore an ApsaraDB RDS for MySQL instance to a user-created MySQL database.md) and [Restore data from logical backup files of an ApsaraDB RDS for MySQL instance to a user-created database](/intl.en-US/RDS MySQL Database/Restoration/Restore data from logical backup files of an ApsaraDB RDS for MySQL instance to a user-created database.md).

## Why does my RDS instance have a small volume of data but the size of the generated snapshot is large?

When ApsaraDB for RDS takes a snapshot of your RDS instance, it eliminates empty blocks. This allows the size of the snapshot to be smaller than the required disk space. Each block is 2 MB in size. If write operations are dispersed, a large number of blocks are not full. For example, 3 MB of data may be written into two, three, or four blocks, and none of these blocks is full. When ApsaraDB for RDS calculates the size of the snapshot, it counts in all of these non-empty blocks to which data is written. As a result, the disk space occupied by the snapshot is greater than the actual size of the snapshot.
