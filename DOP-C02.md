| ﻿问题编号 | 问题本身（英文） | 各选项（英文） | 翻译问题本身 | 分析各选项（中文） | 答案 |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | A company has a mobile application that makes HTTP API calls to an Application Load Balancer (ALB). The ALB routes requests to an AWS
Lambda function. Many different versions of the application are in use at any given time, including versions that are in testing by a subset of
users. The version of the application is dened in the user-agent header that is sent with all requests to the API.
After a series of recent changes to the API, the company has observed issues with the application. The company needs to gather a metric for
each API operation by response code for each version of the application that is in use. A DevOps engineer has modied the Lambda function
to extract the API operation name, version information from the user-agent header and response code. | A. Modify the Lambda function to write the API operation name, response code, and version number as a log line to an Amazon
CloudWatch Logs log group. Congure a CloudWatch Logs metric lter that increments a metric for each API operation name. Specify
response code and application version as dimensions for the metric.
B. Modify the Lambda function to write the API operation name, response code, and version number as a log line to an Amazon
CloudWatch Logs log group. Congure a CloudWatch Logs Insights query to populate CloudWatch metrics from the log lines. Specify
response code and application version as dimensions for the metric.
C. Congure the ALB access logs to write to an Amazon CloudWatch Logs log group. Modify the Lambda function to respond to the ALB
with the API operation name, response code, and version number as response metadata. Congure a CloudWatch Logs metric lter that
increments a metric for each API operation name. Specify response code and application version as dimensions for the metric.
D. Congure AWS X-Ray integration on the Lambda function. Modify the Lambda function to create an X-Ray subsegment with the API
operation name, response code, and version number. Congure X-Ray insights to extract an aggregated metric for each API operation
name and to publish the metric to Amazon CloudWatch. Specify response code and application version as dimensions for the metric. | 一家公司有一个移动应用程序，该程序向应用程序负载均衡器(ALB)发出HTTP API调用。ALB将请求路由到AWS Lambda函数。在任何给定时间都有许多不同版本的应用程序在使用，包括正在由部分用户测试的版本。应用程序的版本在发送给API的所有请求的user-agent头中定义。

在最近对API进行一系列更改后，公司观察到应用程序出现了问题。公司需要为正在使用的每个应用程序版本收集按响应代码分类的每个API操作的指标。DevOps工程师已经修改了Lambda函数，以提取API操作名称、从user-agent头中获取版本信息和响应代码。

 | **选项A：** 修改Lambda函数，将API操作名称、响应代码和版本号作为日志行写入Amazon CloudWatch Logs日志组。配置CloudWatch Logs指标过滤器，为每个API操作名称递增指标。将响应代码和应用程序版本指定为指标的维度。
- **正确性：高** - 这是一个直接有效的解决方案。CloudWatch Logs指标过滤器可以实时处理日志并创建自定义指标，支持多维度指标。

**选项B：** 修改Lambda函数，将API操作名称、响应代码和版本号作为日志行写入Amazon CloudWatch Logs日志组。配置CloudWatch Logs Insights查询从日志行填充CloudWatch指标。将响应代码和应用程序版本指定为指标的维度。
- **正确性：低** - CloudWatch Logs Insights主要用于交互式查询和分析，不是用来实时创建指标的工具。它不能自动持续地将日志转换为指标。

**选项C：** 配置ALB访问日志写入Amazon CloudWatch Logs日志组。修改Lambda函数以响应ALB，将API操作名称、响应代码和版本号作为响应元数据。配置CloudWatch Logs指标过滤器，为每个API操作名称递增指标。将响应代码和应用程序版本指定为指标的维度。
- **正确性：中等** - 虽然技术上可行，但这种方法更复杂，需要额外配置ALB访问日志，并且依赖于响应元数据的解析，不如直接在Lambda中记录日志简单。

**选项D：** 在Lambda函数上配置AWS X-Ray集成。修改Lambda函数创建包含API操作名称、响应代码和版本号的X-Ray子段。配置X-Ray insights提取每个API操作名称的聚合指标并将指标发布到Amazon CloudWatch。将响应代码和应用程序版本指定为指标的维度。
- **正确性：低** - X-Ray主要用于分布式跟踪和性能分析，虽然可以提供一些指标，但不是为创建自定义业务指标而设计的最佳工具。

 | A |  |  |
| 2 | A company provides an application to customers. The application has an Amazon API Gateway REST API that invokes an AWS Lambda
function. On initialization, the Lambda function loads a large amount of data from an Amazon DynamoDB table. The data load process results
in long cold-start times of 8-10 seconds. The DynamoDB table has DynamoDB Accelerator (DAX) congured.
Customers report that the application intermittently takes a long time to respond to requests. The application receives thousands of requests
throughout the day. In the middle of the day, the application experiences 10 times more requests than at any other time of the day. Near the
end of the day, the application's request volume decreases to 10% of its normal total.
A DevOps engineer needs to reduce the latency of the Lambda function at all times of the day. | A. Congure provisioned concurrency on the Lambda function with a concurrency value of 1. Delete the DAX cluster for the DynamoDB
table.
B. Congure reserved concurrency on the Lambda function with a concurrency value of 0.
C. Congure provisioned concurrency on the Lambda function. Congure AWS Application Auto Scaling on the Lambda function with
provisioned concurrency values set to a minimum of 1 and a maximum of 100.
D. Congure reserved concurrency on the Lambda function. Congure AWS Application Auto Scaling on the API Gateway API with a
reserved concurrency maximum value of 100. | 一家公司为客户提供应用程序。该应用程序有一个Amazon API Gateway REST API，它调用AWS Lambda函数。在初始化时，Lambda函数从Amazon DynamoDB表中加载大量数据。数据加载过程导致8-10秒的长冷启动时间。DynamoDB表已配置了DynamoDB Accelerator (DAX)。

客户报告应用程序间歇性地需要很长时间才能响应请求。应用程序全天接收数千个请求。在一天的中间时段，应用程序经历的请求量是其他任何时间的10倍。在一天接近结束时，应用程序的请求量降至正常总量的10%。

DevOps工程师需要在一天的所有时间都减少Lambda函数的延迟。

 | **选项A：** 在Lambda函数上配置预置并发，并发值为1。删除DynamoDB表的DAX集群。
- 错误：预置并发值为1太低，无法处理高峰期的10倍流量
- 错误：删除DAX集群会增加DynamoDB访问延迟，与减少延迟的目标相反
- DAX是用于加速DynamoDB读取的缓存服务，删除它会恶化性能

**选项B：** 在Lambda函数上配置保留并发，并发值为0。
- 错误：保留并发值为0意味着函数无法执行任何请求
- 这完全不能解决问题，反而会阻止所有请求的处理

**选项C：** 在Lambda函数上配置预置并发。在Lambda函数上配置AWS Application Auto Scaling，预置并发值设置为最小1，最大100。
- 正确：预置并发可以消除冷启动问题，保持函数始终处于温热状态
- 正确：Auto Scaling可以根据流量变化自动调整预置并发数量
- 正确：最小值1确保始终有预热的实例，最大值100可以处理高峰期的10倍流量
- 正确：在低流量时期会自动缩减，节省成本

**选项D：** 在Lambda函数上配置保留并发。在API Gateway API上配置AWS Application Auto Scaling，保留并发最大值为100。
- 错误：保留并发不能解决冷启动问题，只是限制最大并发数
- 错误：API Gateway不支持基于保留并发的Auto Scaling配置
- 错误：这种配置无法解决Lambda函数的冷启动延迟问题

 |  |  |  |
| 3 | A company is adopting AWS CodeDeploy to automate its application deployments for a Java-Apache Tomcat application with an Apache
Webserver. The development team started with a proof of concept, created a deployment group for a developer environment, and performed
functional tests within the application. After completion, the team will create additional deployment groups for staging and production.
The current log level is congured within the Apache settings, but the team wants to change this conguration dynamically when the
deployment occurs, so that they can set different log level congurations depending on the deployment group without having a different
application revision for each group.
How can these requirements be met with the LEAST management overhead and without requiring different script versions for each
deployment group? | A. Tag the Amazon EC2 instances depending on the deployment group. Then place a script into the application revision that calls the
metadata service and the EC2 API to identify which deployment group the instance is part of. Use this information to congure the log
level settings. Reference the script as part of the AfterInstall lifecycle hook in the appspec.yml le.
B. Create a script that uses the CodeDeploy environment variable DEPLOYMENT_GROUP_ NAME to identify which deployment group the
instance is part of. Use this information to congure the log level settings. Reference this script as part of the BeforeInstall lifecycle hook
in the appspec.yml le.
C. Create a CodeDeploy custom environment variable for each environment. Then place a script into the application revision that checks
this environment variable to identify which deployment group the instance is part of. Use this information to congure the log level
settings. Reference this script as part of the ValidateService lifecycle hook in the appspec.yml le.
D. Create a script that uses the CodeDeploy environment variable DEPLOYMENT_GROUP_ID to identify which deployment group the
instance is part of to congure the log level settings. Reference this script as part of the Install lifecycle hook in the appspec.yml le. | 一家公司正在采用AWS CodeDeploy来自动化其Java-Apache Tomcat应用程序与Apache Web服务器的应用部署。开发团队从概念验证开始，为开发环境创建了一个部署组，并在应用程序内执行了功能测试。完成后，团队将为预发布和生产环境创建额外的部署组。

当前的日志级别在Apache设置中配置，但团队希望在部署发生时动态更改此配置，以便他们可以根据部署组设置不同的日志级别配置，而无需为每个组准备不同的应用程序版本。

如何以最少的管理开销满足这些要求，且不需要为每个部署组准备不同的脚本版本？

 | **选项A：** 根据部署组标记Amazon EC2实例。然后在应用程序版本中放置一个脚本，该脚本调用元数据服务和EC2 API来识别实例属于哪个部署组。使用此信息配置日志级别设置。在appspec.yml文件中将脚本作为AfterInstall生命周期钩子的一部分引用。
- 分析：这种方法需要额外的EC2标记管理和API调用，增加了复杂性和管理开销。不是最优解。

**选项B：** 创建一个使用CodeDeploy环境变量DEPLOYMENT_GROUP_NAME来识别实例属于哪个部署组的脚本。使用此信息配置日志级别设置。在appspec.yml文件中将此脚本作为BeforeInstall生命周期钩子的一部分引用。
- 分析：DEPLOYMENT_GROUP_NAME是CodeDeploy提供的内置环境变量，可以直接获取部署组名称。BeforeInstall钩子在应用程序安装之前执行，适合进行配置准备工作。这是一个简洁有效的解决方案。

**选项C：** 为每个环境创建CodeDeploy自定义环境变量。然后在应用程序版本中放置一个脚本，检查此环境变量以识别实例属于哪个部署组。使用此信息配置日志级别设置。在appspec.yml文件中将此脚本作为ValidateService生命周期钩子的一部分引用。
- 分析：需要创建和管理自定义环境变量，增加了管理开销。ValidateService钩子用于验证服务，不是配置设置的最佳时机。

**选项D：** 创建一个使用CodeDeploy环境变量DEPLOYMENT_GROUP_ID来识别实例属于哪个部署组的脚本，以配置日志级别设置。在appspec.yml文件中将此脚本作为Install生命周期钩子的一部分引用。
- 分析：DEPLOYMENT_GROUP_ID提供的是ID而不是名称，对于基于名称的配置逻辑不够直观。Install钩子主要用于文件复制，不是配置修改的最佳时机。

 |  |  |  |
| 4 | A company requires its developers to tag all Amazon Elastic Block Store (Amazon EBS) volumes in an account to indicate a desired backup
frequency. This requirement Includes EBS volumes that do not require backups. The company uses custom tags named Backup_Frequency
that have values of none, dally, or weekly that correspond to the desired backup frequency. An audit nds that developers are occasionally not
tagging the EBS volumes.
A DevOps engineer needs to ensure that all EBS volumes always have the Backup_Frequency tag so that the company can perform backups at
least weekly unless a different value is specied. | A. Set up AWS Cong in the account. Create a custom rule that returns a compliance failure for all Amazon EC2 resources that do not have
a Backup Frequency tag applied. Congure a remediation action that uses a custom AWS Systems Manager Automation runbook to apply
the Backup_Frequency tag with a value of weekly.
B. Set up AWS Cong in the account. Use a managed rule that returns a compliance failure for EC2::Volume resources that do not have a
Backup Frequency tag applied. Congure a remediation action that uses a custom AWS Systems Manager Automation runbook to apply
the Backup_Frequency tag with a value of weekly.
C. Turn on AWS CloudTrail in the account. Create an Amazon EventBridge rule that reacts to EBS CreateVolume events. Congure a
custom AWS Systems Manager Automation runbook to apply the Backup_Frequency tag with a value of weekly. Specify the runbook as the
target of the rule.
D. Turn on AWS CloudTrail in the account. Create an Amazon EventBridge rule that reacts to EBS CreateVolume events or EBS
ModifyVolume events. Congure a custom AWS Systems Manager Automation runbook to apply the Backup_Frequency tag with a value of
weekly. Specify the runbook as the target of the rule. | 一家公司要求其开发人员为账户中的所有Amazon弹性块存储(Amazon EBS)卷打标签，以指示所需的备份频率。此要求包括不需要备份的EBS卷。公司使用名为Backup_Frequency的自定义标签，其值为none、daily或weekly，对应所需的备份频率。审计发现开发人员偶尔不会为EBS卷打标签。

DevOps工程师需要确保所有EBS卷始终具有Backup_Frequency标签，以便公司可以至少每周执行一次备份，除非指定了不同的值。

 | **选项A：** 
- 设置AWS Config并创建自定义规则，对所有没有Backup_Frequency标签的Amazon EC2资源返回合规性失败
- 问题：范围过于宽泛，针对所有EC2资源而不是专门针对EBS卷
- 优点：使用Config进行合规性监控和自动修复

**选项B：**
- 设置AWS Config并使用托管规则，对没有Backup_Frequency标签的EC2::Volume资源返回合规性失败
- 优点：精确针对EBS卷(EC2::Volume)，使用托管规则更可靠，配置自动修复
- 这是最精确和高效的解决方案

**选项C：**
- 启用CloudTrail并创建EventBridge规则响应EBS CreateVolume事件
- 问题：只处理新创建的卷，不处理现有的未标记卷
- 不能解决审计发现的现有卷缺少标签的问题

**选项D：**
- 启用CloudTrail并创建EventBridge规则响应CreateVolume和ModifyVolume事件
- 问题：仍然只是响应式处理，不能处理现有的未标记卷
- ModifyVolume事件与标签管理无直接关系

 |  |  |  |
| 5 | A company is using an Amazon Aurora cluster as the data store for its application. The Aurora cluster is congured with a single DB instance.
The application performs read and write operations on the database by using the cluster's instance endpoint.
The company has scheduled an update to be applied to the cluster during an upcoming maintenance window. The cluster must remain
available with the least possible interruption during the maintenance window. | A. Add a reader instance to the Aurora cluster. Update the application to use the Aurora cluster endpoint for write operations. Update the
Aurora cluster's reader endpoint for reads.
B. Add a reader instance to the Aurora cluster. Create a custom ANY endpoint for the cluster. Update the application to use the Aurora
cluster's custom ANY endpoint for read and write operations.
C. Turn on the Multi-AZ option on the Aurora cluster. Update the application to use the Aurora cluster endpoint for write operations.
Update the Aurora cluster’s reader endpoint for reads.
D. Turn on the Multi-AZ option on the Aurora cluster. Create a custom ANY endpoint for the cluster. Update the application to use the
Aurora cluster's custom ANY endpoint for read and write operations | 一家公司正在使用Amazon Aurora集群作为其应用程序的数据存储。该Aurora集群配置了单个数据库实例。应用程序通过使用集群的实例端点对数据库执行读写操作。公司已安排在即将到来的维护窗口期间对集群应用更新。集群必须在维护窗口期间保持可用，并且中断时间尽可能少。

 | **选项A：** 向Aurora集群添加一个读取器实例。更新应用程序以使用Aurora集群端点进行写操作。更新Aurora集群的读取器端点用于读取操作。
- **正确性：高** - 这是标准的Aurora高可用性配置
- 添加读取器实例提供了故障转移能力
- 使用集群端点（写入）和读取器端点（读取）是AWS推荐的最佳实践
- 在维护期间，如果主实例需要重启，可以快速故障转移到读取器实例

**选项B：** 向Aurora集群添加一个读取器实例。为集群创建自定义ANY端点。更新应用程序以使用Aurora集群的自定义ANY端点进行读写操作。
- **正确性：中等** - 技术上可行但不是最佳实践
- ANY端点会将连接路由到任何可用实例，但这可能导致读写操作路由到不合适的实例
- 不如使用专门的集群端点和读取器端点来区分读写操作

**选项C：** 在Aurora集群上启用Multi-AZ选项。更新应用程序以使用Aurora集群端点进行写操作。更新Aurora集群的读取器端点用于读取操作。
- **正确性：低** - 概念混淆
- Aurora本身就是Multi-AZ的，不需要单独"启用Multi-AZ选项"
- Aurora的Multi-AZ是通过添加读取器实例实现的，而不是像RDS那样的独立选项

**选项D：** 在Aurora集群上启用Multi-AZ选项。为集群创建自定义ANY端点。更新应用程序以使用Aurora集群的自定义ANY端点进行读写操作。
- **正确性：低** - 结合了选项B和C的问题
- 同样存在对Aurora Multi-AZ的误解
- ANY端点不是处理读写分离的最佳方式

 |  |  |  |
| 6 | A company must encrypt all AMIs that the company shares across accounts. A DevOps engineer has access to a source account where an
unencrypted custom AMI has been built. The DevOps engineer also has access to a target account where an Amazon EC2 Auto Scaling group
will launch EC2 instances from the AMI. The DevOps engineer must share the AMI with the target account.
The company has created an AWS Key Management Service (AWS KMS) key in the source account. | A. In the source account, copy the unencrypted AMI to an encrypted AMI. Specify the KMS key in the copy action.
B. In the source account, copy the unencrypted AMI to an encrypted AMI. Specify the default Amazon Elastic Block Store (Amazon EBS)
encryption key in the copy action.
C. In the source account, create a KMS grant that delegates permissions to the Auto Scaling group service-linked role in the target
account.
D. In the source account, modify the key policy to give the target account permissions to create a grant. In the target account, create a
KMS grant that delegates permissions to the Auto Scaling group service-linked role.
E. In the source account, share the unencrypted AMI with the target account.
F. In the source account, share the encrypted AMI with the target account. | 一家公司必须加密所有跨账户共享的AMI。一名DevOps工程师可以访问源账户，该账户中已构建了一个未加密的自定义AMI。该DevOps工程师还可以访问目标账户，目标账户中的Amazon EC2 Auto Scaling组将从该AMI启动EC2实例。DevOps工程师必须与目标账户共享该AMI。

公司已在源账户中创建了一个AWS Key Management Service (AWS KMS) 密钥。

 | **A. 在源账户中，将未加密的AMI复制为加密的AMI。在复制操作中指定KMS密钥。**
- 正确。这是加密AMI的标准做法，可以使用指定的KMS密钥对AMI进行加密。

**B. 在源账户中，将未加密的AMI复制为加密的AMI。在复制操作中指定默认的Amazon Elastic Block Store (Amazon EBS) 加密密钥。**
- 部分正确，但不是最佳选择。使用默认EBS加密密钥可能会在跨账户共享时产生权限问题。

**C. 在源账户中，创建一个KMS授权，将权限委托给目标账户中的Auto Scaling组服务链接角色。**
- 不完整。仅创建授权不足以完成整个流程，还需要先加密AMI并共享。

**D. 在源账户中，修改密钥策略以给予目标账户创建授权的权限。在目标账户中，创建一个KMS授权，将权限委托给Auto Scaling组服务链接角色。**
- 正确。这是跨账户KMS密钥访问的标准配置方法。

**E. 在源账户中，与目标账户共享未加密的AMI。**
- 错误。题目明确要求必须加密所有共享的AMI。

**F. 在源账户中，与目标账户共享加密的AMI。**
- 正确。这是共享加密AMI的必要步骤。 |  |  |  |
| 7 | A company uses AWS CodePipeline pipelines to automate releases of its application A typical pipeline consists of three stages build, test, and
deployment. The company has been using a separate AWS CodeBuild project to run scripts for each stage. However, the company now wants
to use AWS CodeDeploy to handle the deployment stage of the pipelines.
The company has packaged the application as an RPM package and must deploy the application to a eet of Amazon EC2 instances. The EC2
instances are in an EC2 Auto Scaling group and are launched from a common AMI. | A. Create a new version of the common AMI with the CodeDeploy agent installed. Update the IAM role of the EC2 instances to allow
access to CodeDeploy.
B. Create a new version of the common AMI with the CodeDeploy agent installed. Create an AppSpec le that contains application
deployment scripts and grants access to CodeDeploy.
C. Create an application in CodeDeploy. Congure an in-place deployment type. Specify the Auto Scaling group as the deployment target.
Add a step to the CodePipeline pipeline to use EC2 Image Builder to create a new AMI. Congure CodeDeploy to deploy the newly created
AMI.
D. Create an application in CodeDeploy. Congure an in-place deployment type. Specify the Auto Scaling group as the deployment target.
Update the CodePipeline pipeline to use the CodeDeploy action to deploy the application.
E. Create an application in CodeDeploy. Congure an in-place deployment type. Specify the EC2 instances that are launched from the
common AMI as the deployment target. Update the CodePipeline pipeline to use the CodeDeploy action to deploy the application. | 一家公司使用AWS CodePipeline管道来自动化其应用程序的发布。典型的管道包含三个阶段：构建、测试和部署。该公司一直使用单独的AWS CodeBuild项目来为每个阶段运行脚本。但是，公司现在希望使用AWS CodeDeploy来处理管道的部署阶段。

公司已将应用程序打包为RPM包，并且必须将应用程序部署到一组Amazon EC2实例。这些EC2实例位于EC2 Auto Scaling组中，并从通用AMI启动。

 | **选项A：** 创建安装了CodeDeploy代理的通用AMI新版本。更新EC2实例的IAM角色以允许访问CodeDeploy。
- 分析：这个选项只涉及准备工作（安装代理和权限配置），但没有实际创建CodeDeploy应用程序或配置部署流程，不完整。

**选项B：** 创建安装了CodeDeploy代理的通用AMI新版本。创建包含应用程序部署脚本的AppSpec文件并授予对CodeDeploy的访问权限。
- 分析：同样只涉及准备工作，没有创建CodeDeploy应用程序或将其集成到CodePipeline中，不完整。

**选项C：** 在CodeDeploy中创建应用程序。配置就地部署类型。指定Auto Scaling组作为部署目标。向CodePipeline管道添加步骤以使用EC2 Image Builder创建新AMI。配置CodeDeploy部署新创建的AMI。
- 分析：这个方案过于复杂，使用EC2 Image Builder创建新AMI不是必需的，而且CodeDeploy不是用来部署AMI的，而是部署应用程序代码。

**选项D：** 在CodeDeploy中创建应用程序。配置就地部署类型。指定Auto Scaling组作为部署目标。更新CodePipeline管道以使用CodeDeploy操作来部署应用程序。
- 分析：这是完整的解决方案，包括创建CodeDeploy应用程序、配置正确的部署类型、指定合适的目标，并集成到CodePipeline中。

**选项E：** 在CodeDeploy中创建应用程序。配置就地部署类型。指定从通用AMI启动的EC2实例作为部署目标。更新CodePipeline管道以使用CodeDeploy操作来部署应用程序。
- 分析：虽然逻辑正确，但指定具体的EC2实例作为目标不如指定Auto Scaling组灵活，因为Auto Scaling组中的实例可能会动态变化。 |  |  |  |
| 8 | A company’s security team requires that all external Application Load Balancers (ALBs) and Amazon API Gateway APIs are associated with
AWS WAF web ACLs. The company has hundreds of AWS accounts, all of which are included in a single organization in AWS Organizations. The
company has congured AWS Cong for the organization. During an audit, the company nds some externally facing ALBs that are not
associated with AWS WAF web ACLs. | A. Delegate AWS Firewall Manager to a security account.
B. Delegate Amazon GuardDuty to a security account.
C. Create an AWS Firewall Manager policy to attach AWS WAF web ACLs to any newly created ALBs and API Gateway APIs.
D. Create an Amazon GuardDuty policy to attach AWS WAF web ACLs to any newly created ALBs and API Gateway APIs.
E. Congure an AWS Cong managed rule to attach AWS WAF web ACLs to any newly created ALBs and API Gateway APIs. | 公司的安全团队要求所有外部应用负载均衡器(ALB)和Amazon API Gateway API都必须与AWS WAF web ACL关联。公司有数百个AWS账户，全部包含在AWS Organizations的单个组织中。公司已为组织配置了AWS Config。在审计期间，公司发现一些面向外部的ALB没有与AWS WAF web ACL关联。
DevOps工程师应该采取哪些步骤组合来防止未来的违规？ | A. 将AWS Firewall Manager委托给安全账户。
✅ 专门设计：Firewall Manager专为Organizations环境中的集中化防火墙管理而设计
✅ 委托管理：支持委托给专门的安全账户进行集中管理
✅ 组织级别：可以跨所有成员账户执行策略
✅ 最佳实践：这是管理多账户WAF策略的标准方法
B. 将Amazon GuardDuty委托给安全账户。
❌ 功能不匹配：GuardDuty是威胁检测服务，不是策略管理工具
❌ 不解决问题：不能自动附加WAF web ACL到资源
❌ 用途错误：虽然GuardDuty很重要，但不适用于这个场景
C. 创建AWS Firewall Manager策略，将AWS WAF web ACL附加到任何新创建的ALB和API Gateway API。
✅ 核心功能：这正是Firewall Manager的主要用途
✅ 自动化：可以自动将WAF web ACL应用到新资源
✅ 预防性：防止未来创建不合规的资源
✅ 支持多资源类型：同时支持ALB和API Gateway
D. 创建Amazon GuardDuty策略，将AWS WAF web ACL附加到任何新创建的ALB和API Gateway API。
❌ 服务能力不匹配：GuardDuty不具备创建或管理WAF策略的能力
❌ 功能错误：GuardDuty专注于威胁检测，不是资源配置管理
E. 配置AWS Config管理规则，将AWS WAF web ACL附加到任何新创建的ALB和API Gateway API。
❌ 功能限制：Config主要用于合规性检测，不是自动修复
❌ 不是最佳工具：虽然Config可以检测违规，但Firewall Manager是更合适的解决方案
❌ 需要额外配置：需要额外的Lambda函数来执行修复操作 |  |  |  |
| 9 | A company uses AWS Key Management Service (AWS KMS) keys and manual key rotation to meet regulatory compliance requirements. The
security team wants to be notied when any keys have not been rotated after 90 days. | A. Congure AWS KMS to publish to an Amazon Simple Notication Service (Amazon SNS) topic when keys are more than 90 days old.
B. Congure an Amazon EventBridge event to launch an AWS Lambda function to call the AWS Trusted Advisor API and publish to an
Amazon Simple Notication Service (Amazon SNS) topic.
C. Develop an AWS Cong custom rule that publishes to an Amazon Simple Notication Service (Amazon SNS) topic when keys are more
than 90 days old.
D. Congure AWS Security Hub to publish to an Amazon Simple Notication Service (Amazon SNS) topic when keys are more than 90 days
old. | 一家公司使用AWS密钥管理服务(AWS KMS)密钥和手动密钥轮换来满足监管合规要求。安全团队希望在任何密钥超过90天未轮换时收到通知。

选项：
A. 配置AWS KMS在密钥超过90天时发布到Amazon简单通知服务(Amazon SNS)主题。
B. 配置Amazon EventBridge事件来启动AWS Lambda函数，调用AWS Trusted Advisor API并发布到Amazon简单通知服务(Amazon SNS)主题。
C. 开发一个AWS Config自定义规则，当密钥超过90天时发布到Amazon简单通知服务(Amazon SNS)主题。
D. 配置AWS Security Hub在密钥超过90天时发布到Amazon简单通知服务(Amazon SNS)主题。

 | **选项A：配置AWS KMS发布到SNS主题**
- 不正确。AWS KMS本身不提供基于密钥年龄的自动通知功能。KMS没有内置的监控机制来跟踪密钥的轮换时间并主动发送通知。

**选项B：使用EventBridge + Lambda + Trusted Advisor API**
- 不正确。AWS Trusted Advisor主要关注成本优化、性能、安全性和容错性的最佳实践建议，但它不提供专门的KMS密钥轮换年龄检查功能。这种方法过于复杂且不是针对此用例的最佳解决方案。

**选项C：开发AWS Config自定义规则**
- 正确。AWS Config可以创建自定义规则来评估AWS资源的配置合规性。可以开发一个自定义规则来检查KMS密钥的创建时间或最后轮换时间，当超过90天时触发不合规状态，并通过SNS发送通知。这是一个完全可行且符合AWS最佳实践的解决方案。

**选项D：配置AWS Security Hub发布到SNS**
- 不正确。虽然Security Hub是一个很好的安全管理服务，但它本身不提供专门针对KMS密钥轮换年龄的内置检查。Security Hub主要聚合来自其他安全服务的发现，而不是主动监控密钥轮换策略。 |  |  |  |
| 10 | A security review has identied that an AWS CodeBuild project is downloading a database population script from an Amazon S3 bucket using
an unauthenticated request. The security team does not allow unauthenticated requests to S3 buckets for this project.
How can this issue be corrected in the MOST secure manner? | A. Add the bucket name to the AllowedBuckets section of the CodeBuild project settings. Update the build spec to use the AWS CLI to
download the database population script.
B. Modify the S3 bucket settings to enable HTTPS basic authentication and specify a token. Update the build spec to use cURL to pass the
token and download the database population script.
C. Remove unauthenticated access from the S3 bucket with a bucket policy. Modify the service role for the CodeBuild project to include
Amazon S3 access. Use the AWS CLI to download the database population script.
D. Remove unauthenticated access from the S3 bucket with a bucket policy. Use the AWS CLI to download the database population script
using an IAM access key and a secret access key. | 一次安全审查发现，AWS CodeBuild项目正在使用未经身份验证的请求从Amazon S3存储桶下载数据库填充脚本。安全团队不允许此项目对S3存储桶进行未经身份验证的请求。

如何以最安全的方式纠正这个问题？

 | **选项A：** 将存储桶名称添加到CodeBuild项目设置的AllowedBuckets部分。更新构建规范以使用AWS CLI下载数据库填充脚本。
- **错误**：CodeBuild项目设置中没有"AllowedBuckets"这样的配置选项。这个选项描述的功能在AWS CodeBuild中并不存在。

**选项B：** 修改S3存储桶设置以启用HTTPS基本身份验证并指定令牌。更新构建规范以使用cURL传递令牌并下载数据库填充脚本。
- **错误**：Amazon S3不支持HTTPS基本身份验证。S3使用AWS的签名验证机制，而不是传统的HTTP基本身份验证。这种方法在技术上不可行。

**选项C：** 使用存储桶策略移除S3存储桶的未经身份验证访问。修改CodeBuild项目的服务角色以包含Amazon S3访问权限。使用AWS CLI下载数据库填充脚本。
- **正确**：这是最佳实践方法。通过IAM服务角色提供必要的S3访问权限，移除公共访问，使用AWS CLI进行身份验证的访问。

**选项D：** 使用存储桶策略移除S3存储桶的未经身份验证访问。使用IAM访问密钥和秘密访问密钥通过AWS CLI下载数据库填充脚本。
- **不推荐**：虽然技术上可行，但在构建脚本中硬编码或存储访问密钥和秘密密钥存在安全风险。这违反了AWS安全最佳实践。 |  |  |  |
| 11 | An ecommerce company has chosen AWS to host its new platform. The company's DevOps team has started building an AWS Control Tower
landing zone. The DevOps team has set the identity store within AWS IAM Identity Center (AWS Single Sign-On) to external identity provider
(IdP) and has congured SAML 2.0.
The DevOps team wants a robust permission model that applies the principle of least privilege. The model must allow the team to build and
manage only the team's own resources. | A. Create IAM policies that include the required permissions. Include the aws:PrincipalTag condition key.
B. Create permission sets. Attach an inline policy that includes the required permissions and uses the aws:PrincipalTag condition key to
scope the permissions.
C. Create a group in the IdP. Place users in the group. Assign the group to accounts and the permission sets in IAM Identity Center.
D. Create a group in the IdP. Place users in the group. Assign the group to OUs and IAM policies.
E. Enable attributes for access control in IAM Identity Center. Apply tags to users. Map the tags as key-value pairs.
F. Enable attributes for access control in IAM Identity Center. Map attributes from the IdP as key-value pairs. |  |  |  |  |  |
| 12 | An ecommerce company is receiving reports that its order history page is experiencing delays in reecting the processing status of orders.
The order processing system consists of an AWS Lambda function that uses reserved concurrency. The Lambda function processes order
messages from an Amazon Simple Queue Service (Amazon SQS) queue and inserts processed orders into an Amazon DynamoDB table. The
DynamoDB table has auto scaling enabled for read and write capacity. | A. Check the ApproximateAgeOfOldestMessage metric for the SQS queue. Increase the Lambda function concurrency limit.
B. Check the ApproximateAgeOfOldestMessage metnc for the SQS queue Congure a redrive policy on the SQS queue.
C. Check the NumberOfMessagesSent metric for the SQS queue. Increase the SQS queue visibility timeout.
D. Check the WriteThrottleEvents metric for the DynamoDB table. Increase the maximum write capacity units (WCUs) for the table's scaling
policy.
E. Check the Throttles metric for the Lambda function. Increase the Lambda function timeout. |  |  |  |  |  |
| 13 | A company has a single AWS account that runs hundreds of Amazon EC2 instances in a single AWS Region. New EC2 instances are launched
and terminated each hour in the account. The account also includes existing EC2 instances that have been running for longer than a week.
The company's security policy requires all running EC2 instances to use an EC2 instance prole. If an EC2 instance does not have an instance
prole attached, the EC2 instance must use a default instance prole that has no IAM permissions assigned.
A DevOps engineer reviews the account and discovers EC2 instances that are running without an instance prole. During the review, the
DevOps engineer also observes that new EC2 instances are being launched without an instance prole. | A. Congure an Amazon EventBridge rule that reacts to EC2 RunInstances API calls. Congure the rule to invoke an AWS Lambda function
to attach the default instance prole to the EC2 instances.
B. Congure the ec2-instance-prole-attached AWS Cong managed rule with a trigger type of conguration changes. Congure an
automatic remediation action that invokes an AWS Systems Manager Automation runbook to attach the default instance prole to the EC2
instances.
C. Congure an Amazon EventBridge rule that reacts to EC2 StartInstances API calls. Congure the rule to invoke an AWS Systems
Manager Automation runbook to attach the default instance prole to the EC2 instances
D. Congure the iam-role-managed-policy-check AWS Cong managed rule with a trigger type of conguration changes. Congure an
automatic remediation action that invokes an AWS Lambda function to attach the default instance prole to the EC2 instances. |  |  |  |  |  |
| 14 | A DevOps engineer is building a continuous deployment pipeline for a serverless application that uses AWS Lambda functions. The company
wants to reduce the customer impact of an unsuccessful deployment. The company also wants to monitor for issues. | A. Use an AWS Serverless Application Model (AWS SAM) template to dene the serverless application. Use AWS CodeDeploy to deploy the
Lambda functions with the Canary10Percent15Minutes Deployment Preference Type. Use Amazon CloudWatch alarms to monitor the
health of the functions.
B. Use AWS CloudFormation to publish a new stack update, and include Amazon CloudWatch alarms on all resources. Set up an AWS
CodePipeline approval action for a developer to verify and approve the AWS CloudFormation change set.
C. Use AWS CloudFormation to publish a new version on every stack update, and include Amazon CloudWatch alarms on all resources. Use
the RoutingCong property of the AWS::Lambda::Alias resource to update the trac routing during the stack update.
D. Use AWS CodeBuild to add sample event payloads for testing to the Lambda functions. Publish a new version of the functions, and
include Amazon CloudWatch alarms. Update the production alias to point to the new version. Congure rollbacks to occur when an alarm
is in the ALARM state. |  |  |  |  |  |
| 15 | To run an application, a DevOps engineer launches an Amazon EC2 instance with public IP addresses in a public subnet. A user data script
obtains the application artifacts and installs them on the instances upon launch. A change to the security classication of the application now
requires the instances to run with no access to the internet. While the instances launch successfully and show as healthy, the application
does not seem to be installed. | A. Launch the instances in a public subnet with Elastic IP addresses attached. Once the application is installed and running, run a script to
disassociate the Elastic IP addresses afterwards.
B. Set up a NAT gateway. Deploy the EC2 instances to a private subnet. Update the private subnet's route table to use the NAT gateway as
the default route.
C. Publish the application artifacts to an Amazon S3 bucket and create a VPC endpoint for S3. Assign an IAM instance prole to the EC2
instances so they can read the application artifacts from the S3 bucket.
D. Create a security group for the application instances and allow only outbound trac to the artifact repository. Remove the security
group rule once the install is complete. | 为了运行一个应用程序，DevOps工程师在公有子网中启动了一个带有公网IP地址的Amazon EC2实例。用户数据脚本在启动时获取应用程序构件并将其安装在实例上。应用程序安全分类的变更现在要求实例在没有互联网访问的情况下运行。虽然实例启动成功并显示为健康状态，但应用程序似乎没有被安装。

 | **选项A：** 在公有子网中启动实例并附加弹性IP地址。一旦应用程序安装并运行，运行脚本来解除弹性IP地址的关联。
- **问题：** 这种方法虽然可以临时解决安装问题，但存在安全风险。在安装过程中实例仍然暴露在互联网上，不符合新的安全分类要求。而且需要手动管理IP地址的关联和解除关联，增加了操作复杂性。

**选项B：** 设置NAT网关。将EC2实例部署到私有子网。更新私有子网的路由表以使用NAT网关作为默认路由。
- **问题：** NAT网关允许私有子网中的实例访问互联网，这违反了"实例运行时不能访问互联网"的安全要求。虽然能解决应用安装问题，但不符合安全分类要求。

**选项C：** 将应用程序构件发布到Amazon S3存储桶，并为S3创建VPC端点。为EC2实例分配IAM实例配置文件，以便它们可以从S3存储桶读取应用程序构件。
- **优势：** 这是最佳解决方案。通过VPC端点，实例可以在不访问互联网的情况下访问S3服务。IAM实例配置文件提供安全的身份验证机制。完全符合安全要求且提供可靠的解决方案。

**选项D：** 为应用程序实例创建安全组，仅允许到构件仓库的出站流量。安装完成后删除安全组规则。
- **问题：** 这种方法仍然需要互联网访问来到达外部构件仓库，不符合"无互联网访问"的安全要求。而且手动管理安全组规则增加了操作复杂性和出错风险。

 |  |  |  |
| 16 | A development team is using AWS CodeCommit to version control application code and AWS CodePipeline to orchestrate software
deployments. The team has decided to use a remote main branch as the trigger for the pipeline to integrate code changes. A developer has
pushed code changes to the CodeCommit repository, but noticed that the pipeline had no reaction, even after 10 minutes. | A. Check that an Amazon EventBridge rule has been created for the main branch to trigger the pipeline.
B. Check that the CodePipeline service role has permission to access the CodeCommit repository.
C. Check that the developer’s IAM role has permission to push to the CodeCommit repository.
D. Check to see if the pipeline failed to start because of CodeCommit errors in Amazon CloudWatch Logs. | 一个开发团队正在使用AWS CodeCommit进行应用程序代码的版本控制，使用AWS CodePipeline来编排软件部署。团队决定使用远程主分支作为触发器来触发管道以集成代码更改。一名开发人员已经将代码更改推送到CodeCommit存储库，但注意到管道没有任何反应，即使在10分钟后也是如此。

 | **A. 检查是否为主分支创建了Amazon EventBridge规则来触发管道。**
- 这是正确的排查方向。CodePipeline通过EventBridge（以前称为CloudWatch Events）来监听CodeCommit的推送事件。如果EventBridge规则配置不正确或缺失，管道就不会被触发。
- 当配置CodePipeline以CodeCommit为源时，需要创建相应的EventBridge规则来监听特定分支的推送事件。

**B. 检查CodePipeline服务角色是否有权限访问CodeCommit存储库。**
- 虽然这个权限很重要，但如果权限不足，通常会在管道启动后的执行阶段出现错误，而不是完全不触发管道。
- 权限问题通常会在CloudWatch Logs中显示相关错误信息。

**C. 检查开发人员的IAM角色是否有权限推送到CodeCommit存储库。**
- 如果开发人员没有推送权限，推送操作本身就会失败，不会成功推送代码到存储库。
- 题目中提到开发人员已经成功推送了代码更改，所以这个选项不是问题所在。

**D. 检查管道是否因为CloudWatch Logs中的CodeCommit错误而启动失败。**
- 如果管道完全没有反应，通常不会在CloudWatch Logs中看到相关的启动尝试记录。
- 这个选项更适用于管道启动了但执行失败的情况。

 |  |  |  |
| 17 | A company's developers use Amazon EC2 instances as remote workstations. The company is concerned that users can create or modify EC2
security groups to allow unrestricted inbound access.
A DevOps engineer needs to develop a solution to detect when users create unrestricted security group rules. The solution must detect
changes to security group rules in near real time, remove unrestricted rules, and send email notications to the security team. The DevOps
engineer has created an AWS Lambda function that checks for security group ID from input, removes rules that grant unrestricted access, and
sends notications through Amazon Simple Notication Service (Amazon SNS). | A. Congure the Lambda function to be invoked by the SNS topic. Create an AWS CloudTrail subscription for the SNS topic. Congure a
subscription lter for security group modication events.
B. Create an Amazon EventBridge scheduled rule to invoke the Lambda function. Dene a schedule pattern that runs the Lambda function
every hour.
C. Create an Amazon EventBridge event rule that has the default event bus as the source. Dene the rule’s event pattern to match EC2
security group creation and modication events. Congure the rule to invoke the Lambda function.
D. Create an Amazon EventBridge custom event bus that subscribes to events from all AWS services. Congure the Lambda function to be
invoked by the custom event bus. |  |  |  |  |  |
| 18 | A DevOps engineer is creating an AWS CloudFormation template to deploy a web service. The web service will run on Amazon EC2 instances
in a private subnet behind an Application Load Balancer (ALB). The DevOps engineer must ensure that the service can accept requests from
clients that have IPv6 addresses. | A. Add an IPv6 CIDR block to the VPC and the private subnet for the EC2 instances. Create route table entries for the IPv6 network, use
EC2 instance types that support IPv6, and assign IPv6 addresses to each EC2 instance.
B. 
C. Replace the ALB with a Network Load Balancer (NLB). Add an IPv6 CIDR block to the VPC and subnets for the NLB, and assign the NLB
an IPv6 Elastic IP address.
D. Add an IPv6 CIDR block to the VPC and subnets for the AL | 一名DevOps工程师正在创建AWS CloudFormation模板来部署Web服务。该Web服务将在位于应用负载均衡器(ALB)后面私有子网中的Amazon EC2实例上运行。DevOps工程师必须确保该服务能够接受来自具有IPv6地址的客户端的请求。

2. | **选项A：** 向VPC和EC2实例的私有子网添加IPv6 CIDR块。为IPv6网络创建路由表条目，使用支持IPv6的EC2实例类型，并为每个EC2实例分配IPv6地址。
- 分析：这个选项只配置了后端EC2实例的IPv6支持，但没有配置ALB的IPv6支持。客户端的IPv6请求无法到达ALB，因为ALB本身没有IPv6配置。这不能解决问题。

**选项B：** [选项内容缺失]

**选项C：** 将ALB替换为网络负载均衡器(NLB)。向VPC和NLB的子网添加IPv6 CIDR块，并为NLB分配IPv6弹性IP地址。
- 分析：虽然NLB支持IPv6并且可以分配IPv6弹性IP地址，但这需要更改架构（从ALB改为NLB）。NLB工作在第4层，而ALB工作在第7层，功能特性不同。这不是最优解决方案。

**选项D：** 向VPC和ALB的子网添加IPv6 CIDR块...[选项内容不完整]
- 分析：选项内容被截断，无法完整分析，但从开头可以看出这是在为ALB配置IPv6支持的正确方向。

3. | D |  |  |
| 19 | A company uses AWS Organizations and AWS Control Tower to manage all the company's AWS accounts. The company uses the Enterprise
Support plan.
A DevOps engineer is using Account Factory for Terraform (AFT) to provision new accounts. When new accounts are provisioned, the DevOps
engineer notices that the support plan for the new accounts is set to the Basic Support plan. The DevOps engineer needs to implement a
solution to provision the new accounts with the Enterprise Support plan. | A. Use an AWS Cong conformance pack to deploy the account-part-of-organizations AWS Cong rule and to automatically remediate any
noncompliant accounts.
B. Create an AWS Lambda function to create a ticket for AWS Support to add the account to the Enterprise Support plan. Grant the Lambda
function the support:ResolveCase permission.
C. Add an additional value to the control_tower_parameters input to set the AWSEnterpriseSupport parameter as the organization's
management account number.
D. Set the aft_feature_enterprise_support feature ag to True in the AFT deployment input conguration. Redeploy AFT and apply the
changes. | 一家公司使用AWS Organizations和AWS Control Tower来管理公司的所有AWS账户。该公司使用企业支持计划。

一名DevOps工程师正在使用Account Factory for Terraform (AFT)来配置新账户。当配置新账户时，DevOps工程师注意到新账户的支持计划被设置为基础支持计划。DevOps工程师需要实施一个解决方案，以便在配置新账户时使用企业支持计划。

 | **选项A：使用AWS Config一致性包来部署account-part-of-organizations AWS Config规则，并自动修复任何不合规的账户。**
- 不正确。AWS Config主要用于监控和评估AWS资源配置的合规性，而不是用于设置支持计划。account-part-of-organizations规则只是检查账户是否属于组织，与支持计划设置无关。

**选项B：创建AWS Lambda函数为AWS Support创建工单，将账户添加到企业支持计划中。为Lambda函数授予support:ResolveCase权限。**
- 不正确。虽然技术上可行，但这不是最佳实践。首先，support:ResolveCase权限是用于解决案例的，不是创建工单的权限。其次，这种方法过于复杂且不是AFT的标准做法。

**选项C：在control_tower_parameters输入中添加额外的值，将AWSEnterpriseSupport参数设置为组织管理账户号码。**
- 不正确。control_tower_parameters主要用于Control Tower的配置参数，而且没有名为AWSEnterpriseSupport的标准参数用于设置支持计划。

**选项D：在AFT部署输入配置中将aft_feature_enterprise_support功能标志设置为True。重新部署AFT并应用更改。**
- 正确。这是AFT的标准功能。AFT提供了专门的功能标志来启用企业支持计划，这是处理此问题的正确和直接的方法。

 |  |  |  |
| 20 | A company's DevOps engineer uses AWS Systems Manager to perform maintenance tasks during maintenance windows. The company has a
few Amazon EC2 instances that require a restart after notications from AWS Health. The DevOps engineer needs to implement an automated
solution to remediate these notications. The DevOps engineer creates an Amazon EventBridge rule.
How should the DevOps engineer congure the EventBridge rule to meet these requirements? | A. Congure an event source of AWS Health, a service of EC2. and an event type that indicates instance maintenance. Target a Systems
Manager document to restart the EC2 instance.
B. Congure an event source of Systems Manager and an event type that indicates a maintenance window. Target a Systems Manager
document to restart the EC2 instance.
C. Congure an event source of AWS Health, a service of EC2, and an event type that indicates instance maintenance. Target a newly
created AWS Lambda function that registers an automation task to restart the EC2 instance during a maintenance window.
D. Congure an event source of EC2 and an event type that indicates instance maintenance. Target a newly created AWS Lambda function
that registers an automation task to restart the EC2 instance during a maintenance window. | 一家公司的DevOps工程师使用AWS Systems Manager在维护窗口期间执行维护任务。该公司有一些Amazon EC2实例在收到AWS Health通知后需要重启。DevOps工程师需要实现一个自动化解决方案来修复这些通知。DevOps工程师创建了一个Amazon EventBridge规则。

DevOps工程师应该如何配置EventBridge规则来满足这些要求？

 | **选项A：** 配置AWS Health作为事件源，EC2作为服务，以及指示实例维护的事件类型。目标为Systems Manager文档来重启EC2实例。
- 优点：正确识别了AWS Health作为事件源，这是获取维护通知的正确来源
- 缺点：直接触发重启，没有考虑维护窗口的要求

**选项B：** 配置Systems Manager作为事件源，以及指示维护窗口的事件类型。目标为Systems Manager文档来重启EC2实例。
- 缺点：事件源错误，维护通知来自AWS Health而不是Systems Manager
- 缺点：这种配置无法捕获AWS Health的维护通知

**选项C：** 配置AWS Health作为事件源，EC2作为服务，以及指示实例维护的事件类型。目标为新创建的AWS Lambda函数，该函数注册一个自动化任务在维护窗口期间重启EC2实例。
- 优点：正确识别AWS Health作为事件源
- 优点：使用Lambda函数提供了灵活性
- 优点：明确提到在维护窗口期间执行任务，符合题目要求

**选项D：** 配置EC2作为事件源，以及指示实例维护的事件类型。目标为新创建的AWS Lambda函数，该函数注册一个自动化任务在维护窗口期间重启EC2实例。
- 缺点：事件源错误，应该是AWS Health而不是EC2
- 优点：使用Lambda和维护窗口的概念是正确的

 |  |  |  |
| 21 | A company has containerized all of its in-house quality control applications. The company is running Jenkins on Amazon EC2 instances, which
require patching and upgrading. The compliance ocer has requested a DevOps engineer begin encrypting build artifacts since they contain
company intellectual property. | A. Automate patching and upgrading using AWS Systems Manager on EC2 instances and encrypt Amazon EBS volumes by default.
B. Deploy Jenkins to an Amazon ECS cluster and copy build artifacts to an Amazon S3 bucket with default encryption enabled.
C. Leverage AWS CodePipeline with a build action and encrypt the artifacts using AWS Secrets Manager.
D. Use AWS CodeBuild with artifact encryption to replace the Jenkins instance running on EC2 instances. |  |  |  |  |  |
| 22 | An IT team has built an AWS CloudFormation template so others in the company can quickly and reliably deploy and terminate an application.
The template creates an Amazon EC2 instance with a user data script to install the application and an Amazon S3 bucket that the application
uses to serve static webpages while it is running.
All resources should be removed when the CloudFormation stack is deleted. However, the team observes that CloudFormation reports an error
during stack deletion, and the S3 bucket created by the stack is not deleted.
How can the team resolve the error in the MOST ecient manner to ensure that all resources are deleted without errors? | A. Add a DelelionPolicy attribute to the S3 bucket resource, with the value Delete forcing the bucket to be removed when the stack is
deleted.
B. Add a custom resource with an AWS Lambda function with the DependsOn attribute specifying the S3 bucket, and an IAM role. Write the
Lambda function to delete all objects from the bucket when RequestType is Delete.
C. Identify the resource that was not deleted. Manually empty the S3 bucket and then delete it.
D. Replace the EC2 and S3 bucket resources with a single AWS OpsWorks Stacks resource. Dene a custom recipe for the stack to create
and delete the EC2 instance and the S3 bucket. | 一个IT团队构建了一个AWS CloudFormation模板，以便公司中的其他人可以快速可靠地部署和终止应用程序。该模板创建了一个带有用户数据脚本的Amazon EC2实例来安装应用程序，以及一个Amazon S3存储桶，应用程序在运行时使用该存储桶来提供静态网页服务。

当CloudFormation堆栈被删除时，所有资源都应该被移除。然而，团队观察到CloudFormation在堆栈删除过程中报告错误，并且由堆栈创建的S3存储桶没有被删除。

团队如何以最高效的方式解决这个错误，以确保所有资源都能无错误地被删除？

 | **选项A：** 向S3存储桶资源添加DeletionPolicy属性，值为Delete，强制在删除堆栈时移除存储桶。
- **错误**：DeletionPolicy的Delete值是默认行为，不会解决根本问题。S3存储桶无法删除的原因通常是因为存储桶不为空，而不是删除策略问题。此外，题目中的"DelelionPolicy"有拼写错误。

**选项B：** 添加一个自定义资源，包含AWS Lambda函数和DependsOn属性指定S3存储桶，以及IAM角色。编写Lambda函数在RequestType为Delete时删除存储桶中的所有对象。
- **正确**：这是解决问题的最佳方案。S3存储桶无法删除通常是因为存储桶中还有对象。通过Lambda自定义资源可以在堆栈删除时自动清空存储桶，然后CloudFormation就能成功删除空的存储桶。

**选项C：** 识别未被删除的资源。手动清空S3存储桶然后删除它。
- **不是最佳方案**：虽然这能解决当前问题，但不是"最高效"的方式，因为每次删除堆栈时都需要手动干预，违背了自动化的原则。

**选项D：** 用单个AWS OpsWorks Stacks资源替换EC2和S3存储桶资源。为堆栈定义自定义配方来创建和删除EC2实例和S3存储桶。
- **过度复杂**：这种方法过于复杂，引入了不必要的OpsWorks复杂性，不是解决S3删除问题的高效方式。

 |  |  |  |
| 23 | A company has an AWS CodePipeline pipeline that is congured with an Amazon S3 bucket in the eu-west-1 Region. The pipeline deploys an
AWS Lambda application to the same Region. The pipeline consists of an AWS CodeBuild project build action and an AWS CloudFormation
deploy action.
The CodeBuild project uses the aws cloudformation package AWS CLI command to build an artifact that contains the Lambda function code’s
.zip le and the CloudFormation template. The CloudFormation deploy action references the CloudFormation template from the output
artifact of the CodeBuild project’s build action.
The company wants to also deploy the Lambda application to the us-east-1 Region by using the pipeline in eu-west-1. A DevOps engineer has
already updated the CodeBuild project to use the aws cloudformation package command to produce an additional output artifact for us-east-
1. | A. Modify the CloudFormation template to include a parameter for the Lambda function code’s zip le location. Create a new
CloudFormation deploy action for us-east-1 in the pipeline. Congure the new deploy action to pass in the us-east-1 artifact location as a
parameter override.
B. Create a new CloudFormation deploy action for us-east-1 in the pipeline. Congure the new deploy action to use the CloudFormation
template from the us-east-1 output artifact.
C. Create an S3 bucket in us-east-1. Congure the S3 bucket policy to allow CodePipeline to have read and write access.
D. Create an S3 bucket in us-east-1. Congure S3 Cross-Region Replication (CRR) from the S3 bucket in eu-west-1 to the S3 bucket in us-
east-1.
E. Modify the pipeline to include the S3 bucket for us-east-1 as an artifact store. Create a new CloudFormation deploy action for us-east-1
in the pipeline. Congure the new deploy action to use the CloudFormation template from the us-east-1 output artifact. | 一家公司有一个AWS CodePipeline流水线，配置了位于eu-west-1区域的Amazon S3存储桶。该流水线将AWS Lambda应用程序部署到同一区域。流水线包含一个AWS CodeBuild项目构建操作和一个AWS CloudFormation部署操作。

CodeBuild项目使用`aws cloudformation package` AWS CLI命令来构建一个包含Lambda函数代码.zip文件和CloudFormation模板的构件。CloudFormation部署操作引用来自CodeBuild项目构建操作输出构件中的CloudFormation模板。

公司希望通过位于eu-west-1的流水线将Lambda应用程序也部署到us-east-1区域。DevOps工程师已经更新了CodeBuild项目，使用`aws cloudformation package`命令为us-east-1生成额外的输出构件。

 | **选项A：** 修改CloudFormation模板以包含Lambda函数代码zip文件位置的参数。在流水线中为us-east-1创建新的CloudFormation部署操作。配置新的部署操作，将us-east-1构件位置作为参数覆盖传入。
- 这种方法可行，但不是最优解。需要修改模板并管理参数，增加了复杂性。

**选项B：** 在流水线中为us-east-1创建新的CloudFormation部署操作。配置新的部署操作使用来自us-east-1输出构件的CloudFormation模板。
- 这个方案忽略了跨区域构件存储的问题。us-east-1的部署操作无法直接访问存储在eu-west-1的构件。

**选项C：** 在us-east-1创建S3存储桶。配置S3存储桶策略以允许CodePipeline具有读写访问权限。
- 仅创建存储桶不足以解决问题，还需要配置为构件存储并创建部署操作。

**选项D：** 在us-east-1创建S3存储桶。配置从eu-west-1的S3存储桶到us-east-1的S3存储桶的S3跨区域复制(CRR)。
- CRR不是CodePipeline跨区域部署的正确方法，且不能解决构件访问问题。

**选项E：** 修改流水线以包含us-east-1的S3存储桶作为构件存储。在流水线中为us-east-1创建新的CloudFormation部署操作。配置新的部署操作使用来自us-east-1输出构件的CloudFormation模板。
- 这是完整的解决方案：配置跨区域构件存储，创建部署操作，并正确引用构件。

 |  |  |  |
| 24 | A company runs an application on one Amazon EC2 instance. Application metadata is stored in Amazon S3 and must be retrieved if the
instance is restarted. The instance must restart or relaunch automatically if the instance becomes unresponsive. | A. Create an Amazon CloudWatch alarm for the StatusCheckFailed metric. Use the recover action to stop and start the instance. Use an S3
event notication to push the metadata to the instance when the instance is back up and running.
B. Congure AWS OpsWorks, and use the auto healing feature to stop and start the instance. Use a lifecycle event in OpsWorks to pull the
metadata from Amazon S3 and update it on the instance.
C. Use EC2 Auto Recovery to automatically stop and start the instance in case of a failure. Use an S3 event notication to push the
metadata to the instance when the instance is back up and running.
D. Use AWS CloudFormation to create an EC2 instance that includes the UserData property for the EC2 resource. Add a command in
UserData to retrieve the application metadata from Amazon S3. |  |  |  |  |  |
| 25 | A company has multiple AWS accounts. The company uses AWS IAM Identity Center (AWS Single Sign-On) that is integrated with AWS Toolkit
for Microsoft Azure DevOps. The attributes for access control feature is enabled in IAM Identity Center.
The attribute mapping list contains two entries. The department key is mapped to ${path:enterprise.department}. The costCenter key is
mapped to ${path:enterprise.costCenter}.
All existing Amazon EC2 instances have a department tag that corresponds to three company departments (d1, d2, d3). A DevOps engineer
must create policies based on the matching attributes. The policies must minimize administrative effort and must grant each Azure AD user
access to only the EC2 instances that are tagged with the user’s respective department name. | A. 
B. 
C. 
D.  | 一家公司拥有多个AWS账户。该公司使用与Microsoft Azure DevOps的AWS工具包集成的AWS IAM Identity Center（AWS Single Sign-On）。IAM Identity Center中启用了访问控制属性功能。

属性映射列表包含两个条目：
- department键映射到${path:enterprise.department}
- costCenter键映射到${path:enterprise.costCenter}

所有现有的Amazon EC2实例都有一个department标签，对应公司的三个部门（d1、d2、d3）。DevOps工程师必须基于匹配属性创建策略。这些策略必须最小化管理工作量，并且必须授予每个Azure AD用户仅访问标记有用户各自部门名称的EC2实例的权限。

 | 由于选项A、B、C、D的具体内容为空，我无法进行逐一分析。

 |  |  |  |
| 26 | A company hosts a security auditing application in an AWS account. The auditing application uses an IAM role to access other AWS accounts.
All the accounts are in the same organization in AWS Organizations.
A recent security audit revealed that users in the audited AWS accounts could modify or delete the auditing application's IAM role. The
company needs to prevent any modication to the auditing application's IAM role by any entity other than a trusted administrator IAM role. | A. Create an SCP that includes a Deny statement for changes to the auditing application's IAM role. Include a condition that allows the
trusted administrator IAM role to make changes. Attach the SCP to the root of the organization.
B. Create an SCP that includes an Allow statement for changes to the auditing application's IAM role by the trusted administrator IAM role.
Include a Deny statement for changes by all other IAM principals. Attach the SCP to the IAM service in each AWS account where the
auditing application has an IAM role.
C. Create an IAM permissions boundary that includes a Deny statement for changes to the auditing application's IAM role. Include a
condition that allows the trusted administrator IAM role to make changes. Attach the permissions boundary to the audited AWS accounts.
D. Create an IAM permissions boundary that includes a Deny statement for changes to the auditing application’s IAM role. Include a
condition that allows the trusted administrator IAM role to make changes. Attach the permissions boundary to the auditing application's
IAM role in the AWS accounts. | 一家公司在AWS账户中托管了一个安全审计应用程序。该审计应用程序使用IAM角色来访问其他AWS账户。所有账户都在AWS Organizations的同一个组织中。

最近的安全审计发现，被审计AWS账户中的用户可以修改或删除审计应用程序的IAM角色。公司需要防止除受信任的管理员IAM角色之外的任何实体对审计应用程序的IAM角色进行任何修改。

 | **选项A：** 创建一个SCP（服务控制策略），包含拒绝更改审计应用程序IAM角色的Deny语句。包含一个允许受信任管理员IAM角色进行更改的条件。将SCP附加到组织的根部。
- **正确性：高** - SCP是组织级别的防护措施，可以有效防止跨账户的未授权修改
- **优势：** 在组织根部应用，覆盖所有账户；使用Deny语句配合条件例外，符合最小权限原则

**选项B：** 创建一个SCP，包含允许受信任管理员IAM角色更改审计应用程序IAM角色的Allow语句。包含拒绝所有其他IAM主体更改的Deny语句。将SCP附加到每个有审计应用程序IAM角色的AWS账户的IAM服务。
- **正确性：低** - SCP不能附加到特定的AWS服务，只能附加到组织单位或账户
- **技术错误：** "附加到IAM服务"的表述不正确

**选项C：** 创建一个IAM权限边界，包含拒绝更改审计应用程序IAM角色的Deny语句。包含一个允许受信任管理员IAM角色进行更改的条件。将权限边界附加到被审计的AWS账户。
- **正确性：低** - 权限边界不能直接附加到AWS账户，只能附加到IAM用户或角色
- **技术错误：** 权限边界的应用范围理解错误

**选项D：** 创建一个IAM权限边界，包含拒绝更改审计应用程序IAM角色的Deny语句。包含一个允许受信任管理员IAM角色进行更改的条件。将权限边界附加到AWS账户中审计应用程序的IAM角色。
- **正确性：低** - 权限边界附加到被保护的角色本身无法防止其他用户修改该角色
- **逻辑错误：** 权限边界限制的是角色本身的权限，而不是谁可以修改这个角色

 |  |  |  |
| 27 | A company has an on-premises application that is written in Go. A DevOps engineer must move the application to AWS. The company's
development team wants to enable blue/green deployments and perform A/B testing. | A. Deploy the application on an Amazon EC2 instance, and create an AMI of the instance. Use the AMI to create an automatic scaling
launch conguration that is used in an Auto Scaling group. Use Elastic Load Balancing to distribute trac. When changes are made to the
application, a new AMI will be created, which will initiate an EC2 instance refresh.
B. Use Amazon Lightsail to deploy the application. Store the application in a zipped format in an Amazon S3 bucket. Use this zipped
version to deploy new versions of the application to Lightsail. Use Lightsail deployment options to manage the deployment.
C. Use AWS CodeArtifact to store the application code. Use AWS CodeDeploy to deploy the application to a eet of Amazon EC2 instances.
Use Elastic Load Balancing to distribute the trac to the EC2 instances. When making changes to the application, upload a new version to
CodeArtifact and create a new CodeDeploy deployment.
D. Use AWS Elastic Beanstalk to host the application. Store a zipped version of the application in Amazon S3. Use that location to deploy
new versions of the application. Use Elastic Beanstalk to manage the deployment options. |  |  |  |  |  |
| 28 | A developer is maintaining a eet of 50 Amazon EC2 Linux servers. The servers are part of an Amazon EC2 Auto Scaling group, and also use
Elastic Load Balancing for load balancing.
Occasionally, some application servers are being terminated after failing ELB HTTP health checks. The developer would like to perform a root
cause analysis on the issue, but before being able to access application logs, the server is terminated.
How can log collection be automated? | A. Use Auto Scaling lifecycle hooks to put instances in a Pending:Wait state. Create an Amazon CloudWatch alarm for EC2 Instance
Terminate Successful and trigger an AWS Lambda function that invokes an SSM Run Command script to collect logs, push them to Amazon
S3, and complete the lifecycle action once logs are collected.
B. Use Auto Scaling lifecycle hooks to put instances in a Terminating:Wait state. Create an AWS Cong rule for EC2 Instance-terminate
Lifecycle Action and trigger a step function that invokes a script to collect logs, push them to Amazon S3, and complete the lifecycle
action once logs are collected.
C. Use Auto Scaling lifecycle hooks to put instances in a Terminating:Wait state. Create an Amazon CloudWatch subscription lter for EC2
Instance Terminate Successful and trigger a CloudWatch agent that invokes a script to collect logs, push them to Amazon S3, and
complete the lifecycle action once logs are collected.
D. Use Auto Scaling lifecycle hooks to put instances in a Terminating:Wait state. Create an Amazon EventBridge rule for EC2 Instance-
terminate Lifecycle Action and trigger an AWS Lambda function that invokes an SSM Run Command script to collect logs, push them to
Amazon S3, and complete the lifecycle action once logs are collected. |  |  |  |  |  |
| 29 | A company has an organization in AWS Organizations. The organization includes workload accounts that contain enterprise applications. The
company centrally manages users from an operations account. No users can be created in the workload accounts. The company recently
added an operations team and must provide the operations team members with administrator access to each workload account. | A. Create a SysAdmin role in the operations account. Attach the AdministratorAccess policy to the role. Modify the trust relationship to
allow the sts:AssumeRole action from the workload accounts.
B. Create a SysAdmin role in each workload account. Attach the AdministratorAccess policy to the role. Modify the trust relationship to
allow the sts:AssumeRole action from the operations account.
C. Create an Amazon Cognito identity pool in the operations account. Attach the SysAdmin role as an authenticated role.
D. In the operations account, create an IAM user for each operations team member.
E. In the operations account, create an IAM user group that is named SysAdmins. Add an IAM policy that allows the sts:AssumeRole action
for the SysAdmin role in each workload account. Add all operations team members to the group. | 一家公司在AWS Organizations中有一个组织。该组织包含含有企业应用程序的工作负载账户。公司从运营账户集中管理用户。不能在工作负载账户中创建用户。公司最近新增了一个运营团队，必须为运营团队成员提供对每个工作负载账户的管理员访问权限。

 | **选项A：** 在运营账户中创建SysAdmin角色。为该角色附加AdministratorAccess策略。修改信任关系以允许来自工作负载账户的sts:AssumeRole操作。
- **错误**：信任关系方向错误。应该是运营账户的用户承担工作负载账户中的角色，而不是相反。

**选项B：** 在每个工作负载账户中创建SysAdmin角色。为该角色附加AdministratorAccess策略。修改信任关系以允许来自运营账户的sts:AssumeRole操作。
- **正确**：这是跨账户角色承担的正确方式。在目标账户（工作负载账户）中创建角色，并信任源账户（运营账户）。

**选项C：** 在运营账户中创建Amazon Cognito身份池。将SysAdmin角色作为已认证角色附加。
- **错误**：Cognito主要用于应用程序用户身份管理，不适用于AWS账户间的管理访问场景。

**选项D：** 在运营账户中，为每个运营团队成员创建IAM用户。
- **不完整**：仅创建用户不足以提供跨账户访问权限，还需要配置跨账户角色承担机制。

**选项E：** 在运营账户中，创建名为SysAdmins的IAM用户组。添加允许对每个工作负载账户中SysAdmin角色执行sts:AssumeRole操作的IAM策略。将所有运营团队成员添加到该组中。
- **正确**：这提供了完整的解决方案，包括用户管理和跨账户访问权限。

 |  |  |  |
| 30 | A company has multiple accounts in an organization in AWS Organizations. The company's SecOps team needs to receive an Amazon Simple
Notication Service (Amazon SNS) notication if any account in the organization turns off the Block Public Access feature on an Amazon S3
bucket. A DevOps engineer must implement this change without affecting the operation of any AWS accounts. The implementation must
ensure that individual member accounts in the organization cannot turn off the notication. | A. Designate an account to be the delegated Amazon GuardDuty administrator account. Turn on GuardDuty for all accounts across the
organization. In the GuardDuty administrator account, create an SNS topic. Subscribe the SecOps team's email address to the SNS topic. In
the same account, create an Amazon EventBridge rule that uses an event pattern for GuardDuty ndings and a target of the SNS topic.
B. Create an AWS CloudFormation template that creates an SNS topic and subscribes the SecOps team’s email address to the SNS topic.
In the template, include an Amazon EventBridge rule that uses an event pattern of CloudTrail activity for s3:PutBucketPublicAccessBlock
and a target of the SNS topic. Deploy the stack to every account in the organization by using CloudFormation StackSets.
C. Turn on AWS Cong across the organization. In the delegated administrator account, create an SNS topic. Subscribe the SecOps team's
email address to the SNS topic. Deploy a conformance pack that uses the s3-bucket-level-public-access-prohibited AWS Cong managed
rule in each account and uses an AWS Systems Manager document to publish an event to the SNS topic to notify the SecOps team.
D. Turn on Amazon Inspector across the organization. In the Amazon Inspector delegated administrator account, create an SNS topic.
Subscribe the SecOps team’s email address to the SNS topic. In the same account, create an Amazon EventBridge rule that uses an event
pattern for public network exposure of the S3 bucket and publishes an event to the SNS topic to notify the SecOps team. | 一家公司在AWS Organizations中有多个账户。公司的SecOps团队需要在组织中任何账户关闭Amazon S3存储桶的"阻止公共访问"功能时收到Amazon Simple Notification Service (Amazon SNS)通知。DevOps工程师必须在不影响任何AWS账户操作的情况下实施此更改。实施方案必须确保组织中的各个成员账户无法关闭通知功能。

 | **选项A：** 
- 使用GuardDuty作为监控服务
- 问题：GuardDuty主要用于威胁检测和安全监控，虽然可能检测到一些S3相关的安全问题，但不是专门用于监控S3存储桶配置更改的服务
- GuardDuty不会直接监控S3存储桶的"阻止公共访问"设置变更

**选项B：**
- 使用CloudFormation StackSets部署到所有账户
- 监控CloudTrail中的s3:PutBucketPublicAccessBlock API调用
- 问题：违反了"个别成员账户无法关闭通知"的要求，因为每个账户都有自己的资源副本，成员账户可能有权限修改或删除这些资源

**选项C：**
- 使用AWS Config跨组织监控
- 使用委托管理员账户集中管理
- 使用s3-bucket-level-public-access-prohibited管理规则
- 优势：Config可以持续监控合规性，委托管理员模式确保成员账户无法关闭监控

**选项D：**
- 使用Amazon Inspector进行监控
- 问题：Inspector主要用于应用程序安全评估和漏洞管理，不是用于监控S3配置更改的合适服务

 | C |  |  |
| 31 | A company has migrated its container-based applications to Amazon EKS and want to establish automated email notications. The
notications sent to each email address are for specic activities related to EKS components. The solution will include Amazon SNS topics
and an AWS Lambda function to evaluate incoming log events and publish messages to the correct SNS topic. | A. Enable Amazon CloudWatch Logs to log the EKS components. Create a CloudWatch subscription lter for each component with Lambda
as the subscription feed destination.
B. Enable Amazon CloudWatch Logs to log the EKS components. Create CloudWatch Logs Insights queries linked to Amazon EventBridge
events that invoke Lambda.
C. Enable Amazon S3 logging for the EKS components. Congure an Amazon CloudWatch subscription lter for each component with
Lambda as the subscription feed destination.
D. Enable Amazon S3 logging for the EKS components. Congure S3 PUT Object event notications with AWS Lambda as the destination. | 一家公司已将其基于容器的应用程序迁移到Amazon EKS，并希望建立自动化的电子邮件通知。发送到每个电子邮件地址的通知是针对与EKS组件相关的特定活动。该解决方案将包括Amazon SNS主题和AWS Lambda函数来评估传入的日志事件并将消息发布到正确的SNS主题。

 | **选项A：启用Amazon CloudWatch Logs来记录EKS组件。为每个组件创建CloudWatch订阅过滤器，以Lambda作为订阅源目标。**
- ✅ 正确的日志收集方式：EKS组件的日志自然流向CloudWatch Logs
- ✅ CloudWatch订阅过滤器是实时处理日志事件的标准方法
- ✅ 可以为不同组件设置不同的过滤器，实现精确的事件处理
- ✅ Lambda可以直接从订阅过滤器接收日志事件并处理

**选项B：启用Amazon CloudWatch Logs来记录EKS组件。创建CloudWatch Logs Insights查询链接到Amazon EventBridge事件来调用Lambda。**
- ✅ 日志收集方式正确
- ❌ CloudWatch Logs Insights主要用于交互式查询分析，不是实时事件处理的最佳选择
- ❌ 架构过于复杂，增加了不必要的EventBridge层
- ❌ 不如订阅过滤器直接和高效

**选项C：为EKS组件启用Amazon S3日志记录。为每个组件配置Amazon CloudWatch订阅过滤器，以Lambda作为订阅源目标。**
- ❌ EKS组件日志不直接存储到S3，通常先到CloudWatch Logs
- ❌ S3不支持CloudWatch订阅过滤器
- ❌ 架构设计不合理

**选项D：为EKS组件启用Amazon S3日志记录。配置S3 PUT Object事件通知，以AWS Lambda作为目标。**
- ❌ EKS日志不直接写入S3
- ❌ S3事件通知不适合实时日志处理需求
- ❌ 会有延迟，不符合实时通知的要求

 |  |  |  |
| 32 | A company is implementing an Amazon Elastic Container Service (Amazon ECS) cluster to run its workload. The company architecture will run
multiple ECS services on the cluster. The architecture includes an Application Load Balancer on the front end and uses multiple target groups
to route trac.
A DevOps engineer must collect application and access logs. The DevOps engineer then needs to send the logs to an Amazon S3 bucket for
near-real-time analysis. | A. Download the Amazon CloudWatch Logs container instance from AWS. Congure this instance as a task. Update the application service
denitions to include the logging task.
B. Then point the ALB directly to the logging S3 bucket.
C. Use Amazon EventBridge to schedule an AWS Lambda function that will run every 60 seconds and will run the Amazon CloudWatch
Logs create-export-task command. Then point the output to the logging S3 bucket.
D. Activate access logging on the AL
E. Activate access logging on the target groups that the ECS services use. Then send the logs directly to the logging S3 bucket.
F. Create an Amazon Kinesis Data Firehose delivery stream that has a destination of the logging S3 bucket. Then create an Amazon
CloudWatch Logs subscription lter for Kinesis Data Firehose. |  |  |  |  |  |
| 33 | A company that uses electronic health records is running a eet of Amazon EC2 instances with an Amazon Linux operating system. As part of
patient privacy requirements, the company must ensure continuous compliance for patches for operating system and applications running on
the EC2 instances.
How can the deployments of the operating system and application patches be automated using a default and custom repository? | A. Use AWS Systems Manager to create a new patch baseline including the custom repository. Run the AWS-RunPatchBaseline document
using the run command to verify and install patches.
B. Use AWS Direct Connect to integrate the corporate repository and deploy the patches using Amazon CloudWatch scheduled events,
then use the CloudWatch dashboard to create reports.
C. Use yum-cong-manager to add the custom repository under /etc/yum.repos.d and run yum-cong-manager-enable to activate the
repository.
D. Use AWS Systems Manager to create a new patch baseline including the corporate repository. Run the AWS-
AmazonLinuxDefaultPatchBaseline document using the run command to verify and install patches. |  |  |  |  |  |
| 34 | A company is using AWS CodePipeline to automate its release pipeline. AWS CodeDeploy is being used in the pipeline to deploy an
application to Amazon Elastic Container Service (Amazon ECS) using the blue/green deployment model. The company wants to implement
scripts to test the green version of the application before shifting trac. These scripts will complete in 5 minutes or less. If errors are
discovered during these tests, the application must be rolled back. | A. Add a stage to the CodePipeline pipeline between the source and deploy stages. Use AWS CodeBuild to create a runtime environment
and build commands in the buildspec le to invoke test scripts. If errors are found, use the aws deploy stop-deployment command to stop
the deployment.
B. Add a stage to the CodePipeline pipeline between the source and deploy stages. Use this stage to invoke an AWS Lambda function that
will run the test scripts. If errors are found, use the aws deploy stop-deployment command to stop the deployment.
C. Add a hooks section to the CodeDeploy AppSpec le. Use the AfterAllowTestTrac lifecycle event to invoke an AWS Lambda function to
run the test scripts. If errors are found, exit the Lambda function with an error to initiate rollback.
D. Add a hooks section to the CodeDeploy AppSpec le. Use the AfterAllowTrac lifecycle event to invoke the test scripts. If errors are
found, use the aws deploy stop-deployment CLI command to stop the deployment. | 一家公司正在使用AWS CodePipeline来自动化其发布管道。管道中使用AWS CodeDeploy将应用程序部署到Amazon Elastic Container Service (Amazon ECS)，采用蓝/绿部署模型。公司希望实现脚本来测试应用程序的绿色版本，然后再切换流量。这些脚本将在5分钟或更短时间内完成。如果在测试过程中发现错误，应用程序必须回滚。

 | **选项A：** 在CodePipeline管道的源阶段和部署阶段之间添加一个阶段。使用AWS CodeBuild创建运行时环境，并在buildspec文件中构建命令来调用测试脚本。如果发现错误，使用aws deploy stop-deployment命令停止部署。
- **问题：** 这种方法在部署之前运行测试，而不是在绿色环境部署后测试绿色版本。不符合蓝/绿部署的测试需求。

**选项B：** 在CodePipeline管道的源阶段和部署阶段之间添加一个阶段。使用此阶段调用AWS Lambda函数来运行测试脚本。如果发现错误，使用aws deploy stop-deployment命令停止部署。
- **问题：** 同选项A，测试时机不正确，是在部署前而不是部署后测试绿色环境。

**选项C：** 在CodeDeploy AppSpec文件中添加hooks部分。使用AfterAllowTestTraffic生命周期事件调用AWS Lambda函数运行测试脚本。如果发现错误，让Lambda函数以错误退出来启动回滚。
- **优势：** 正确的时机（AfterAllowTestTraffic），在绿色环境接收测试流量后进行测试。Lambda函数退出错误会自动触发CodeDeploy回滚机制。

**选项D：** 在CodeDeploy AppSpec文件中添加hooks部分。使用AfterAllowTraffic生命周期事件调用测试脚本。如果发现错误，使用aws deploy stop-deployment CLI命令停止部署。
- **问题：** AfterAllowTraffic是在所有流量都切换到绿色环境后执行，这时测试已经太晚了。应该在AfterAllowTestTraffic阶段测试。

 |  |  |  |
| 35 | A company uses AWS Storage Gateway in le gateway mode in front of an Amazon S3 bucket that is used by multiple resources. In the
morning when business begins, users do not see the objects processed by a third party the previous evening. When a DevOps engineer looks
directly at the S3 bucket, the data is there, but it is missing in Storage Gateway. | A. Congure a nightly Amazon EventBridge event to invoke an AWS Lambda function to run the RefreshCache command for Storage
Gateway.
B. Instruct the third party to put data into the S3 bucket using AWS Transfer for SFTP.
C. Modify Storage Gateway to run in volume gateway mode.
D. Use S3 Same-Region Replication to replicate any changes made directly in the S3 bucket to Storage Gateway. |  |  |  |  |  |
| 36 | A DevOps engineer needs to back up sensitive Amazon S3 objects that are stored within an S3 bucket with a private bucket policy using S3
cross-Region replication functionality. The objects need to be copied to a target bucket in a different AWS Region and account. | A. Create a replication IAM role in the source account
B. Create a replication I AM role in the target account.
C. Add statements to the source bucket policy allowing the replication IAM role to replicate objects.
D. Add statements to the target bucket policy allowing the replication IAM role to replicate objects.
E. Create a replication rule in the source bucket to enable the replication. | 一名DevOps工程师需要备份存储在S3存储桶中的敏感Amazon S3对象，该存储桶具有私有存储桶策略，需要使用S3跨区域复制功能。这些对象需要复制到不同AWS区域和不同AWS账户中的目标存储桶。

 | **A. 在源账户中创建复制IAM角色**
- ✅ **正确**：S3跨区域复制需要在源账户中创建IAM角色，该角色具有从源存储桶读取对象并写入目标存储桶的权限。这是跨区域复制的基本要求。

**B. 在目标账户中创建复制IAM角色**
- ❌ **错误**：复制IAM角色必须在源账户中创建，而不是目标账户。源账户的IAM角色负责执行复制操作。

**C. 在源存储桶策略中添加语句，允许复制IAM角色复制对象**
- ✅ **正确**：源存储桶策略需要明确授权复制IAM角色读取源存储桶中的对象。特别是当源存储桶有私有策略时，必须显式授权。

**D. 在目标存储桶策略中添加语句，允许复制IAM角色复制对象**
- ✅ **正确**：由于目标存储桶在不同的AWS账户中，目标存储桶策略必须授权源账户的复制IAM角色向目标存储桶写入对象。这是跨账户访问的必要条件。

**E. 在源存储桶中创建复制规则以启用复制**
- ✅ **正确**：必须在源存储桶上配置复制规则，指定要复制的对象、目标存储桶和使用的IAM角色。这是启动复制过程的必要步骤。

 |  |  |  |
| 37 | A company has multiple member accounts that are part of an organization in AWS Organizations. The security team needs to review every
Amazon EC2 security group and their inbound and outbound rules. The security team wants to programmatically retrieve this information from
the member accounts using an AWS Lambda function in the management account of the organization. | A. Create a trust relationship that allows users in the member accounts to assume the management account IAM role.
B. Create a trust relationship that allows users in the management account to assume the IAM roles of the member accounts.
C. Create an IAM role in each member account that has access to the AmazonEC2ReadOnlyAccess managed policy.
D. Create an I AM role in each member account to allow the sts:AssumeRole action against the management account IAM role's ARN.
E. Create an I AM role in the management account that allows the sts:AssumeRole action against the member account IAM role's ARN. | 一家公司有多个成员账户，这些账户是AWS Organizations中某个组织的一部分。安全团队需要审查每个Amazon EC2安全组及其入站和出站规则。安全团队希望使用组织管理账户中的AWS Lambda函数以编程方式从成员账户中检索这些信息。

 | **A. 创建信任关系，允许成员账户中的用户承担管理账户的IAM角色。**
- 错误。这个方向是反的。我们需要管理账户访问成员账户，而不是成员账户访问管理账户。

**B. 创建信任关系，允许管理账户中的用户承担成员账户的IAM角色。**
- 部分正确，但不完整。这只是描述了信任关系的方向，但没有说明具体的实现细节。

**C. 在每个成员账户中创建一个IAM角色，该角色具有AmazonEC2ReadOnlyAccess托管策略的访问权限。**
- 部分正确，但不完整。这只创建了角色和权限，但没有建立跨账户访问的信任关系。

**D. 在每个成员账户中创建一个IAM角色，允许对管理账户IAM角色的ARN执行sts:AssumeRole操作。**
- 错误。这个配置是反向的，应该是管理账户的角色能够assume成员账户的角色。

**E. 在管理账户中创建一个IAM角色，允许对成员账户IAM角色的ARN执行sts:AssumeRole操作。**
- 部分正确，但不完整。这只是管理账户端的配置，还需要成员账户端的配置。

 |  |  |  |
| 38 | A space exploration company receives telemetry data from multiple satellites. Small packets of data are received through Amazon API
Gateway and are placed directly into an Amazon Simple Queue Service (Amazon SQS) standard queue. A custom application is subscribed to
the queue and transforms the data into a standard format.
Because of inconsistencies in the data that the satellites produce, the application is occasionally unable to transform the data. In these
cases, the messages remain in the SQS queue. A DevOps engineer must develop a solution that retains the failed messages and makes them
available to scientists for review and future processing. | A. Congure AWS Lambda to poll the SQS queue and invoke a Lambda function to check whether the queue messages are valid. If
validation fails, send a copy of the data that is not valid to an Amazon S3 bucket so that the scientists can review and correct the data.
When the data is corrected, amend the message in the SQS queue by using a replay Lambda function with the corrected data.
B. Convert the SQS standard queue to an SQS FIFO queue. Congure AWS Lambda to poll the SQS queue every 10 minutes by using an
Amazon EventBridge schedule. Invoke the Lambda function to identify any messages with a SentTimestamp value that is older than 5
minutes, push the data to the same location as the application's output location, and remove the messages from the queue.
C. Create an SQS dead-letter queue. Modify the existing queue by including a redrive policy that sets the Maximum Receives setting to 1
and sets the dead-letter queue ARN to the ARN of the newly created queue. Instruct the scientists to use the dead-letter queue to review
the data that is not valid. Reprocess this data at a later time.
D. Congure API Gateway to send messages to different SQS virtual queues that are named for each of the satellites. Update the
application to use a new virtual queue for any data that it cannot transform, and send the message to the new virtual queue. Instruct the
scientists to use the virtual queue to review the data that is not valid. Reprocess this data at a later time. |  |  |  |  |  |
| 39 | A company wants to use AWS CloudFormation for infrastructure deployment. The company has strict tagging and resource requirements and
wants to limit the deployment to two Regions. Developers will need to deploy multiple versions of the same application. | A. Create AWS Trusted Advisor checks to nd and remediate unapproved CloudFormation StackSets.
B. Create a Cloud Formation drift detection operation to nd and remediate unapproved CloudFormation StackSets.
C. Create CloudFormation StackSets with approved CloudFormation templates.
D. Create AWS Service Catalog products with approved CloudFormation templates. | 一家公司希望使用AWS CloudFormation进行基础设施部署。该公司有严格的标签和资源要求，并希望将部署限制在两个区域内。开发人员需要部署同一应用程序的多个版本。

 | **A. 创建AWS Trusted Advisor检查来发现和修复未批准的CloudFormation StackSets**
- 错误：Trusted Advisor主要用于成本优化、性能、安全性和容错性建议
- 它不是用来控制或限制CloudFormation部署的工具
- 无法解决标签要求、区域限制和模板标准化的需求

**B. 创建CloudFormation漂移检测操作来发现和修复未批准的CloudFormation StackSets**
- 错误：漂移检测用于识别堆栈资源与模板定义之间的差异
- 它是事后检测工具，不是预防性控制机制
- 无法在部署前强制执行标签和区域限制

**C. 使用批准的CloudFormation模板创建CloudFormation StackSets**
- 部分正确：StackSets可以跨多个区域部署
- 但缺乏治理和访问控制机制
- 开发人员仍可能使用未批准的模板或违反标签要求
- 没有内置的产品目录和版本管理功能

**D. 使用批准的CloudFormation模板创建AWS Service Catalog产品**
- 正确：Service Catalog提供集中的产品目录管理
- 可以预定义批准的CloudFormation模板
- 内置IAM集成，可控制谁能部署什么资源
- 支持产品版本管理，满足"多版本应用程序"需求
- 可以强制执行标签策略和区域限制
- 提供治理和合规性控制

 |  |  |  |
| 40 | A company requires that its internally facing web application be highly available. The architecture is made up of one Amazon EC2 web server
instance and one NAT instance that provides outbound internet access for updates and accessing public data. | A. Add the NAT instance to an EC2 Auto Scaling group that spans multiple Availability Zones. Update the route tables.
B. Create additional EC2 instances spanning multiple Availability Zones. Add an Application Load Balancer to split the load between
them.
C. Congure an Application Load Balancer in front of the EC2 instance. Congure Amazon CloudWatch alarms to recover the EC2 instance
upon host failure.
D. Replace the NAT instance with a NAT gateway in each Availability Zone. Update the route tables.
E. Replace the NAT instance with a NAT gateway that spans multiple Availability Zones. Update the route tables. |  |  |  |  |  |
| 41 | A DevOps engineer is building a multistage pipeline with AWS CodePipeline to build, verify, stage, test, and deploy an application. A manual
approval stage is required between the test stage and the deploy stage. The development team uses a custom chat tool with webhook
support that requires near-real-time notications.
How should the DevOps engineer congure status updates for pipeline activity and approval requests to post to the chat tool? | A. Create an Amazon CloudWatch Logs subscription that lters on CodePipeline Pipeline Execution State Change. Publish subscription
events to an Amazon Simple Notication Service (Amazon SNS) topic. Subscribe the chat webhook URL to the SNS topic, and complete the
subscription validation.
B. Create an AWS Lambda function that is invoked by AWS CloudTrail events. When a CodePipeline Pipeline Execution State Change event
is detected, send the event details to the chat webhook URL.
C. Create an Amazon EventBridge rule that lters on CodePipeline Pipeline Execution State Change. Publish the events to an Amazon
Simple Notication Service (Amazon SNS) topic. Create an AWS Lambda function that sends event details to the chat webhook URL.
Subscribe the function to the SNS topic.
D. Modify the pipeline code to send the event details to the chat webhook URL at the end of each stage. Parameterize the URL so that
each pipeline can send to a different URL based on the pipeline environment. |  |  |  |  |  |
| 42 | A company's application development team uses Linux-based Amazon EC2 instances as bastion hosts. Inbound SSH access to the bastion
hosts is restricted to specic IP addresses, as dened in the associated security groups. The company's security team wants to receive a
notication if the security group rules are modied to allow SSH access from any IP address. | A. Create an Amazon EventBridge rule with a source of aws.cloudtrail and the event name AuthorizeSecurityGroupIngress. Dene an
Amazon Simple Notication Service (Amazon SNS) topic as the target.
B. Enable Amazon GuardDuty and check the ndings for security groups in AWS Security Hub. Congure an Amazon EventBridge rule with
a custom pattern that matches GuardDuty events with an output of NON_COMPLIANT. Dene an Amazon Simple Notication Service
(Amazon SNS) topic as the target.
C. Create an AWS Cong rule by using the restricted-ssh managed rule to check whether security groups disallow unrestricted incoming
SSH trac. Congure automatic remediation to publish a message to an Amazon Simple Notication Service (Amazon SNS) topic.
D. Enable Amazon Inspector. Include the Common Vulnerabilities and Exposures-1.1 rules package to check the security groups that are
associated with the bastion hosts. Congure Amazon Inspector to publish a message to an Amazon Simple Notication Service (Amazon
SNS) topic. | 一家公司的应用程序开发团队使用基于Linux的Amazon EC2实例作为堡垒主机。对堡垒主机的入站SSH访问被限制为特定的IP地址，这些地址在相关的安全组中定义。公司的安全团队希望在安全组规则被修改为允许来自任何IP地址的SSH访问时收到通知。

 | **选项A：** 创建一个Amazon EventBridge规则，源为aws.cloudtrail，事件名称为AuthorizeSecurityGroupIngress。定义Amazon Simple Notification Service (Amazon SNS)主题作为目标。
- **分析：** 这个方案可以监控安全组规则的修改，但仅仅监控AuthorizeSecurityGroupIngress事件无法确定是否允许了来自任何IP地址(0.0.0.0/0)的SSH访问。需要更复杂的事件模式匹配来检查具体的IP范围。

**选项B：** 启用Amazon GuardDuty并在AWS Security Hub中检查安全组的发现结果。配置Amazon EventBridge规则，使用自定义模式匹配输出为NON_COMPLIANT的GuardDuty事件。定义Amazon Simple Notification Service (Amazon SNS)主题作为目标。
- **分析：** GuardDuty主要用于威胁检测，虽然它可能检测到一些安全组配置问题，但它不是专门用于配置合规性检查的服务。这个方案过于复杂且不是最佳实践。

**选项C：** 使用restricted-ssh托管规则创建AWS Config规则，检查安全组是否禁止不受限制的入站SSH流量。配置自动修复以向Amazon Simple Notification Service (Amazon SNS)主题发布消息。
- **分析：** 这是最合适的方案。AWS Config的restricted-ssh托管规则专门用于检查安全组是否允许来自0.0.0.0/0的SSH访问（端口22）。当检测到违规配置时，可以触发SNS通知。这正好满足题目要求。

**选项D：** 启用Amazon Inspector。包含Common Vulnerabilities and Exposures-1.1规则包来检查与堡垒主机关联的安全组。配置Amazon Inspector向Amazon Simple Notification Service (Amazon SNS)主题发布消息。
- **分析：** Amazon Inspector主要用于应用程序安全评估和漏洞扫描，不是用于监控安全组配置变更的工具。CVE规则包也不会检查安全组配置。

 |  |  |  |
| 43 | A DevOps team manages an API running on-premises that serves as a backend for an Amazon API Gateway endpoint. Customers have been
complaining about high response latencies, which the development team has veried using the API Gateway latency metrics in Amazon
CloudWatch. To identify the cause, the team needs to collect relevant data without introducing additional latency. | A. Install the CloudWatch agent server side and congure the agent to upload relevant logs to CloudWatch.
B. Enable AWS X-Ray tracing in API Gateway, modify the application to capture request segments, and upload those segments to X-Ray
during each request.
C. Enable AWS X-Ray tracing in API Gateway, modify the application to capture request segments, and use the X-Ray daemon to upload
segments to X-Ray.
D. Modify the on-premises application to send log information back to API Gateway with each request.
E. Modify the on-premises application to calculate and upload statistical data relevant to the API service requests to CloudWatch metrics. | 一个DevOps团队管理着一个运行在本地的API，该API作为Amazon API Gateway端点的后端服务。客户一直在抱怨响应延迟过高，开发团队已经通过Amazon CloudWatch中的API Gateway延迟指标验证了这个问题。为了识别原因，团队需要收集相关数据而不引入额外的延迟。

 | **选项A：在服务器端安装CloudWatch代理并配置代理将相关日志上传到CloudWatch。**
- 优点：可以收集详细的日志信息
- 缺点：CloudWatch代理需要实时上传日志，会在每个请求处理过程中引入网络I/O开销，可能增加延迟
- 不符合"不引入额外延迟"的要求

**选项B：在API Gateway中启用AWS X-Ray跟踪，修改应用程序以捕获请求段，并在每个请求期间将这些段上传到X-Ray。**
- 优点：X-Ray可以提供详细的请求跟踪和性能分析
- 缺点：在每个请求处理过程中直接上传段数据会引入同步网络调用，增加请求延迟
- 不符合"不引入额外延迟"的要求

**选项C：在API Gateway中启用AWS X-Ray跟踪，修改应用程序以捕获请求段，并使用X-Ray守护进程将段上传到X-Ray。**
- 优点：X-Ray守护进程异步处理段数据上传，不会阻塞请求处理
- 优点：可以提供端到端的请求跟踪，包括API Gateway和后端应用的性能数据
- 优点：异步上传机制最小化对请求延迟的影响
- 符合"不引入额外延迟"的要求

**选项D：修改本地应用程序，在每个请求中将日志信息发送回API Gateway。**
- 缺点：这种方法在技术上不可行，API Gateway不是日志收集服务
- 缺点：会显著增加请求处理时间和网络开销
- 不符合要求

**选项E：修改本地应用程序以计算并上传与API服务请求相关的统计数据到CloudWatch指标。**
- 优点：可以提供聚合的性能指标
- 缺点：同步上传指标会在请求处理过程中引入延迟
- 缺点：统计数据粒度较粗，难以定位具体的性能瓶颈
- 不完全符合要求

 | C |  |  |
| 44 | A company has an application that is using a MySQL-compatible Amazon Aurora Multi-AZ DB cluster as the database. A cross-Region read
replica has been created for disaster recovery purposes. A DevOps engineer wants to automate the promotion of the replica so it becomes the
primary database instance in the event of a failure. | A. Congure a latency-based Amazon Route 53 CNAME with health checks so it points to both the primary and replica endpoints.
Subscribe an Amazon SNS topic to Amazon RDS failure notications from AWS CloudTrail and use that topic to invoke an AWS Lambda
function that will promote the replica instance as the primary.
B. Create an Aurora custom endpoint to point to the primary database instance. Congure the application to use this endpoint. Congure
AWS CloudTrail to run an AWS Lambda function to promote the replica instance and modify the custom endpoint to point to the newly
promoted instance.
C. Create an AWS Lambda function to modify the application's AWS CloudFormation template to promote the replica, apply the template to
update the stack, and point the application to the newly promoted instance. Create an Amazon CloudWatch alarm to invoke this Lambda
function after the failure event occurs.
D. Store the Aurora endpoint in AWS Systems Manager Parameter Store. Create an Amazon EventBridge event that detects the database
failure and runs an AWS Lambda function to promote the replica instance and update the endpoint URL stored in AWS Systems Manager
Parameter Store. Code the application to reload the endpoint from Parameter Store if a database connection fails. | 一家公司有一个应用程序，使用与MySQL兼容的Amazon Aurora Multi-AZ数据库集群作为数据库。已经创建了一个跨区域只读副本用于灾难恢复目的。DevOps工程师希望自动化副本的提升过程，使其在发生故障时成为主数据库实例。

 | **选项A：** 配置基于延迟的Amazon Route 53 CNAME记录并进行健康检查，使其指向主数据库和副本端点。订阅Amazon SNS主题以接收来自AWS CloudTrail的Amazon RDS故障通知，并使用该主题调用AWS Lambda函数来提升副本实例为主实例。

- **问题分析：** 
  - Route 53基于延迟的路由不适用于数据库故障转移场景
  - CloudTrail主要用于API调用日志记录，不是实时监控服务
  - 数据库故障通知应该来自CloudWatch Events/EventBridge，而不是CloudTrail
  - 架构复杂且不够可靠

**选项B：** 创建Aurora自定义端点指向主数据库实例。配置应用程序使用此端点。配置AWS CloudTrail运行AWS Lambda函数来提升副本实例并修改自定义端点指向新提升的实例。

- **问题分析：**
  - CloudTrail不能直接触发Lambda函数进行实时响应
  - CloudTrail主要用于审计，不适合实时故障检测
  - 缺乏可靠的故障检测机制

**选项C：** 创建AWS Lambda函数修改应用程序的AWS CloudFormation模板来提升副本，应用模板更新堆栈，并将应用程序指向新提升的实例。创建Amazon CloudWatch告警在故障事件发生后调用此Lambda函数。

- **问题分析：**
  - 使用CloudFormation进行故障转移过于复杂和缓慢
  - CloudFormation更新过程耗时较长，不适合紧急故障转移
  - 架构过于复杂，增加了故障点

**选项D：** 将Aurora端点存储在AWS Systems Manager Parameter Store中。创建Amazon EventBridge事件来检测数据库故障并运行AWS Lambda函数来提升副本实例，同时更新存储在AWS Systems Manager Parameter Store中的端点URL。编写应用程序代码，在数据库连接失败时从Parameter Store重新加载端点。

- **优势分析：**
  - EventBridge是检测AWS服务事件的正确服务
  - Parameter Store提供了集中化的配置管理
  - 应用程序具有自动重新加载配置的能力
  - 架构简洁且可靠
  - 符合AWS最佳实践

 |  |  |  |
| 45 | A company hosts its staging website using an Amazon EC2 instance backed with Amazon EBS storage. The company wants to recover quickly
with minimal data losses in the event of network connectivity issues or power failures on the EC2 instance. | A. Add the instance to an EC2 Auto Scaling group with the minimum, maximum, and desired capacity set to 1.
B. Add the instance to an EC2 Auto Scaling group with a lifecycle hook to detach the EBS volume when the EC2 instance shuts down or
terminates.
C. Create an Amazon CloudWatch alarm for the StatusCheckFailed System metric and select the EC2 action to recover the instance.
D. Create an Amazon CloudWatch alarm for the StatusCheckFailed Instance metric and select the EC2 action to reboot the instance. | 一家公司使用由Amazon EBS存储支持的Amazon EC2实例来托管其预发布网站。该公司希望在EC2实例出现网络连接问题或电源故障时能够快速恢复，并将数据丢失降到最低。

 | **选项A：将实例添加到EC2 Auto Scaling组中，最小、最大和期望容量都设置为1。**
- 这个方案可以在实例失败时自动启动新实例
- 但是新实例会使用新的EBS卷，无法保留原有数据
- 不能满足"最小数据丢失"的要求
- 适用于无状态应用，但不适合需要数据持久性的场景

**选项B：将实例添加到EC2 Auto Scaling组中，并使用生命周期钩子在EC2实例关闭或终止时分离EBS卷。**
- 生命周期钩子可以在实例终止前执行自定义操作
- 分离EBS卷可以保护数据不被删除
- 但这种方案复杂度较高，需要额外的自动化脚本来重新附加卷
- 恢复时间可能较长

**选项C：为StatusCheckFailed System指标创建Amazon CloudWatch告警，并选择EC2操作来恢复实例。**
- StatusCheckFailed System指标检测底层硬件或网络问题
- EC2恢复操作会在相同的硬件上重启实例，保持相同的实例ID、私有IP地址、弹性IP地址和所有实例元数据
- EBS卷保持附加状态，数据完全保留
- 恢复速度快，通常几分钟内完成
- 完美匹配题目要求的快速恢复和最小数据丢失

**选项D：为StatusCheckFailed Instance指标创建Amazon CloudWatch告警，并选择EC2操作来重启实例。**
- StatusCheckFailed Instance指标检测实例级别的问题（如操作系统问题）
- 重启操作只是简单重启，不能解决底层硬件或网络连接问题
- 如果是硬件故障，重启无法解决问题

 |  |  |  |
| 46 | A company wants to use AWS development tools to replace its current bash deployment scripts. The company currently deploys a LAMP
application to a group of Amazon EC2 instances behind an Application Load Balancer (ALB). During the deployments, the company unit tests
the committed application, stops and starts services, unregisters and re-registers instances with the load balancer, and updates le
permissions. The company wants to maintain the same deployment functionality through the shift to using AWS services. | A. Use AWS CodeBuild to test the application. Use bash scripts invoked by AWS CodeDeploy's appspec.yml le to restart services, and
deregister and register instances with the AL
B. Update the
appspec.yml le to update le permissions without a custom script.
C. Use AWS CodePipeline to move the application source code from the AWS CodeCommit repository to AWS CodeDeploy. Use CodeDeploy
to test the application. Use CodeDeploy's appspec.yml le to restart services and update permissions without a custom script. Use AWS
CodeBuild to unregister and re-register instances with the AL
D. Use AWS CodePipeline to trigger AWS CodeBuild to test the application. Use bash scripts invoked by AWS CodeDeploy's appspec.yml le
to restart services. Unregister and re-register the instances in the AWS CodeDeploy deployment group with the AL | 一家公司希望使用AWS开发工具来替换其当前的bash部署脚本。该公司目前将LAMP应用程序部署到位于应用程序负载均衡器(ALB)后面的一组Amazon EC2实例上。在部署过程中，公司会对提交的应用程序进行单元测试，停止和启动服务，从负载均衡器注销和重新注册实例，以及更新文件权限。公司希望在转向使用AWS服务的过程中保持相同的部署功能。

 | **选项A：** 使用AWS CodeBuild测试应用程序。使用AWS CodeDeploy的appspec.yml文件调用bash脚本来重启服务，并从ALB注销和注册实例。更新appspec.yml文件以在不使用自定义脚本的情况下更新文件权限。

- ✅ CodeBuild用于测试应用程序 - 正确
- ✅ 使用appspec.yml调用bash脚本重启服务 - 可行
- ✅ CodeDeploy可以处理ALB的实例注销/注册
- ✅ appspec.yml可以原生处理文件权限设置
- 这个选项涵盖了所有必需的功能

**选项B：** 使用AWS CodePipeline将应用程序源代码从AWS CodeCommit存储库移动到AWS CodeDeploy。使用CodeDeploy测试应用程序。使用CodeDeploy的appspec.yml文件重启服务并更新权限而不使用自定义脚本。使用AWS CodeBuild注销和重新注册ALB实例。

- ❌ CodeDeploy不是用于测试应用程序的工具
- ❌ CodeBuild不应该用于处理ALB实例注册/注销
- ❌ 架构设计不合理

**选项C：** 使用AWS CodePipeline触发AWS CodeBuild测试应用程序。使用AWS CodeDeploy的appspec.yml文件调用bash脚本重启服务。在AWS CodeDeploy部署组中注销和重新注册ALB实例。

- ✅ CodePipeline编排整个流程 - 最佳实践
- ✅ CodeBuild用于测试 - 正确
- ✅ appspec.yml调用bash脚本重启服务 - 可行
- ✅ CodeDeploy部署组自动处理ALB实例管理
- 这个选项提供了最完整和最佳实践的解决方案

 |  |  |  |
| 47 | A company runs an application with an Amazon EC2 and on-premises conguration. A DevOps engineer needs to standardize patching across
both environments. Company policy dictates that patching only happens during non-business hours. | A. Add the physical machines into AWS Systems Manager using Systems Manager Hybrid Activations.
B. Attach an IAM role to the EC2 instances, allowing them to be managed by AWS Systems Manager.
C. Create IAM access keys for the on-premises machines to interact with AWS Systems Manager.
D. Run an AWS Systems Manager Automation document to patch the systems every hour
E. Use Amazon EventBridge scheduled events to schedule a patch window.
F. Use AWS Systems Manager Maintenance Windows to schedule a patch window. | 一家公司运行着一个包含Amazon EC2和本地配置的应用程序。DevOps工程师需要在两个环境中标准化补丁管理。公司政策规定补丁只能在非工作时间进行。

 | **A. 使用Systems Manager混合激活将物理机器添加到AWS Systems Manager中**
- ✅ **正确**：这是管理本地服务器的标准方法。通过混合激活，可以将本地服务器注册到Systems Manager，使其能够像EC2实例一样被管理。

**B. 为EC2实例附加IAM角色，允许它们被AWS Systems Manager管理**
- ✅ **正确**：EC2实例需要适当的IAM角色（如AmazonSSMManagedInstanceCore策略）才能与Systems Manager通信并接受管理。

**C. 为本地机器创建IAM访问密钥以与AWS Systems Manager交互**
- ❌ **错误**：虽然技术上可行，但这不是最佳实践。使用访问密钥存在安全风险，混合激活是更安全的方法。

**D. 运行AWS Systems Manager自动化文档每小时修补系统**
- ❌ **错误**：每小时修补违反了公司"仅在非工作时间修补"的政策要求。

**E. 使用Amazon EventBridge计划事件来安排补丁窗口**
- ⚠️ **部分正确**：EventBridge可以触发补丁作业，但Systems Manager Maintenance Windows是专门为此设计的更合适的服务。

**F. 使用AWS Systems Manager维护窗口来安排补丁窗口**
- ✅ **正确**：维护窗口专门设计用于在指定时间执行维护任务（如补丁），完全符合"仅在非工作时间"的要求。

 |  |  |  |
| 48 | A company has chosen AWS to host a new application. The company needs to implement a multi-account strategy. A DevOps engineer creates
a new AWS account and an organization in AWS Organizations. The DevOps engineer also creates the OU structure for the organization and
sets up a landing zone by using AWS Control Tower.
The DevOps engineer must implement a solution that automatically deploys resources for new accounts that users create through AWS
Control Tower Account Factory. When a user creates a new account, the solution must apply AWS CloudFormation templates and SCPs that are
customized for the OU or the account to automatically deploy all the resources that are attached to the account. All the OUs are enrolled in
AWS Control Tower. | A. Use AWS Service Catalog with AWS Control Tower. Create portfolios and products in AWS Service Catalog. Grant granular permissions to
provision these resources. Deploy SCPs by using the AWS CLI and JSON documents.
B. Deploy CloudFormation stack sets by using the required templates. Enable automatic deployment. Deploy stack instances to the
required accounts. Deploy a CloudFormation stack set to the organization’s management account to deploy SCPs.
C. Create an Amazon EventBridge rule to detect the CreateManagedAccount event. Congure AWS Service Catalog as the target to deploy
resources to any new accounts. Deploy SCPs by using the AWS CLI and JSON documents.
D. Deploy the Customizations for AWS Control Tower (CfCT) solution. Use an AWS CodeCommit repository as the source. In the repository,
create a custom package that includes the CloudFormation templates and the SCP JSON documents. | 一家公司选择了AWS来托管新应用程序。该公司需要实施多账户策略。DevOps工程师创建了一个新的AWS账户和AWS Organizations中的组织。DevOps工程师还为组织创建了OU（组织单元）结构，并使用AWS Control Tower设置了着陆区。

DevOps工程师必须实施一个解决方案，当用户通过AWS Control Tower Account Factory创建新账户时，该解决方案能够自动为新账户部署资源。当用户创建新账户时，解决方案必须应用针对OU或账户定制的AWS CloudFormation模板和SCP（服务控制策略），以自动部署附加到账户的所有资源。所有OU都已注册到AWS Control Tower。

 | **选项A：** 使用AWS Service Catalog与AWS Control Tower。在AWS Service Catalog中创建产品组合和产品。授予精细权限来配置这些资源。使用AWS CLI和JSON文档部署SCP。
- 问题：Service Catalog需要手动操作来配置资源，不能实现账户创建时的自动部署
- SCP部署方式不够自动化和集成化

**选项B：** 使用所需模板部署CloudFormation堆栈集。启用自动部署。将堆栈实例部署到所需账户。向组织的管理账户部署CloudFormation堆栈集以部署SCP。
- 问题：虽然StackSets可以跨账户部署，但不能与Control Tower Account Factory的账户创建事件自动集成
- 需要手动管理新账户的资源部署

**选项C：** 创建Amazon EventBridge规则来检测CreateManagedAccount事件。配置AWS Service Catalog作为目标，向任何新账户部署资源。使用AWS CLI和JSON文档部署SCP。
- 问题：Service Catalog不是为跨账户自动部署设计的
- 这种方法过于复杂且不是AWS推荐的最佳实践

**选项D：** 部署Customizations for AWS Control Tower (CfCT)解决方案。使用AWS CodeCommit存储库作为源。在存储库中创建包含CloudFormation模板和SCP JSON文档的自定义包。
- 正确：CfCT是AWS官方提供的解决方案，专门用于在Control Tower环境中自动化部署定制资源
- 与Control Tower Account Factory完全集成
- 支持基于OU和账户级别的定制
- 可以同时管理CloudFormation模板和SCP

 |  |  |  |
| 49 | An online retail company based in the United States plans to expand its operations to Europe and Asia in the next six months. Its product
currently runs on Amazon EC2 instances behind an Application Load Balancer. The instances run in an Amazon EC2 Auto Scaling group across
multiple Availability Zones. All data is stored in an Amazon Aurora database instance.
When the product is deployed in multiple regions, the company wants a single product catalog across all regions, but for compliance
purposes, its customer information and purchases must be kept in each region.
How should the company meet these requirements with the LEAST amount of application changes? | A. Use Amazon Redshift for the product catalog and Amazon DynamoDB tables for the customer information and purchases.
B. Use Amazon DynamoDB global tables for the product catalog and regional tables for the customer information and purchases.
C. Use Aurora with read replicas for the product catalog and additional local Aurora instances in each region for the customer information
and purchases.
D. Use Aurora for the product catalog and Amazon DynamoDB global tables for the customer information and purchases. |  |  |  |  |  |
| 50 | A company is implementing a well-architected design for its globally accessible API stack. The design needs to ensure both high reliability
and fast response times for users located in North America and Europe.
The API stack contains the following three tiers:
Amazon API Gateway -
AWS Lambda -
Amazon DynamoDB - | A. Congure Amazon Route 53 to point to API Gateway APIs in North America and Europe using health checks. Congure the APIs to
forward requests to a Lambda function in that Region. Congure the Lambda functions to retrieve and update the data in a DynamoDB
table in the same Region as the Lambda function.
B. Congure Amazon Route 53 to point to API Gateway APIs in North America and Europe using latency-based routing and health checks.
Congure the APIs to forward requests to a Lambda function in that Region. Congure the Lambda functions to retrieve and update the
data in a DynamoDB global table.
C. Congure Amazon Route 53 to point to API Gateway in North America, create a disaster recovery API in Europe, and congure both APIs
to forward requests to the Lambda functions in that Region. Retrieve the data from a DynamoDB global table. Deploy a Lambda function
to check the North America API health every 5 minutes. In the event of a failure, update Route 53 to point to the disaster recovery API.
D. Congure Amazon Route 53 to point to API Gateway API in North America using latency-based routing. Congure the API to forward
requests to the Lambda function in the Region nearest to the user. Congure the Lambda function to retrieve and update the data in a
DynamoDB table. | 一家公司正在为其全球可访问的API堆栈实施良好架构设计。该设计需要确保位于北美和欧洲的用户都能获得高可靠性和快速响应时间。

API堆栈包含以下三层：
- Amazon API Gateway
- AWS Lambda  
- Amazon DynamoDB

 | **选项A：** 配置Amazon Route 53使用健康检查指向北美和欧洲的API Gateway API。配置API将请求转发到该区域的Lambda函数。配置Lambda函数在与Lambda函数相同区域的DynamoDB表中检索和更新数据。

- **问题：** 没有使用基于延迟的路由来优化响应时间
- **问题：** 使用独立的DynamoDB表而非全局表，无法保证数据一致性
- **问题：** 跨区域数据同步会成为问题

**选项B：** 配置Amazon Route 53使用基于延迟的路由和健康检查指向北美和欧洲的API Gateway API。配置API将请求转发到该区域的Lambda函数。配置Lambda函数从DynamoDB全局表中检索和更新数据。

- **优点：** 使用基于延迟的路由确保最快响应时间
- **优点：** 包含健康检查确保高可靠性
- **优点：** 使用DynamoDB全局表确保数据一致性
- **优点：** 多区域部署提供冗余和容错能力

**选项C：** 配置Amazon Route 53指向北美的API Gateway，在欧洲创建灾难恢复API，配置两个API将请求转发到该区域的Lambda函数。从DynamoDB全局表检索数据。部署Lambda函数每5分钟检查北美API健康状况。在故障时，更新Route 53指向灾难恢复API。

- **问题：** 主要依赖北美区域，欧洲用户延迟较高
- **问题：** 手动故障转移机制不够自动化
- **问题：** 5分钟检查间隔太长，影响可用性

**选项D：** 配置Amazon Route 53使用基于延迟的路由指向北美的API Gateway API。配置API将请求转发到距离用户最近区域的Lambda函数。配置Lambda函数在DynamoDB表中检索和更新数据。

- **问题：** 只在北美部署API Gateway，欧洲用户仍需跨区域访问
- **问题：** 没有明确使用DynamoDB全局表
- **问题：** 缺乏真正的多区域冗余

 |  |  |  |
| 51 | A rapidly growing company wants to scale for developer demand for AWS development environments. Development environments are created
manually in the AWS Management Console. The networking team uses AWS CloudFormation to manage the networking infrastructure,
exporting stack output values for the Amazon VPC and all subnets. The development environments have common standards, such as
Application Load Balancers, Amazon EC2 Auto Scaling groups, security groups, and Amazon DynamoDB tables.
To keep up with demand, the DevOps engineer wants to automate the creation of development environments. Because the infrastructure
required to support the application is expected to grow, there must be a way to easily update the deployed infrastructure. CloudFormation will
be used to create a template for the development environments. | A. Use Fn::ImportValue intrinsic functions in the Resources section of the template to retrieve Virtual Private Cloud (VPC) and subnet
values. Use CloudFormation StackSets for the development environments, using the Count input parameter to indicate the number of
environments needed. Use the UpdateStackSet command to update existing development environments.
B. Use nested stacks to dene common infrastructure components. To access the exported values, use TemplateURL to reference the
networking team’s template. To retrieve Virtual Private Cloud (VPC) and subnet values, use Fn::ImportValue intrinsic functions in the
Parameters section of the root template. Use the CreateChangeSet and ExecuteChangeSet commands to update existing development
environments.
C. Use nested stacks to dene common infrastructure components. Use Fn::ImportValue intrinsic functions with the resources of the
nested stack to retrieve Virtual Private Cloud (VPC) and subnet values. Use the CreateChangeSet and ExecuteChangeSet commands to
update existing development environments.
D. Use Fn::ImportValue intrinsic functions in the Parameters section of the root template to retrieve Virtual Private Cloud (VPC) and
subnet values. Dene the development resources in the order they need to be created in the CloudFormation nested stacks. Use the
CreateChangeSet. and ExecuteChangeSet commands to update existing development environments. | 一家快速增长的公司希望扩展以满足开发人员对AWS开发环境的需求。开发环境目前在AWS管理控制台中手动创建。网络团队使用AWS CloudFormation来管理网络基础设施，导出Amazon VPC和所有子网的堆栈输出值。开发环境有通用标准，如应用程序负载均衡器、Amazon EC2自动扩展组、安全组和Amazon DynamoDB表。

为了跟上需求，DevOps工程师希望自动化创建开发环境。由于支持应用程序所需的基础设施预计会增长，必须有一种方法来轻松更新已部署的基础设施。将使用CloudFormation为开发环境创建模板。

 | **选项A：**
- 使用Fn::ImportValue在Resources部分检索VPC和子网值 - 正确用法
- 使用CloudFormation StackSets和Count参数 - **错误**：CloudFormation没有Count参数，StackSets主要用于跨账户/区域部署
- 使用UpdateStackSet命令更新环境 - 不适合单个开发环境的更新

**选项B：**
- 使用嵌套堆栈定义通用基础设施组件 - 正确方法
- 使用TemplateURL引用网络团队模板 - **错误**：应该使用Fn::ImportValue导入导出值，而不是直接引用模板
- 在Parameters部分使用Fn::ImportValue - **错误**：Fn::ImportValue应该在Resources部分使用
- 使用CreateChangeSet和ExecuteChangeSet更新 - 正确的更新方法

**选项C：**
- 使用嵌套堆栈定义通用基础设施组件 - 正确方法
- 在嵌套堆栈的资源中使用Fn::ImportValue检索VPC和子网值 - 正确用法
- 使用CreateChangeSet和ExecuteChangeSet更新环境 - 正确的更新方法

**选项D：**
- 在Parameters部分使用Fn::ImportValue - **错误**：Fn::ImportValue不能在Parameters部分使用
- 在嵌套堆栈中按创建顺序定义资源 - CloudFormation会自动处理依赖关系
- 使用CreateChangeSet和ExecuteChangeSet更新 - 正确方法

 |  |  |  |
| 52 | A company uses AWS Organizations to manage multiple accounts. Information security policies require that all unencrypted Amazon EBS
volumes be marked as non-compliant. A DevOps engineer needs to automatically deploy the solution and ensure that this compliance check is
always present. | A. Create an AWS CloudFormation template that denes an AWS Inspector rule to check whether EBS encryption is enabled. Save the
template to an Amazon S3 bucket that has been shared with all accounts within the company. Update the account creation script pointing
to the CloudFormation template in Amazon S3.
B. Create an AWS Cong organizational rule to check whether EBS encryption is enabled and deploy the rule using the AWS CLI. Create
and apply an SCP to prohibit stopping and deleting AWS Cong across the organization.
C. Create an SCP in Organizations. Set the policy to prevent the launch of Amazon EC2 instances without encryption on the EBS volumes
using a conditional expression. Apply the SCP to all AWS accounts. Use Amazon Athena to analyze the AWS CloudTrail output, looking for
events that deny an ec2:RunInstances action.
D. Deploy an IAM role to all accounts from a single trusted account. Build a pipeline with AWS CodePipeline with a stage in AWS Lambda
to assume the IAM role, and list all EBS volumes in the account. Publish a report to Amazon S3. | 一家公司使用AWS Organizations来管理多个账户。信息安全策略要求所有未加密的Amazon EBS卷都必须标记为不合规。DevOps工程师需要自动部署解决方案，并确保此合规性检查始终存在。

 | **选项A：** 创建AWS CloudFormation模板，定义AWS Inspector规则来检查EBS加密是否启用。将模板保存到与公司内所有账户共享的Amazon S3存储桶中。更新账户创建脚本，指向Amazon S3中的CloudFormation模板。
- **问题：** AWS Inspector主要用于应用程序安全评估和漏洞检测，不是用于检查EBS加密合规性的正确服务。这个方案在技术上不可行。

**选项B：** 创建AWS Config组织规则来检查EBS加密是否启用，并使用AWS CLI部署规则。创建并应用SCP来禁止在整个组织中停止和删除AWS Config。
- **优势：** AWS Config是专门用于合规性检查的服务，可以检查EBS卷加密状态。组织规则可以在所有账户中自动部署。SCP可以防止Config被意外删除或停用。
- **符合要求：** 自动部署、持续监控、防止规则被删除。

**选项C：** 在Organizations中创建SCP。设置策略使用条件表达式防止启动没有EBS卷加密的Amazon EC2实例。将SCP应用到所有AWS账户。使用Amazon Athena分析AWS CloudTrail输出，查找拒绝ec2:RunInstances操作的事件。
- **问题：** 这是预防性措施而不是合规性检查。它阻止创建未加密的EBS卷，但不能标记现有的未加密卷为不合规。不符合题目要求的"标记为不合规"。

**选项D：** 从单个受信任账户向所有账户部署IAM角色。使用AWS CodePipeline构建管道，在AWS Lambda阶段中承担IAM角色，列出账户中的所有EBS卷。将报告发布到Amazon S3。
- **问题：** 这只是生成报告，没有合规性检查和标记功能。需要手动维护和执行，不是自动化的合规性解决方案。

 |  |  |  |
| 53 | A company is performing vulnerability scanning for all Amazon EC2 instances across many accounts. The accounts are in an organization in
AWS Organizations. Each account's VPCs are attached to a shared transit gateway. The VPCs send trac to the internet through a central
egress VP | C. Grant inspector:StartAssessmentRun permissions to the IAM role that the DevOps engineer is using.
A. Verify that AWS Systems Manager Agent is installed and is running on the EC2 instances that Amazon Inspector is not scanning.
B. Associate the target EC2 instances with security groups that allow outbound communication on port 443 to the AWS Systems Manager
service endpoint.
D. Congure EC2 Instance Connect for the EC2 instances that Amazon Inspector is not scanning.
E. Associate the target EC2 instances with instance proles that grant permissions to communicate with AWS Systems Manager. | **
一家公司正在对AWS Organizations组织中多个账户的所有Amazon EC2实例执行漏洞扫描。每个账户的VPC都连接到一个共享的传输网关。这些VPC通过中央出口VPC将流量发送到互联网。

（注：题目似乎不完整，但从选项可以推断这是关于Amazon Inspector漏洞扫描无法正常工作的问题）

2. ** | **

**A. 验证AWS Systems Manager Agent已安装并在Amazon Inspector未扫描的EC2实例上运行**
- 正确。Amazon Inspector需要SSM Agent来收集实例信息和执行漏洞评估
- SSM Agent是Inspector正常工作的必要组件
- 如果Agent未安装或未运行，Inspector无法扫描这些实例

**B. 将目标EC2实例与允许通过端口443向AWS Systems Manager服务端点进行出站通信的安全组关联**
- 正确。EC2实例需要通过HTTPS（端口443）与SSM服务端点通信
- 如果安全组阻止了这种通信，Inspector将无法正常工作
- 这是网络连接的基本要求

**C. 向DevOps工程师使用的IAM角色授予inspector:StartAssessmentRun权限**
- 部分正确，但这主要解决的是启动评估的权限问题
- 如果实例本身无法被扫描，仅有启动权限是不够的
- 这更多是管理层面的权限问题

**D. 为Amazon Inspector未扫描的EC2实例配置EC2 Instance Connect**
- 不正确。EC2 Instance Connect主要用于SSH连接管理
- 与Inspector的漏洞扫描功能没有直接关系
- 不是解决Inspector扫描问题的必要配置

**E. 将目标EC2实例与授予与AWS Systems Manager通信权限的实例配置文件关联**
- 正确。EC2实例需要适当的IAM权限来与SSM服务通信
- 实例配置文件必须包含SSM相关权限（如ssm:UpdateInstanceInformation等）
- 没有这些权限，实例无法向SSM注册或接收指令

3. ** |  |  |  |
| 54 | A development team uses AWS CodeCommit for version control for applications. The development team uses AWS CodePipeline, AWS
CodeBuild. and AWS CodeDeploy for CI/CD infrastructure. In CodeCommit, the development team recently merged pull requests that did not
pass long-running tests in the code base. The development team needed to perform rollbacks to branches in the codebase, resulting in lost
time and wasted effort.
A DevOps engineer must automate testing of pull requests in CodeCommit to ensure that reviewers more easily see the results of automated
tests as part of the pull request review. | A. Create an Amazon EventBridge rule that reacts to the pullRequestStatusChanged event. Create an AWS Lambda function that invokes a
CodePipeline pipeline with a CodeBuild action that runs the tests for the application. Program the Lambda function to post the CodeBuild
badge as a comment on the pull request so that developers will see the badge in their code review.
B. Create an Amazon EventBridge rule that reacts to the pullRequestCreated event. Create an AWS Lambda function that invokes a
CodePipeline pipeline with a CodeBuild action that runs the tests for the application. Program the Lambda function to post the CodeBuild
test results as a comment on the pull request when the test results are complete.
C. Create an Amazon EventBridge rule that reacts to pullRequestCreated and pullRequestSourceBranchUpdated events. Create an AWS
Lambda function that invokes a CodePipeline pipeline with a CodeBuild action that runs the tests for the application. Program the
Lambda function to post the CodeBuild badge as a comment on the pull request so that developers will see the badge in their code
review.
D. Create an Amazon EventBridge rule that reacts to the pullRequestStatusChanged event. Create an AWS Lambda function that invokes a
CodePipeline pipeline with a CodeBuild action that runs the tests for the application. Program the Lambda function to post the CodeBuild
test results as a comment on the pull request when the test results are complete. |  |  |  |  |  |
| 55 | A company has deployed an application in a production VPC in a single AWS account. The application is popular and is experiencing heavy
usage. The company’s security team wants to add additional security, such as AWS WAF, to the application deployment. However, the
application's product manager is concerned about cost and does not want to approve the change unless the security team can prove that
additional security is necessary.
The security team believes that some of the application's demand might come from users that have IP addresses that are on a deny list. The
security team provides the deny list to a DevOps engineer. If any of the IP addresses on the deny list access the application, the security team
wants to receive automated notication in near real time so that the security team can document that the application needs additional
security. The DevOps engineer creates a VPC ow log for the production VP | C. Create an Amazon S3 bucket for log les. Congure the VPC ow log to capture accepted trac and to send the data to the S3 bucket.
Congure an Amazon OpenSearch Service cluster and domain for the log les. Create an AWS Lambda function to retrieve the logs from
the S3 bucket, format the logs, and load the logs into the OpenSearch Service cluster. Schedule the Lambda function to run every 5
minutes. Congure an alert and condition in OpenSearch Service to send alerts to the security team through an Amazon Simple
Notication Service (Amazon SNS) topic when access from the IP addresses on the deny list is detected.
A. Create a log group in Amazon CloudWatch Logs. Congure the VPC ow log to capture accepted trac and to send the data to the log
group. Create an Amazon CloudWatch metric lter for IP addresses on the deny list. Create a CloudWatch alarm with the metric lter as
input. Set the period to 5 minutes and the datapoints to alarm to 1. Use an Amazon Simple Notication Service (Amazon SNS) topic to
send alarm notices to the security team.
B. Create an Amazon S3 bucket for log les. Congure the VPC ow log to capture all trac and to send the data to the S3 bucket.
Congure Amazon Athena to return all log les in the S3 bucket for IP addresses on the deny list. Congure Amazon QuickSight to accept
data from Athena and to publish the data as a dashboard that the security team can access. Create a threshold alert of 1 for successful
access. Congure the alert to automatically notify the security team as frequently as possible when the alert threshold is met.
D. Create a log group in Amazon CloudWatch Logs. Create an Amazon S3 bucket to hold query results. Congure the VPC ow log to
capture all trac and to send the data to the log group. Deploy an Amazon Athena CloudWatch connector in AWS Lambda. Connect the
connector to the log group. Congure Athena to periodically query for all accepted trac from the IP addresses on the deny list and to
store the results in the S3 bucket. Congure an S3 event notication to automatically notify the security team through an Amazon Simple
Notication Service (Amazon SNS) topic when new objects are added to the S3 bucket. |  |  |  |  |  |
| 56 | A DevOps engineer has automated a web service deployment by using AWS CodePipeline with the following steps:
1. An AWS CodeBuild project compiles the deployment artifact and runs unit tests.
2. An AWS CodeDeploy deployment group deploys the web service to Amazon EC2 instances in the staging environment.
3. A CodeDeploy deployment group deploys the web service to EC2 instances in the production environment.
The quality assurance (QA) team requests permission to inspect the build artifact before the deployment to the production environment
occurs. The QA team wants to run an internal penetration testing tool to conduct manual tests. The tool will be invoked by a REST API call. | A. Insert a manual approval action between the test actions and deployment actions of the pipeline.
B. Modify the buildspec.yml le for the compilation stage to require manual approval before completion.
C. Update the CodeDeploy deployment groups so that they require manual approval to proceed.
D. Update the pipeline to directly call the REST API for the penetration testing tool.
E. Update the pipeline to invoke an AWS Lambda function that calls the REST API for the penetration testing tool. |  |  |  |  |  |
| 57 | A company is hosting a web application in an AWS Region. For disaster recovery purposes, a second region is being used as a standby.
Disaster recovery requirements state that session data must be replicated between regions in near-real time and 1% of requests should route
to the secondary region to continuously verify system functionality. Additionally, if there is a disruption in service in the main region, trac
should be automatically routed to the secondary region, and the secondary region must be able to scale up to handle all trac.
How should a DevOps engineer meet these requirements? | A. In both regions, deploy the application on AWS Elastic Beanstalk and use Amazon DynamoDB global tables for session data. Use an
Amazon Route 53 weighted routing policy with health checks to distribute the trac across the regions.
B. In both regions, launch the application in Auto Scaling groups and use DynamoDB for session data. Use a Route 53 failover routing
policy with health checks to distribute the trac across the regions.
C. In both regions, deploy the application in AWS Lambda, exposed by Amazon API Gateway, and use Amazon RDS for PostgreSQL with
cross-region replication for session data. Deploy the web application with client-side logic to call the API Gateway directly.
D. In both regions, launch the application in Auto Scaling groups and use DynamoDB global tables for session data. Enable an Amazon
CloudFront weighted distribution across regions. Point the Amazon Route 53 DNS record at the CloudFront distribution. |  |  |  |  |  |
| 58 | A company runs an application on Amazon EC2 instances. The company uses a series of AWS CloudFormation stacks to dene the application
resources. A developer performs updates by building and testing the application on a laptop and then uploading the build output and
CloudFormation stack templates to Amazon S3. The developer's peers review the changes before the developer performs the CloudFormation
stack update and installs a new version of the application onto the EC2 instances.
The deployment process is prone to errors and is time-consuming when the developer updates each EC2 instance with the new application.
The company wants to automate as much of the application deployment process as possible while retaining a nal manual approval step
before the modication of the application or resources.
The company already has moved the source code for the application and the CloudFormation templates to AWS CodeCommit. The company
also has created an AWS CodeBuild project to build and test the application. | A. Create an application group and a deployment group in AWS CodeDeploy. Install the CodeDeploy agent on the EC2 instances.
B. Create an application revision and a deployment group in AWS CodeDeploy. Create an environment in CodeDeploy. Register the EC2
instances to the CodeDeploy environment.
C. Use AWS CodePipeline to invoke the CodeBuild job, run the CloudFormation update, and pause for a manual approval step. After
approval, start the AWS CodeDeploy deployment.
D. Use AWS CodePipeline to invoke the CodeBuild job, create CloudFormation change sets for each of the application stacks, and pause
for a manual approval step. After approval, run the CloudFormation change sets and start the AWS CodeDeploy deployment.
E. Use AWS CodePipeline to invoke the CodeBuild job, create CloudFormation change sets for each of the application stacks, and pause
for a manual approval step. After approval, start the AWS CodeDeploy deployment. |  |  |  |  |  |
| 59 | A DevOps engineer manages a web application that runs on Amazon EC2 instances behind an Application Load Balancer (ALB). The instances
run in an EC2 Auto Scaling group across multiple Availability Zones. The engineer needs to implement a deployment strategy that:
Launches a second eet of instances with the same capacity as the original eet.
Maintains the original eet unchanged while the second eet is launched.
Transitions trac to the second eet when the second eet is fully deployed.
Terminates the original eet automatically 1 hour after transition. | A. Use an AWS CloudFormation template with a retention policy for the ALB set to 1 hour. Update the Amazon Route 53 record to reect
the new AL
B. Use two AWS Elastic Beanstalk environments to perform a blue/green deployment from the original environment to the new one. Create
an application version lifecycle policy to terminate the original environment in 1 hour.
C. Use AWS CodeDeploy with a deployment group congured with a blue/green deployment conguration Select the option Terminate the
original instances in the deployment group with a waiting period of 1 hour.
D. Use AWS Elastic Beanstalk with the conguration set to Immutable. Create an .ebextension using the Resources key that sets the
deletion policy of the ALB to 1 hour, and deploy the application. | 一名DevOps工程师管理着一个运行在Amazon EC2实例上的Web应用程序，这些实例位于应用负载均衡器(ALB)后面。实例在跨多个可用区的EC2 Auto Scaling组中运行。工程师需要实施一个部署策略，该策略需要：
- 启动与原始实例组相同容量的第二个实例组
- 在启动第二个实例组时保持原始实例组不变
- 当第二个实例组完全部署后将流量转移到第二个实例组
- 在转移后1小时自动终止原始实例组

 | **选项A：** 使用AWS CloudFormation模板，为ALB设置1小时的保留策略。更新Amazon Route 53记录以反映新的ALB。
- 这个方案没有提供完整的蓝绿部署解决方案
- CloudFormation的保留策略不是用于这种场景的
- 需要手动管理两个实例组和流量切换
- 不符合自动化部署的最佳实践

**选项B：** 使用两个AWS Elastic Beanstalk环境执行从原始环境到新环境的蓝绿部署。创建应用程序版本生命周期策略，在1小时后终止原始环境。
- Elastic Beanstalk原生支持蓝绿部署
- 可以轻松管理两个独立的环境
- 但是应用程序版本生命周期策略主要用于管理应用版本，不是用于环境终止的定时器
- 需要手动或通过其他机制来实现1小时后的环境终止

**选项C：** 使用AWS CodeDeploy配置部署组进行蓝绿部署配置。选择在1小时等待期后终止部署组中原始实例的选项。
- CodeDeploy专门为蓝绿部署设计
- 原生支持EC2/Auto Scaling组的蓝绿部署
- 提供内置的等待期配置，可以设置在流量切换后等待指定时间再终止原始实例
- 完全符合题目要求的所有条件

**选项D：** 使用AWS Elastic Beanstalk的不可变(Immutable)配置。创建.ebextension使用Resources键设置ALB的删除策略为1小时，并部署应用程序。
- 不可变部署不是蓝绿部署，它是滚动替换实例
- ALB的删除策略设置不正确，不符合需求
- 这种方法无法满足题目要求的部署策略

 |  |  |  |
| 60 | A video-sharing company stores its videos in Amazon S3. The company has observed a sudden increase in video access requests, but the
company does not know which videos are most popular. The company needs to identify the general access pattern for the video les. This
pattern includes the number of users who access a certain le on a given day, as well as the number of pull requests for certain les.
How can the company meet these requirements with the LEAST amount of effort? | A. Activate S3 server access logging. Import the access logs into an Amazon Aurora database. Use an Aurora SQL query to analyze the
access patterns.
B. Activate S3 server access logging. Use Amazon Athena to create an external table with the log les. Use Athena to create a SQL query
to analyze the access patterns.
C. Invoke an AWS Lambda function for every S3 object access event. Congure the Lambda function to write the le access information,
such as user. S3 bucket, and le key, to an Amazon Aurora database. Use an Aurora SQL query to analyze the access patterns.
D. Record an Amazon CloudWatch Logs log message for every S3 object access event. Congure a CloudWatch Logs log stream to write
the le access information, such as user, S3 bucket, and le key, to an Amazon Kinesis Data Analytics for SQL application. Perform a
sliding window analysis. | 一家视频分享公司将其视频存储在Amazon S3中。该公司观察到视频访问请求突然增加，但公司不知道哪些视频最受欢迎。公司需要识别视频文件的一般访问模式。这种模式包括在给定日期访问某个文件的用户数量，以及某些文件的拉取请求数量。
公司如何以最少的工作量满足这些要求？

 | **选项A：激活S3服务器访问日志记录。将访问日志导入Amazon Aurora数据库。使用Aurora SQL查询来分析访问模式。**
- 需要激活S3访问日志记录（正确）
- 需要手动导入日志到Aurora数据库，这增加了工作量和复杂性
- 需要管理Aurora数据库的维护、扩展等
- 不是最少工作量的解决方案

**选项B：激活S3服务器访问日志记录。使用Amazon Athena创建带有日志文件的外部表。使用Athena创建SQL查询来分析访问模式。**
- 激活S3访问日志记录（正确）
- Athena是无服务器查询服务，可以直接查询S3中的日志文件
- 无需数据导入或数据库管理
- 支持标准SQL查询进行访问模式分析
- 工作量最少，成本效益高

**选项C：为每个S3对象访问事件调用AWS Lambda函数。配置Lambda函数将文件访问信息（如用户、S3存储桶和文件键）写入Amazon Aurora数据库。使用Aurora SQL查询来分析访问模式。**
- 需要开发和维护Lambda函数
- 高访问量会导致大量Lambda调用，成本高
- 需要管理Aurora数据库
- 复杂度高，工作量大

**选项D：为每个S3对象访问事件记录Amazon CloudWatch Logs日志消息。配置CloudWatch Logs日志流将文件访问信息写入Amazon Kinesis Data Analytics for SQL应用程序。执行滑动窗口分析。**
- 需要配置复杂的实时流处理架构
- 涉及多个服务的集成和管理
- 主要用于实时分析，而题目需求是识别访问模式
- 工作量大，过度工程化

 |  |  |  |
| 61 | A development team wants to use AWS CloudFormation stacks to deploy an application. However, the developer IAM role does not have the
required permissions to provision the resources that are specied in the AWS CloudFormation template. A DevOps engineer needs to
implement a solution that allows the developers to deploy the stacks. The solution must follow the principle of least privilege. | A. Create an IAM policy that allows the developers to provision the required resources. Attach the policy to the developer IAM role.
B. Create an IAM policy that allows full access to AWS CloudFormation. Attach the policy to the developer IAM role.
C. Create an AWS CloudFormation service role that has the required permissions. Grant the developer IAM role a cloudformation:* action.
Use the new service role during stack deployments.
D. Create an AWS CloudFormation service role that has the required permissions. Grant the developer IAM role the iam:PassRole
permission. Use the new service role during stack deployments. | 一个开发团队想要使用AWS CloudFormation堆栈来部署应用程序。但是，开发者IAM角色没有所需的权限来预置AWS CloudFormation模板中指定的资源。DevOps工程师需要实施一个解决方案，允许开发者部署堆栈。该解决方案必须遵循最小权限原则。

 | **选项A：创建一个IAM策略，允许开发者预置所需的资源。将策略附加到开发者IAM角色。**
- 这种方法直接给开发者角色添加资源预置权限
- 虽然可行，但违反了最小权限原则，因为开发者将获得直接操作AWS资源的权限
- 可能导致权限过度授予，存在安全风险

**选项B：创建一个IAM策略，允许完全访问AWS CloudFormation。将策略附加到开发者IAM角色。**
- 这是最不安全的选项，给予了CloudFormation的完全访问权限
- 严重违反最小权限原则
- 开发者可能获得超出需要的权限，包括删除或修改其他堆栈的能力

**选项C：创建一个具有所需权限的AWS CloudFormation服务角色。授予开发者IAM角色cloudformation:*操作权限。在堆栈部署期间使用新的服务角色。**
- 创建服务角色的思路正确，但给予cloudformation:*权限过于宽泛
- cloudformation:*包含所有CloudFormation操作，违反最小权限原则
- 开发者仍然可能执行不必要的CloudFormation操作

**选项D：创建一个具有所需权限的AWS CloudFormation服务角色。授予开发者IAM角色iam:PassRole权限。在堆栈部署期间使用新的服务角色。**
- 创建专门的CloudFormation服务角色来处理资源预置
- 开发者只需要iam:PassRole权限来传递服务角色给CloudFormation
- 符合最小权限原则：开发者不直接获得资源操作权限，而是通过服务角色间接获得
- 这是AWS推荐的最佳实践模式

 |  |  |  |
| 62 | A production account has a requirement that any Amazon EC2 instance that has been logged in to manually must be terminated within 24
hours. All applications in the production account are using Auto Scaling groups with the Amazon CloudWatch Logs agent congured.
How can this process be automated? | A. Create a CloudWatch Logs subscription to an AWS Step Functions application. Congure an AWS Lambda function to add a tag to the
EC2 instance that produced the login event and mark the instance to be decommissioned. Create an Amazon EventBridge rule to invoke a
second Lambda function once a day that will terminate all instances with this tag.
B. Create an Amazon CloudWatch alarm that will be invoked by the login event. Send the notication to an Amazon Simple Notication
Service (Amazon SNS) topic that the operations team is subscribed to, and have them terminate the EC2 instance within 24 hours.
C. Create an Amazon CloudWatch alarm that will be invoked by the login event. Congure the alarm to send to an Amazon Simple Queue
Service (Amazon SQS) queue. Use a group of worker instances to process messages from the queue, which then schedules an Amazon
EventBridge rule to be invoked.
D. Create a CloudWatch Logs subscription to an AWS Lambda function. Congure the function to add a tag to the EC2 instance that
produced the login event and mark the instance to be decommissioned. Create an Amazon EventBridge rule to invoke a daily Lambda
function that terminates all instances with this tag. | 一个生产账户有一个要求：任何被手动登录过的Amazon EC2实例必须在24小时内终止。生产账户中的所有应用程序都使用配置了Amazon CloudWatch Logs代理的Auto Scaling组。

如何自动化这个过程？

 | **选项A：** 创建一个CloudWatch Logs订阅到AWS Step Functions应用程序。配置AWS Lambda函数为产生登录事件的EC2实例添加标签并标记实例待停用。创建Amazon EventBridge规则每天调用第二个Lambda函数来终止所有带有此标签的实例。

- **问题分析：** 使用Step Functions增加了不必要的复杂性。对于这个相对简单的工作流，直接使用Lambda函数更合适。Step Functions适用于复杂的多步骤工作流，这里只需要标记和定时终止两个步骤。

**选项B：** 创建一个由登录事件触发的Amazon CloudWatch告警。将通知发送到运维团队订阅的Amazon SNS主题，让他们在24小时内终止EC2实例。

- **问题分析：** 这是手动解决方案，不符合"自动化这个过程"的要求。依赖人工干预违背了自动化的初衷。

**选项C：** 创建一个由登录事件触发的Amazon CloudWatch告警。配置告警发送到Amazon SQS队列。使用一组工作实例处理队列中的消息，然后调度Amazon EventBridge规则。

- **问题分析：** 架构过于复杂，使用了不必要的组件（SQS队列和工作实例）。CloudWatch告警不是处理日志事件的最佳方式，CloudWatch Logs订阅更适合。

**选项D：** 创建CloudWatch Logs订阅到AWS Lambda函数。配置函数为产生登录事件的EC2实例添加标签并标记实例待停用。创建Amazon EventBridge规则调用每日Lambda函数来终止所有带有此标签的实例。

- **优势分析：** 
  - 使用CloudWatch Logs订阅直接处理日志事件，这是最直接和高效的方法
  - 架构简洁，只使用必要的服务
  - 通过标签系统实现实例标记和批量处理
  - EventBridge提供可靠的定时调度机制

 |  |  |  |
| 63 | A company has enabled all features for its organization in AWS Organizations. The organization contains 10 AWS accounts. The company has
turned on AWS CloudTrail in all the accounts. The company expects the number of AWS accounts in the organization to increase to 500 during
the next year. The company plans to use multiple OUs for these accounts.
The company has enabled AWS Cong in each existing AWS account in the organization. A DevOps engineer must implement a solution that
enables AWS Cong automatically for all future AWS accounts that are created in the organization. | A. In the organization's management account, create an Amazon EventBridge rule that reacts to a CreateAccount API call. Congure the
rule to invoke an AWS Lambda function that enables trusted access to AWS Cong for the organization.
B. In the organization's management account, create an AWS CloudFormation stack set to enable AWS Cong. Congure the stack set to
deploy automatically when an account is created through Organizations.
C. In the organization's management account, create an SCP that allows the appropriate AWS Cong API calls to enable AWS Cong. Apply
the SCP to the root-level OU.
D. In the organization's management account, create an Amazon EventBridge rule that reacts to a CreateAccount API call. Congure the
rule to invoke an AWS Systems Manager Automation runbook to enable AWS Cong for the account. |  |  |  |  |  |
| 64 | A company has many applications. Different teams in the company developed the applications by using multiple languages and frameworks.
The applications run on premises and on different servers with different operating systems. Each team has its own release protocol and
process. The company wants to reduce the complexity of the release and maintenance of these applications.
The company is migrating its technology stacks, including these applications, to AWS. The company wants centralized control of source code,
a consistent and automatic delivery pipeline, and as few maintenance tasks as possible on the underlying infrastructure. | A. Create one AWS CodeCommit repository for all applications. Put each application's code in a different branch. Merge the branches, and
use AWS CodeBuild to build the applications. Use AWS CodeDeploy to deploy the applications to one centralized application server.
B. Create one AWS CodeCommit repository for each of the applications. Use AWS CodeBuild to build the applications one at a time. Use
AWS CodeDeploy to deploy the applications to one centralized application server.
C. Create one AWS CodeCommit repository for each of the applications. Use AWS CodeBuild to build the applications one at a time and to
create one AMI for each server. Use AWS CloudFormation StackSets to automatically provision and decommission Amazon EC2 eets by
using these AMIs.
D. Create one AWS CodeCommit repository for each of the applications. Use AWS CodeBuild to build one Docker image for each
application in Amazon Elastic Container Registry (Amazon ECR). Use AWS CodeDeploy to deploy the applications to Amazon Elastic
Container Service (Amazon ECS) on infrastructure that AWS Fargate manages. |  |  |  |  |  |
| 65 | A company's application is currently deployed to a single AWS Region. Recently, the company opened a new oce on a different continent.
The users in the new oce are experiencing high latency. The company's application runs on Amazon EC2 instances behind an Application
Load Balancer (ALB) and uses Amazon DynamoDB as the database layer. The instances run in an EC2 Auto Scaling group across multiple
Availability Zones. A DevOps engineer is tasked with minimizing application response times and improving availability for users in both
Regions. | A. Create a new DynamoDB table in the new Region with cross-Region replication enabled.
B. F. Convert the DynamoDB table to a global table.
C. Create new ALB and Auto Scaling group resources in the new Region and congure the new ALB to direct trac to the new Auto Scaling
group.
D. Create Amazon Route 53 records, health checks, and latency-based routing policies to route to the AL
E. Create Amazon Route 53 aliases, health checks, and failover routing policies to route to the AL | 一家公司的应用程序目前部署在单个AWS区域中。最近，该公司在不同大陆开设了新办公室。新办公室的用户遇到了高延迟问题。该公司的应用程序运行在应用负载均衡器(ALB)后面的Amazon EC2实例上，并使用Amazon DynamoDB作为数据库层。这些实例在跨多个可用区的EC2 Auto Scaling组中运行。DevOps工程师的任务是最小化应用程序响应时间并提高两个区域用户的可用性。

 | **A. 在新区域创建新的DynamoDB表并启用跨区域复制**
- 这个选项不完整，只解决了数据库层的问题
- 跨区域复制可以减少数据访问延迟，但没有解决应用层的延迟问题
- 单独使用此选项无法完全解决用户体验问题

**B. 将DynamoDB表转换为全局表**
- 全局表提供多区域、多主复制，可以显著减少数据库访问延迟
- 这是处理多区域数据库需求的最佳实践
- 但同样只解决了数据库层问题，没有解决应用层延迟

**C. 在新区域创建新的ALB和Auto Scaling组资源，并配置新的ALB将流量导向新的Auto Scaling组**
- 这解决了应用层的延迟问题，通过在新区域部署应用实例
- 可以显著减少新办公室用户的网络延迟
- 但没有解决数据库层的延迟问题

**D. 创建Amazon Route 53记录、健康检查和基于延迟的路由策略来路由到ALB**
- 基于延迟的路由可以自动将用户路由到延迟最低的区域
- 这是多区域部署中流量管理的最佳实践
- 但需要配合多区域的基础设施部署才有效

**E. 创建Amazon Route 53别名、健康检查和故障转移路由策略来路由到ALB**
- 故障转移路由主要用于灾难恢复场景
- 不是为了优化延迟而设计的
- 不适合解决用户体验延迟问题

 |  |  |  |
| 66 | A DevOps engineer needs to apply a core set of security controls to an existing set of AWS accounts. The accounts are in an organization in
AWS Organizations. Individual teams will administer individual accounts by using the AdministratorAccess AWS managed policy. For all
accounts. AWS CloudTrail and AWS Cong must be turned on in all available AWS Regions. Individual account administrators must not be able
to edit or delete any of the baseline resources. However, individual account administrators must be able to edit or delete their own CloudTrail
trails and AWS Cong rules. | A. Create an AWS CloudFormation template that denes the standard account resources. Deploy the template to all accounts from the
organization's management account by using CloudFormation StackSets. Set the stack policy to deny Update:Delete actions.
B. Enable AWS Control Tower. Enroll the existing accounts in AWS Control Tower. Grant the individual account administrators access to
CloudTrail and AWS Cong.
C. Designate an AWS Cong management account. Create AWS Cong recorders in all accounts by using AWS CloudFormation StackSets.
Deploy AWS Cong rules to the organization by using the AWS Cong management account. Create a CloudTrail organization trail in the
organization’s management account. Deny modication or deletion of the AWS Cong recorders by using an SCP.
D. Create an AWS CloudFormation template that denes the standard account resources. Deploy the template to all accounts from the
organization's management account by using Cloud Formation StackSets Create an SCP that prevents updates or deletions to CloudTrail
resources or AWS Cong resources unless the principal is an administrator of the organization's management account. | 一名DevOps工程师需要对AWS Organizations中现有的一组AWS账户应用一套核心安全控制措施。这些账户位于AWS Organizations的组织中。各个团队将使用AdministratorAccess AWS托管策略来管理各自的账户。对于所有账户，必须在所有可用的AWS区域中启用AWS CloudTrail和AWS Config。各个账户管理员不得编辑或删除任何基线资源。但是，各个账户管理员必须能够编辑或删除他们自己的CloudTrail跟踪和AWS Config规则。

 | **选项A：** 创建定义标准账户资源的AWS CloudFormation模板。使用CloudFormation StackSets从组织的管理账户将模板部署到所有账户。设置堆栈策略以拒绝Update:Delete操作。
- 问题：堆栈策略只能防止对CloudFormation堆栈本身的修改，但不能防止通过其他方式（如控制台、CLI）直接修改资源。无法满足"个人管理员可以创建自己的CloudTrail和Config规则"的要求。

**选项B：** 启用AWS Control Tower。将现有账户注册到AWS Control Tower中。授予各个账户管理员访问CloudTrail和AWS Config的权限。
- 问题：Control Tower主要用于新账户的设置和治理，对现有账户的注册过程复杂且可能有限制。没有明确说明如何防止基线资源被修改，同时允许创建新的资源。

**选项C：** 指定一个AWS Config管理账户。使用AWS CloudFormation StackSets在所有账户中创建AWS Config记录器。使用AWS Config管理账户将AWS Config规则部署到组织。在组织的管理账户中创建CloudTrail组织跟踪。使用SCP拒绝对AWS Config记录器的修改或删除。
- 优点：使用组织级CloudTrail和Config管理账户提供集中控制。SCP可以精确控制权限。
- 问题：只提到了Config记录器的保护，没有完整覆盖CloudTrail的保护，且实现相对复杂。

**选项D：** 创建定义标准账户资源的AWS CloudFormation模板。使用CloudFormation StackSets从组织的管理账户将模板部署到所有账户。创建SCP，防止对CloudTrail资源或AWS Config资源的更新或删除，除非主体是组织管理账户的管理员。
- 优点：使用StackSets确保一致部署，SCP提供强制性权限控制，可以精确控制谁能修改基线资源，同时允许账户管理员创建自己的资源。

 |  |  |  |
| 67 | A company has its AWS accounts in an organization in AWS Organizations. AWS Cong is manually congured in each AWS account. The
company needs to implement a solution to centrally congure AWS Cong for all accounts in the organization The solution also must record
resource changes to a central account. | A. Congure a delegated administrator account for AWS Cong. Enable trusted access for AWS Cong in the organization.
B. Congure a delegated administrator account for AWS Cong. Create a service-linked role for AWS Cong in the organization’s
management account.
C. Create an AWS CloudFormation template to create an AWS Cong aggregator. Congure a CloudFormation stack set to deploy the
template to all accounts in the organization.
D. Create an AWS Cong organization aggregator in the organization's management account. Congure data collection from all AWS
accounts in the organization and from all AWS Regions.
E. Create an AWS Cong organization aggregator in the delegated administrator account. Congure data collection from all AWS accounts
in the organization and from all AWS Regions. | 一家公司在AWS Organizations中拥有多个AWS账户。AWS Config在每个AWS账户中都是手动配置的。公司需要实施一个解决方案来为组织中的所有账户集中配置AWS Config。该解决方案还必须将资源变更记录到一个中央账户中。

 | **选项A：为AWS Config配置委托管理员账户。在组织中为AWS Config启用可信访问。**
- 这是设置集中化AWS Config管理的第一步
- 委托管理员账户允许非管理账户来管理组织级别的AWS Config
- 启用可信访问是必需的，但这个选项没有提到如何收集和聚合数据

**选项B：为AWS Config配置委托管理员账户。在组织的管理账户中为AWS Config创建服务链接角色。**
- 委托管理员账户的配置是正确的
- 但是服务链接角色通常是自动创建的，手动创建不是最佳实践
- 没有涉及数据聚合的部分

**选项C：创建AWS CloudFormation模板来创建AWS Config聚合器。配置CloudFormation堆栈集将模板部署到组织中的所有账户。**
- 这种方法会在每个账户中创建聚合器，这不是集中化的解决方案
- 会导致重复和管理复杂性
- 不符合"集中配置"的要求

**选项D：在组织的管理账户中创建AWS Config组织聚合器。配置从组织中所有AWS账户和所有AWS区域收集数据。**
- 在管理账户中创建聚合器不是最佳实践
- AWS建议使用委托管理员账户而不是管理账户来处理这类操作
- 虽然能实现数据收集，但违反了最佳实践

**选项E：在委托管理员账户中创建AWS Config组织聚合器。配置从组织中所有AWS账户和所有AWS区域收集数据。**
- 使用委托管理员账户符合AWS最佳实践
- 组织聚合器可以自动从所有成员账户收集配置数据
- 实现了集中化管理和数据收集的要求

 |  |  |  |
| 68 | A company wants to migrate its content sharing web application hosted on Amazon EC2 to a serverless architecture. The company currently
deploys changes to its application by creating a new Auto Scaling group of EC2 instances and a new Elastic Load Balancer, and then shifting
the trac away using an Amazon Route 53 weighted routing policy.
For its new serverless application, the company is planning to use Amazon API Gateway and AWS Lambda. The company will need to update
its deployment processes to work with the new application. It will also need to retain the ability to test new features on a small number of
users before rolling the features out to the entire user base. | A. Use AWS CDK to deploy API Gateway and Lambda functions. When code needs to be changed, update the AWS CloudFormation stack
and deploy the new version of the APIs and Lambda functions. Use a Route 53 failover routing policy for the canary release strategy.
B. Use AWS CloudFormation to deploy API Gateway and Lambda functions using Lambda function versions. When code needs to be
changed, update the CloudFormation stack with the new Lambda code and update the API versions using a canary release strategy.
Promote the new version when testing is complete.
C. Use AWS Elastic Beanstalk to deploy API Gateway and Lambda functions. When code needs to be changed, deploy a new version of the
API and Lambda functions. Shift trac gradually using an Elastic Beanstalk blue/green deployment.
D. Use AWS OpsWorks to deploy API Gateway in the service layer and Lambda functions in a custom layer. When code needs to be
changed, use OpsWorks to perform a blue/green deployment and shift trac gradually. |  |  |  |  |  |
| 69 | A development team uses AWS CodeCommit, AWS CodePipeline, and AWS CodeBuild to develop and deploy an application. Changes to the
code are submitted by pull requests. The development team reviews and merges the pull requests, and then the pipeline builds and tests the
application.
Over time, the number of pull requests has increased. The pipeline is frequently blocked because of failing tests. To prevent this blockage, the
development team wants to run the unit and integration tests on each pull request before it is merged. | A. Create a CodeBuild project to run the unit and integration tests. Create a CodeCommit approval rule template. Congure the template
to require the successful invocation of the CodeBuild project. Attach the approval rule to the project's CodeCommit repository.
B. Create an Amazon EventBridge rule to match pullRequestCreated events from CodeCommit Create a CodeBuild project to run the unit
and integration tests. Congure the CodeBuild project as a target of the EventBridge rule that includes a custom event payload with the
CodeCommit repository and branch information from the event.
C. Create an Amazon EventBridge rule to match pullRequestCreated events from CodeCommit. Modify the existing CodePipeline pipeline
to not run the deploy steps if the build is started from a pull request. Congure the EventBridge rule to run the pipeline with a custom
payload that contains the CodeCommit repository and branch information from the event.
D. Create a CodeBuild project to run the unit and integration tests. Create a CodeCommit notication rule that matches when a pull
request is created or updated. Congure the notication rule to invoke the CodeBuild project. |  |  |  |  |  |
| 70 | A company has an application that runs on a eet of Amazon EC2 instances. The application requires frequent restarts. The application logs
contain error messages when a restart is required. The application logs are published to a log group in Amazon CloudWatch Logs.
An Amazon CloudWatch alarm noties an application engineer through an Amazon Simple Notication Service (Amazon SNS) topic when the
logs contain a large number of restart-related error messages. The application engineer manually restarts the application on the instances
after the application engineer receives a notication from the SNS topic.
A DevOps engineer needs to implement a solution to automate the application restart on the instances without restarting the instances. | A. Congure an AWS Systems Manager Automation runbook that runs a script to restart the application on the instances. Congure the
SNS topic to invoke the runbook.
B. Create an AWS Lambda function that restarts the application on the instances. Congure the Lambda function as an event destination
of the SNS topic.
C. Congure an AWS Systems Manager Automation runbook that runs a script to restart the application on the instances. Create an AWS
Lambda function to invoke the runbook. Congure the Lambda function as an event destination of the SNS topic.
D. Congure an AWS Systems Manager Automation runbook that runs a script to restart the application on the instances. Congure an
Amazon EventBridge rule that reacts when the CloudWatch alarm enters ALARM state. Specify the runbook as a target of the rule. | 一家公司有一个运行在Amazon EC2实例集群上的应用程序。该应用程序需要频繁重启。当需要重启时，应用程序日志会包含错误消息。应用程序日志发布到Amazon CloudWatch Logs中的日志组。

当日志包含大量重启相关错误消息时，Amazon CloudWatch告警会通过Amazon Simple Notification Service (Amazon SNS)主题通知应用程序工程师。应用程序工程师在收到SNS主题通知后手动重启实例上的应用程序。

DevOps工程师需要实现一个解决方案来自动化实例上的应用程序重启，而不重启实例本身。

 | **选项A：配置AWS Systems Manager自动化运行手册来运行脚本重启实例上的应用程序。配置SNS主题来调用运行手册。**
- 问题：SNS主题无法直接调用Systems Manager自动化运行手册。SNS只能发送消息到支持的目标（如Lambda、SQS、HTTP端点等），不能直接触发SSM自动化文档。

**选项B：创建AWS Lambda函数来重启实例上的应用程序。将Lambda函数配置为SNS主题的事件目标。**
- 可行性：SNS可以直接触发Lambda函数，这是有效的集成方式。
- 考虑：Lambda函数需要实现重启应用程序的逻辑，可能需要使用SSM Run Command或其他方式连接到EC2实例。

**选项C：配置AWS Systems Manager自动化运行手册来运行脚本重启实例上的应用程序。创建AWS Lambda函数来调用运行手册。将Lambda函数配置为SNS主题的事件目标。**
- 可行性：这是一个完整的解决方案链：SNS → Lambda → SSM自动化运行手册
- 优势：利用了SSM自动化运行手册的强大功能来管理EC2实例上的操作，同时通过Lambda作为桥梁连接SNS和SSM。

**选项D：配置AWS Systems Manager自动化运行手册来运行脚本重启实例上的应用程序。配置Amazon EventBridge规则来响应CloudWatch告警进入ALARM状态。将运行手册指定为规则的目标。**
- 问题：这个方案绕过了现有的SNS通知机制，直接从CloudWatch告警触发。虽然技术上可行，但改变了现有的架构设计。

 |  |  |  |
| 71 | A DevOps engineer at a company is supporting an AWS environment in which all users use AWS IAM Identity Center (AWS Single Sign-On). The
company wants to immediately disable credentials of any new IAM user and wants the security team to receive a notication. | A. Create an Amazon EventBridge rule that reacts to an IAM CreateUser API call in AWS CloudTrail.
B. Create an Amazon EventBridge rule that reacts to an IAM GetLoginProle API call in AWS CloudTrail.
C. Create an AWS Lambda function that is a target of the EventBridge rule. Congure the Lambda function to disable any access keys and
delete the login proles that are associated with the IAM user.
D. Create an AWS Lambda function that is a target of the EventBridge rule. Congure the Lambda function to delete the login proles that
are associated with the IAM user.
E. Create an Amazon Simple Notication Service (Amazon SNS) topic that is a target of the EventBridge rule. Subscribe the security team's
group email address to the topic. |  |  |  |  |  |
| 72 | A company wants to set up a continuous delivery pipeline. The company stores application code in a private GitHub repository. The company
needs to deploy the application components to Amazon Elastic Container Service (Amazon ECS). Amazon EC2, and AWS Lambda. The pipeline
must support manual approval actions. | A. Use AWS CodePipeline with Amazon ECS. Amazon EC2, and Lambda as deploy providers.
B. Use AWS CodePipeline with AWS CodeDeploy as the deploy provider.
C. Use AWS CodePipeline with AWS Elastic Beanstalk as the deploy provider.
D. Use AWS CodeDeploy with GitHub integration to deploy the application. | 一家公司想要建立一个持续交付管道。该公司将应用程序代码存储在私有GitHub存储库中。公司需要将应用程序组件部署到Amazon Elastic Container Service (Amazon ECS)、Amazon EC2和AWS Lambda。该管道必须支持手动批准操作。

 | **选项A：使用AWS CodePipeline，以Amazon ECS、Amazon EC2和Lambda作为部署提供商**
- CodePipeline确实支持手动批准操作
- 可以连接私有GitHub存储库作为源
- 但是，CodePipeline本身不能直接将ECS、EC2和Lambda作为"部署提供商"
- ECS、EC2和Lambda是目标服务，而不是部署提供商
- 需要通过其他部署服务（如CodeDeploy）来实现部署

**选项B：使用AWS CodePipeline，以AWS CodeDeploy作为部署提供商**
- CodePipeline支持手动批准操作 ✓
- 可以连接私有GitHub存储库 ✓
- CodeDeploy可以部署到EC2实例 ✓
- CodeDeploy可以部署到ECS服务 ✓
- CodeDeploy可以部署到Lambda函数 ✓
- 这是正确的架构组合

**选项C：使用AWS CodePipeline，以AWS Elastic Beanstalk作为部署提供商**
- CodePipeline支持手动批准操作 ✓
- 可以连接私有GitHub存储库 ✓
- 但Elastic Beanstalk主要用于Web应用程序部署，不适合同时部署到ECS、EC2和Lambda的多样化需求
- 不是最佳选择

**选项D：使用AWS CodeDeploy与GitHub集成来部署应用程序**
- CodeDeploy可以与GitHub集成 ✓
- CodeDeploy可以部署到多个目标服务 ✓
- 但CodeDeploy本身不提供完整的CI/CD管道功能
- 缺少手动批准操作的原生支持
- 没有CodePipeline提供的完整管道编排功能

 |  |  |  |
| 73 | A company has an application that runs on Amazon EC2 instances that are in an Auto Scaling group. When the application starts up. the
application needs to process data from an Amazon S3 bucket before the application can start to serve requests.
The size of the data that is stored in the S3 bucket is growing. When the Auto Scaling group adds new instances, the application now takes
several minutes to download and process the data before the application can serve requests. The company must reduce the time that elapses
before new EC2 instances are ready to serve requests. | A. Congure a warm pool for the Auto Scaling group with warmed EC2 instances in the Stopped state. Congure an
autoscaling:EC2_INSTANCE_LAUNCHING lifecycle hook on the Auto Scaling group. Modify the application to complete the lifecycle hook
when the application is ready to serve requests.
B. Increase the maximum instance count of the Auto Scaling group. Congure an autoscaling:EC2_INSTANCE_LAUNCHING lifecycle hook
on the Auto Scaling group. Modify the application to complete the lifecycle hook when the application is ready to serve requests.
C. Congure a warm pool for the Auto Scaling group with warmed EC2 instances in the Running state. Congure an
autoscaling:EC2_INSTANCE_LAUNCHING lifecycle hook on the Auto Scaling group. Modify the application to complete the lifecycle hook
when the application is ready to serve requests.
D. Increase the maximum instance count of the Auto Scaling group. Congure an autoscaling:EC2_INSTANCE_LAUNCHING lifecycle hook
on the Auto Scaling group. Modify the application to complete the lifecycle hook and to place the new instance in the Standby state when
the application is ready to serve requests. | 一家公司有一个运行在Amazon EC2实例上的应用程序，这些实例位于Auto Scaling组中。当应用程序启动时，应用程序需要先处理Amazon S3存储桶中的数据，然后才能开始处理请求。

存储在S3存储桶中的数据大小正在增长。当Auto Scaling组添加新实例时，应用程序现在需要几分钟时间来下载和处理数据，然后才能处理请求。公司必须减少新EC2实例准备好处理请求之前所需的时间。

 | **选项A：** 为Auto Scaling组配置warm pool，其中预热的EC2实例处于Stopped状态。在Auto Scaling组上配置autoscaling:EC2_INSTANCE_LAUNCHING生命周期钩子。修改应用程序以在准备好处理请求时完成生命周期钩子。
- **分析：** 这个方案有问题。如果实例在warm pool中处于Stopped状态，当需要启动时仍然需要启动实例并重新处理S3数据，无法真正减少准备时间。

**选项B：** 增加Auto Scaling组的最大实例数。在Auto Scaling组上配置autoscaling:EC2_INSTANCE_LAUNCHING生命周期钩子。修改应用程序以在准备好处理请求时完成生命周期钩子。
- **分析：** 仅仅增加最大实例数并不能解决数据处理时间长的问题。每个新实例仍然需要花费几分钟下载和处理S3数据。

**选项C：** 为Auto Scaling组配置warm pool，其中预热的EC2实例处于Running状态。在Auto Scaling组上配置autoscaling:EC2_INSTANCE_LAUNCHING生命周期钩子。修改应用程序以在准备好处理请求时完成生命周期钩子。
- **分析：** 这是最佳方案。Running状态的warm pool实例可以预先下载和处理S3数据，当需要扩容时可以快速投入使用。生命周期钩子确保实例完全准备好后才开始接收流量。

**选项D：** 增加Auto Scaling组的最大实例数。在Auto Scaling组上配置autoscaling:EC2_INSTANCE_LAUNCHING生命周期钩子。修改应用程序以在准备好处理请求时完成生命周期钩子，并在应用程序准备好处理请求时将新实例置于Standby状态。
- **分析：** 这个方案逻辑有误。将准备好的实例置于Standby状态意味着它们不会接收流量，这与目标相反。

 |  |  |  |
| 74 | A company is using an AWS CodeBuild project to build and package an application. The packages are copied to a shared Amazon S3 bucket
before being deployed across multiple AWS accounts.
The buildspec.yml le contains the following:
The DevOps engineer has noticed that anybody with an AWS account is able to download the artifacts. | A. Modify the post_build command to use --acl public-read and congure a bucket policy that grants read access to the relevant AWS
accounts only.
B. Congure a default ACL for the S3 bucket that denes the set of authenticated users as the relevant AWS accounts only and grants
read-only access.
C. Create an S3 bucket policy that grants read access to the relevant AWS accounts and denies read access to the principal “*”.
D. Modify the post_build command to remove --acl authenticated-read and congure a bucket policy that allows read access to the
relevant AWS accounts only. | 一家公司正在使用AWS CodeBuild项目来构建和打包应用程序。这些包在部署到多个AWS账户之前，会被复制到一个共享的Amazon S3存储桶中。

buildspec.yml文件包含以下内容：（题目中buildspec.yml的具体内容似乎被截断了）

DevOps工程师注意到任何拥有AWS账户的人都能够下载这些构件。

 | **选项A：修改post_build命令使用--acl public-read，并配置存储桶策略，仅向相关AWS账户授予读取访问权限。**
- 错误。使用`--acl public-read`会使对象对所有人公开可读，这与题目要求限制访问权限的目标相反。即使配置了存储桶策略，ACL的public-read设置仍然会允许公共访问。

**选项B：为S3存储桶配置默认ACL，将经过身份验证的用户集定义为仅相关的AWS账户，并授予只读访问权限。**
- 错误。AWS S3的默认ACL中的"authenticated users"是指所有AWS用户，不能限制为特定的AWS账户。这个选项在技术上不可行，因为无法将authenticated users组限制为特定账户。

**选项C：创建S3存储桶策略，向相关AWS账户授予读取访问权限，并拒绝主体"*"的读取访问权限。**
- 错误。虽然思路正确，但实施上有问题。如果先拒绝所有主体("*")的访问，然后再允许特定账户访问，由于AWS IAM中拒绝(Deny)优先于允许(Allow)的原则，这可能会导致即使是授权的账户也无法访问。

**选项D：修改post_build命令移除--acl authenticated-read，并配置存储桶策略，仅允许相关AWS账户的读取访问权限。**
- 正确。移除`--acl authenticated-read`可以防止所有经过身份验证的AWS用户访问对象。然后通过存储桶策略精确控制哪些特定的AWS账户可以访问，这是最安全和最精确的方法。

 |  |  |  |
| 75 | A company has developed a serverless web application that is hosted on AWS. The application consists of Amazon S3. Amazon API Gateway,
several AWS Lambda functions, and an Amazon RDS for MySQL database. The company is using AWS CodeCommit to store the source code.
The source code is a combination of AWS Serverless Application Model (AWS SAM) templates and Python code.
A security audit and penetration test reveal that user names and passwords for authentication to the database are hardcoded within
CodeCommit repositories. A DevOps engineer must implement a solution to automatically detect and prevent hardcoded secrets. | A. Enable Amazon CodeGuru Proler. Decorate the handler function with @with_lambda_proler(). Manually review the recommendation
report. Write the secret to AWS Systems Manager Parameter Store as a secure string. Update the SAM templates and the Python code to
pull the secret from Parameter Store.
B. Associate the CodeCommit repository with Amazon CodeGuru Reviewer. Manually check the code review for any recommendations.
Choose the option to protect the secret. Update the SAM templates and the Python code to pull the secret from AWS Secrets Manager.
C. Enable Amazon CodeGuru Proler. Decorate the handler function with @with_lambda_proler(). Manually review the recommendation
report. Choose the option to protect the secret. Update the SAM templates and the Python code to pull the secret from AWS Secrets
Manager.
D. Associate the CodeCommit repository with Amazon CodeGuru Reviewer. Manually check the code review for any recommendations.
Write the secret to AWS Systems Manager Parameter Store as a string. Update the SAM templates and the Python code to pull the secret
from Parameter Store. | 一家公司开发了一个托管在AWS上的无服务器Web应用程序。该应用程序由Amazon S3、Amazon API Gateway、多个AWS Lambda函数和Amazon RDS for MySQL数据库组成。公司使用AWS CodeCommit存储源代码。源代码是AWS无服务器应用程序模型(AWS SAM)模板和Python代码的组合。

安全审计和渗透测试发现，用于数据库身份验证的用户名和密码在CodeCommit存储库中是硬编码的。DevOps工程师必须实施一个解决方案来自动检测和防止硬编码的秘密信息。

 | **选项A：**
- 启用Amazon CodeGuru Profiler并使用@with_lambda_profiler()装饰器
- 问题：CodeGuru Profiler主要用于性能分析，不是用于代码安全审查和检测硬编码秘密
- 使用Systems Manager Parameter Store作为安全字符串存储秘密是可行的
- 但工具选择错误

**选项B：**
- 将CodeCommit存储库与Amazon CodeGuru Reviewer关联
- 正确：CodeGuru Reviewer专门用于代码质量和安全审查，能够检测硬编码秘密
- 使用AWS Secrets Manager存储秘密信息
- 正确：Secrets Manager是专门为管理敏感信息设计的服务
- 手动检查代码审查建议是合理的流程

**选项C：**
- 使用CodeGuru Profiler
- 问题：同选项A，工具选择错误，Profiler不是用于安全审查的
- 虽然使用Secrets Manager是正确的，但基础工具选择错误

**选项D：**
- 使用CodeGuru Reviewer是正确的
- 问题：将秘密作为普通字符串写入Parameter Store，而不是安全字符串
- 这不符合安全最佳实践，敏感信息应该加密存储

 |  |  |  |
| 76 | A company is using Amazon S3 buckets to store important documents. The company discovers that some S3 buckets are not encrypted.
Currently, the company’s IAM users can create new S3 buckets without encryption. The company is implementing a new requirement that all
S3 buckets must be encrypted.
A DevOps engineer must implement a solution to ensure that server-side encryption is enabled on all existing S3 buckets and all new S3
buckets. The encryption must be enabled on new S3 buckets as soon as the S3 buckets are created. The default encryption type must be 256-
bit Advanced Encryption Standard (AES-256). | A. Create an AWS Lambda function that is invoked periodically by an Amazon EventBridge scheduled rule. Program the Lambda function
to scan all current S3 buckets for encryption status and to set AES-256 as the default encryption for any S3 bucket that does not have an
encryption conguration.
B. Set up and activate the s3-bucket-server-side-encryption-enabled AWS Cong managed rule. Congure the rule to use the AWS-
EnableS3BucketEncryption AWS Systems Manager Automation runbook as the remediation action. Manually run the re-evaluation process
to ensure that existing S3 buckets are compliant.
C. Create an AWS Lambda function that is invoked by an Amazon EventBridge event rule. Dene the rule with an event pattern that
matches the creation of new S3 buckets. Program the Lambda function to parse the EventBridge event, check the conguration of the S3
buckets from the event, and set AES-256 as the default encryption.
D. Congure an IAM policy that denies the s3:CreateBucket action if the s3:x-amz-server-side-encryption condition key has a value that is
not AES-256. Create an IAM group for all the company’s IAM users. Associate the IAM policy with the IAM group. | 一家公司正在使用Amazon S3存储桶来存储重要文档。该公司发现一些S3存储桶没有加密。目前，该公司的IAM用户可以创建没有加密的新S3存储桶。该公司正在实施一项新要求，即所有S3存储桶都必须加密。

DevOps工程师必须实施一个解决方案，确保在所有现有S3存储桶和所有新S3存储桶上启用服务器端加密。加密必须在创建新S3存储桶后立即启用。默认加密类型必须是256位高级加密标准(AES-256)。

 | **选项A：** 创建一个AWS Lambda函数，由Amazon EventBridge定时规则定期调用。编程Lambda函数扫描所有当前S3存储桶的加密状态，并为任何没有加密配置的S3存储桶设置AES-256作为默认加密。
- **分析：** 这个方案只能处理现有存储桶的加密问题，但无法确保新创建的存储桶立即启用加密。定期扫描存在时间延迟，不符合"立即启用"的要求。

**选项B：** 设置并激活s3-bucket-server-side-encryption-enabled AWS Config托管规则。配置该规则使用AWS-EnableS3BucketEncryption AWS Systems Manager自动化运行手册作为修复操作。手动运行重新评估过程以确保现有S3存储桶合规。
- **分析：** 这是一个全面的解决方案。AWS Config可以监控合规性并自动修复不合规的存储桶。可以处理现有存储桶（通过重新评估）和新存储桶（通过持续监控和自动修复）。

**选项C：** 创建一个由Amazon EventBridge事件规则调用的AWS Lambda函数。定义规则，使用匹配新S3存储桶创建的事件模式。编程Lambda函数解析EventBridge事件，检查事件中S3存储桶的配置，并设置AES-256作为默认加密。
- **分析：** 这个方案可以处理新创建的存储桶，但无法处理现有未加密的存储桶。只解决了问题的一半。

**选项D：** 配置一个IAM策略，如果s3:x-amz-server-side-encryption条件键的值不是AES-256，则拒绝s3:CreateBucket操作。为所有公司的IAM用户创建一个IAM组，并将IAM策略与IAM组关联。
- **分析：** 这个方案只能阻止创建未加密的新存储桶，但无法处理现有未加密的存储桶，也无法自动为新存储桶设置加密。

 |  |  |  |
| 77 | A DevOps engineer is architecting a continuous development strategy for a company’s software as a service (SaaS) web application running
on AWS. For application and security reasons, users subscribing to this application are distributed across multiple Application Load Balancers
(ALBs), each of which has a dedicated Auto Scaling group and eet of Amazon EC2 instances. The application does not require a build stage,
and when it is committed to AWS CodeCommit, the application must trigger a simultaneous deployment to all ALBs, Auto Scaling groups, and
EC2 eets. | A. Create a single AWS CodePipeline pipeline that deploys the application in parallel using unique AWS CodeDeploy applications and
deployment groups created for each ALB-Auto Scaling group pair.
B. Create a single AWS CodePipeline pipeline that deploys the application using a single AWS CodeDeploy application and single
deployment group.
C. Create a single AWS CodePipeline pipeline that deploys the application in parallel using a single AWS CodeDeploy application and
unique deployment group for each ALB-Auto Scaling group pair.
D. Create an AWS CodePipeline pipeline for each ALB-Auto Scaling group pair that deploys the application using an AWS CodeDeploy
application and deployment group created for the same ALB-Auto Scaling group pair. |  |  |  |  |  |
| 78 | A company is hosting a static website from an Amazon S3 bucket. The website is available to customers at example.com. The company uses
an Amazon Route 53 weighted routing policy with a TTL of 1 day. The company has decided to replace the existing static website with a
dynamic web application. The dynamic web application uses an Application Load Balancer (ALB) in front of a eet of Amazon EC2 instances.
On the day of production launch to customers, the company creates an additional Route 53 weighted DNS record entry that points to the ALB
with a weight of 255 and a TTL of 1 hour. Two days later, a DevOps engineer notices that the previous static website is displayed sometimes
when customers navigate to example.com.
How can the DevOps engineer ensure that the company serves only dynamic content for example.com? | A. Delete all objects, including previous versions, from the S3 bucket that contains the static website content.
B. 
C. Congure webpage redirect requests on the S3 bucket with a hostname that redirects to the AL
D. Remove the weighted DNS record entry that points to the S3 bucket from the example.com hosted zone. Wait for DNS propagation to
become complete. | 一家公司正在从Amazon S3存储桶托管静态网站。该网站通过example.com向客户提供服务。公司使用Amazon Route 53加权路由策略，TTL为1天。公司决定用动态Web应用程序替换现有的静态网站。动态Web应用程序在一组Amazon EC2实例前使用应用负载均衡器(ALB)。在向客户正式发布的当天，公司创建了一个额外的Route 53加权DNS记录条目，指向ALB，权重为255，TTL为1小时。两天后，DevOps工程师注意到当客户访问example.com时，有时仍然显示之前的静态网站。

DevOps工程师如何确保公司只为example.com提供动态内容？

2. | A. 删除S3存储桶中包含静态网站内容的所有对象，包括以前的版本。
- 这个方案不能解决根本问题。问题在于DNS路由配置，而不是S3中的内容。即使删除S3内容，DNS仍然可能将流量路由到S3，只是会返回404错误而不是动态内容。

B. [选项B内容缺失]

C. 在S3存储桶上配置网页重定向请求，使用重定向到ALB的主机名。
- 这是一个临时解决方案，但不是最佳实践。虽然可以工作，但会增加额外的重定向跳转，影响性能，并且仍然依赖于DNS将流量路由到S3。

D. 从example.com托管区域中删除指向S3存储桶的加权DNS记录条目。等待DNS传播完成。
- 这是正确的解决方案。问题的根源是仍然存在指向S3的DNS记录，由于加权路由策略，流量被分配到两个目标。删除指向S3的记录后，所有流量都会路由到ALB。

3. | D |  |  |
| 79 | A company is implementing AWS CodePipeline to automate its testing process. The company wants to be notied when the execution state
fails and used the following custom event pattern in Amazon EventBridge: | A. Failed deploy and build actions across all the pipelines
B. All rejected or failed approval actions across all the pipelines
C. All the events across all pipelines
D. Approval actions across all the pipelines | 一家公司正在实施AWS CodePipeline来自动化其测试流程。该公司希望在执行状态失败时收到通知，并在Amazon EventBridge中使用了以下自定义事件模式：

 | **A. 所有管道中失败的部署和构建操作**
- 这个选项符合题目要求，专门针对失败状态的事件
- 涵盖了部署(deploy)和构建(build)两个关键阶段的失败情况
- 与"希望在执行状态失败时收到通知"的需求完全匹配

**B. 所有管道中被拒绝或失败的审批操作**
- 这个选项过于狭窄，只关注审批(approval)操作
- 虽然包含了失败状态，但遗漏了其他重要的失败场景
- 不能全面满足监控执行失败的需求

**C. 所有管道中的所有事件**
- 这个选项过于宽泛，会产生大量不必要的通知
- 包含成功、进行中、失败等所有状态的事件
- 不符合只在失败时通知的具体需求

**D. 所有管道中的审批操作**
- 这个选项只关注审批操作，范围太窄
- 没有特别针对失败状态，可能包含成功的审批
- 不符合失败通知的需求

 | A |  |  |
| 80 | An application running on a set of Amazon EC2 instances in an Auto Scaling group requires a conguration le to operate. The instances are
created and maintained with AWS CloudFormation. A DevOps engineer wants the instances to have the latest conguration le when
launched, and wants changes to the conguration le to be reected on all the instances with a minimal delay when the CloudFormation
template is updated. Company policy requires that application conguration les be maintained along with AWS infrastructure conguration
les in source control. | A. In the CloudFormation template, add an AWS Cong rule. Place the conguration le content in the rule’s InputParameters property, and
set the Scope property to the EC2 Auto Scaling group. Add an AWS Systems Manager Resource Data Sync resource to the template to poll
for updates to the conguration.
B. In the CloudFormation template, add an EC2 launch template resource. Place the conguration le content in the launch template.
Congure the cfn-init script to run when the instance is launched, and congure the cfn-hup script to poll for updates to the conguration.
C. In the CloudFormation template, add an EC2 launch template resource. Place the conguration le content in the launch template. Add
an AWS Systems Manager Resource Data Sync resource to the template to poll for updates to the conguration.
D. In the CloudFormation template, add CloudFormation init metadata. Place the conguration le content in the metadata. Congure the
cfn-init script to run when the instance is launched, and congure the cfn-hup script to poll for updates to the conguration. |  |  |  |  |  |
| 81 | A company manages an application that stores logs in Amazon CloudWatch Logs. The company wants to archive the logs to an Amazon S3
bucket. Logs are rarely accessed after 90 days and must be retained for 10 years. | A. Congure a CloudWatch Logs subscription lter to use AWS Glue to transfer all logs to an S3 bucket.
B. Congure a CloudWatch Logs subscription lter to use Amazon Kinesis Data Firehose to stream all logs to an S3 bucket.
C. Congure a CloudWatch Logs subscription lter to stream all logs to an S3 bucket.
D. Congure the S3 bucket lifecycle policy to transition logs to S3 Glacier after 90 days and to expire logs after 3.650 days.
E. Congure the S3 bucket lifecycle policy to transition logs to Reduced Redundancy after 90 days and to expire logs after 3.650 days. | 一家公司管理一个将日志存储在Amazon CloudWatch Logs中的应用程序。该公司希望将日志归档到Amazon S3存储桶中。日志在90天后很少被访问，但必须保留10年。

选项：
A. 配置CloudWatch Logs订阅过滤器，使用AWS Glue将所有日志传输到S3存储桶。
B. 配置CloudWatch Logs订阅过滤器，使用Amazon Kinesis Data Firehose将所有日志流式传输到S3存储桶。
C. 配置CloudWatch Logs订阅过滤器，将所有日志直接流式传输到S3存储桶。
D. 配置S3存储桶生命周期策略，在90天后将日志转换到S3 Glacier，并在3,650天后使日志过期。
E. 配置S3存储桶生命周期策略，在90天后将日志转换到Reduced Redundancy，并在3,650天后使日志过期。

 | **选项A：** AWS Glue主要用于ETL（提取、转换、加载）作业，不是CloudWatch Logs订阅过滤器的标准目标。虽然技术上可行，但不是最佳实践，且会增加不必要的复杂性和成本。

**选项B：** 这是正确的方法。CloudWatch Logs订阅过滤器可以直接与Kinesis Data Firehose集成，Firehose专门设计用于将流数据可靠地传输到S3。这是AWS推荐的标准做法。

**选项C：** CloudWatch Logs订阅过滤器不能直接流式传输到S3存储桶。必须通过中间服务（如Kinesis Data Firehose、Lambda函数等）来实现。

**选项D：** 这是正确的生命周期管理策略。S3 Glacier适合长期归档存储，成本低廉，符合"90天后很少访问"的要求。3,650天正好是10年（10×365=3,650天）。

**选项E：** Reduced Redundancy Storage (RRS)已被AWS弃用，不再推荐使用。而且RRS的成本比标准存储类只便宜一点点，不适合长期归档需求。

 |  |  |  |
| 82 | A company is developing a new application. The application uses AWS Lambda functions for its compute tier. The company must use a canary
deployment for any changes to the Lambda functions. Automated rollback must occur if any failures are reported.
The company’s DevOps team needs to create the infrastructure as code (IaC) and the CI/CD pipeline for this solution. | A. Create an AWS CloudFormation template for the application. Dene each Lambda function in the template by using the
AWS::Lambda::Function resource type. In the template, include a version for the Lambda function by using the AWS::Lambda::Version
resource type. Declare the CodeSha256 property. Congure an AWS::Lambda::Alias resource that references the latest version of the
Lambda function.
B. Create an AWS Serverless Application Model (AWS SAM) template for the application. Dene each Lambda function in the template by
using the AWS::Serverless::Function resource type. For each function, include congurations for the AutoPublishAlias property and the
DeploymentPreference property. Congure the deployment conguration type to LambdaCanary10Percent10Minutes.
C. Create an AWS CodeCommit repository. Create an AWS CodePipeline pipeline. Use the CodeCommit repository in a new source stage
that starts the pipeline. Create an AWS CodeBuild project to deploy the AWS Serverless Application Model (AWS SAM) template. Upload
the template and source code to the CodeCommit repository. In the CodeCommit repository, create a buildspec.yml le that includes the
commands to build and deploy the SAM application.
D. Create an AWS CodeCommit repository. Create an AWS CodePipeline pipeline. Use the CodeCommit repository in a new source stage
that starts the pipeline. Create an AWS CodeDeploy deployment group that is congured for canary deployments with a
DeploymentPreference type of Canary10Percent10Minutes. Upload the AWS CloudFormation template and source code to the
CodeCommit repository. In the CodeCommit repository, create an appspec.yml le that includes the commands to deploy the
CloudFormation template.
E. Create an Amazon CloudWatch composite alarm for all the Lambda functions. Congure an evaluation period and dimensions for
Lambda. Congure the alarm to enter the ALARM state if any errors are detected or if there is insucient data.
F. Create an Amazon CloudWatch alarm for each Lambda function. Congure the alarms to enter the ALARM state if any errors are
detected. Congure an evaluation period, dimensions for each Lambda function and version, and the namespace as AWS/Lambda on the
Errors metric. | 一家公司正在开发一个新应用程序。该应用程序使用AWS Lambda函数作为其计算层。公司必须对Lambda函数的任何更改使用金丝雀部署。如果报告任何故障，必须进行自动回滚。

公司的DevOps团队需要为此解决方案创建基础设施即代码(IaC)和CI/CD管道。

 | **选项A：** 使用CloudFormation模板定义Lambda函数，包含版本和别名资源。这提供了基本的版本控制，但没有内置的金丝雀部署功能，需要额外配置才能实现金丝雀部署和自动回滚。

**选项B：** 使用AWS SAM模板，配置AutoPublishAlias和DeploymentPreference属性，设置LambdaCanary10Percent10Minutes部署类型。SAM原生支持金丝雀部署，可以自动处理流量分配和回滚机制。

**选项C：** 创建完整的CI/CD管道，包括CodeCommit、CodePipeline和CodeBuild，使用SAM进行部署。这提供了完整的自动化部署流程，配合SAM的金丝雀部署功能。

**选项D：** 使用CodeDeploy进行金丝雀部署，但CodeDeploy主要用于EC2和本地服务器部署，对Lambda的支持有限，且使用appspec.yml部署CloudFormation模板不是标准做法。

**选项E：** 创建复合CloudWatch告警监控所有Lambda函数。虽然提供了监控功能，但复合告警可能不够精确，无法准确识别特定函数的问题。

**选项F：** 为每个Lambda函数创建独立的CloudWatch告警，监控错误指标。这提供了精确的监控和告警机制，是自动回滚的必要组件。

 |  |  |  |
| 83 | A DevOps engineer is deploying a new version of a company’s application in an AWS CodeDeploy deployment group associated with its
Amazon EC2 instances. After some time, the deployment fails. The engineer realizes that all the events associated with the specic
deployment ID are in a Skipped status, and code was not deployed in the instances associated with the deployment group. | A. The networking conguration does not allow the EC2 instances to reach the internet via a NAT gateway or internet gateway, and the
CodeDeploy endpoint cannot be reached.
B. The IAM user who triggered the application deployment does not have permission to interact with the CodeDeploy endpoint.
C. The target EC2 instances were not properly registered with the CodeDeploy endpoint.
D. An instance prole with proper permissions was not attached to the target EC2 instances.
E. The appspec.yml le was not included in the application revision. | 一名DevOps工程师正在使用AWS CodeDeploy部署组为公司应用程序部署新版本，该部署组与Amazon EC2实例相关联。一段时间后，部署失败了。工程师发现与特定部署ID相关的所有事件都处于"跳过"(Skipped)状态，代码没有部署到与部署组关联的实例上。

 | **A. 网络配置不允许EC2实例通过NAT网关或互联网网关访问互联网，无法访问CodeDeploy端点。**
- 如果网络连接有问题，通常会显示连接超时或网络错误，而不是"Skipped"状态
- 网络问题通常会产生更明确的错误信息

**B. 触发应用程序部署的IAM用户没有与CodeDeploy端点交互的权限。**
- 如果IAM用户权限不足，部署根本无法启动，会在初始阶段就失败
- 不会导致事件显示为"Skipped"状态

**C. 目标EC2实例没有正确注册到CodeDeploy端点。**
- 这种情况可能导致实例无法被识别，但通常会显示为实例不可用，而不是"Skipped"

**D. 没有为目标EC2实例附加具有适当权限的实例配置文件(instance profile)。**
- 这是最可能的原因。EC2实例需要适当的IAM角色和权限来与CodeDeploy服务通信
- 当实例缺少必要的权限时，CodeDeploy代理无法正常工作，导致部署事件被跳过
- "Skipped"状态通常表示实例无法参与部署过程，这与权限问题高度吻合

**E. 应用程序修订版本中没有包含appspec.yml文件。**
- 缺少appspec.yml文件通常会导致验证错误或部署失败，而不是"Skipped"状态
- 这种错误会在部署的早期阶段被检测到

 |  |  |  |
| 84 | A company has a guideline that every Amazon EC2 instance must be launched from an AMI that the company’s security team produces. Every
month, the security team sends an email message with the latest approved AMIs to all the development teams.
The development teams use AWS CloudFormation to deploy their applications. When developers launch a new service, they have to search
their email for the latest AMIs that the security department sent. A DevOps engineer wants to automate the process that the security team
uses to provide the AMI IDs to the development teams. | A. Direct the security team to use CloudFormation to create new versions of the AMIs and to list the AMI ARNs in an encrypted Amazon S3
object as part of the stack’s Outputs section. Instruct the developers to use a cross-stack reference to load the encrypted S3 object and
obtain the most recent AMI ARNs.
B. Direct the security team to use a CloudFormation stack to create an AWS CodePipeline pipeline that builds new AMIs and places the
latest AMI ARNs in an encrypted Amazon S3 object as part of the pipeline output. Instruct the developers to use a cross-stack reference
within their own CloudFormation template to obtain the S3 object location and the most recent AMI ARNs.
C. Direct the security team to use Amazon EC2 Image Builder to create new AMIs and to place the AMI ARNs as parameters in AWS
Systems Manager Parameter Store. Instruct the developers to specify a parameter of type SSM in their CloudFormation stack to obtain
the most recent AMI ARNs from Parameter Store.
D. Direct the security team to use Amazon EC2 Image Builder to create new AMIs and to create an Amazon Simple Notication Service
(Amazon SNS) topic so that every development team can receive notications. When the development teams receive a notication,
instruct them to write an AWS Lambda function that will update their CloudFormation stack with the most recent AMI ARNs. | 一家公司有一个准则，即每个Amazon EC2实例都必须从公司安全团队制作的AMI启动。每个月，安全团队会向所有开发团队发送一封包含最新批准AMI的电子邮件。

开发团队使用AWS CloudFormation来部署他们的应用程序。当开发人员启动新服务时，他们必须在邮件中搜索安全部门发送的最新AMI。一位DevOps工程师希望自动化安全团队向开发团队提供AMI ID的流程。

 | **选项A：** 指导安全团队使用CloudFormation创建新版本的AMI，并将AMI ARN列在加密的Amazon S3对象中作为堆栈输出部分的一部分。指导开发人员使用跨堆栈引用来加载加密的S3对象并获取最新的AMI ARN。
- **问题：** CloudFormation不是用来创建AMI的合适工具，它主要用于基础设施即代码。此外，跨堆栈引用通常用于CloudFormation输出，而不是S3对象。

**选项B：** 指导安全团队使用CloudFormation堆栈创建AWS CodePipeline管道，该管道构建新的AMI并将最新的AMI ARN放在加密的Amazon S3对象中作为管道输出。指导开发人员在自己的CloudFormation模板中使用跨堆栈引用来获取S3对象位置和最新的AMI ARN。
- **问题：** 虽然CodePipeline可以用于构建AMI，但使用S3对象存储AMI ARN并通过跨堆栈引用访问的方式过于复杂，不是最佳实践。

**选项C：** 指导安全团队使用Amazon EC2 Image Builder创建新的AMI，并将AMI ARN作为参数放在AWS Systems Manager Parameter Store中。指导开发人员在CloudFormation堆栈中指定SSM类型的参数，从Parameter Store获取最新的AMI ARN。
- **优点：** EC2 Image Builder是专门用于创建和管理AMI的服务。Parameter Store是存储配置数据的理想选择，CloudFormation原生支持SSM参数类型，可以动态获取最新值。这是一个完全自动化且符合最佳实践的解决方案。

**选项D：** 指导安全团队使用Amazon EC2 Image Builder创建新的AMI，并创建Amazon SNS主题，以便每个开发团队都能收到通知。当开发团队收到通知时，指导他们编写AWS Lambda函数来更新他们的CloudFormation堆栈。
- **问题：** 虽然使用了正确的AMI构建服务，但仍然需要手动干预（编写Lambda函数来更新堆栈），没有实现完全自动化。

 |  |  |  |
| 85 | An application runs on Amazon EC2 instances behind an Application Load Balancer (ALB). A DevOps engineer is using AWS CodeDeploy to
release a new version. The deployment fails during the AllowTrac lifecycle event, but a cause for the failure is not indicated in the
deployment logs. | A. The appspec.yml le contains an invalid script that runs in the AllowTrac lifecycle hook.
B. 
C. The health checks specied for the ALB target group are miscongured.
D. The CodeDeploy agent was not installed in the EC2 instances that are part of the ALB target group. | **
一个应用程序运行在应用负载均衡器(ALB)后面的Amazon EC2实例上。DevOps工程师正在使用AWS CodeDeploy发布新版本。部署在AllowTraffic生命周期事件期间失败，但部署日志中没有显示失败的原因。

2. ** | **

**A. appspec.yml文件包含在AllowTraffic生命周期钩子中运行的无效脚本。**
- 如果appspec.yml中的脚本有问题，通常会在部署日志中显示脚本执行错误
- 题目明确提到"部署日志中没有显示失败的原因"，这与脚本错误的典型表现不符
- 脚本错误通常会有明确的错误信息和堆栈跟踪

**B. [选项内容缺失]**
- 无法分析此选项

**C. 为ALB目标组指定的健康检查配置错误。**
- 在CodeDeploy的蓝绿部署中，AllowTraffic阶段是将流量从旧版本切换到新版本的关键步骤
- 如果ALB的健康检查配置不正确（如健康检查路径错误、超时设置不当、健康阈值设置错误等），新部署的实例可能无法通过健康检查
- 当实例无法通过ALB健康检查时，CodeDeploy会认为部署失败，但这种失败可能不会在CodeDeploy的部署日志中显示详细原因
- 这种情况下，问题实际出现在ALB层面，而不是CodeDeploy应用层面

**D. CodeDeploy代理没有安装在作为ALB目标组一部分的EC2实例上。**
- 如果CodeDeploy代理没有安装，部署会在更早的阶段失败（如DownloadBundle或Install阶段）
- 不会到达AllowTraffic阶段
- 这种错误通常会在部署日志中明确显示

3. ** | C |  |  |
| 86 | A company has 20 service teams. Each service team is responsible for its own microservice. Each service team uses a separate AWS account
for its microservice and a VPC with the 192.168.0.0/22 CIDR block. The company manages the AWS accounts with AWS Organizations.
Each service team hosts its microservice on multiple Amazon EC2 instances behind an Application Load Balancer. The microservices
communicate with each other across the public internet. The company’s security team has issued a new guideline that all communication
between microservices must use HTTPS over private network connections and cannot traverse the public internet.
A DevOps engineer must implement a solution that fullls these obligations and minimizes the number of changes for each service team. | A. Create a new AWS account in AWS Organizations. Create a VPC in this account, and use AWS Resource Access Manager to share the
private subnets of this VPC with the organization. Instruct the service teams to launch a new Network Load Balancer (NLB) and EC2
instances that use the shared private subnets. Use the NLB DNS names for communication between microservices.
B. Create a Network Load Balancer (NLB) in each of the microservice VPCs. Use AWS PrivateLink to create VPC endpoints in each AWS
account for the NLBs. Create subscriptions to each VPC endpoint in each of the other AWS accounts. Use the VPC endpoint DNS names
for communication between microservices.
C. Create a Network Load Balancer (NLB) in each of the microservice VPCs. Create VPC peering connections between each of the
microservice VPCs. Update the route tables for each VPC to use the peering links. Use the NLB DNS names for communication between
microservices.
D. Create a new AWS account in AWS Organizations. Create a transit gateway in this account, and use AWS Resource Access Manager to
share the transit gateway with the organization. In each of the microservice VPCs, create a transit gateway attachment to the shared
transit gateway. Update the route tables of each VPC to use the transit gateway. Create a Network Load Balancer (NLB) in each of the
microservice VPCs. Use the NLB DNS names for communication between microservices. | 一家公司有20个服务团队。每个服务团队负责自己的微服务。每个服务团队为其微服务使用单独的AWS账户和一个CIDR块为192.168.0.0/22的VPC。公司使用AWS Organizations管理这些AWS账户。

每个服务团队在应用负载均衡器后面的多个Amazon EC2实例上托管其微服务。微服务之间通过公共互联网相互通信。公司的安全团队发布了新的指导原则，要求所有微服务之间的通信必须在私有网络连接上使用HTTPS，不能通过公共互联网传输。

DevOps工程师必须实施一个满足这些要求并最小化每个服务团队更改数量的解决方案。

 | **选项A：** 
- 创建新的AWS账户，在其中创建VPC，使用AWS Resource Access Manager共享私有子网
- 问题：要求服务团队启动新的NLB和EC2实例到共享子网中，这意味着需要重新部署所有微服务，变更量很大
- 不符合"最小化更改"的要求

**选项B：**
- 在每个微服务VPC中创建NLB，使用AWS PrivateLink创建VPC端点
- 为每个NLB创建VPC端点，在其他账户中创建订阅
- 优点：通过PrivateLink实现私有连接，无需重新部署现有服务，只需添加NLB
- 符合私有网络通信要求，变更最小

**选项C：**
- 在每个VPC中创建NLB，创建VPC对等连接
- 问题：20个VPC需要创建190个对等连接（n*(n-1)/2），管理复杂度极高
- 路由表更新工作量巨大，不现实

**选项D：**
- 创建新账户，部署Transit Gateway并共享
- 每个VPC创建Transit Gateway附件，更新路由表
- 虽然技术可行，但需要大量的网络配置更改，复杂度较高

 | B |  |  |
| 87 | An Amazon EC2 instance is running in a VPC and needs to download an object from a restricted Amazon S3 bucket. When the DevOps
engineer tries to download the object, an AccessDenied error is received. | A. The S3 bucket default encryption is enabled.
B. There is an error in the S3 bucket policy.
C. The object has been moved to S3 Glacier.
D. There is an error in the IAM role conguration.
E. S3 Versioning is enabled. |  |  |  |  |  |
| 88 | A company wants to use a grid system for a proprietary enterprise in-memory data store on top of AWS. This system can run in multiple server
nodes in any Linux-based distribution. The system must be able to recongure the entire cluster every time a node is added or removed.
When adding or removing nodes, an /etc/cluster/nodes.cong le must be updated, listing the IP addresses of the current node members of
that cluster.
The company wants to automate the task of adding new nodes to a cluster. | A. Use AWS OpsWorks Stacks to layer the server nodes of that cluster. Create a Chef recipe that populates the content of the
/etc/cluster/nodes.cong le and restarts the service by using the current members of the layer. Assign that recipe to the Congure
lifecycle event.
B. Put the le nodes.cong in version control. Create an AWS CodeDeploy deployment conguration and deployment group based on an
Amazon EC2 tag value for the cluster nodes. When adding a new node to the cluster, update the le with all tagged instances, and make a
commit in version control. Deploy the new le and restart the services.
C. Create an Amazon S3 bucket and upload a version of the /etc/cluster/nodes.cong le. Create a crontab script that will poll for that S3
le and download it frequently. Use a process manager, such as Monit or systemd, to restart the cluster services when it detects that the
new le was modied. When adding a node to the cluster, edit the le’s most recent members. Upload the new le to the S3 bucket.
D. Create a user data script that lists all members of the current security group of the cluster and automatically updates the
/etc/cluster/nodes.cong le whenever a new instance is added to the cluster. | 一家公司希望在AWS上为专有企业内存数据存储使用网格系统。该系统可以在任何基于Linux发行版的多个服务器节点上运行。系统必须能够在每次添加或删除节点时重新配置整个集群。

当添加或删除节点时，必须更新/etc/cluster/nodes.config文件，列出该集群当前节点成员的IP地址。

公司希望自动化向集群添加新节点的任务。

 | **选项A：使用AWS OpsWorks Stacks对集群的服务器节点进行分层。创建一个Chef配方，使用当前层成员填充/etc/cluster/nodes.config文件的内容并重启服务。将该配方分配给Configure生命周期事件。**
- ✅ 优点：OpsWorks Stacks专门设计用于管理应用程序栈和层
- ✅ Configure生命周期事件会在节点添加/删除时自动触发
- ✅ Chef配方可以动态获取当前层的所有成员信息
- ✅ 完全自动化，无需手动干预

**选项B：将nodes.config文件放入版本控制。基于集群节点的Amazon EC2标签值创建AWS CodeDeploy部署配置和部署组。向集群添加新节点时，使用所有标记的实例更新文件，并在版本控制中提交。部署新文件并重启服务。**
- ❌ 需要手动更新文件和提交版本控制
- ❌ 不是完全自动化的解决方案
- ❌ 每次添加节点都需要人工干预

**选项C：创建Amazon S3存储桶并上传/etc/cluster/nodes.config文件的版本。创建crontab脚本定期轮询该S3文件并下载。使用进程管理器（如Monit或systemd）在检测到新文件被修改时重启集群服务。向集群添加节点时，编辑文件的最新成员，将新文件上传到S3存储桶。**
- ❌ 需要手动编辑和上传文件
- ❌ 依赖轮询机制，可能有延迟
- ❌ 不是实时响应的解决方案
- ❌ 需要人工干预

**选项D：创建用户数据脚本，列出集群当前安全组的所有成员，并在新实例添加到集群时自动更新/etc/cluster/nodes.config文件。**
- ❌ 用户数据脚本只在实例启动时执行一次
- ❌ 无法在其他节点添加时动态更新现有节点的配置
- ❌ 不能实现集群范围的配置同步

 | A |  |  |
| 89 | A DevOps engineer is working on a data archival project that requires the migration of on-premises data to an Amazon S3 bucket. The DevOps
engineer develops a script that incrementally archives on-premises data that is older than 1 month to Amazon S3. Data that is transferred to
Amazon S3 is deleted from the on-premises location. The script uses the S3 PutObject operation.
During a code review, the DevOps engineer notices that the script does not verify whether the data was successfully copied to Amazon S3. The
DevOps engineer must update the script to ensure that data is not corrupted during transmission. The script must use MD5 checksums to
verify data integrity before the on-premises data is deleted. | A. Check the returned response for the VersionId. Compare the returned VersionId against the MD5 checksum.
B. Include the MD5 checksum within the Content-MD5 parameter. Check the operation call’s return status to nd out if an error was
returned.
C. Include the checksum digest within the tagging parameter as a URL query parameter.
D. Check the returned response for the ETag. Compare the returned ETag against the MD5 checksum.
E. Include the checksum digest within the Metadata parameter as a name-value pair. After upload, use the S3 HeadObject operation to
retrieve metadata from the object. |  |  |  |  |  |
| 90 | A company deploys updates to its Amazon API Gateway API several times a week by using an AWS CodePipeline pipeline. As part of the
update process, the company exports the JavaScript SDK for the API from the API Gateway console and uploads the SDK to an Amazon S3
bucket.
The company has congured an Amazon CloudFront distribution that uses the S3 bucket as an origin. Web clients then download the SDK by
using the CloudFront distribution’s endpoint. A DevOps engineer needs to implement a solution to make the new SDK available automatically
during new API deployments. | A. Create a CodePipeline action immediately after the deployment stage of the API. Congure the action to invoke an AWS Lambda
function. Congure the Lambda function to download the SDK from API Gateway, upload the SDK to the S3 bucket, and create a
CloudFront invalidation for the SDK path.
B. Create a CodePipeline action immediately after the deployment stage of the API. Congure the action to use the CodePipeline
integration with API Gateway to export the SDK to Amazon S3. Create another action that uses the CodePipeline integration with Amazon
S3 to invalidate the cache for the SDK path.
C. Create an Amazon EventBridge rule that reacts to UpdateStage events from aws.apigateway. Congure the rule to invoke an AWS
Lambda function to download the SDK from API Gateway, upload the SDK to the S3 bucket, and call the CloudFront API to create an
invalidation for the SDK path.
D. Create an Amazon EventBridge rule that reacts to CreateDeployment events from aws.apigateway. Congure the rule to invoke an AWS
Lambda function to download the SDK from API Gateway, upload the SDK to the S3 bucket, and call the S3 API to invalidate the cache for
the SDK path. | 一家公司每周多次使用AWS CodePipeline管道向其Amazon API Gateway API部署更新。作为更新过程的一部分，公司从API Gateway控制台导出API的JavaScript SDK，并将SDK上传到Amazon S3存储桶。

公司已配置了一个Amazon CloudFront分发，该分发使用S3存储桶作为源。然后Web客户端通过CloudFront分发的端点下载SDK。DevOps工程师需要实现一个解决方案，在新的API部署期间自动使新的SDK可用。

 | **选项A：** 在API部署阶段之后立即创建一个CodePipeline操作。配置该操作调用AWS Lambda函数。配置Lambda函数从API Gateway下载SDK，将SDK上传到S3存储桶，并为SDK路径创建CloudFront失效。
- ✅ 正确的流程：在部署后立即执行
- ✅ 使用Lambda自动化整个过程
- ✅ 正确调用CloudFront失效API
- ✅ 与现有CodePipeline集成良好

**选项B：** 在API部署阶段之后立即创建一个CodePipeline操作。配置该操作使用CodePipeline与API Gateway的集成将SDK导出到Amazon S3。创建另一个操作，使用CodePipeline与Amazon S3的集成使SDK路径的缓存失效。
- ❌ CodePipeline没有直接的API Gateway SDK导出集成
- ❌ CodePipeline没有直接的S3缓存失效集成
- ❌ 这些集成功能实际上不存在

**选项C：** 创建一个Amazon EventBridge规则，响应来自aws.apigateway的UpdateStage事件。配置规则调用AWS Lambda函数从API Gateway下载SDK，将SDK上传到S3存储桶，并调用CloudFront API为SDK路径创建失效。
- ✅ 使用事件驱动架构
- ✅ 正确的Lambda函数逻辑
- ✅ 正确调用CloudFront API
- ⚠️ UpdateStage事件可能不是最准确的触发器，因为部署和阶段更新是不同的概念

**选项D：** 创建一个Amazon EventBridge规则，响应来自aws.apigateway的CreateDeployment事件。配置规则调用AWS Lambda函数从API Gateway下载SDK，将SDK上传到S3存储桶，并调用S3 API使SDK路径的缓存失效。
- ✅ 使用事件驱动架构
- ✅ CreateDeployment是更准确的触发事件
- ✅ 正确的Lambda函数逻辑
- ❌ S3 API无法使CloudFront缓存失效，应该调用CloudFront API

 | A |  |  |
| 91 | A company has developed an AWS Lambda function that handles orders received through an API. The company is using AWS CodeDeploy to
deploy the Lambda function as the nal stage of a CI/CD pipeline.
A DevOps engineer has noticed there are intermittent failures of the ordering API for a few seconds after deployment. After some
investigation, the DevOps engineer believes the failures are due to database changes not having fully propagated before the Lambda function
is invoked.
How should the DevOps engineer overcome this? | A. Add a BeforeAllowTrac hook to the AppSpec le that tests and waits for any necessary database changes before trac can ow to the
new version of the Lambda function.
B. Add an AfterAllowTrac hook to the AppSpec le that forces trac to wait for any pending database changes before allowing the new
version of the Lambda function to respond.
C. Add a BeforeInstall hook to the AppSpec le that tests and waits for any necessary database changes before deploying the new version
of the Lambda function.
D. Add a ValidateService hook to the AppSpec le that inspects incoming trac and rejects the payload if dependent services, such as the
database, are not yet ready. | 一家公司开发了一个AWS Lambda函数来处理通过API接收的订单。该公司正在使用AWS CodeDeploy来部署Lambda函数，作为CI/CD流水线的最终阶段。

一名DevOps工程师注意到在部署后的几秒钟内，订单API会出现间歇性故障。经过一些调查，DevOps工程师认为故障是由于在Lambda函数被调用之前，数据库更改尚未完全传播导致的。

DevOps工程师应该如何解决这个问题？

 | **A. 在AppSpec文件中添加BeforeAllowTraffic钩子，在流量流向Lambda函数新版本之前测试并等待任何必要的数据库更改。**
- 这是正确的方法。BeforeAllowTraffic钩子在新版本部署完成后、但在流量切换到新版本之前执行
- 可以在此钩子中添加数据库就绪检查，确保数据库更改已完全传播
- 这样可以防止新版本在依赖服务未就绪时接收流量

**B. 在AppSpec文件中添加AfterAllowTraffic钩子，强制流量等待任何待处理的数据库更改，然后允许Lambda函数新版本响应。**
- 不正确。AfterAllowTraffic钩子在流量已经切换到新版本之后执行
- 此时流量已经开始流向新版本，无法阻止故障的发生
- 时机太晚，无法解决问题

**C. 在AppSpec文件中添加BeforeInstall钩子，在部署Lambda函数新版本之前测试并等待任何必要的数据库更改。**
- 不正确。BeforeInstall钩子在安装新版本之前执行
- 此时数据库更改可能还没有开始，检查时机过早
- Lambda部署和数据库更改可能是并行进行的

**D. 在AppSpec文件中添加ValidateService钩子，检查传入流量并在依赖服务（如数据库）尚未就绪时拒绝负载。**
- 不正确。ValidateService钩子主要用于验证部署是否成功
- 这种方法会导致请求被拒绝，而不是等待依赖服务就绪
- 不是解决根本问题的最佳方案

 |  |  |  |
| 92 | A company uses a single AWS account to test applications on Amazon EC2 instances. The company has turned on AWS Cong in the AWS
account and has activated the restricted-ssh AWS Cong managed rule.
The company needs an automated monitoring solution that will provide a customized notication in real time if any security group in the
account is not compliant with the restricted-ssh rule. The customized notication must contain the name and ID of the noncompliant security
group.
A DevOps engineer creates an Amazon Simple Notication Service (Amazon SNS) topic in the account and subscribes the appropriate
personnel to the topic. | A. Create an Amazon EventBridge rule that matches an AWS Cong evaluation result of NON_COMPLIANT for the restricted-ssh rule.
Congure an input transformer for the EventBridge rule. Congure the EventBridge rule to publish a notication to the SNS topic.
B. Congure AWS Cong to send all evaluation results for the restricted-ssh rule to the SNS topic. Congure a lter policy on the SNS topic
to send only notications that contain the text of NON_COMPLIANT in the notication to subscribers.
C. Create an Amazon EventBridge rule that matches an AWS Cong evaluation result of NON_COMPLIANT for the restricted-ssh rule.
Congure the EventBridge rule to invoke AWS Systems Manager Run Command on the SNS topic to customize a notication and to publish
the notication to the SNS topic.
D. Create an Amazon EventBridge rule that matches all AWS Cong evaluation results of NON_COMPLIANT. Congure an input transformer
for the restricted-ssh rule. Congure the EventBridge rule to publish a notication to the SNS topic. | 一家公司使用单个AWS账户在Amazon EC2实例上测试应用程序。该公司已在AWS账户中启用了AWS Config，并激活了restricted-ssh AWS Config托管规则。

该公司需要一个自动化监控解决方案，当账户中任何安全组不符合restricted-ssh规则时，能够实时提供自定义通知。自定义通知必须包含不合规安全组的名称和ID。

一名DevOps工程师在账户中创建了Amazon Simple Notification Service (Amazon SNS)主题，并让相关人员订阅了该主题。

 | **选项A：** 创建Amazon EventBridge规则，匹配restricted-ssh规则的NON_COMPLIANT AWS Config评估结果。为EventBridge规则配置输入转换器。配置EventBridge规则向SNS主题发布通知。
- ✅ **正确**：这是最佳解决方案
- EventBridge可以精确匹配特定Config规则的NON_COMPLIANT事件
- 输入转换器可以自定义通知内容，包含安全组名称和ID
- 直接向SNS发布通知，架构简洁高效

**选项B：** 配置AWS Config将restricted-ssh规则的所有评估结果发送到SNS主题。在SNS主题上配置过滤策略，仅向订阅者发送包含NON_COMPLIANT文本的通知。
- ❌ **不正确**：虽然技术上可行，但不是最优解决方案
- 会发送所有评估结果（包括COMPLIANT），增加不必要的流量
- SNS过滤策略的自定义能力有限，难以提取安全组名称和ID
- 缺乏灵活的消息格式化能力

**选项C：** 创建Amazon EventBridge规则，匹配restricted-ssh规则的NON_COMPLIANT AWS Config评估结果。配置EventBridge规则调用AWS Systems Manager Run Command在SNS主题上自定义通知并发布到SNS主题。
- ❌ **不正确**：架构过于复杂且不合理
- Systems Manager Run Command用于在EC2实例上执行命令，不适用于SNS通知自定义
- 增加了不必要的复杂性和潜在故障点
- Run Command无法直接操作SNS主题

**选项D：** 创建Amazon EventBridge规则，匹配所有NON_COMPLIANT的AWS Config评估结果。为restricted-ssh规则配置输入转换器。配置EventBridge规则向SNS主题发布通知。
- ❌ **不正确**：规则范围过于宽泛
- 会匹配所有Config规则的NON_COMPLIANT结果，不仅仅是restricted-ssh
- 可能产生大量不相关的通知
- 输入转换器配置描述不清晰且逻辑有误

 | A |  |  |
| 93 | A company requires an RPO of 2 hours and an RTO of 10 minutes for its data and application at all times. An application uses a MySQL
database and Amazon EC2 web servers. The development team needs a strategy for failover and disaster recovery. | A. Create an Amazon Aurora cluster in one Availability Zone across multiple Regions as the data store. Use Aurora’s automatic recovery
capabilities in the event of a disaster.
B. Create an Amazon Aurora global database in two Regions as the data store. In the event of a failure, promote the secondary Region as
the primary for the application.
C. Create an Amazon Aurora multi-master cluster across multiple Regions as the data store. Use a Network Load Balancer to balance the
database trac in different Regions.
D. Set up the application in two Regions and use Amazon Route 53 failover-based routing that points to the Application Load Balancers in
both Regions. Use health checks to determine the availability in a given Region. Use Auto Scaling groups in each Region to adjust capacity
based on demand.
E. Set up the application in two Regions and use a multi-Region Auto Scaling group behind Application Load Balancers to manage the
capacity based on demand. In the event of a disaster, adjust the Auto Scaling group’s desired instance count to increase baseline capacity
in the failover Region. | 一家公司要求其数据和应用程序在任何时候都要满足RPO（恢复点目标）为2小时，RTO（恢复时间目标）为10分钟的要求。应用程序使用MySQL数据库和Amazon EC2 Web服务器。开发团队需要一个故障转移和灾难恢复策略。

 | **选项A：** 在多个区域的一个可用区中创建Amazon Aurora集群作为数据存储。在发生灾难时使用Aurora的自动恢复功能。
- **错误**：描述不准确，Aurora集群不能同时在一个可用区和多个区域中。此外，单区域部署无法满足灾难恢复要求，因为整个区域故障时无法恢复。

**选项B：** 在两个区域创建Amazon Aurora全球数据库作为数据存储。在发生故障时，将辅助区域提升为应用程序的主区域。
- **部分正确**：Aurora全球数据库可以满足RPO要求（通常<1秒的跨区域复制延迟），提升辅助区域可以满足RTO要求。但这个选项只涉及数据库层面，没有涉及应用程序层的故障转移。

**选项C：** 在多个区域创建Amazon Aurora多主集群作为数据存储。使用网络负载均衡器来平衡不同区域的数据库流量。
- **错误**：Aurora多主集群目前只支持单区域内的多个可用区，不支持跨区域部署。此外，直接对数据库进行负载均衡不是最佳实践。

**选项D：** 在两个区域设置应用程序，使用Amazon Route 53基于故障转移的路由指向两个区域的应用程序负载均衡器。使用健康检查来确定给定区域的可用性。在每个区域使用Auto Scaling组根据需求调整容量。
- **正确**：这是一个完整的灾难恢复解决方案，涵盖了应用程序层和数据库层。Route 53故障转移路由可以快速切换流量，满足RTO要求。

**选项E：** 在两个区域设置应用程序，在应用程序负载均衡器后使用多区域Auto Scaling组来根据需求管理容量。在发生灾难时，调整Auto Scaling组的期望实例数量以增加故障转移区域的基线容量。
- **错误**：Auto Scaling组不能跨区域工作，每个区域需要独立的Auto Scaling组。此外，手动调整容量无法满足10分钟的RTO要求。

 |  |  |  |
| 94 | A business has an application that consists of ve independent AWS Lambda functions.
The DevOps engineer has built a CI/CD pipeline using AWS CodePipeline and AWS CodeBuild that builds, tests, packages, and deploys each
Lambda function in sequence. The pipeline uses an Amazon EventBridge rule to ensure the pipeline starts as quickly as possible after a
change is made to the application source code.
After working with the pipeline for a few months, the DevOps engineer has noticed the pipeline takes too long to complete. | A. Modify the CodeBuild projects within the pipeline to use a compute type with more available network throughput.
B. Create a custom CodeBuild execution environment that includes a symmetric multiprocessing conguration to run the builds in parallel.
C. Modify the CodePipeline conguration to run actions for each Lambda function in parallel by specifying the same runOrder.
D. Modify each CodeBuild project to run within a VPC and use dedicated instances to increase throughput. |  |  |  |  |  |
| 95 | A company uses AWS CloudFormation stacks to deploy updates to its application. The stacks consist of different resources. The resources
include AWS Auto Scaling groups, Amazon EC2 instances, Application Load Balancers (ALBs), and other resources that are necessary to
launch and maintain independent stacks. Changes to application resources outside of CloudFormation stack updates are not allowed.
The company recently attempted to update the application stack by using the AWS CLI. The stack failed to update and produced the following
error message: “ERROR: both the deployment and the CloudFormation stack rollback failed. The deployment failed because the following
resource(s) failed to update: [AutoScalingGroup].”
The stack remains in a status of UPDATE_ROLLBACK_FAILE | D. Delete the Auto Scaling group resource. Run the aws cloudformation rollback-stack AWS CLI command.
A. Update the subnet mappings that are congured for the ALBs. Run the aws cloudformation update-stack-set AWS CLI command.
B. Update the IAM role by providing the necessary permissions to update the stack. Run the aws cloudformation continue-update-rollback
AWS CLI command.
C. Submit a request for a quota increase for the number of EC2 instances for the account. Run the aws cloudformation cancel-update-
stack AWS CLI command. | 一家公司使用AWS CloudFormation堆栈来部署应用程序更新。这些堆栈由不同的资源组成，包括AWS Auto Scaling组、Amazon EC2实例、应用程序负载均衡器(ALB)以及启动和维护独立堆栈所需的其他资源。不允许在CloudFormation堆栈更新之外对应用程序资源进行更改。

该公司最近尝试使用AWS CLI更新应用程序堆栈。堆栈更新失败并产生以下错误消息："ERROR: both the deployment and the CloudFormation stack rollback failed. The deployment failed because the following resource(s) failed to update: [AutoScalingGroup]."

堆栈保持在UPDATE_ROLLBACK_FAILED状态。

# | **选项A：** 更新为ALB配置的子网映射。运行aws cloudformation update-stack-set AWS CLI命令。
- 错误：update-stack-set用于管理StackSets，不适用于单个堆栈的回滚失败问题
- 子网映射问题与Auto Scaling组更新失败没有直接关系
- 不能解决UPDATE_ROLLBACK_FAILED状态

**选项B：** 通过提供必要的权限来更新IAM角色以更新堆栈。运行aws cloudformation continue-update-rollback AWS CLI命令。
- 正确：continue-update-rollback是专门用于处理UPDATE_ROLLBACK_FAILED状态的命令
- IAM权限不足是导致回滚失败的常见原因
- 这个命令可以继续完成失败的回滚操作

**选项C：** 提交增加账户EC2实例数量配额的请求。运行aws cloudformation cancel-update-stack AWS CLI命令。
- 错误：cancel-update-stack用于取消正在进行的更新，不适用于已经失败的回滚
- 配额问题可能是原因之一，但cancel-update-stack不能解决UPDATE_ROLLBACK_FAILED状态

**选项D：** 删除Auto Scaling组资源。运行aws cloudformation rollback-stack AWS CLI命令。
- 错误：手动删除资源违反了题目中"不允许在CloudFormation堆栈更新之外对应用程序资源进行更改"的要求
- rollback-stack不是有效的AWS CLI命令

# |  |  |  |
| 96 | A company is deploying a new application that uses Amazon EC2 instances. The company needs a solution to query application logs and AWS
account API activity. | A. Use the Amazon CloudWatch agent to send logs from the EC2 instances to Amazon CloudWatch Logs. Congure AWS CloudTrail to
deliver the API logs to Amazon S3. Use CloudWatch to query both sets of logs.
B. Use the Amazon CloudWatch agent to send logs from the EC2 instances to Amazon CloudWatch Logs. Congure AWS CloudTrail to
deliver the API logs to CloudWatch Logs. Use CloudWatch Logs Insights to query both sets of logs.
C. Use the Amazon CloudWatch agent to send logs from the EC2 instances to Amazon Kinesis. Congure AWS CloudTrail to deliver the API
logs to Kinesis. Use Kinesis to load the data into Amazon Redshift. Use Amazon Redshift to query both sets of logs.
D. Use the Amazon CloudWatch agent to send logs from the EC2 instances to Amazon S3. Use AWS CloudTrail to deliver the API logs to
Amazon S3. Use Amazon Athena to query both sets of logs in Amazon S3. | 一家公司正在部署一个使用Amazon EC2实例的新应用程序。该公司需要一个解决方案来查询应用程序日志和AWS账户API活动。

 | **选项A：** 使用Amazon CloudWatch代理将EC2实例的日志发送到Amazon CloudWatch Logs。配置AWS CloudTrail将API日志传送到Amazon S3。使用CloudWatch查询两组日志。
- **问题：** CloudWatch本身不能直接查询存储在S3中的CloudTrail日志。CloudWatch主要用于监控指标，而不是查询S3中的日志文件。

**选项B：** 使用Amazon CloudWatch代理将EC2实例的日志发送到Amazon CloudWatch Logs。配置AWS CloudTrail将API日志传送到CloudWatch Logs。使用CloudWatch Logs Insights查询两组日志。
- **优势：** 
  - CloudWatch代理正确用于收集EC2日志
  - CloudTrail可以配置将日志发送到CloudWatch Logs
  - CloudWatch Logs Insights是专门用于查询和分析CloudWatch Logs的强大工具
  - 两组日志都在同一服务中，便于统一查询和关联分析

**选项C：** 使用Amazon CloudWatch代理将EC2实例的日志发送到Amazon Kinesis。配置AWS CloudTrail将API日志传送到Kinesis。使用Kinesis将数据加载到Amazon Redshift。使用Amazon Redshift查询两组日志。
- **问题：** 
  - CloudWatch代理不能直接发送日志到Kinesis
  - 架构过于复杂，增加了不必要的成本和维护复杂性
  - Redshift更适合大规模数据仓库场景，对于日志查询来说过于重量级

**选项D：** 使用Amazon CloudWatch代理将EC2实例的日志发送到Amazon S3。使用AWS CloudTrail将API日志传送到Amazon S3。使用Amazon Athena查询S3中的两组日志。
- **问题：** CloudWatch代理的主要目的是将日志发送到CloudWatch Logs，而不是直接发送到S3。虽然可以通过其他方式实现，但这不是标准配置。

 |  |  |  |
| 97 | A company wants to ensure that their EC2 instances are secure. They want to be notied if any new vulnerabilities are discovered on their
instances, and they also want an audit trail of all login activities on the instances. | A. Use AWS Systems Manager to detect vulnerabilities on the EC2 instances. Install the Amazon Kinesis Agent to capture system logs and
deliver them to Amazon S3.
B. Use AWS Systems Manager to detect vulnerabilities on the EC2 instances. Install the Systems Manager Agent to capture system logs
and view login activity in the CloudTrail console.
C. Congure Amazon CloudWatch to detect vulnerabilities on the EC2 instances. Install the AWS Cong daemon to capture system logs
and view them in the AWS Cong console.
D. Congure Amazon Inspector to detect vulnerabilities on the EC2 instances. Install the Amazon CloudWatch Agent to capture system
logs and record them via Amazon CloudWatch Logs. | 一家公司希望确保他们的EC2实例是安全的。他们希望在实例上发现任何新漏洞时收到通知，同时还希望获得实例上所有登录活动的审计跟踪。

# | **选项A：使用AWS Systems Manager检测EC2实例上的漏洞。安装Amazon Kinesis Agent来捕获系统日志并将其传送到Amazon S3。**
- ❌ **错误**：AWS Systems Manager本身不是专门用于漏洞检测的服务，它主要用于系统管理和配置
- ✅ **部分正确**：Kinesis Agent可以捕获日志并传送到S3，但这不是最直接的解决方案

**选项B：使用AWS Systems Manager检测EC2实例上的漏洞。安装Systems Manager Agent来捕获系统日志并在CloudTrail控制台中查看登录活动。**
- ❌ **错误**：AWS Systems Manager不是漏洞检测服务
- ❌ **错误**：CloudTrail主要记录AWS API调用，不记录EC2实例内部的登录活动
- ❌ **错误**：Systems Manager Agent不是专门用于日志捕获的

**选项C：配置Amazon CloudWatch检测EC2实例上的漏洞。安装AWS Config守护进程来捕获系统日志并在AWS Config控制台中查看。**
- ❌ **错误**：CloudWatch是监控服务，不是漏洞检测服务
- ❌ **错误**：AWS Config用于配置合规性检查，不是用于捕获系统日志的
- ❌ **错误**：AWS Config不适合查看登录活动日志

**选项D：配置Amazon Inspector检测EC2实例上的漏洞。安装Amazon CloudWatch Agent来捕获系统日志并通过Amazon CloudWatch Logs记录。**
- ✅ **正确**：Amazon Inspector是AWS专门的漏洞评估服务，可以检测EC2实例和容器镜像中的软件漏洞
- ✅ **正确**：CloudWatch Agent可以收集系统日志、应用程序日志和自定义指标
- ✅ **正确**：CloudWatch Logs可以存储和监控日志数据，包括登录活动

# |  |  |  |
| 98 | A company is running an application on Amazon EC2 instances in an Auto Scaling group. Recently, an issue occurred that prevented EC2
instances from launching successfully, and it took several hours for the support team to discover the issue. The support team wants to be
notied by email whenever an EC2 instance does not start successfully. | A. Add a health check to the Auto Scaling group to invoke an AWS Lambda function whenever an instance status is impaired.
B. Congure the Auto Scaling group to send a notication to an Amazon SNS topic whenever a failed instance launch occurs.
C. Create an Amazon CloudWatch alarm that invokes an AWS Lambda function when a failed AttachInstances Auto Scaling API call is
made.
D. Create a status check alarm on Amazon EC2 to send a notication to an Amazon SNS topic whenever a status check fail occurs. | 一家公司在Auto Scaling组中的Amazon EC2实例上运行应用程序。最近发生了一个问题，导致EC2实例无法成功启动，支持团队花了几个小时才发现这个问题。支持团队希望在EC2实例启动失败时能够通过电子邮件收到通知。

 | **选项A：向Auto Scaling组添加健康检查，以便在实例状态受损时调用AWS Lambda函数。**
- 不正确。健康检查是用于检测已运行实例的健康状态，而不是检测实例启动失败的情况。健康检查只在实例成功启动后才会生效，无法解决实例启动失败的通知问题。

**选项B：配置Auto Scaling组在实例启动失败时向Amazon SNS主题发送通知。**
- 正确。Auto Scaling组原生支持通知功能，可以配置在特定事件（包括实例启动失败）发生时向SNS主题发送通知。SNS可以进一步配置电子邮件订阅来实现邮件通知。这是最直接和简单的解决方案。

**选项C：创建Amazon CloudWatch告警，当AttachInstances Auto Scaling API调用失败时调用AWS Lambda函数。**
- 不正确。AttachInstances API是用于将现有实例附加到Auto Scaling组的，而不是用于启动新实例。启动新实例使用的是RunInstances API。此外，这种方法过于复杂，不是最佳实践。

**选项D：在Amazon EC2上创建状态检查告警，当状态检查失败时向Amazon SNS主题发送通知。**
- 不正确。EC2状态检查只能在实例成功启动后进行，无法检测到实例启动失败的情况。如果实例根本无法启动，就不会有状态检查。

 |  |  |  |
| 99 | A company is using AWS Organizations to centrally manage its AWS accounts. The company has turned on AWS Cong in each member
account by using AWS CloudFormation StackSets. The company has congured trusted access in Organizations for AWS Cong and has
congured a member account as a delegated administrator account for AWS Cong.
A DevOps engineer needs to implement a new security policy. The policy must require all current and future AWS member accounts to use a
common baseline of AWS Cong rules that contain remediation actions that are managed from a central account. Non-administrator users
who can access member accounts must not be able to modify this common baseline of AWS Cong rules that are deployed into each member
account. | A. Create a CloudFormation template that contains the AWS Cong rules and remediation actions. Deploy the template from the
Organizations management account by using CloudFormation StackSets.
B. Create an AWS Cong conformance pack that contains the AWS Cong rules and remediation actions. Deploy the pack from the
Organizations management account by using CloudFormation StackSets.
C. Create a CloudFormation template that contains the AWS Cong rules and remediation actions. Deploy the template from the
delegated administrator account by using AWS Cong.
D. Create an AWS Cong conformance pack that contains the AWS Cong rules and remediation actions. Deploy the pack from the
delegated administrator account by using AWS Cong. |  |  |  |  |  |
| 100 | A DevOps engineer manages a large commercial website that runs on Amazon EC2. The website uses Amazon Kinesis Data Streams to collect
and process web logs. The DevOps engineer manages the Kinesis consumer application, which also runs on Amazon EC2.
Sudden increases of data cause the Kinesis consumer application to fall behind, and the Kinesis data streams drop records before the records
can be processed. The DevOps engineer must implement a solution to improve stream handling. | A. Modify the Kinesis consumer application to store the logs durably in Amazon S3. Use Amazon EMR to process the data directly on
Amazon S3 to derive customer insights. Store the results in Amazon S3.
B. Horizontally scale the Kinesis consumer application by adding more EC2 instances based on the Amazon CloudWatch
GetRecords.IteratorAgeMilliseconds metric. Increase the retention period of the Kinesis data streams.
C. Convert the Kinesis consumer application to run as an AWS Lambda function. Congure the Kinesis data streams as the event source
for the Lambda function to process the data streams.
D. Increase the number of shards in the Kinesis data streams to increase the overall throughput so that the consumer application
processes the data faster. |  |  |  |  |  |
| 101 | A company recently created a new AWS Control Tower landing zone in a new organization in AWS Organizations. The landing zone must be
able to demonstrate compliance with the Center for Internet Security (CIS) Benchmarks for AWS Foundations.
The company’s security team wants to use AWS Security Hub to view compliance across all accounts. Only the security team can be allowed to
view aggregated Security Hub ndings. In addition, specic users must be able to view ndings from their own accounts within the
organization. All accounts must be enrolled in Security Hub after the accounts are created. | A. Turn on trusted access for Security Hub in the organization’s management account. Create a new security account by using AWS Control
Tower. Congure the new security account as the delegated administrator account for Security Hub. In the new security account, provide
Security Hub with the CIS Benchmarks for AWS Foundations standards.
B. Turn on trusted access for Security Hub in the organization’s management account. From the management account, provide Security
Hub with the CIS Benchmarks for AWS Foundations standards.
C. Create an AWS IAM Identity Center (AWS Single Sign-On) permission set that includes the required permissions. Use the
CreateAccountAssignment API operation to associate the security team users with the permission set and with the delegated security
account.
D. Create an SCP that explicitly denies any user who is not on the security team from accessing Security Hub.
E. In Security Hub, turn on automatic enablement.
F. In the organization’s management account, create an Amazon EventBridge rule that reacts to the CreateManagedAccount event. Create
an AWS Lambda function that uses the Security Hub CreateMembers API operation to add new accounts to Security Hub. Congure the
EventBridge rule to invoke the Lambda function. |  |  |  |  |  |
| 102 | A company runs applications in AWS accounts that are in an organization in AWS Organizations. The applications use Amazon EC2 instances
and Amazon S3.
The company wants to detect potentially compromised EC2 instances, suspicious network activity, and unusual API activity in its existing AWS
accounts and in any AWS accounts that the company creates in the future. When the company detects one of these events, the company
wants to use an existing Amazon Simple Notication Service (Amazon SNS) topic to send a notication to its operational support team for
investigation and remediation. | A. In the organization’s management account, congure an AWS account as the Amazon GuardDuty administrator account. In the
GuardDuty administrator account, add the company’s existing AWS accounts to GuardDuty as members. In the GuardDuty administrator
account, create an Amazon EventBridge rule with an event pattern to match GuardDuty events and to forward matching events to the SNS
topic.
B. In the organization’s management account, congure Amazon GuardDuty to add newly created AWS accounts by invitation and to send
invitations to the existing AWS accounts. Create an AWS CloudFormation stack set that accepts the GuardDuty invitation and creates an
Amazon EventBridge rule. Congure the rule with an event pattern to match GuardDuty events and to forward matching events to the SNS
topic. Congure the CloudFormation stack set to deploy into all AWS accounts in the organization.
C. In the organization’s management account, create an AWS CloudTrail organization trail. Activate the organization trail in all AWS
accounts in the organization. Create an SCP that enables VPC Flow Logs in each account in the organization. Congure AWS Security Hub
for the organization. Create an Amazon EventBridge rule with an event pattern to match Security Hub events and to forward matching
events to the SNS topic.
D. In the organization’s management account, congure an AWS account as the AWS CloudTrail administrator account. In the CloudTrail
administrator account, create a CloudTrail organization trail. Add the company’s existing AWS accounts to the organization trail. Create an
SCP that enables VPC Flow Logs in each account in the organization. Congure AWS Security Hub for the organization. Create an Amazon
EventBridge rule with an event pattern to match Security Hub events and to forward matching events to the SNS topic. |  |  |  |  |  |
| 103 | A company’s DevOps engineer is working in a multi-account environment. The company uses AWS Transit Gateway to route all outbound trac
through a network operations account. In the network operations account, all account trac passes through a rewall appliance for inspection
before the trac goes to an internet gateway.
The rewall appliance sends logs to Amazon CloudWatch Logs and includes event severities of CRITICAL, HIGH, MEDIUM, LOW, and INFO. The
security team wants to receive an alert if any CRITICAL events occur. | A. Create an Amazon CloudWatch Synthetics canary to monitor the rewall state. If the rewall reaches a CRITICAL state or logs a
CRITICAL event, use a CloudWatch alarm to publish a notication to an Amazon Simple Notication Service (Amazon SNS) topic. Subscribe
the security team’s email address to the topic.
B. Create an Amazon CloudWatch metric lter by using a search for CRITICAL events. Publish a custom metric for the nding. Use a
CloudWatch alarm based on the custom metric to publish a notication to an Amazon Simple Notication Service (Amazon SNS) topic.
Subscribe the security team’s email address to the topic.
C. Enable Amazon GuardDuty in the network operations account. Congure GuardDuty to monitor ow logs. Create an Amazon EventBridge
event rule that is invoked by GuardDuty events that are CRITICAL. Dene an Amazon Simple Notication Service (Amazon SNS) topic as a
target. Subscribe the security team’s email address to the topic.
D. Use AWS Firewall Manager to apply consistent policies across all accounts. Create an Amazon EventBridge event rule that is invoked by
Firewall Manager events that are CRITICAL. Dene an Amazon Simple Notication Service (Amazon SNS) topic as a target. Subscribe the
security team’s email address to the topic. | 一家公司的DevOps工程师在多账户环境中工作。该公司使用AWS Transit Gateway将所有出站流量通过网络运营账户进行路由。在网络运营账户中，所有账户流量在到达互联网网关之前都要通过防火墙设备进行检查。

防火墙设备将日志发送到Amazon CloudWatch Logs，包含事件严重性级别：CRITICAL（严重）、HIGH（高）、MEDIUM（中等）、LOW（低）和INFO（信息）。安全团队希望在发生任何CRITICAL事件时收到警报。

 | **选项A：** 创建Amazon CloudWatch Synthetics canary来监控防火墙状态。如果防火墙达到CRITICAL状态或记录CRITICAL事件，使用CloudWatch警报发布通知到Amazon SNS主题。将安全团队的邮箱地址订阅该主题。
- **分析：** CloudWatch Synthetics主要用于监控应用程序端点和API，不适合监控日志中的特定事件。这个方案不符合需求。

**选项B：** 创建Amazon CloudWatch指标过滤器，搜索CRITICAL事件。为发现的事件发布自定义指标。基于自定义指标使用CloudWatch警报发布通知到Amazon SNS主题。将安全团队的邮箱地址订阅该主题。
- **分析：** 这是正确的方法。CloudWatch指标过滤器可以扫描日志数据中的特定模式（CRITICAL），创建自定义指标，然后基于该指标触发警报。这是处理日志监控的标准AWS方法。

**选项C：** 在网络运营账户中启用Amazon GuardDuty。配置GuardDuty监控流日志。创建Amazon EventBridge事件规则，由CRITICAL级别的GuardDuty事件触发。定义Amazon SNS主题作为目标。将安全团队的邮箱地址订阅该主题。
- **分析：** GuardDuty是威胁检测服务，主要分析VPC流日志、DNS日志等来检测恶意活动，但它不能直接监控防火墙设备发送到CloudWatch Logs的自定义日志格式。

**选项D：** 使用AWS Firewall Manager在所有账户中应用一致的策略。创建Amazon EventBridge事件规则，由Firewall Manager的CRITICAL事件触发。定义Amazon SNS主题作为目标。将安全团队的邮箱地址订阅该主题。
- **分析：** Firewall Manager用于集中管理防火墙规则，但不能监控第三方防火墙设备发送到CloudWatch Logs的日志内容。

 |  |  |  |
| 104 | A company is divided into teams. Each team has an AWS account, and all the accounts are in an organization in AWS Organizations. Each
team must retain full administrative rights to its AWS account. Each team also must be allowed to access only AWS services that the company
approves for use. AWS services must gain approval through a request and approval process.
How should a DevOps engineer congure the accounts to meet these requirements? | A. Use AWS CloudFormation StackSets to provision IAM policies in each account to deny access to restricted AWS services. In each
account, congure AWS Cong rules that ensure that the policies are attached to IAM principals in the account.
B. Use AWS Control Tower to provision the accounts into OUs within the organization. Congure AWS Control Tower to enable AWS IAM
Identity Center (AWS Single Sign-On). Congure IAM Identity Center to provide administrative access. Include deny policies on user roles
for restricted AWS services.
C. Place all the accounts under a new top-level OU within the organization. Create an SCP that denies access to restricted AWS services.
Attach the SCP to the OU.
D. Create an SCP that allows access to only approved AWS services. Attach the SCP to the root OU of the organization. Remove the
FullAWSAccess SCP from the root OU of the organization. | 一家公司分为多个团队。每个团队都有一个AWS账户，所有账户都在AWS Organizations的一个组织中。每个团队必须保留对其AWS账户的完全管理权限。每个团队也必须只能访问公司批准使用的AWS服务。AWS服务必须通过请求和批准流程获得批准。

DevOps工程师应该如何配置账户以满足这些要求？

 | **选项A：使用AWS CloudFormation StackSets在每个账户中配置IAM策略以拒绝访问受限制的AWS服务。在每个账户中，配置AWS Config规则以确保策略附加到账户中的IAM主体。**
- 问题：这种方法过于复杂且不够可靠
- IAM策略可能被具有管理员权限的团队成员修改或删除
- 无法从组织层面强制执行限制
- 管理和维护成本高

**选项B：使用AWS Control Tower将账户配置到组织内的OU中。配置AWS Control Tower以启用AWS IAM Identity Center（AWS Single Sign-On）。配置IAM Identity Center提供管理访问权限。在用户角色上包含对受限制AWS服务的拒绝策略。**
- 问题：这种方法主要解决的是身份管理和访问控制
- 无法满足"每个团队必须保留对其AWS账户的完全管理权限"的要求
- 通过IAM Identity Center的角色限制与完全管理权限相矛盾

**选项C：将所有账户放在组织内新的顶级OU下。创建一个拒绝访问受限制AWS服务的SCP。将SCP附加到OU。**
- 优点：SCP（服务控制策略）从组织层面强制执行限制
- SCP无法被账户内的管理员绕过或删除
- 团队仍然保持对批准服务的完全管理权限
- 集中管理，易于维护和更新

**选项D：创建一个只允许访问已批准AWS服务的SCP。将SCP附加到组织的根OU。从组织的根OU中删除FullAWSAccess SCP。**
- 问题：影响范围过大，会影响整个组织的所有账户
- 可能影响到不应该受限制的管理账户或其他特殊账户
- 缺乏灵活性，无法为不同团队设置不同的限制

 |  |  |  |
| 105 | A DevOps engineer used an AWS CloudFormation custom resource to set up AD Connector. The AWS Lambda function ran and created AD
Connector, but CloudFormation is not transitioning from CREATE_IN_PROGRESS to CREATE_COMPLET | E. Which action should the engineer take to resolve this issue?
A. Ensure the Lambda function code has exited successfully.
B. Ensure the Lambda function code returns a response to the pre-signed URL.
C. Ensure the Lambda function IAM role has cloudformation:UpdateStack permissions for the stack ARN.
D. Ensure the Lambda function IAM role has ds:ConnectDirectory permissions for the AWS account. |  |  |  |  |  |
| 106 | A company uses AWS CodeCommit for source code control. Developers apply their changes to various feature branches and create pull
requests to move those changes to the main branch when the changes are ready for production.
The developers should not be able to push changes directly to the main branch. The company applied the AWSCodeCommitPowerUser
managed policy to the developers’ IAM role, and now these developers can push changes to the main branch directly on every repository in
the AWS account. | A. Create an additional policy to include a Deny rule for the GitPush and PutFile actions. Include a restriction for the specic repositories
in the policy statement with a condition that references the main branch.
B. Remove the IAM policy, and add an AWSCodeCommitReadOnly managed policy. Add an Allow rule for the GitPush and PutFile actions
for the specic repositories in the policy statement with a condition that references the main branch.
C. Modify the IAM policy. Include a Deny rule for the GitPush and PutFile actions for the specic repositories in the policy statement with a
condition that references the main branch.
D. Create an additional policy to include an Allow rule for the GitPush and PutFile actions. Include a restriction for the specic repositories
in the policy statement with a condition that references the feature branches. | 一家公司使用AWS CodeCommit进行源代码控制。开发人员将他们的更改应用到各种功能分支，并在更改准备好投入生产时创建拉取请求将这些更改移动到主分支。

开发人员不应该能够直接向主分支推送更改。公司为开发人员的IAM角色应用了AWSCodeCommitPowerUser托管策略，现在这些开发人员可以在AWS账户中的每个存储库上直接向主分支推送更改。

 | **选项A：** 创建一个额外的策略，包含对GitPush和PutFile操作的拒绝规则。在策略声明中包含对特定存储库的限制，并添加引用主分支的条件。
- 这个选项通过创建额外的拒绝策略来限制主分支的推送权限
- 使用拒绝规则可以有效覆盖现有的允许权限
- 可以针对特定存储库和主分支进行精确控制

**选项B：** 移除IAM策略，添加AWSCodeCommitReadOnly托管策略。为特定存储库的GitPush和PutFile操作添加允许规则，在策略声明中添加引用主分支的条件。
- 这个选项首先移除了PowerUser权限，然后只给予只读权限
- 但是后面又为主分支添加了允许规则，这与需求相反（需求是不允许推送到主分支）
- 逻辑上存在矛盾

**选项C：** 修改IAM策略。为特定存储库的GitPush和PutFile操作包含拒绝规则，在策略声明中添加引用主分支的条件。
- 这个选项直接修改现有的IAM策略
- 但是AWSCodeCommitPowerUser是AWS托管策略，无法直接修改
- 技术上不可行

**选项D：** 创建一个额外的策略，包含对GitPush和PutFile操作的允许规则。在策略声明中包含对特定存储库的限制，并添加引用功能分支的条件。
- 这个选项试图通过只允许功能分支的推送来解决问题
- 但是由于已经有PowerUser权限，额外的允许规则不会限制现有权限
- 无法解决主分支推送的问题

 |  |  |  |
| 107 | A company manages a web application that runs on Amazon EC2 instances behind an Application Load Balancer (ALB). The EC2 instances run
in an Auto Scaling group across multiple Availability Zones. The application uses an Amazon RDS for MySQL DB instance to store the data.
The company has congured Amazon Route 53 with an alias record that points to the AL | B. Launch a replica environment of everything except Amazon RDS in a different AWS Region. Create an RDS read replica in the new
Region, and congure the new stack to point to the local RDS DB instance. Add the new stack to the Route 53 record set by using a health
check to congure a latency routing policy.
A. Launch a replica environment of everything except Amazon RDS in a different Availability Zone. Create an RDS read replica in the new
Availability Zone, and congure the new stack to point to the local RDS DB instance. Add the new stack to the Route 53 record set by using
a health check to congure a failover routing policy.
C. Launch a replica environment of everything except Amazon RDS in a different AWS Region. In the event of an outage, copy and restore
the latest RDS snapshot from the primary Region to the DR Region. Adjust the Route 53 record set to point to the ALB in the DR Region.
D. Launch a replica environment of everything except Amazon RDS in a different AWS Region. Create an RDS read replica in the new
Region, and congure the new environment to point to the local RDS DB instance. Add the new stack to the Route 53 record set by using a
health check to congure a failover routing policy. In the event of an outage, promote the read replica to primary. |  |  |  |  |  |
| 108 | A large enterprise is deploying a web application on AWS. The application runs on Amazon EC2 instances behind an Application Load
Balancer. The instances run in an Auto Scaling group across multiple Availability Zones. The application stores data in an Amazon RDS for
Oracle DB instance and Amazon DynamoD | B. Launch the EC2 instances with an EC2 IAM role to access AWS services. Retrieve the database credentials from AWS Secrets Manager.
A. Retrieve an access key from an AWS Systems Manager SecureString parameter to access AWS services. Retrieve the database
credentials from a Systems Manager SecureString parameter.
C. Retrieve an access key from an AWS Systems Manager plaintext parameter to access AWS services. Retrieve the database credentials
from a Systems Manager SecureString parameter.
D. Launch the EC2 instances with an EC2 IAM role to access AWS services. Store the database passwords in an encrypted cong le with
the application artifacts. | 一家大型企业正在AWS上部署Web应用程序。该应用程序运行在应用负载均衡器后面的Amazon EC2实例上。这些实例在Auto Scaling组中运行，跨越多个可用区。应用程序将数据存储在Amazon RDS for Oracle数据库实例和Amazon DynamoDB中。

（注：题目描述似乎不完整，但从选项可以推断这是关于如何安全地配置EC2实例访问AWS服务和数据库凭证的问题）

 | **选项A：从AWS Systems Manager SecureString参数检索访问密钥来访问AWS服务。从Systems Manager SecureString参数检索数据库凭证。**
- 不推荐：使用访问密钥（Access Key）在EC2实例上访问AWS服务不是最佳实践
- 优点：使用SecureString参数存储数据库凭证是安全的
- 缺点：访问密钥需要硬编码或存储在实例上，存在安全风险

**选项B：使用EC2 IAM角色启动EC2实例来访问AWS服务。从AWS Secrets Manager检索数据库凭证。**
- 推荐：IAM角色是EC2实例访问AWS服务的最佳实践
- 优点：无需管理访问密钥，自动轮换临时凭证
- 优点：Secrets Manager专门用于管理敏感信息，支持自动轮换
- 符合AWS安全最佳实践

**选项C：从AWS Systems Manager明文参数检索访问密钥来访问AWS服务。从Systems Manager SecureString参数检索数据库凭证。**
- 不推荐：使用明文参数存储访问密钥极不安全
- 严重安全漏洞：访问密钥以明文形式存储
- 不符合任何安全标准

**选项D：使用EC2 IAM角色启动EC2实例来访问AWS服务。将数据库密码存储在加密配置文件中与应用程序工件一起。**
- 部分正确：IAM角色的使用是正确的
- 不推荐：将数据库密码存储在配置文件中，即使加密也不是最佳实践
- 缺点：密码轮换困难，密钥管理复杂

 |  |  |  |
| 109 | The security team depends on AWS CloudTrail to detect sensitive security issues in the company’s AWS account. The DevOps engineer needs a
solution to auto-remediate CloudTrail being turned off in an AWS account. | A. Create an Amazon EventBridge rule for the CloudTrail StopLogging event. Create an AWS Lambda function that uses the AWS SDK to
call StartLogging on the ARN of the resource in which StopLogging was called. Add the Lambda function ARN as a target to the
EventBridge rule.
B. Deploy the AWS-managed CloudTrail-enabled AWS Cong rule, set with a periodic interval of 1 hour. Create an Amazon EventBridge rule
for AWS Cong rules compliance change. Create an AWS Lambda function that uses the AWS SDK to call StartLogging on the ARN of the
resource in which StopLogging was called. Add the Lambda function ARN as a target to the EventBridge rule.
C. Create an Amazon EventBridge rule for a scheduled event every 5 minutes. Create an AWS Lambda function that uses the AWS SDK to
call StartLogging on a CloudTrail trail in the AWS account. Add the Lambda function ARN as a target to the EventBridge rule.
D. Launch a t2.nano instance with a script running every 5 minutes that uses the AWS SDK to query CloudTrail in the current account. If the
CloudTrail trail is disabled, have the script re-enable the trail. | 安全团队依赖AWS CloudTrail来检测公司AWS账户中的敏感安全问题。DevOps工程师需要一个解决方案来自动修复AWS账户中CloudTrail被关闭的情况。

 | **选项A：** 为CloudTrail StopLogging事件创建Amazon EventBridge规则。创建一个AWS Lambda函数，使用AWS SDK在调用StopLogging的资源ARN上调用StartLogging。将Lambda函数ARN作为目标添加到EventBridge规则中。
- **分析：** 这是一个事件驱动的解决方案，能够实时响应CloudTrail被关闭的事件。当CloudTrail的StopLogging API被调用时，EventBridge会捕获这个事件并触发Lambda函数立即重新启用CloudTrail。这种方法响应迅速且资源效率高。

**选项B：** 部署AWS托管的CloudTrail-enabled AWS Config规则，设置为1小时的周期性间隔。为AWS Config规则合规性变更创建Amazon EventBridge规则。创建一个AWS Lambda函数，使用AWS SDK在调用StopLogging的资源ARN上调用StartLogging。将Lambda函数ARN作为目标添加到EventBridge规则中。
- **分析：** 这个方案使用AWS Config来监控CloudTrail的合规性状态。虽然可行，但存在延迟问题（最多1小时），且增加了额外的复杂性和成本（AWS Config服务费用）。

**选项C：** 创建一个每5分钟调度的Amazon EventBridge规则。创建一个AWS Lambda函数，使用AWS SDK在AWS账户中的CloudTrail跟踪上调用StartLogging。将Lambda函数ARN作为目标添加到EventBridge规则中。
- **分析：** 这是一个定时轮询的方案，每5分钟检查一次并尝试启用CloudTrail。虽然简单，但不够高效，可能会产生不必要的API调用，且存在最多5分钟的延迟。

**选项D：** 启动一个t2.nano实例，运行每5分钟执行的脚本，使用AWS SDK查询当前账户中的CloudTrail。如果CloudTrail跟踪被禁用，脚本会重新启用跟踪。
- **分析：** 这个方案需要维护EC2实例，增加了基础设施成本和管理复杂性。不符合无服务器架构的最佳实践，且存在单点故障风险。

 |  |  |  |
| 110 | A company uses AWS CodeArtifact to centrally store Python packages. The CodeArtifact repository is congured with the following repository
policy:
A development team is building a new project in an account that is in an organization in AWS Organizations. The development team wants to
use a Python library that has already been stored in the CodeArtifact repository in the organization. The development team uses AWS
CodePipeline and AWS CodeBuild to build the new application. The CodeBuild job that the development team uses to build the application is
congured to run in a VP | C. Share the CodeArtifact repository with the organization by using AWS Resource Access Manager (AWS RAM).
A. Create an Amazon S3 gateway endpoint. Update the route tables for the subnets that are running the CodeBuild job.
B. Update the repository policy’s Principal statement to include the ARN of the role that the CodeBuild project uses.
D. Update the role that the CodeBuild project uses so that the role has sucient permissions to use the CodeArtifact repository.
E. Specify the account that hosts the repository as the delegated administrator for CodeArtifact in the organization. | 一家公司使用AWS CodeArtifact来集中存储Python包。CodeArtifact存储库配置了相应的存储库策略。

一个开发团队正在AWS Organizations组织中的一个账户中构建新项目。开发团队希望使用已经存储在组织内CodeArtifact存储库中的Python库。开发团队使用AWS CodePipeline和AWS CodeBuild来构建新应用程序。开发团队用于构建应用程序的CodeBuild作业配置为在VPC中运行。

 | **选项A：创建Amazon S3网关端点。更新运行CodeBuild作业的子网的路由表。**
- 不正确。S3网关端点用于访问S3服务，与CodeArtifact访问无关。CodeArtifact有自己的VPC端点类型。

**选项B：更新存储库策略的Principal语句，包含CodeBuild项目使用的角色ARN。**
- 正确。这是跨账户访问CodeArtifact的关键步骤。需要在存储库策略中明确授权其他账户的角色访问权限。

**选项C：使用AWS Resource Access Manager (AWS RAM)与组织共享CodeArtifact存储库。**
- 不正确。CodeArtifact不支持通过AWS RAM进行资源共享。CodeArtifact的跨账户访问需要通过存储库策略来实现。

**选项D：更新CodeBuild项目使用的角色，使该角色具有使用CodeArtifact存储库的足够权限。**
- 正确。除了存储库策略授权外，CodeBuild角色本身也需要具备访问CodeArtifact的IAM权限，如`codeartifact:GetAuthorizationToken`、`codeartifact:ReadFromRepository`等。

**选项E：将托管存储库的账户指定为组织中CodeArtifact的委托管理员。**
- 不正确。委托管理员主要用于集中管理和监控，但不能直接解决跨账户访问权限问题。

 |  |  |  |
| 111 | A company uses a series of individual Amazon CloudFormation templates to deploy its multi-Region applications. These templates must be
deployed in a specic order. The company is making more changes to the templates than previously expected and wants to deploy new
templates more eciently. Additionally, the data engineering team must be notied of all changes to the templates. | A. Create an AWS Lambda function to deploy the CloudFormation templates in the required order. Use stack policies to alert the data
engineering team.
B. Host the CloudFormation templates in Amazon S3. Use Amazon S3 events to directly trigger CloudFormation updates and Amazon SNS
notications.
C. Implement CloudFormation StackSets and use drift detection to trigger update alerts to the data engineering team.
D. Leverage CloudFormation nested stacks and stack sets for deployments. Use Amazon SNS to notify the data engineering team. | 一家公司使用一系列独立的Amazon CloudFormation模板来部署其多区域应用程序。这些模板必须按特定顺序部署。该公司对模板的更改比预期的更频繁，希望更高效地部署新模板。此外，数据工程团队必须收到所有模板更改的通知。

 | **选项A：创建AWS Lambda函数按所需顺序部署CloudFormation模板。使用堆栈策略来警告数据工程团队。**
- 优点：Lambda可以控制部署顺序
- 缺点：需要自定义开发和维护Lambda函数；堆栈策略主要用于防止意外更新，不是通知机制；不够高效，需要额外的运维工作

**选项B：将CloudFormation模板托管在Amazon S3中。使用Amazon S3事件直接触发CloudFormation更新和Amazon SNS通知。**
- 优点：可以实现自动化触发和通知
- 缺点：S3事件直接触发CloudFormation更新无法保证特定的部署顺序；缺乏对多区域部署的统一管理；可能导致并发部署问题

**选项C：实施CloudFormation StackSets并使用漂移检测来触发更新警告给数据工程团队。**
- 优点：StackSets适合多区域部署
- 缺点：漂移检测主要用于检测配置偏差，不是用于模板更改通知；没有解决模板间依赖顺序的问题；不是最佳的通知机制

**选项D：利用CloudFormation嵌套堆栈和堆栈集进行部署。使用Amazon SNS通知数据工程团队。**
- 优点：嵌套堆栈可以管理模板间的依赖关系和部署顺序；StackSets非常适合多区域部署；SNS是标准的通知服务；组合使用提供了完整的解决方案
- 缺点：需要重构现有模板结构，但这是长期最佳实践

 |  |  |  |
| 112 | A DevOps engineer has implemented a CI/CD pipeline to deploy an AWS CloudFormation template that provisions a web application. The web
application consists of an Application Load Balancer (ALB), a target group, a launch template that uses an Amazon Linux 2 AMI, an Auto
Scaling group of Amazon EC2 instances, a security group, and an Amazon RDS for MySQL database. The launch template includes user data
that species a script to install and start the application.
The initial deployment of the application was successful. The DevOps engineer made changes to update the version of the application with
the user data. The CI/CD pipeline has deployed a new version of the template. However, the health checks on the ALB are now failing. The
health checks have marked all targets as unhealthy.
During investigation, the DevOps engineer notices that the CloudFormation stack has a status of UPDATE_COMPLET | E. However, when the
DevOps engineer connects to one of the EC2 instances and checks /var/log/messages, the DevOps engineer notices that the Apache web
server failed to start successfully because of a conguration error.
How can the DevOps engineer ensure that the CloudFormation deployment will fail if the user data fails to successfully nish running?
A. Use the cfn-signal helper script to signal success or failure to CloudFormation. Use the WaitOnResourceSignals update policy within the
CloudFormation template. Set an appropriate timeout for the update policy.
B. Create an Amazon CloudWatch alarm for the UnhealthyHostCount metric. Include an appropriate alarm threshold for the target group.
Create an Amazon Simple Notication Service (Amazon SNS) topic as the target to signal success or failure to CloudFormation.
C. Create a lifecycle hook on the Auto Scaling group by using the AWS::AutoScaling::LifecycleHook resource. Create an Amazon Simple
Notication Service (Amazon SNS) topic as the target to signal success or failure to CloudFormation. Set an appropriate timeout on the
lifecycle hook.
D. Use the Amazon CloudWatch agent to stream the cloud-init logs. Create a subscription lter that includes an AWS Lambda function with
an appropriate invocation timeout. Congure the Lambda function to use the SignalResource API operation to signal success or failure to
CloudFormation. | 一名DevOps工程师实施了一个CI/CD流水线来部署AWS CloudFormation模板，该模板用于配置一个Web应用程序。该Web应用程序包含一个应用负载均衡器(ALB)、一个目标组、一个使用Amazon Linux 2 AMI的启动模板、一个Amazon EC2实例的Auto Scaling组、一个安全组，以及一个Amazon RDS for MySQL数据库。启动模板包含用户数据，指定了安装和启动应用程序的脚本。

应用程序的初始部署是成功的。DevOps工程师通过用户数据进行了更改以更新应用程序版本。CI/CD流水线已部署了新版本的模板。然而，ALB上的健康检查现在失败了。健康检查将所有目标标记为不健康。

在调查过程中，DevOps工程师注意到CloudFormation堆栈的状态为UPDATE_COMPLETE。然而，当DevOps工程师连接到其中一个EC2实例并检查/var/log/messages时，发现Apache Web服务器由于配置错误而未能成功启动。

如何确保当用户数据未能成功完成运行时，CloudFormation部署会失败？

 | **选项A：使用cfn-signal辅助脚本向CloudFormation发送成功或失败信号。在CloudFormation模板中使用WaitOnResourceSignals更新策略。为更新策略设置适当的超时时间。**
- 这是处理用户数据执行状态的标准AWS方法
- cfn-signal可以在用户数据脚本中使用，根据脚本执行结果发送成功或失败信号
- WaitOnResourceSignals策略会等待接收到信号后才认为资源创建/更新完成
- 如果在超时时间内未收到成功信号，CloudFormation会将部署标记为失败

**选项B：为UnhealthyHostCount指标创建Amazon CloudWatch告警。为目标组包含适当的告警阈值。创建Amazon SNS主题作为目标，向CloudFormation发送成功或失败信号。**
- CloudWatch告警无法直接影响CloudFormation部署状态
- SNS主题不能直接向CloudFormation发送资源信号
- 这种方法只能用于监控，不能阻止部署完成

**选项C：使用AWS::AutoScaling::LifecycleHook资源在Auto Scaling组上创建生命周期钩子。创建Amazon SNS主题作为目标，向CloudFormation发送成功或失败信号。为生命周期钩子设置适当的超时时间。**
- 生命周期钩子主要用于在实例启动/终止时执行自定义操作
- SNS主题无法直接向CloudFormation发送资源完成信号
- 这不是处理用户数据执行状态的正确方法

**选项D：使用Amazon CloudWatch代理流式传输cloud-init日志。创建包含AWS Lambda函数的订阅过滤器，设置适当的调用超时。配置Lambda函数使用SignalResource API操作向CloudFormation发送成功或失败信号。**
- 虽然技术上可行，但过于复杂
- 需要额外的资源和配置
- 不是AWS推荐的标准做法

 |  |  |  |
| 113 | A company has a data ingestion application that runs across multiple AWS accounts. The accounts are in an organization in AWS
Organizations. The company needs to monitor the application and consolidate access to the application. Currently, the company is running
the application on Amazon EC2 instances from several Auto Scaling groups. The EC2 instances have no access to the internet because the
data is sensitive. Engineers have deployed the necessary VPC endpoints. The EC2 instances run a custom AMI that is built specically for the
application.
To maintain and troubleshoot the application, system administrators need the ability to log in to the EC2 instances. This access must be
automated and controlled centrally. The company’s security team must receive a notication whenever the instances are accessed. | A. Create an Amazon EventBridge rule to send notications to the security team whenever a user logs in to an EC2 instance. Use EC2
Instance Connect to log in to the instances. Deploy Auto Scaling groups by using AWS CloudFormation. Use the cfn-init helper script to
deploy appropriate VPC routes for external access. Rebuild the custom AMI so that the custom AMI includes AWS Systems Manager Agent.
B. Deploy a NAT gateway and a bastion host that has internet access. Create a security group that allows incoming trac on all the EC2
instances from the bastion host. Install AWS Systems Manager Agent on all the EC2 instances. Use Auto Scaling group lifecycle hooks for
monitoring and auditing access. Use Systems Manager Session Manager to log in to the instances. Send logs to a log group in Amazon
CloudWatch Logs. Export data to Amazon S3 for auditing. Send notications to the security team by using S3 event notications.
C. Use EC2 Image Builder to rebuild the custom AMI. Include the most recent version of AWS Systems Manager Agent in the image.
Congure the Auto Scaling group to attach the AmazonSSMManagedInstanceCore role to all the EC2 instances. Use Systems Manager
Session Manager to log in to the instances. Enable logging of session details to Amazon S3. Create an S3 event notication for new le
uploads to send a message to the security team through an Amazon Simple Notication Service (Amazon SNS) topic.
D. Use AWS Systems Manager Automation to build Systems Manager Agent into the custom AMI. Congure AWS Cong to attach an SCP to
the root organization account to allow the EC2 instances to connect to Systems Manager. Use Systems Manager Session Manager to log
in to the instances. Enable logging of session details to Amazon S3. Create an S3 event notication for new le uploads to send a
message to the security team through an Amazon Simple Notication Service (Amazon SNS) topic. | 一家公司有一个跨多个AWS账户运行的数据摄取应用程序。这些账户在AWS Organizations的组织中。公司需要监控应用程序并整合对应用程序的访问。目前，公司在来自多个Auto Scaling组的Amazon EC2实例上运行应用程序。由于数据敏感，EC2实例无法访问互联网。工程师已经部署了必要的VPC端点。EC2实例运行专门为应用程序构建的自定义AMI。

为了维护和故障排除应用程序，系统管理员需要能够登录到EC2实例。这种访问必须是自动化的并且集中控制。公司的安全团队必须在实例被访问时收到通知。

 | **选项A：**
- 使用EventBridge规则发送通知 - 可行
- 使用EC2 Instance Connect登录 - 需要互联网访问，与题目要求冲突
- 使用cfn-init部署VPC路由进行外部访问 - 违反了无互联网访问的安全要求
- 重建AMI包含SSM Agent - 正确做法
- **问题：** 违反了无互联网访问的要求

**选项B：**
- 部署NAT网关和堡垒主机 - 增加了不必要的复杂性和成本
- 创建安全组允许从堡垒主机访问 - 可行但不是最佳实践
- 使用Auto Scaling生命周期钩子进行监控 - 不是最直接的方法
- 使用Session Manager - 正确的方法
- 通过CloudWatch Logs和S3进行日志记录和通知 - 过于复杂
- **问题：** 架构过于复杂，不必要的组件

**选项C：**
- 使用EC2 Image Builder重建AMI - 最佳实践
- 包含最新版本的SSM Agent - 正确
- 配置Auto Scaling组附加AmazonSSMManagedInstanceCore角色 - 正确的权限配置
- 使用Session Manager登录 - 完美适合无互联网访问环境
- 启用会话详情日志记录到S3 - 符合审计要求
- 使用S3事件通知和SNS发送消息给安全团队 - 简洁有效的通知机制
- **优点：** 完全符合所有要求，架构简洁

**选项D：**
- 使用Systems Manager Automation构建SSM Agent到AMI - 可行但不如Image Builder标准
- 配置AWS Config附加SCP到根组织账户 - 配置错误，SCP不是通过Config附加的
- 其他部分与选项C类似
- **问题：** 配置方法错误

 |  |  |  |
| 114 | A company uses Amazon S3 to store proprietary information. The development team creates buckets for new projects on a daily basis. The
security team wants to ensure that all existing and future buckets have encryption, logging, and versioning enabled. Additionally, no buckets
should ever be publicly read or write accessible. | A. Enable AWS CloudTrail and congure automatic remediation using AWS Lambda.
B. Enable AWS Cong rules and congure automatic remediation using AWS Systems Manager documents.
C. Enable AWS Trusted Advisor and congure automatic remediation using Amazon EventBridge.
D. Enable AWS Systems Manager and congure automatic remediation using Systems Manager documents. | 一家公司使用Amazon S3存储专有信息。开发团队每天都会为新项目创建存储桶。安全团队希望确保所有现有和未来的存储桶都启用了加密、日志记录和版本控制。此外，任何存储桶都不应该允许公共读取或写入访问。

选项：
A. 启用AWS CloudTrail并使用AWS Lambda配置自动修复。
B. 启用AWS Config规则并使用AWS Systems Manager文档配置自动修复。
C. 启用AWS Trusted Advisor并使用Amazon EventBridge配置自动修复。
D. 启用AWS Systems Manager并使用Systems Manager文档配置自动修复。

 | **选项A：启用AWS CloudTrail并使用AWS Lambda配置自动修复**
- CloudTrail主要用于记录API调用和审计，不是用于合规性检查和配置管理
- 虽然Lambda可以用于自动修复，但CloudTrail不是检测配置违规的最佳工具
- 这种方案需要大量自定义代码来检测S3配置问题

**选项B：启用AWS Config规则并使用AWS Systems Manager文档配置自动修复**
- AWS Config专门用于监控和评估AWS资源的配置合规性
- Config提供预构建的规则来检查S3加密、版本控制、公共访问等设置
- Systems Manager文档可以定义标准化的修复操作
- Config支持自动修复功能，可以与SSM文档集成
- 这是AWS推荐的配置合规性管理方案

**选项C：启用AWS Trusted Advisor并使用Amazon EventBridge配置自动修复**
- Trusted Advisor主要提供成本优化、性能和安全建议
- 它不是实时配置监控工具，检查频率有限
- EventBridge虽然可以处理事件，但Trusted Advisor不是配置合规性的最佳数据源

**选项D：启用AWS Systems Manager并使用Systems Manager文档配置自动修复**
- Systems Manager本身不提供配置合规性检查功能
- 缺少触发机制来检测何时需要修复
- 需要其他服务来检测配置违规

 |  |  |  |
| 115 | A DevOps engineer is researching the least expensive way to implement an image batch processing cluster on AWS. The application cannot
run in Docker containers and must run on Amazon EC2. The batch job stores checkpoint data on an NFS volume and can tolerate interruptions.
Conguring the cluster software from a generic EC2 Linux image takes 30 minutes. | A. Use Amazon EFS for checkpoint data. To complete the job, use an EC2 Auto Scaling group and an On-Demand pricing model to provision
EC2 instances temporarily.
B. Use GlusterFS on EC2 instances for checkpoint data. To run the batch job, congure EC2 instances manually. When the job completes,
shut down the instances manually.
C. Use Amazon EFS for checkpoint data. Use EC2 Fleet to launch EC2 Spot Instances, and utilize user data to congure the EC2 Linux
instance on startup.
D. Use Amazon EFS for checkpoint data. Use EC2 Fleet to launch EC2 Spot Instances. Create a custom AMI for the cluster and use the
latest AMI when creating instances. | 一名DevOps工程师正在研究在AWS上实现图像批处理集群的最经济方式。该应用程序无法在Docker容器中运行，必须在Amazon EC2上运行。批处理作业将检查点数据存储在NFS卷上，并且可以容忍中断。从通用EC2 Linux镜像配置集群软件需要30分钟。

 | **选项A：使用Amazon EFS存储检查点数据。为完成作业，使用EC2 Auto Scaling组和按需定价模型临时配置EC2实例。**
- 优点：Amazon EFS提供了托管的NFS服务，符合要求
- 缺点：使用按需实例成本较高，不是最经济的选择
- 每次启动都需要30分钟配置时间

**选项B：在EC2实例上使用GlusterFS存储检查点数据。运行批处理作业时手动配置EC2实例，作业完成后手动关闭实例。**
- 缺点：GlusterFS需要自己管理和维护，增加运维复杂性
- 手动操作效率低，容易出错
- 不符合DevOps自动化最佳实践

**选项C：使用Amazon EFS存储检查点数据。使用EC2 Fleet启动EC2 Spot实例，并利用用户数据在启动时配置EC2 Linux实例。**
- 优点：使用Spot实例成本最低，Amazon EFS提供托管NFS服务
- 缺点：每次启动仍需30分钟配置时间，影响效率
- 用户数据脚本可能因为复杂性导致配置失败

**选项D：使用Amazon EFS存储检查点数据。使用EC2 Fleet启动EC2 Spot实例。为集群创建自定义AMI，并在创建实例时使用最新的AMI。**
- 优点：使用Spot实例成本最低
- 优点：Amazon EFS提供托管的NFS服务
- 优点：自定义AMI预装了所有必要软件，避免了30分钟的配置时间
- 优点：启动速度快，提高了整体效率
- 符合批处理作业可容忍中断的特性（Spot实例可能被回收）

 |  |  |  |
| 116 | A company recently migrated its legacy application from on-premises to AWS. The application is hosted on Amazon EC2 instances behind an
Application Load Balancer, which is behind Amazon API Gateway. The company wants to ensure users experience minimal disruptions during
any deployment of a new version of the application. The company also wants to ensure it can quickly roll back updates if there is an issue. | A. Introduce changes as a separate environment parallel to the existing one. Congure API Gateway to use a canary release deployment
to send a small subset of user trac to the new environment.
B. Introduce changes as a separate environment parallel to the existing one. Update the application’s DNS alias records to point to the
new environment.
C. Introduce changes as a separate target group behind the existing Application Load Balancer. Congure API Gateway to route user
trac to the new target group in steps.
D. Introduce changes as a separate target group behind the existing Application Load Balancer. Congure API Gateway to route all trac
to the Application Load Balancer, which then sends the trac to the new target group. | 一家公司最近将其传统应用程序从本地迁移到AWS。该应用程序托管在Amazon EC2实例上，这些实例位于Application Load Balancer后面，而Application Load Balancer又位于Amazon API Gateway后面。公司希望确保用户在部署新版本应用程序时体验到最小的中断。公司还希望确保在出现问题时能够快速回滚更新。

选项：
A. 将更改作为与现有环境并行的独立环境引入。配置API Gateway使用金丝雀发布部署，将一小部分用户流量发送到新环境。
B. 将更改作为与现有环境并行的独立环境引入。更新应用程序的DNS别名记录以指向新环境。
C. 将更改作为现有Application Load Balancer后面的独立目标组引入。配置API Gateway分步骤将用户流量路由到新目标组。
D. 将更改作为现有Application Load Balancer后面的独立目标组引入。配置API Gateway将所有流量路由到Application Load Balancer，然后由负载均衡器将流量发送到新目标组。

 | **选项A：** 
- 优点：创建完全独立的环境，提供完整的隔离；API Gateway的金丝雀发布功能可以精确控制流量分配；支持快速回滚
- 缺点：资源成本较高，需要维护两套完整环境
- 技术可行性：高，符合AWS最佳实践

**选项B：**
- 优点：创建独立环境提供隔离
- 缺点：DNS更改不支持渐进式部署，是全量切换；DNS传播有延迟；回滚需要再次更改DNS，不够快速
- 技术可行性：可行但不是最佳方案

**选项C：**
- 优点：成本效率高，使用现有负载均衡器；支持渐进式流量切换
- 缺点：API Gateway无法直接路由到特定的ALB目标组，这在技术架构上不正确
- 技术可行性：低，架构概念错误

**选项D：**
- 优点：使用现有基础设施，成本较低
- 缺点：没有渐进式部署机制；如果配置为将所有流量发送到新目标组，则是全量切换，风险较高
- 技术可行性：可行但不符合最小中断要求

 | A |  |  |
| 117 | A company is storing 100 GB of log data in .csv format in an Amazon S3 bucket. SQL developers want to query this data and generate graphs
to visualize it. The SQL developers also need an ecient, automated way to store metadata from the .csv le. | A. Filter the data through AWS X-Ray to visualize the data.
B. Filter the data through Amazon QuickSight to visualize the data.
C. Query the data with Amazon Athena.
D. Query the data with Amazon Redshift.
E. Use the AWS Glue Data Catalog as the persistent metadata store. | 一家公司在Amazon S3存储桶中存储了100 GB的.csv格式日志数据。SQL开发人员希望查询这些数据并生成图表来可视化展示。SQL开发人员还需要一种高效的、自动化的方式来存储.csv文件的元数据。

 | **A. 通过AWS X-Ray过滤数据以可视化数据**
- 错误。AWS X-Ray是用于应用程序性能监控和分布式跟踪的服务，主要用于分析微服务架构中的请求流和性能瓶颈，不适用于查询和可视化S3中的CSV数据。

**B. 通过Amazon QuickSight过滤数据以可视化数据**
- 正确。Amazon QuickSight是AWS的商业智能服务，专门用于数据可视化和生成图表。它可以直接连接S3数据源，支持CSV格式，并提供丰富的图表和仪表板功能。

**C. 使用Amazon Athena查询数据**
- 正确。Amazon Athena是无服务器的交互式查询服务，可以直接使用标准SQL查询存储在S3中的数据，包括CSV格式。它无需预先加载数据，按查询付费，非常适合这种场景。

**D. 使用Amazon Redshift查询数据**
- 部分正确但不是最佳选择。Redshift是数据仓库服务，需要先将数据加载到集群中才能查询，对于100GB的数据来说过于复杂且成本较高，不如Athena直接查询S3数据来得高效。

**E. 使用AWS Glue Data Catalog作为持久化元数据存储**
- 正确。AWS Glue Data Catalog是完全托管的元数据存储库，可以自动发现和存储CSV文件的schema信息，与Athena和QuickSight无缝集成，提供自动化的元数据管理。

 |  |  |  |
| 118 | A company deploys its corporate infrastructure on AWS across multiple AWS Regions and Availability Zones. The infrastructure is deployed on
Amazon EC2 instances and connects with AWS IoT Greengrass devices. The company deploys additional resources on on-premises servers
that are located in the corporate headquarters.
The company wants to reduce the overhead involved in maintaining and updating its resources. The company’s DevOps team plans to use
AWS Systems Manager to implement automated management and application of patches. The DevOps team conrms that Systems Manager
is available in the Regions that the resources are deployed in. Systems Manager also is available in a Region near the corporate
headquarters. | A. Apply tags to all the EC2 instances, AWS IoT Greengrass devices, and on-premises servers. Use Systems Manager Session Manager to
push patches to all the tagged devices.
B. Use Systems Manager Run Command to schedule patching for the EC2 instances, AWS IoT Greengrass devices, and on-premises
servers.
C. Use Systems Manager Patch Manager to schedule patching for the EC2 instances, AWS IoT Greengrass devices, and on-premises
servers as a Systems Manager maintenance window task.
D. Congure Amazon EventBridge to monitor Systems Manager Patch Manager for updates to patch baselines. Associate Systems
Manager Run Command with the event to initiate a patch action for all EC2 instances, AWS IoT Greengrass devices, and on-premises
servers.
E. Create an IAM instance prole for Systems Manager. Attach the instance prole to all the EC2 instances in the AWS account. For the
AWS IoT Greengrass devices and on-premises servers, create an IAM service role for Systems Manager. | 一家公司在AWS上跨多个AWS区域和可用区部署其企业基础设施。基础设施部署在Amazon EC2实例上，并与AWS IoT Greengrass设备连接。该公司还在位于企业总部的本地服务器上部署了额外的资源。

该公司希望减少维护和更新其资源所涉及的开销。公司的DevOps团队计划使用AWS Systems Manager来实现补丁的自动化管理和应用。DevOps团队确认Systems Manager在部署资源的区域中可用，并且在企业总部附近的区域中也可用。

 | **选项A：** 对所有EC2实例、AWS IoT Greengrass设备和本地服务器应用标签。使用Systems Manager Session Manager向所有标记的设备推送补丁。
- **错误**：Session Manager主要用于安全的shell访问，不是用于补丁管理的工具。这不是补丁管理的正确方法。

**选项B：** 使用Systems Manager Run Command为EC2实例、AWS IoT Greengrass设备和本地服务器安排补丁。
- **部分正确但不完整**：Run Command可以执行补丁操作，但它不是专门为补丁管理设计的工具，缺乏补丁管理的完整功能如补丁基线、合规性报告等。

**选项C：** 使用Systems Manager Patch Manager作为Systems Manager维护窗口任务，为EC2实例、AWS IoT Greengrass设备和本地服务器安排补丁。
- **正确**：Patch Manager是专门为补丁管理设计的服务，支持所有提到的资源类型，维护窗口可以确保在合适的时间进行补丁操作。

**选项D：** 配置Amazon EventBridge监控Systems Manager Patch Manager的补丁基线更新。将Systems Manager Run Command与事件关联，为所有EC2实例、AWS IoT Greengrass设备和本地服务器启动补丁操作。
- **过于复杂**：虽然技术上可行，但这种方法比直接使用Patch Manager更复杂，不是最佳实践。

**选项E：** 为Systems Manager创建IAM实例配置文件。将实例配置文件附加到AWS账户中的所有EC2实例。对于AWS IoT Greengrass设备和本地服务器，创建Systems Manager的IAM服务角色。
- **不完整**：这只是配置权限的步骤，没有描述实际的补丁管理实施方案。

 |  |  |  |
| 119 | A company is testing a web application that runs on Amazon EC2 instances behind an Application Load Balancer. The instances run in an Auto
Scaling group across multiple Availability Zones. The company uses a blue/green deployment process with immutable instances when
deploying new software.
During testing, users are being automatically logged out of the application at random times. Testers also report that, when a new version of
the application is deployed, all users are logged out. The development team needs a solution to ensure users remain logged in across scaling
events and application deployments. | A. Enable smart sessions on the load balancer and modify the application to check for an existing session.
B. Enable session sharing on the load balancer and modify the application to read from the session store.
C. Store user session information in an Amazon S3 bucket and modify the application to read session information from the bucket.
D. Modify the application to store user session information in an Amazon ElastiCache cluster. |  |  |  |  |  |
| 120 | A DevOps engineer needs to congure a blue/green deployment for an existing three-tier application. The application runs on Amazon EC2
instances and uses an Amazon RDS database. The EC2 instances run behind an Application Load Balancer (ALB) and are in an Auto Scaling
group.
The DevOps engineer has created a launch template and an Auto Scaling group for the blue environment. The DevOps engineer also has
created a launch template and an Auto Scaling group for the green environment. Each Auto Scaling group deploys to a matching blue or green
target group. The target group also species which software, blue or green, gets loaded on the EC2 instances. The ALB can be congured to
send trac to the blue environment’s target group or the green environment’s target group. An Amazon Route 53 record for www.example.com
points to the AL | B. 
A. Start a rolling restart of the Auto Scaling group for the green environment to deploy the new software on the green environment’s EC2
instances. When the rolling restart is complete, use an AWS CLI command to update the ALB to send trac to the green environment’s
target group.
C. Update the launch template to deploy the green environment’s software on the blue environment’s EC2 instances. Keep the target
groups and Auto Scaling groups unchanged in both environments. Perform a rolling restart of the blue environment’s EC2 instances.
D. Start a rolling restart of the Auto Scaling group for the green environment to deploy the new software on the green environment’s EC2
instances. When the rolling restart is complete, update the Route 53 DNS to point to the green environment’s endpoint on the AL | 一名DevOps工程师需要为现有的三层应用程序配置蓝/绿部署。该应用程序运行在Amazon EC2实例上，并使用Amazon RDS数据库。EC2实例运行在应用程序负载均衡器(ALB)后面，并位于Auto Scaling组中。

DevOps工程师已经为蓝环境创建了启动模板和Auto Scaling组。DevOps工程师还为绿环境创建了启动模板和Auto Scaling组。每个Auto Scaling组部署到匹配的蓝色或绿色目标组。目标组还指定在EC2实例上加载哪个软件版本（蓝色或绿色）。ALB可以配置为将流量发送到蓝环境的目标组或绿环境的目标组。Amazon Route 53记录www.example.com指向ALB。

 | **选项A：** 题目中未完整显示，无法分析。

**选项B：** 启动绿环境Auto Scaling组的滚动重启来在绿环境的EC2实例上部署新软件。当滚动重启完成后，使用AWS CLI命令更新ALB将流量发送到绿环境的目标组。
- 这个方案有问题：滚动重启会导致绿环境在部署过程中出现服务中断
- 蓝/绿部署的核心是零停机时间，滚动重启违背了这一原则

**选项C：** 更新启动模板以在蓝环境的EC2实例上部署绿环境的软件。保持两个环境中的目标组和Auto Scaling组不变。对蓝环境的EC2实例执行滚动重启。
- 这不是真正的蓝/绿部署，而是就地更新
- 滚动重启会造成服务中断
- 没有利用已经准备好的绿环境基础设施

**选项D：** 启动绿环境Auto Scaling组的滚动重启来在绿环境的EC2实例上部署新软件。当滚动重启完成后，更新Route 53 DNS指向ALB上的绿环境端点。
- 同样存在滚动重启导致的服务中断问题
- 但是使用DNS切换比直接修改ALB配置更符合蓝/绿部署的最佳实践
- DNS切换提供了更好的回滚能力

 |  |  |  |
| 121 | A company is building a new pipeline by using AWS CodePipeline and AWS CodeBuild in a build account. The pipeline consists of two stages.
The rst stage is a CodeBuild job to build and package an AWS Lambda function. The second stage consists of deployment actions that
operate on two different AWS accounts: a development environment account and a production environment account. The deployment stages
use the AWS CloudFormation action that CodePipeline invokes to deploy the infrastructure that the Lambda function requires.
A DevOps engineer creates the CodePipeline pipeline and congures the pipeline to encrypt build artifacts by using the AWS Key
Management Service (AWS KMS) AWS managed key for Amazon S3 (the aws/s3 key). The artifacts are stored in an S3 bucket. When the
pipeline runs, the CloudFormation actions fail with an access denied error. | A. Create an S3 bucket in each AWS account for the artifacts. Allow the pipeline to write to the S3 buckets. Create a CodePipeline S3
action to copy the artifacts to the S3 bucket in each AWS account. Update the CloudFormation actions to reference the artifacts S3 bucket
in the production account.
B. Create a customer managed KMS key. Congure the KMS key policy to allow the IAM roles used by the CloudFormation action to
perform decrypt operations. Modify the pipeline to use the customer managed KMS key to encrypt artifacts.
C. Create an AWS managed KMS key. Congure the KMS key policy to allow the development account and the production account to
perform decrypt operations. Modify the pipeline to use the KMS key to encrypt artifacts.
D. In the development account and in the production account, create an IAM role for CodePipeline. Congure the roles with permissions to
perform CloudFormation operations and with permissions to retrieve and decrypt objects from the artifacts S3 bucket. In the CodePipeline
account, congure the CodePipeline CloudFormation action to use the roles.
E. In the development account and in the production account, create an IAM role for CodePipeline. Congure the roles with permissions to
perform CloudFormation operations and with permissions to retrieve and decrypt objects from the artifacts S3 bucket. In the CodePipeline
account, modify the artifacts S3 bucket policy to allow the roles access. Congure the CodePipeline CloudFormation action to use the
roles. | 一家公司正在使用AWS CodePipeline和AWS CodeBuild在构建账户中构建新的管道。该管道包含两个阶段。

第一个阶段是CodeBuild作业，用于构建和打包AWS Lambda函数。第二个阶段包含在两个不同AWS账户上操作的部署操作：开发环境账户和生产环境账户。部署阶段使用CodePipeline调用的AWS CloudFormation操作来部署Lambda函数所需的基础设施。

DevOps工程师创建了CodePipeline管道，并配置管道使用AWS密钥管理服务(AWS KMS)的AWS托管密钥for Amazon S3(aws/s3密钥)来加密构建工件。工件存储在S3存储桶中。当管道运行时，CloudFormation操作失败并出现访问拒绝错误。

 | **选项A：** 在每个AWS账户中创建S3存储桶用于工件。允许管道写入S3存储桶。创建CodePipeline S3操作将工件复制到每个账户的S3存储桶。更新CloudFormation操作以引用生产账户中的工件S3存储桶。
- 这种方法过于复杂，需要在每个账户中创建额外的S3存储桶，并且没有解决KMS密钥权限的根本问题。

**选项B：** 创建客户托管的KMS密钥。配置KMS密钥策略以允许CloudFormation操作使用的IAM角色执行解密操作。修改管道以使用客户托管的KMS密钥来加密工件。
- 这是一个有效的解决方案。客户托管的KMS密钥可以配置跨账户权限，允许其他账户的角色进行解密操作。

**选项C：** 创建AWS托管的KMS密钥。配置KMS密钥策略以允许开发账户和生产账户执行解密操作。修改管道以使用KMS密钥来加密工件。
- 这个选项有误，因为AWS托管的KMS密钥策略无法由用户修改。用户无法为AWS托管密钥配置跨账户权限。

**选项D：** 在开发账户和生产账户中，为CodePipeline创建IAM角色。配置角色具有执行CloudFormation操作的权限以及从工件S3存储桶检索和解密对象的权限。在CodePipeline账户中，配置CodePipeline CloudFormation操作使用这些角色。
- 这个方案缺少S3存储桶策略的配置，仅有IAM角色权限可能不足以解决跨账户访问问题。

**选项E：** 在开发账户和生产账户中，为CodePipeline创建IAM角色。配置角色具有执行CloudFormation操作的权限以及从工件S3存储桶检索和解decrypt对象的权限。在CodePipeline账户中，修改工件S3存储桶策略以允许角色访问。配置CodePipeline CloudFormation操作使用这些角色。
- 这是一个全面的解决方案，包括IAM角色配置和S3存储桶策略修改，但仍然没有解决KMS密钥权限问题。

 |  |  |  |
| 122 | A company is using an organization in AWS Organizations to manage multiple AWS accounts. The company’s development team wants to use
AWS Lambda functions to meet resiliency requirements and is rewriting all applications to work with Lambda functions that are deployed in a
VP | C. Create a new EFS le system in Account
B. 
A. 
D. Update the Lambda execution roles with permission to access the VPC and the EFS le system.
E. Create a VPC peering connection to connect Account A to Account | 一家公司正在使用AWS Organizations中的组织来管理多个AWS账户。公司的开发团队希望使用AWS Lambda函数来满足弹性要求，并正在重写所有应用程序以使用部署在VPC中的Lambda函数。

**注意：** 题目描述似乎不完整，选项也存在格式问题和内容缺失。基于现有信息，这似乎是关于Lambda函数在VPC中的部署和跨账户资源访问的问题。

# | **选项A：** [内容缺失，无法分析]

**选项B：** [内容缺失，无法分析]

**选项C：** 在账户中创建一个新的EFS文件系统
- 这个选项提到了EFS（Elastic File System），这是AWS的托管文件存储服务
- EFS可以为Lambda函数提供持久化存储，支持多个Lambda函数并发访问
- 但仅创建EFS文件系统还不足以解决完整的跨账户访问问题

**选项D：** 更新Lambda执行角色，添加访问VPC和EFS文件系统的权限
- 这是一个关键的配置步骤
- Lambda函数需要适当的IAM权限才能访问VPC资源
- 需要`AWSLambdaVPCAccessExecutionRole`策略来访问VPC
- 需要EFS相关权限（如`elasticfilesystem:ClientMount`、`elasticfilesystem:ClientWrite`等）来访问EFS
- 这是实现Lambda在VPC中访问EFS的必要配置

**选项E：** 创建VPC对等连接来连接账户A到账户[内容不完整]
- VPC对等连接用于在不同VPC之间建立网络连接
- 在多账户环境中，这可能是必要的网络配置
- 但选项描述不完整，无法完全评估

# |  |  |  |
| 123 | A media company has several thousand Amazon EC2 instances in an AWS account. The company is using Slack and a shared email inbox for
team communications and important updates. A DevOps engineer needs to send all AWS-scheduled EC2 maintenance notications to the
Slack channel and the shared inbox. The solution must include the instances’ Name and Owner tags. | A. Integrate AWS Trusted Advisor with AWS Cong. Congure a custom AWS Cong rule to invoke an AWS Lambda function to publish
notications to an Amazon Simple Notication Service (Amazon SNS) topic. Subscribe a Slack channel endpoint and the shared inbox to
the topic.
B. Use Amazon EventBridge to monitor for AWS Health events. Congure the maintenance events to target an Amazon Simple Notication
Service (Amazon SNS) topic. Subscribe an AWS Lambda function to the SNS topic to send notications to the Slack channel and the
shared inbox.
C. Create an AWS Lambda function that sends EC2 maintenance notications to the Slack channel and the shared inbox. Monitor EC2
health events by using Amazon CloudWatch metrics. Congure a CloudWatch alarm that invokes the Lambda function when a
maintenance notication is received.
D. Congure AWS Support integration with AWS CloudTrail. Create a CloudTrail lookup event to invoke an AWS Lambda function to pass
EC2 maintenance notications to Amazon Simple Notication Service (Amazon SNS). Congure Amazon SNS to target the Slack channel
and the shared inbox. |  |  |  |  |  |
| 124 | An AWS CodePipeline pipeline has implemented a code release process. The pipeline is integrated with AWS CodeDeploy to deploy versions
of an application to multiple Amazon EC2 instances for each CodePipeline stage.
During a recent deployment, the pipeline failed due to a CodeDeploy issue. The DevOps team wants to improve monitoring and notications
during deployment to decrease resolution times. | A. Implement Amazon CloudWatch Logs for CodePipeline and CodeDeploy, create an AWS Cong rule to evaluate code deployment issues,
and create an Amazon Simple Notication Service (Amazon SNS) topic to notify stakeholders of deployment issues.
B. Implement Amazon EventBridge for CodePipeline and CodeDeploy, create an AWS Lambda function to evaluate code deployment
issues, and create an Amazon Simple Notication Service (Amazon SNS) topic to notify stakeholders of deployment issues.
C. Implement AWS CloudTrail to record CodePipeline and CodeDeploy API call information, create an AWS Lambda function to evaluate
code deployment issues, and create an Amazon Simple Notication Service (Amazon SNS) topic to notify stakeholders of deployment
issues.
D. Implement Amazon EventBridge for CodePipeline and CodeDeploy, create an Amazon Inspector assessment target to evaluate code
deployment issues, and create an Amazon Simple Notication Service (Amazon SNS) topic to notify stakeholders of deployment issues. | 一个AWS CodePipeline流水线已经实现了代码发布流程。该流水线与AWS CodeDeploy集成，为每个CodePipeline阶段将应用程序版本部署到多个Amazon EC2实例。

在最近的一次部署中，流水线由于CodeDeploy问题而失败。DevOps团队希望改进部署期间的监控和通知，以减少问题解决时间。

 | **选项A：** 为CodePipeline和CodeDeploy实施Amazon CloudWatch Logs，创建AWS Config规则来评估代码部署问题，并创建Amazon SNS主题来通知利益相关者部署问题。
- CloudWatch Logs主要用于日志收集和存储，不是事件驱动的监控解决方案
- AWS Config主要用于资源配置合规性检查，不适合实时部署状态监控
- 这种组合不是监控部署事件的最佳实践

**选项B：** 为CodePipeline和CodeDeploy实施Amazon EventBridge，创建AWS Lambda函数来评估代码部署问题，并创建Amazon SNS主题来通知利益相关者部署问题。
- EventBridge是AWS的事件总线服务，可以实时捕获CodePipeline和CodeDeploy的状态变化事件
- Lambda函数可以处理事件并执行自定义逻辑来评估部署问题
- SNS可以及时通知相关人员
- 这是一个完整的事件驱动监控解决方案

**选项C：** 实施AWS CloudTrail来记录CodePipeline和CodeDeploy API调用信息，创建AWS Lambda函数来评估代码部署问题，并创建Amazon SNS主题来通知利益相关者部署问题。
- CloudTrail主要用于API调用审计，记录的是API调用历史，不是实时状态变化
- 虽然有Lambda和SNS，但CloudTrail不适合实时监控部署状态
- 延迟性较高，不符合"减少解决时间"的要求

**选项D：** 为CodePipeline和CodeDeploy实施Amazon EventBridge，创建Amazon Inspector评估目标来评估代码部署问题，并创建Amazon SNS主题来通知利益相关者部署问题。
- EventBridge部分是正确的
- Amazon Inspector主要用于安全漏洞评估和应用程序安全分析，不适合监控部署流程问题
- Inspector不是用于部署状态监控的服务

 |  |  |  |
| 125 | A global company manages multiple AWS accounts by using AWS Control Tower. The company hosts internal applications and public
applications.
Each application team in the company has its own AWS account for application hosting. The accounts are consolidated in an organization in
AWS Organizations. One of the AWS Control Tower member accounts serves as a centralized DevOps account with CI/CD pipelines that
application teams use to deploy applications to their respective target AWS accounts. An IAM role for deployment exists in the centralized
DevOps account.
An application team is attempting to deploy its application to an Amazon Elastic Kubernetes Service (Amazon EKS) cluster in an application
AWS account. An IAM role for deployment exists in the application AWS account. The deployment is through an AWS CodeBuild project that is
set up in the centralized DevOps account. The CodeBuild project uses an IAM service role for CodeBuild. The deployment is failing with an
Unauthorized error during attempts to connect to the cross-account EKS cluster from CodeBuild. | A. Congure the application account’s deployment IAM role to have a trust relationship with the centralized DevOps account. Congure
the trust relationship to allow the sts:AssumeRole action. Congure the application account’s deployment IAM role to have the required
access to the EKS cluster. Congure the EKS cluster aws-auth CongMap to map the role to the appropriate system permissions.
B. Congure the centralized DevOps account’s deployment IAM role to have a trust relationship with the application account. Congure
the trust relationship to allow the sts:AssumeRole action. Congure the centralized DevOps account’s deployment IAM role to allow the
required access to CodeBuild.
C. Congure the centralized DevOps account’s deployment IAM role to have a trust relationship with the application account. Congure
the trust relationship to allow the sts:AssumeRoleWithSAML action. Congure the centralized DevOps account’s deployment IAM role to
allow the required access to CodeBuild.
D. Congure the application account’s deployment IAM role to have a trust relationship with the AWS Control Tower management account.
Congure the trust relationship to allow the sts:AssumeRole action. Congure the application account’s deployment IAM role to have the
required access to the EKS cluster. Congure the EKS cluster aws-auth CongMap to map the role to the appropriate system permissions. | 一家全球公司使用AWS Control Tower管理多个AWS账户。该公司托管内部应用程序和公共应用程序。

公司中的每个应用程序团队都有自己的AWS账户用于应用程序托管。这些账户在AWS Organizations中的一个组织中进行整合。其中一个AWS Control Tower成员账户作为集中式DevOps账户，配备了CI/CD管道，供应用程序团队用于将应用程序部署到各自的目标AWS账户。集中式DevOps账户中存在一个用于部署的IAM角色。

一个应用程序团队正在尝试将其应用程序部署到应用程序AWS账户中的Amazon Elastic Kubernetes Service (Amazon EKS)集群。应用程序AWS账户中存在一个用于部署的IAM角色。部署是通过在集中式DevOps账户中设置的AWS CodeBuild项目进行的。CodeBuild项目使用CodeBuild的IAM服务角色。在尝试从CodeBuild连接到跨账户EKS集群时，部署失败并出现未授权错误。

 | **选项A：** 配置应用程序账户的部署IAM角色与集中式DevOps账户建立信任关系。配置信任关系以允许sts:AssumeRole操作。配置应用程序账户的部署IAM角色具有对EKS集群的必要访问权限。配置EKS集群的aws-auth ConfigMap以将角色映射到适当的系统权限。

- **正确性：** 这是正确的跨账户访问配置方式
- **分析：** 建立了从DevOps账户到应用账户的信任关系，允许CodeBuild承担应用账户中的角色，并正确配置了EKS访问权限

**选项B：** 配置集中式DevOps账户的部署IAM角色与应用程序账户建立信任关系。配置信任关系以允许sts:AssumeRole操作。配置集中式DevOps账户的部署IAM角色允许对CodeBuild的必要访问。

- **正确性：** 信任关系方向错误
- **分析：** 信任关系应该是应用账户信任DevOps账户，而不是相反。且没有配置EKS访问权限

**选项C：** 配置集中式DevOps账户的部署IAM角色与应用程序账户建立信任关系。配置信任关系以允许sts:AssumeRoleWithSAML操作。配置集中式DevOps账户的部署IAM角色允许对CodeBuild的必要访问。

- **正确性：** 错误的操作类型和信任关系方向
- **分析：** 使用了sts:AssumeRoleWithSAML而不是sts:AssumeRole，且信任关系方向错误

**选项D：** 配置应用程序账户的部署IAM角色与AWS Control Tower管理账户建立信任关系。配置信任关系以允许sts:AssumeRole操作。配置应用程序账户的部署IAM角色具有对EKS集群的必要访问权限。配置EKS集群的aws-auth ConfigMap以将角色映射到适当的系统权限。

- **正确性：** 信任关系对象错误
- **分析：** 应该与DevOps账户建立信任关系，而不是与Control Tower管理账户

 |  |  |  |
| 126 | A highly regulated company has a policy that DevOps engineers should not log in to their Amazon EC2 instances except in emergencies. If a
DevOps engineer does log in, the security team must be notied within 15 minutes of the occurrence. | A. Install the Amazon Inspector agent on each EC2 instance. Subscribe to Amazon EventBridge notications. Invoke an AWS Lambda
function to check if a message is about user logins. If it is, send a notication to the security team using Amazon SNS.
B. Install the Amazon CloudWatch agent on each EC2 instance. Congure the agent to push all logs to Amazon CloudWatch Logs and set
up a CloudWatch metric lter that searches for user logins. If a login is found, send a notication to the security team using Amazon SNS.
C. Set up AWS CloudTrail with Amazon CloudWatch Logs. Subscribe CloudWatch Logs to Amazon Kinesis. Attach AWS Lambda to Kinesis
to parse and determine if a log contains a user login. If it does, send a notication to the security team using Amazon SNS.
D. Set up a script on each Amazon EC2 instance to push all logs to Amazon S3. Set up an S3 event to invoke an AWS Lambda function,
which invokes an Amazon Athena query to run. The Athena query checks for logins and sends the output to the security team using
Amazon SNS. |  |  |  |  |  |
| 127 | A company updated the AWS CloudFormation template for a critical business application. The stack update process failed due to an error in
the updated template, and AWS CloudFormation automatically began the stack rollback process. Later, a DevOps engineer discovered that the
application was still unavailable and that the stack was in the UPDATE_ROLLBACK_FAILED state. | A. Attach the AWSCloudFormationFullAccess IAM policy to the AWS CloudFormation role.
B. Automatically recover the stack resources by using AWS CloudFormation drift detection.
C. Issue a ContinueUpdateRollback command from the AWS CloudFormation console or the AWS CLI.
D. Manually adjust the resources to match the expectations of the stack.
E. Update the existing AWS CloudFormation stack by using the original template. |  |  |  |  |  |
| 128 | A development team manually builds an artifact locally and then places it in an Amazon S3 bucket. The application has a local cache that
must be cleared when a deployment occurs. The team runs a command to do this, downloads the artifact from Amazon S3, and unzips the
artifact to complete the deployment.
A DevOps team wants to migrate to a CI/CD process and build in checks to stop and roll back the deployment when a failure occurs. This
requires the team to track the progression of the deployment. | A. Allow developers to check the code into a code repository. Using Amazon EventBridge, on every pull into the main branch, invoke an
AWS Lambda function to build the artifact and store it in Amazon S3.
B. Create a custom script to clear the cache. Specify the script in the BeforeInstall lifecycle hook in the AppSpec le.
C. Create user data for each Amazon EC2 instance that contains the clear cache script. Once deployed, test the application. If it is not
successful, deploy it again.
D. Set up AWS CodePipeline to deploy the application. Allow developers to check the code into a code repository as a source for the
pipeline.
E. Use AWS CodeBuild to build the artifact and place it in Amazon S3. Use AWS CodeDeploy to deploy the artifact to Amazon EC2
instances. |  |  |  |  |  |
| 129 | A DevOps engineer is working on a project that is hosted on Amazon Linux and has failed a security review. The DevOps manager has been
asked to review the company buildspec.yaml le for an AWS CodeBuild project and provide recommendations. The buildspec.yaml le is
congured as follows: | A. Add a post-build command to remove the temporary les from the container before termination to ensure they cannot be seen by other
CodeBuild users.
B. Update the CodeBuild project role with the necessary permissions and then remove the AWS credentials from the environment variable.
C. Store the DB_PASSWORD as a SecureString value in AWS Systems Manager Parameter Store and then remove the DB_PASSWORD from
the environment variables.
D. Move the environment variables to the ‘db-deploy-bucket’ Amazon S3 bucket, add a prebuild stage to download, then export the
variables.
E. Use AWS Systems Manager run command versus scp and ssh commands directly to the instance. | 一名DevOps工程师正在处理一个托管在Amazon Linux上的项目，该项目未通过安全审查。DevOps经理被要求审查公司AWS CodeBuild项目的buildspec.yaml文件并提供建议。buildspec.yaml文件配置如下：

（注：题目中提到了buildspec.yaml文件的配置，但实际内容在题目中没有显示）

 | **A. 添加post-build命令，在容器终止前删除临时文件，确保其他CodeBuild用户无法看到这些文件。**
- 这是一个好的安全实践，可以防止敏感信息泄露
- 清理临时文件有助于提高安全性
- 但这可能不是最主要的安全问题

**B. 更新CodeBuild项目角色的必要权限，然后从环境变量中删除AWS凭证。**
- 这是非常重要的安全最佳实践
- 在环境变量中硬编码AWS凭证是严重的安全风险
- 应该使用IAM角色而不是硬编码凭证
- 这是常见的安全审查失败原因

**C. 将DB_PASSWORD作为SecureString值存储在AWS Systems Manager Parameter Store中，然后从环境变量中删除DB_PASSWORD。**
- 这是处理敏感信息的最佳实践
- Parameter Store的SecureString提供加密存储
- 避免在buildspec文件中明文存储密码
- 这也是常见的安全问题

**D. 将环境变量移动到'db-deploy-bucket' Amazon S3存储桶，添加prebuild阶段下载，然后导出变量。**
- 这不是一个好的安全实践
- 仅仅移动位置并不能解决安全问题
- S3存储桶中的敏感信息仍然存在风险

**E. 使用AWS Systems Manager run command替代直接使用scp和ssh命令连接实例。**
- 这是一个安全改进，但可能不是主要问题
- SSM Run Command提供更安全的实例管理方式
- 减少了直接SSH访问的安全风险

 |  |  |  |
| 130 | A company has a legacy application. A DevOps engineer needs to automate the process of building the deployable artifact for the legacy
application. The solution must store the deployable artifact in an existing Amazon S3 bucket for future deployments to reference. | A. Create a custom Docker image that contains all the dependencies for the legacy application. Store the custom Docker image in a new
Amazon Elastic Container Registry (Amazon ECR) repository. Congure a new AWS CodeBuild project to use the custom Docker image to
build the deployable artifact and to save the artifact to the S3 bucket.
B. Launch a new Amazon EC2 instance. Install all the dependencies for the legacy application on the EC2 instance. Use the EC2 instance
to build the deployable artifact and to save the artifact to the S3 bucket.
C. Create a custom EC2 Image Builder image. Install all the dependencies for the legacy application on the image. Launch a new Amazon
EC2 instance from the image. Use the new EC2 instance to build the deployable artifact and to save the artifact to the S3 bucket.
D. Create an Amazon Elastic Kubernetes Service (Amazon EKS) cluster with an AWS Fargate prole that runs in multiple Availability Zones.
Create a custom Docker image that contains all the dependencies for the legacy application. Store the custom Docker image in a new
Amazon Elastic Container Registry (Amazon ECR) repository. Use the custom Docker image inside the EKS cluster to build the deployable
artifact and to save the artifact to the S3 bucket. | 一家公司有一个遗留应用程序。DevOps工程师需要自动化构建该遗留应用程序可部署构件的过程。解决方案必须将可部署构件存储在现有的Amazon S3存储桶中，以供未来部署时引用。

 | **选项A：** 创建一个包含遗留应用程序所有依赖项的自定义Docker镜像。将自定义Docker镜像存储在新的Amazon Elastic Container Registry (Amazon ECR)仓库中。配置一个新的AWS CodeBuild项目，使用自定义Docker镜像来构建可部署构件并将构件保存到S3存储桶。
- **优点：** 使用AWS原生CI/CD服务CodeBuild，完全托管，无需维护基础设施；Docker镜像确保构建环境一致性；自动化程度高；成本效益好
- **缺点：** 无明显缺点

**选项B：** 启动一个新的Amazon EC2实例。在EC2实例上安装遗留应用程序的所有依赖项。使用EC2实例构建可部署构件并将构件保存到S3存储桶。
- **优点：** 简单直接
- **缺点：** 需要手动管理EC2实例；缺乏自动化；需要维护基础设施；成本较高；不符合DevOps最佳实践

**选项C：** 创建一个自定义EC2 Image Builder镜像。在镜像上安装遗留应用程序的所有依赖项。从该镜像启动新的Amazon EC2实例。使用新EC2实例构建可部署构件并将构件保存到S3存储桶。
- **优点：** 镜像标准化了构建环境
- **缺点：** 仍需管理EC2实例；自动化程度不够；增加了复杂性；成本较高

**选项D：** 创建一个Amazon Elastic Kubernetes Service (Amazon EKS)集群，配置在多个可用区运行的AWS Fargate配置文件。创建包含遗留应用程序所有依赖项的自定义Docker镜像。将自定义Docker镜像存储在新的Amazon Elastic Container Registry (Amazon ECR)仓库中。在EKS集群内使用自定义Docker镜像构建可部署构件并将构件保存到S3存储桶。
- **优点：** 高可用性和可扩展性
- **缺点：** 过度工程化；EKS集群成本高；复杂性高；对于简单的构建任务来说过于复杂

 |  |  |  |
| 131 | A company builds a container image in an AWS CodeBuild project by running Docker commands. After the container image is built, the
CodeBuild project uploads the container image to an Amazon S3 bucket. The CodeBuild project has an IAM service role that has permissions
to access the S3 bucket.
A DevOps engineer needs to replace the S3 bucket with an Amazon Elastic Container Registry (Amazon ECR) repository to store the container
images. The DevOps engineer creates an ECR private image repository in the same AWS Region of the CodeBuild project. The DevOps
engineer adjusts the IAM service role with the permissions that are necessary to work with the new ECR repository. The DevOps engineer also
places new repository information into the docker build command and the docker push command that are used in the buildspec.yml le.
When the CodeBuild project runs a build job, the job fails when the job tries to access the ECR repository. | A. Update the buildspec.yml le to log in to the ECR repository by using the aws ecr get-login-password AWS CLI command to obtain an
authentication token. Update the docker login command to use the authentication token to access the ECR repository.
B. Add an environment variable of type SECRETS_MANAGER to the CodeBuild project. In the environment variable, include the ARN of the
CodeBuild project's IAM service role. Update the buildspec.yml le to use the new environment variable to log in with the docker login
command to access the ECR repository.
C. Update the ECR repository to be a public image repository. Add an ECR repository policy that allows the IAM service role to have access.
D. Update the buildspec.yml le to use the AWS CLI to assume the IAM service role for ECR operations. Add an ECR repository policy that
allows the IAM service role to have access. |  |  |  |  |  |
| 132 | A company manually provisions IAM access for its employees. The company wants to replace the manual process with an automated process.
The company has an existing Active Directory system congured with an external SAML 2.0 identity provider (IdP).
The company wants employees to use their existing corporate credentials to access AWS. The groups from the existing Active Directory
system must be available for permission management in AWS Identity and Access Management (IAM). A DevOps engineer has completed the
initial conguration of AWS IAM Identity Center (AWS Single Sign-On) in the company’s AWS account. | A. Congure an external IdP as an identity source. Congure automatic provisioning of users and groups by using the SCIM protocol.
B. Congure AWS Directory Service as an identity source. Congure automatic provisioning of users and groups by using the SAML
protocol.
C. Congure an AD Connector as an identity source. Congure automatic provisioning of users and groups by using the SCIM protocol.
D. Congure an external IdP as an identity source Congure automatic provisioning of users and groups by using the SAML protocol. | 一家公司手动为其员工配置IAM访问权限。该公司希望用自动化流程替换手动流程。
该公司有一个现有的Active Directory系统，配置了外部SAML 2.0身份提供商(IdP)。
公司希望员工使用其现有的企业凭据来访问AWS。现有Active Directory系统中的组必须在AWS身份和访问管理(IAM)中可用于权限管理。DevOps工程师已经在公司的AWS账户中完成了AWS IAM Identity Center(AWS Single Sign-On)的初始配置。

 | **选项A：配置外部IdP作为身份源。使用SCIM协议配置用户和组的自动配置。**
- 正确。外部SAML 2.0 IdP可以作为身份源
- SCIM(System for Cross-domain Identity Management)协议专门用于自动化用户和组的配置
- 这是处理外部IdP与AWS IAM Identity Center集成的标准方法

**选项B：配置AWS Directory Service作为身份源。使用SAML协议配置用户和组的自动配置。**
- 不正确。题目明确提到已有外部SAML 2.0 IdP，不需要创建新的AWS Directory Service
- SAML协议主要用于身份验证，不是用于自动配置用户和组的协议

**选项C：配置AD Connector作为身份源。使用SCIM协议配置用户和组的自动配置。**
- 部分正确但不是最佳选择。AD Connector可以连接到现有AD，但题目强调的是外部SAML 2.0 IdP
- 虽然SCIM协议正确，但AD Connector主要用于直接连接本地AD，而不是通过SAML IdP

**选项D：配置外部IdP作为身份源。使用SAML协议配置用户和组的自动配置。**
- 身份源配置正确，但协议选择错误
- SAML协议用于身份验证和授权，不是用于自动配置用户和组的协议

 |  |  |  |
| 133 | A company is using AWS to run digital workloads. Each application team in the company has its own AWS account for application hosting. The
accounts are consolidated in an organization in AWS Organizations.
The company wants to enforce security standards across the entire organization. To avoid noncompliance because of security
misconguration, the company has enforced the use of AWS CloudFormation. A production support team can modify resources in the
production environment by using the AWS Management Console to troubleshoot and resolve application-related issues.
A DevOps engineer must implement a solution to identify in near real time any AWS service misconguration that results in noncompliance.
The solution must automatically remediate the issue within 15 minutes of identication. The solution also must track noncompliant resources
and events in a centralized dashboard with accurate timestamps. | A. Use CloudFormation drift detection to identify noncompliant resources. Use drift detection events from CloudFormation to invoke an
AWS Lambda function for remediation. Congure the Lambda function to publish logs to an Amazon CloudWatch Logs log group.
Congure an Amazon CloudWatch dashboard to use the log group for tracking.
B. Turn on AWS CloudTrail in the AWS accounts. Analyze CloudTrail logs by using Amazon Athena to identify noncompliant resources. Use
AWS Step Functions to track query results on Athena for drift detection and to invoke an AWS Lambda function for remediation. For
tracking, set up an Amazon QuickSight dashboard that uses Athena as the data source.
C. Turn on the conguration recorder in AWS Cong in all the AWS accounts to identify noncompliant resources. Enable AWS Security Hub
with the --no-enable-default-standards option in all the AWS accounts. Set up AWS Cong managed rules and custom rules. Set up
automatic remediation by using AWS Cong conformance packs. For tracking, set up a dashboard on Security Hub in a designated Security
Hub administrator account.
D. Turn on AWS CloudTrail in the AWS accounts. Analyze CloudTrail logs by using Amazon CloudWatch Logs to identify noncompliant
resources. Use CloudWatch Logs lters for drift detection. Use Amazon EventBridge to invoke the Lambda function for remediation.
Stream ltered CloudWatch logs to Amazon OpenSearch Service. Set up a dashboard on OpenSearch Service for tracking. | 一家公司正在使用AWS运行数字化工作负载。公司中的每个应用团队都有自己的AWS账户来托管应用程序。这些账户通过AWS Organizations整合在一个组织中。

公司希望在整个组织中强制执行安全标准。为了避免因安全配置错误而导致的不合规问题，公司已强制使用AWS CloudFormation。生产支持团队可以通过AWS管理控制台修改生产环境中的资源，以排查和解决应用程序相关问题。

DevOps工程师必须实施一个解决方案，以近实时识别任何导致不合规的AWS服务配置错误。该解决方案必须在识别后15分钟内自动修复问题。解决方案还必须在集中式仪表板中跟踪不合规资源和事件，并提供准确的时间戳。

 | **选项A：** 使用CloudFormation漂移检测来识别不合规资源，通过漂移检测事件调用Lambda函数进行修复，配置CloudWatch日志和仪表板进行跟踪。
- 问题：CloudFormation漂移检测不是实时的，需要手动触发，无法满足近实时监控要求
- 问题：无法检测到CloudFormation模板之外的资源配置问题
- 不适合此场景的要求

**选项B：** 启用CloudTrail，使用Athena分析日志识别不合规资源，用Step Functions跟踪查询结果并调用Lambda修复，使用QuickSight仪表板跟踪。
- 问题：Athena查询不是实时的，存在延迟
- 问题：CloudTrail主要记录API调用，不直接提供合规性检查
- 复杂度高，不是最佳解决方案

**选项C：** 在所有AWS账户中启用AWS Config配置记录器识别不合规资源，启用Security Hub，设置Config管理规则和自定义规则，使用Config一致性包进行自动修复，在Security Hub管理员账户中设置仪表板跟踪。
- 优势：AWS Config专门用于配置合规性监控，提供近实时检测
- 优势：Config规则可以自动检测配置漂移和不合规
- 优势：一致性包支持自动修复功能
- 优势：Security Hub提供集中式安全仪表板和跟踪
- 完全符合所有要求

**选项D：** 启用CloudTrail，使用CloudWatch Logs分析日志识别不合规资源，使用日志过滤器进行漂移检测，通过EventBridge调用Lambda修复，将过滤后的日志流式传输到OpenSearch Service并设置仪表板。
- 问题：CloudTrail和CloudWatch Logs不是专门的合规性监控工具
- 问题：需要复杂的日志分析来识别配置问题
- 问题：实现复杂，维护困难

 |  |  |  |
| 134 | A company uses AWS Organizations to manage its AWS accounts. The organization root has an OU that is named Environments. The
Environments OU has two child OUs that are named Development and Production, respectively.
The Environments OU and the child OUs have the default FullAWSAccess policy in place. A DevOps engineer plans to remove the
FullAWSAccess policy from the Development OU and replace the policy with a policy that allows all actions on Amazon EC2 resources. | A. All users in the Development OU will be allowed all API actions on all resources.
B. All users in the Development OU will be allowed all API actions on EC2 resources. All other API actions will be denied.
C. All users in the Development OU will be denied all API actions on all resources.
D. All users in the Development OU will be denied all API actions on EC2 resources. All other API actions will be allowed. | 一家公司使用AWS Organizations来管理其AWS账户。组织根有一个名为Environments的OU（组织单位）。Environments OU有两个子OU，分别名为Development和Production。Environments OU和子OU都配置了默认的FullAWSAccess策略。一名DevOps工程师计划从Development OU中移除FullAWSAccess策略，并用一个允许对Amazon EC2资源执行所有操作的策略来替换它。

2. | A. Development OU中的所有用户将被允许对所有资源执行所有API操作。
- 这个选项不正确。如果移除了FullAWSAccess策略并替换为仅允许EC2操作的策略，用户就不会再拥有对所有资源的完全访问权限。

B. Development OU中的所有用户将被允许对EC2资源执行所有API操作。所有其他API操作将被拒绝。
- 这个选项正确。当移除FullAWSAccess策略并替换为仅允许EC2操作的策略时，用户只能对EC2资源执行操作，其他服务的访问将被限制。

C. Development OU中的所有用户将被拒绝对所有资源执行所有API操作。
- 这个选项不正确。题目明确说明会用一个允许EC2操作的策略来替换，而不是完全拒绝所有操作。

D. Development OU中的所有用户将被拒绝对EC2资源执行所有API操作。所有其他API操作将被允许。
- 这个选项不正确。这与题目描述的情况完全相反，新策略是允许EC2操作，而不是拒绝EC2操作。

3. | B |  |  |
| 135 | A company is examining its disaster recovery capability and wants the ability to switch over its daily operations to a secondary AWS Region.
The company uses AWS CodeCommit as a source control tool in the primary Region.
A DevOps engineer must provide the capability for the company to develop code in the secondary Region. If the company needs to use the
secondary Region, developers can add an additional remote URL to their local Git conguration. | A. Create a CodeCommit repository in the secondary Region. Create an AWS CodeBuild project to perform a Git mirror operation of the
primary Region's CodeCommit repository to the secondary Region's CodeCommit repository. Create an AWS Lambda function that invokes
the CodeBuild project. Create an Amazon EventBridge rule that reacts to merge events in the primary Region's CodeCommit repository.
Congure the EventBridge rule to invoke the Lambda function.
B. Create an Amazon S3 bucket in the secondary Region. Create an AWS Fargate task to perform a Git mirror operation of the primary
Region's CodeCommit repository and copy the result to the S3 bucket. Create an AWS Lambda function that initiates the Fargate task.
Create an Amazon EventBridge rule that reacts to merge events in the CodeCommit repository. Congure the EventBridge rule to invoke
the Lambda function.
C. Create an AWS CodeArtifact repository in the secondary Region. Create an AWS CodePipeline pipeline that uses the primary Region’s
CodeCommit repository for the source action. Create a cross-Region stage in the pipeline that packages the CodeCommit repository
contents and stores the contents in the CodeArtifact repository when a pull request is merged into the CodeCommit repository.
D. Create an AWS Cloud9 environment and a CodeCommit repository in the secondary Region. Congure the primary Region's CodeCommit
repository as a remote repository in the AWS Cloud9 environment. Connect the secondary Region's CodeCommit repository to the AWS
Cloud9 environment. |  |  |  |  |  |
| 136 | A DevOps team is merging code revisions for an application that uses an Amazon RDS Multi-AZ DB cluster for its production database. The
DevOps team uses continuous integration to periodically verify that the application works. The DevOps team needs to test the changes before
the changes are deployed to the production database. | A. Use a buildspec le in AWS CodeBuild to restore the DB cluster from a snapshot of the production database, run integration tests, and
drop the restored database after verication.
B. Deploy the application to production. Congure an audit log of data control language (DCL) operations to capture database activities to
perform if verication fails.
C. Create a snapshot of the DB cluster before deploying the application. Use the Update requires:Replacement property on the DB
instance in AWS CloudFormation to deploy the application and apply the changes.
D. Ensure that the DB cluster is a Multi-AZ deployment. Deploy the application with the updates. Fail over to the standby instance if
verication fails. | 一个DevOps团队正在为一个使用Amazon RDS Multi-AZ数据库集群作为生产数据库的应用程序合并代码修订。DevOps团队使用持续集成来定期验证应用程序是否正常工作。DevOps团队需要在将更改部署到生产数据库之前测试这些更改。

 | **选项A：** 在AWS CodeBuild中使用buildspec文件从生产数据库的快照恢复数据库集群，运行集成测试，并在验证后删除恢复的数据库。
- **正确性：高** - 这是一个标准的测试最佳实践，创建独立的测试环境，使用生产数据的快照进行测试，测试完成后清理资源。这样可以确保测试环境与生产环境数据一致，同时不影响生产环境。

**选项B：** 将应用程序部署到生产环境。配置数据控制语言(DCL)操作的审计日志来捕获数据库活动，以便在验证失败时执行回滚操作。
- **正确性：低** - 直接在生产环境中测试是非常危险的做法，违反了DevOps最佳实践。即使有审计日志，也无法保证完全回滚所有更改，可能对生产数据造成不可逆的损害。

**选项C：** 在部署应用程序之前创建数据库集群的快照。在AWS CloudFormation中使用数据库实例的Update requires:Replacement属性来部署应用程序并应用更改。
- **正确性：中等** - 虽然创建快照是好的做法，但使用CloudFormation的Replacement属性会导致数据库实例被完全替换，这会造成生产环境的停机时间，不适合生产环境的持续部署。

**选项D：** 确保数据库集群是Multi-AZ部署。部署带有更新的应用程序。如果验证失败，故障转移到备用实例。
- **正确性：低** - Multi-AZ的备用实例是为了高可用性设计的，不是为了回滚应用程序更改。备用实例会同步复制主实例的所有更改，包括可能有问题的更改，因此无法用作回滚机制。

 |  |  |  |
| 137 | A company manages a multi-tenant environment in its VPC and has congured Amazon GuardDuty for the corresponding AWS account. The
company sends all GuardDuty ndings to AWS Security Hub.
Trac from suspicious sources is generating a large number of ndings. A DevOps engineer needs to implement a solution to automatically
deny trac across the entire VPC when GuardDuty discovers a new suspicious source. | A. Create a GuardDuty threat list. Congure GuardDuty to reference the list. Create an AWS Lambda function that will update the threat
list. Congure the Lambda function to run in response to new Security Hub ndings that come from GuardDuty.
B. Congure an AWS WAF web ACL that includes a custom rule group. Create an AWS Lambda function that will create a block rule in the
custom rule group. Congure the Lambda function to run in response to new Security Hub ndings that come from GuardDuty.
C. Congure a rewall in AWS Network Firewall. Create an AWS Lambda function that will create a Drop action rule in the rewall policy.
Congure the Lambda function to run in response to new Security Hub ndings that come from GuardDuty.
D. Create an AWS Lambda function that will create a GuardDuty suppression rule. Congure the Lambda function to run in response to new
Security Hub ndings that come from GuardDuty. | 一家公司在其VPC中管理多租户环境，并为相应的AWS账户配置了Amazon GuardDuty。该公司将所有GuardDuty发现的问题发送到AWS Security Hub。

来自可疑来源的流量正在产生大量发现结果。DevOps工程师需要实施一个解决方案，当GuardDuty发现新的可疑来源时，自动拒绝整个VPC中的流量。

 | **选项A：创建GuardDuty威胁列表**
- 创建GuardDuty威胁列表并配置GuardDuty引用该列表
- 创建AWS Lambda函数更新威胁列表
- 配置Lambda函数响应来自GuardDuty的新Security Hub发现
- **问题**：GuardDuty威胁列表主要用于检测，而不是主动阻止流量。它只是增强检测能力，不能直接阻止网络流量。

**选项B：配置AWS WAF web ACL**
- 配置包含自定义规则组的AWS WAF web ACL
- 创建Lambda函数在自定义规则组中创建阻止规则
- **问题**：AWS WAF主要保护web应用程序（ALB、CloudFront、API Gateway），不能保护整个VPC的所有流量类型。题目要求保护"整个VPC"。

**选项C：配置AWS Network Firewall**
- 在AWS Network Firewall中配置防火墙
- 创建Lambda函数在防火墙策略中创建Drop动作规则
- **优势**：Network Firewall可以保护整个VPC的网络流量，支持第3-7层过滤，可以基于IP地址、端口、协议等创建阻止规则。

**选项D：创建GuardDuty抑制规则**
- 创建Lambda函数创建GuardDuty抑制规则
- **问题**：抑制规则只是阻止GuardDuty报告某些发现，并不阻止实际的网络流量。这不能解决安全问题，只是隐藏了警报。

 |  |  |  |
| 138 | A company uses AWS Secrets Manager to store a set of sensitive API keys that an AWS Lambda function uses. When the Lambda function is
invoked the Lambda function retrieves the API keys and makes an API call to an external service. The Secrets Manager secret is encrypted
with the default AWS Key Management Service (AWS KMS) key.
A DevOps engineer needs to update the infrastructure to ensure that only the Lambda function’s execution role can access the values in
Secrets Manager. The solution must apply the principle of least privilege. | A. Update the default KMS key for Secrets Manager to allow only the Lambda function’s execution role to decrypt
B. Create a KMS customer managed key that trusts Secrets Manager and allows the Lambda function's execution role to decrypt. Update
Secrets Manager to use the new customer managed key
C. Create a KMS customer managed key that trusts Secrets Manager and allows the account's root principal to decrypt. Update Secrets
Manager to use the new customer managed key
D. Ensure that the Lambda function’s execution role has the KMS permissions scoped on the resource level. Congure the permissions so
that the KMS key can encrypt the Secrets Manager secret
E. Remove all KMS permissions from the Lambda function’s execution role | 一家公司使用AWS Secrets Manager来存储一组敏感的API密钥，这些密钥被AWS Lambda函数使用。当Lambda函数被调用时，Lambda函数会检索API密钥并向外部服务发起API调用。Secrets Manager密钥使用默认的AWS Key Management Service (AWS KMS)密钥进行加密。

DevOps工程师需要更新基础设施，以确保只有Lambda函数的执行角色能够访问Secrets Manager中的值。解决方案必须应用最小权限原则。

 | **A. 更新Secrets Manager的默认KMS密钥，只允许Lambda函数的执行角色进行解密**
- 不正确。默认的AWS托管KMS密钥无法修改其密钥策略，用户无法自定义访问权限。

**B. 创建一个信任Secrets Manager并允许Lambda函数执行角色解密的KMS客户托管密钥。更新Secrets Manager使用新的客户托管密钥**
- 正确。这是最佳实践方案：
  - 创建客户托管的KMS密钥可以完全控制访问权限
  - 密钥策略可以精确指定只有特定的Lambda执行角色可以解密
  - 符合最小权限原则
  - Secrets Manager需要被信任才能使用该密钥进行加密操作

**C. 创建一个信任Secrets Manager并允许账户根主体解密的KMS客户托管密钥。更新Secrets Manager使用新的客户托管密钥**
- 不正确。允许账户根主体访问违反了最小权限原则，给予了过多的权限。

**D. 确保Lambda函数的执行角色具有资源级别的KMS权限。配置权限使KMS密钥能够加密Secrets Manager密钥**
- 不正确。这个选项描述混乱，而且没有解决核心问题。仅仅给Lambda角色KMS权限不足以限制其他角色的访问。

**E. 从Lambda函数的执行角色中移除所有KMS权限**
- 不正确。这样做会导致Lambda函数无法解密Secrets Manager中的密钥，功能将完全失效。

 |  |  |  |
| 139 | A company's DevOps engineer is creating an AWS Lambda function to process notications from an Amazon Simple Notication Service
(Amazon SNS) topic. The Lambda function will process the notication messages and will write the contents of the notication messages to
an Amazon RDS Multi-AZ DB instance.
During testing, a database administrator accidentally shut down the DB instance. While the database was down the company lost several of
the SNS notication messages that were delivered during that time.
The DevOps engineer needs to prevent the loss of notication messages in the future. | A. Replace the RDS Multi-AZ DB instance with an Amazon DynamoDB table.
B. Congure an Amazon Simple Queue Service (Amazon SQS) queue as a destination of the Lambda function.
C. Congure an Amazon Simple Queue Service (Amazon SQS) dead-letter queue for the SNS topic.
D. Subscribe an Amazon Simple Queue Service (Amazon SQS) queue to the SNS topic. Congure the Lambda function to process
messages from the SQS queue.
E. Replace the SNS topic with an Amazon EventBridge event bus. Congure an EventBridge rule on the new event bus to invoke the
Lambda function for each event. | 一家公司的DevOps工程师正在创建一个AWS Lambda函数来处理来自Amazon Simple Notification Service (Amazon SNS)主题的通知。Lambda函数将处理通知消息并将通知消息的内容写入Amazon RDS Multi-AZ数据库实例。

在测试期间，数据库管理员意外关闭了数据库实例。当数据库宕机时，公司丢失了在此期间传递的几条SNS通知消息。

DevOps工程师需要防止将来通知消息的丢失。

 | **A. 将RDS Multi-AZ数据库实例替换为Amazon DynamoDB表。**
- 不正确。虽然DynamoDB具有更高的可用性，但这并不能解决根本问题。如果Lambda函数在处理消息时失败（无论是因为DynamoDB问题还是其他原因），消息仍然会丢失。这个方案没有提供消息持久化和重试机制。

**B. 配置Amazon Simple Queue Service (Amazon SQS)队列作为Lambda函数的目标。**
- 不正确。这个选项描述不清楚且在架构上不合理。SQS队列通常是Lambda函数的事件源，而不是目标。这种配置无法解决消息丢失问题。

**C. 为SNS主题配置Amazon Simple Queue Service (Amazon SQS)死信队列。**
- 不正确。SNS主题本身不能直接配置死信队列。死信队列是为SQS队列或Lambda函数配置的，用于处理失败的消息。

**D. 将Amazon Simple Queue Service (Amazon SQS)队列订阅到SNS主题。配置Lambda函数从SQS队列处理消息。**
- 正确。这是最佳解决方案。通过在SNS和Lambda之间添加SQS队列，可以实现消息的持久化存储。如果Lambda函数处理失败，消息会保留在SQS队列中并可以重试。SQS提供了消息持久性、重试机制和可见性超时等特性。

**E. 将SNS主题替换为Amazon EventBridge事件总线。在新的事件总线上配置EventBridge规则来为每个事件调用Lambda函数。**
- 不正确。虽然EventBridge是一个强大的事件路由服务，但它与SNS一样，在Lambda函数失败时不会自动重试或持久化消息。这种替换并不能解决消息丢失的根本问题。

 |  |  |  |
| 140 | A company has an application that runs on Amazon EC2 instances. The company uses an AWS CodePipeline pipeline to deploy the application
into multiple AWS Regions. The pipeline is congured with a stage for each Region. Each stage contains an AWS CloudFormation action for
each Region.
When the pipeline deploys the application to a Region, the company wants to conrm that the application is in a healthy state before the
pipeline moves on to the next Region. Amazon Route 53 record sets are congured for the application in each Region. A DevOps engineer
creates a Route 53 health check that is based on an Amazon CloudWatch alarm for each Region where the application is deployed. | A. Create an AWS Step Functions workow to check the state of the CloudWatch alarm. Congure the Step Functions workow to exit with
an error if the alarm is in the ALARM state. Create a new stage in the pipeline between each Region deployment stage. In each new stage,
include an action to invoke the Step Functions workow.
B. Congure an AWS CodeDeploy application to deploy a CloudFormation template with automatic rollback. Congure the CloudWatch
alarm as the instance health check for the CodeDeploy application. Remove the CloudFormation actions from the pipeline. Create a
CodeDeploy action in the pipeline stage for each Region.
C. Create a new pipeline stage for each Region where the application is deployed. Congure a CloudWatch alarm action for the new stage
to check the state of the CloudWatch alarm and to exit with an error if the alarm is in the ALARM state
D. Congure the CloudWatch agent on the EC2 instances to report the application status to the Route 53 health check. Create a new
pipeline stage for each Region where the application is deployed. Congure a CloudWatch alarm action to exit with an error if the
CloudWatch alarm is in the ALARM state. | 一家公司有一个运行在Amazon EC2实例上的应用程序。该公司使用AWS CodePipeline流水线将应用程序部署到多个AWS区域。流水线配置了每个区域对应的阶段。每个阶段包含针对每个区域的AWS CloudFormation操作。

当流水线将应用程序部署到一个区域时，公司希望在流水线继续到下一个区域之前确认应用程序处于健康状态。Amazon Route 53记录集已为每个区域的应用程序配置。DevOps工程师为部署应用程序的每个区域创建了基于Amazon CloudWatch告警的Route 53健康检查。

 | **选项A：** 创建AWS Step Functions工作流来检查CloudWatch告警状态。配置Step Functions工作流在告警处于ALARM状态时退出并报错。在每个区域部署阶段之间创建新的流水线阶段。在每个新阶段中，包含调用Step Functions工作流的操作。
- **分析：** 这是一个可行的解决方案。Step Functions可以有效地检查CloudWatch告警状态，并在应用程序不健康时阻止流水线继续执行。这种方法提供了良好的控制流和错误处理机制。

**选项B：** 配置AWS CodeDeploy应用程序来部署带有自动回滚的CloudFormation模板。将CloudWatch告警配置为CodeDeploy应用程序的实例健康检查。从流水线中移除CloudFormation操作。在每个区域的流水线阶段中创建CodeDeploy操作。
- **分析：** 这个方案改变了整个部署架构，从CloudFormation切换到CodeDeploy。虽然CodeDeploy提供健康检查功能，但这需要重新设计现有的部署流程，复杂度较高且不必要。

**选项C：** 为部署应用程序的每个区域创建新的流水线阶段。为新阶段配置CloudWatch告警操作来检查CloudWatch告警状态，如果告警处于ALARM状态则退出并报错。
- **分析：** CodePipeline本身没有直接的"CloudWatch告警操作"。这个选项描述的功能在CodePipeline中不存在，因此不可行。

**选项D：** 在EC2实例上配置CloudWatch代理来向Route 53健康检查报告应用程序状态。为部署应用程序的每个区域创建新的流水线阶段。配置CloudWatch告警操作在CloudWatch告警处于ALARM状态时退出并报错。
- **分析：** 与选项C类似，CodePipeline没有直接的CloudWatch告警操作。此外，CloudWatch代理通常不直接与Route 53健康检查集成。

 | A |  |  |
| 141 | A company plans to use Amazon CloudWatch to monitor its Amazon EC2 instances. The company needs to stop EC2 instances when the
average of the NetworkPacketsIn metric is less than 5 for at least 3 hours in a 12-hour time window. The company must evaluate the metric
every hour. The EC2 instances must continue to run if there is missing data for the NetworkPacketsIn metric during the evaluation period.
A DevOps engineer creates a CloudWatch alarm for the NetworkPacketsIn metric. The DevOps engineer congures a threshold value of 5 and
an evaluation period of 1 hour. | A. Congure the Datapoints to Alarm value to be 3 out of 12. Congure the alarm to treat missing data as breaching the threshold. Add an
AWS Systems Manager action to stop the instance when the alarm enters the ALARM state.
B. Congure the Datapoints to Alarm value to be 3 out of 12. Congure the alarm to treat missing data as not breaching the threshold.
Add an EC2 action to stop the instance when the alarm enters the ALARM state.
C. Congure the Datapoints to Alarm value to be 9 out of 12. Congure the alarm to treat missing data as breaching the threshold. Add an
EC2 action to stop the instance when the alarm enters the ALARM state.
D. Congure the Datapoints to Alarm value to be 9 out of 12. Congure the alarm to treat missing data as not breaching the threshold.
Add an AWS Systems Manager action to stop the instance when the alarm enters the ALARM state. | 一家公司计划使用Amazon CloudWatch来监控其Amazon EC2实例。公司需要在12小时时间窗口内，当NetworkPacketsIn指标的平均值连续至少3小时小于5时停止EC2实例。公司必须每小时评估一次该指标。如果在评估期间NetworkPacketsIn指标数据缺失，EC2实例必须继续运行。

一位DevOps工程师为NetworkPacketsIn指标创建了一个CloudWatch告警。该工程师配置了阈值为5，评估周期为1小时。

 | **选项A：**
- 配置"Datapoints to Alarm"值为3 out of 12
- 配置告警将缺失数据视为违反阈值
- 使用AWS Systems Manager操作停止实例
- ❌ 错误：将缺失数据视为违反阈值与需求相反（需求要求缺失数据时实例继续运行）

**选项B：**
- 配置"Datapoints to Alarm"值为3 out of 12
- 配置告警将缺失数据视为不违反阈值
- 使用EC2操作停止实例
- ✅ 正确：3 out of 12意味着在12个数据点中有3个违反阈值就触发告警，符合"至少3小时"的要求；缺失数据不违反阈值符合需求；EC2操作可以直接停止实例

**选项C：**
- 配置"Datapoints to Alarm"值为9 out of 12
- 配置告警将缺失数据视为违反阈值
- 使用EC2操作停止实例
- ❌ 错误：9 out of 12意味着需要9小时违反阈值才触发，不符合"至少3小时"的要求；缺失数据处理方式错误

**选项D：**
- 配置"Datapoints to Alarm"值为9 out of 12
- 配置告警将缺失数据视为不违反阈值
- 使用AWS Systems Manager操作停止实例
- ❌ 错误：9 out of 12不符合"至少3小时"的要求

 |  |  |  |
| 142 | A company manages 500 AWS accounts that are in an organization in AWS Organizations. The company discovers many unattached Amazon
Elastic Block Store (Amazon EBS) volumes in all the accounts. The company wants to automatically tag the unattached EBS volumes for
investigation.
A DevOps engineer needs to deploy an AWS Lambda function to all the AWS accounts. The Lambda function must run every 30 minutes to tag
all the EBS volumes that have been unattached for a period of 7 days or more. | A. Congure a delegated administrator account for the organization. Create an AWS CloudFormation template that contains the Lambda
function. Use CloudFormation StackSets to deploy the CloudFormation template from the delegated administrator account to all the
member accounts in the organization. Create an Amazon EventBridge event bus in the delegated administrator account to invoke the
Lambda function in each member account every 30 minutes.
B. Create a cross-account IAM role in the organization's member accounts. Attach the AWSLambda_FullAccess policy and the
AWSCloudFormationFullAccess policy to the role. Create an AWS CloudFormation template that contains the Lambda function and an
Amazon EventBridge scheduled rule to invoke the Lambda function every 30 minutes. Create a custom script in the organization’s
management account that assumes the role and deploys the CloudFormation template to the member accounts.
C. Congure a delegated administrator account for the organization. Create an AWS CloudFormation template that contains the Lambda
function and an Amazon EventBridge scheduled rule to invoke the Lambda function every 30 minutes. Use CloudFormation StackSets to
deploy the CloudFormation template from the delegated administrator account to all the member accounts in the organization
D. Create a cross-account IAM role in the organization's member accounts. Attach the AmazonS3FullAccess policy and the
AWSCodeDeployDeployerAccess policy to the role. Use AWS CodeDeploy to assume the role to deploy the Lambda function from the
organization's management account. Congure an Amazon EventBridge scheduled rule in the member accounts to invoke the Lambda
function every 30 minutes. | 一家公司管理着AWS Organizations中的500个AWS账户。公司发现所有账户中都有许多未挂载的Amazon Elastic Block Store (Amazon EBS)卷。公司希望自动为这些未挂载的EBS卷打标签以便调查。

DevOps工程师需要将AWS Lambda函数部署到所有AWS账户中。Lambda函数必须每30分钟运行一次，为所有未挂载7天或更长时间的EBS卷打标签。

 | **选项A：** 
- 配置委托管理员账户，使用CloudFormation StackSets部署Lambda函数 ✓
- 在委托管理员账户中创建EventBridge事件总线来调用各成员账户中的Lambda函数 ✗
- 问题：跨账户EventBridge调用复杂且不是最佳实践，应该在每个账户内部配置调度规则

**选项B：**
- 创建跨账户IAM角色，附加过于宽泛的权限策略 ✗
- 使用自定义脚本从管理账户部署 ✗
- 问题：权限过大（FullAccess策略），使用自定义脚本而非AWS原生服务不是最佳实践

**选项C：**
- 配置委托管理员账户 ✓
- CloudFormation模板包含Lambda函数和EventBridge调度规则 ✓
- 使用CloudFormation StackSets从委托管理员账户部署到所有成员账户 ✓
- 每个账户内部都有自己的调度规则，架构简洁高效

**选项D：**
- 使用CodeDeploy部署Lambda函数 ✗
- 附加不相关的权限策略（S3FullAccess, CodeDeployDeployerAccess） ✗
- 问题：CodeDeploy不是部署Lambda函数的最佳选择，权限策略不匹配需求

 | C |  |  |
| 143 | A company's production environment uses an AWS CodeDeploy blue/green deployment to deploy an application. The deployment incudes
Amazon EC2 Auto Scaling groups that launch instances that run Amazon Linux 2.
A working appspec.yml le exists in the code repository and contains the following text:
A DevOps engineer needs to ensure that a script downloads and installs a license le onto the instances before the replacement instances
start to handle request trac. The DevOps engineer adds a hooks section to the appspec.yml le. | A. AfterBlockTrac
B. BeforeBlockTrac
C. BeforeInstall
D. DownloadBundle | 一家公司的生产环境使用AWS CodeDeploy蓝/绿部署来部署应用程序。该部署包括Amazon EC2 Auto Scaling组，这些组启动运行Amazon Linux 2的实例。

代码仓库中存在一个可用的appspec.yml文件并包含以下文本：

一位DevOps工程师需要确保在替换实例开始处理请求流量之前，有一个脚本下载并安装许可证文件到实例上。该DevOps工程师向appspec.yml文件添加了一个hooks部分。

 | **A. AfterBlockTraffic**
- 这个钩子在流量被阻止**之后**执行
- 此时实例已经停止接收流量，不适合在实例开始处理流量前安装许可证文件
- 时机不正确

**B. BeforeBlockTraffic**
- 这个钩子在阻止流量**之前**执行
- 主要用于在停止向旧实例发送流量前执行清理任务
- 不适合用于新实例的初始化设置

**C. BeforeInstall**
- 这个钩子在安装应用程序**之前**执行
- 适合用于准备实例环境，如下载和安装许可证文件
- 在蓝/绿部署中，这发生在新实例创建后但应用程序部署前
- 确保许可证文件在应用程序启动前就位

**D. DownloadBundle**
- 这不是CodeDeploy中的标准钩子名称
- CodeDeploy会自动处理应用程序包的下载
- 这是一个无效选项

 |  |  |  |
| 144 | A company has an application that includes AWS Lambda functions. The Lambda functions run Python code that is stored in an AWS
CodeCommit repository. The company has recently experienced failures in the production environment because of an error in the Python
code. An engineer has written unit tests for the Lambda functions to help avoid releasing any future defects into the production environment.
The company's DevOps team needs to implement a solution to integrate the unit tests into an existing AWS CodePipeline pipeline. The
solution must produce reports about the unit tests for the company to view. | A. Associate the CodeCommit repository with Amazon CodeGuru Reviewer. Create a new AWS CodeBuild project. In the CodePipeline
pipeline, congure a test stage that uses the new CodeBuild project. Create a buildspec.yml le in the CodeCommit repository. In the
buildspec yml le, dene the actions to run a CodeGuru review.
B. Create a new AWS CodeBuild project. In the CodePipeline pipeline, congure a test stage that uses the new CodeBuild project. Create a
CodeBuild report group. Create a buildspec.yml le in the CodeCommit repository. In the buildspec.yml le, dene the actions to run the
unit tests with an output of JUNITXML in the build phase section. Congure the test reports to be uploaded to the new CodeBuild report
group.
C. Create a new AWS CodeArtifact repository. Create a new AWS CodeBuild project. In the CodePipeline pipeline, congure a test stage
that uses the new CodeBuild project. Create an appspec.yml le in the original CodeCommit repository. In the appspec.yml le, dene the
actions to run the unit tests with an output of CUCUMBERJSON in the build phase section. Congure the tests reports to be sent to the
new CodeArtifact repository.
D. Create a new AWS CodeBuild project. In the CodePipeline pipeline, congure a test stage that uses the new CodeBuild project. Create a
new Amazon S3 bucket. Create a buildspec.yml le in the CodeCommit repository. In the buildspec yml le, dene the actions to run the
unit tests with an output of HTML in the phases section. In the reports section, upload the test reports to the S3 bucket. | 一家公司有一个包含AWS Lambda函数的应用程序。Lambda函数运行存储在AWS CodeCommit仓库中的Python代码。该公司最近在生产环境中遇到了由于Python代码错误导致的故障。一名工程师为Lambda函数编写了单元测试，以帮助避免将任何未来的缺陷发布到生产环境中。公司的DevOps团队需要实施一个解决方案，将单元测试集成到现有的AWS CodePipeline管道中。该解决方案必须生成关于单元测试的报告供公司查看。

 | **选项A：**
- 使用Amazon CodeGuru Reviewer进行代码审查
- 问题：CodeGuru Reviewer主要用于静态代码分析和代码质量审查，而不是运行单元测试
- CodeGuru不会执行实际的单元测试，也不会生成单元测试报告
- 不符合题目要求的"运行单元测试并生成报告"

**选项B：**
- 创建新的CodeBuild项目并配置测试阶段
- 创建CodeBuild报告组用于收集测试报告
- 使用buildspec.yml文件定义单元测试执行
- 输出JUNITXML格式，这是标准的测试报告格式
- 将测试报告上传到CodeBuild报告组，这是AWS原生的测试报告功能
- 完全符合要求

**选项C：**
- 使用CodeArtifact仓库（用于包管理，不适合测试报告）
- 使用appspec.yml文件（这是CodeDeploy的配置文件，不是CodeBuild的）
- CUCUMBERJSON格式主要用于BDD测试，对于Python单元测试不是最佳选择
- CodeArtifact不是用来存储测试报告的服务

**选项D：**
- 使用S3存储测试报告
- HTML输出格式可以工作，但不如标准的测试报告格式
- 虽然技术上可行，但不如使用CodeBuild原生报告功能优雅
- 缺乏集成的报告查看体验

 |  |  |  |
| 145 | A company manages multiple AWS accounts in AWS Organizations. The company’s security policy states that AWS account root user
credentials for member accounts must not be used. The company monitors access to the root user credentials.
A recent alert shows that the root user in a member account launched an Amazon EC2 instance. A DevOps engineer must create an SCP at the
organization's root level that will prevent the root user in member accounts from making any AWS service API calls. | A. 
B. 
C. 
D.  | 一家公司在AWS Organizations中管理多个AWS账户。公司的安全策略规定不得使用成员账户的AWS账户根用户凭证。公司监控对根用户凭证的访问。
最近的一个警报显示，成员账户中的根用户启动了一个Amazon EC2实例。DevOps工程师必须在组织的根级别创建一个SCP（服务控制策略），以防止成员账户中的根用户进行任何AWS服务API调用。

 | 由于选项内容缺失，我无法逐一分析具体选项。但基于题目要求，正确的SCP策略应该：

**正确的SCP策略特征：**
- 使用Deny效果来阻止根用户的API调用
- 在Condition中使用`aws:PrincipalType`条件键
- 值应该是"Root"来特指根用户
- 应该拒绝所有AWS服务的操作（使用通配符"*"）

**典型的正确SCP策略示例：**
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Principal": "*",
      "Action": "*",
      "Resource": "*",
      "Condition": {
        "StringEquals": {
          "aws:PrincipalType": "Root"
        }
      }
    }
  ]
}
```

**错误的策略可能包括：**
- 使用错误的条件键（如`aws:userid`而不是`aws:PrincipalType`）
- 使用Allow而不是Deny效果
- 条件值不正确（如使用"root"而不是"Root"）
- 缺少必要的条件语句

 |  |  |  |
| 146 | A company uses AWS and has a VPC that contains critical compute infrastructure with predictable trac patterns. The company has
congured VPC ow logs that are published to a log group in Amazon CloudWatch Logs.
The company's DevOps team needs to congure a monitoring solution for the VPC ow logs to identify anomalies in network trac to the VPC
over time. If the monitoring solution detects an anomaly, the company needs the ability to initiate a response to the anomaly.
How should the DevOps team congure the monitoring solution to meet these requirements? | A. Create an Amazon Kinesis data stream. Subscribe the log group to the data stream. Congure Amazon Kinesis Data Analytics to detect
log anomalies in the data stream. Create an AWS Lambda function to use as the output of the data stream. Congure the Lambda
function to write to the default Amazon EventBridge event bus in the event of an anomaly nding.
B. Create an Amazon Kinesis Data Firehose delivery stream that delivers events to an Amazon S3 bucket. Subscribe the log group to the
delivery stream. Congure Amazon Lookout for Metrics to monitor the data in the S3 bucket for anomalies. Create an AWS Lambda
function to run in response to Lookout for Metrics anomaly ndings. Congure the Lambda function to publish to the default Amazon
EventBridge event bus.
C. Create an AWS Lambda function to detect anomalies. Congure the Lambda function to publish an event to the default Amazon
EventBridge event bus if the Lambda function detects an anomaly. Subscribe the Lambda function to the log group.
D. Create an Amazon Kinesis data stream. Subscribe the log group to the data stream. Create an AWS Lambda function to detect log
anomalies. Congure the Lambda function to write to the default Amazon EventBridge event bus if the Lambda function detects an
anomaly. Set the Lambda function as the processor for the data stream. |  |  |  |  |  |
| 147 | AnyCompany is using AWS Organizations to create and manage multiple AWS accounts. AnyCompany recently acquired a smaller company,
Example Corp. During the acquisition process, Example Corp's single AWS account joined AnyCompany's management account through an
Organizations invitation. AnyCompany moved the new member account under an OU that is dedicated to Example Corp.
AnyCompany's DevOps engineer has an IAM user that assumes a role that is named OrganizationAccountAccessRole to access member
accounts. This role is congured with a full access policy. When the DevOps engineer tries to use the AWS Management Console to assume
the role in Example Corp's new member account, the DevOps engineer receives the following error message: "Invalid information in one or
more elds. Check your information or contact your administrator." | A. In the management account, grant the DevOps engineer's IAM user permission to assume the OrganizationAccountAccessRole IAM role
in the new member account.
B. In the management account, create a new SCP. In the SCP, grant the DevOps engineer's IAM user full access to all resources in the new
member account. Attach the SCP to the OU that contains the new member account.
C. In the new member account, create a new IAM role that is named OrganizationAccountAccessRole. Attach the AdministratorAccess AWS
managed policy to the role. In the role's trust policy, grant the management account permission to assume the role.
D. In the new member account, edit the trust policy for the OrganizationAccountAccessRole IAM role. Grant the management account
permission to assume the role. | AnyCompany正在使用AWS Organizations来创建和管理多个AWS账户。AnyCompany最近收购了一家较小的公司Example Corp。在收购过程中，Example Corp的单个AWS账户通过Organizations邀请加入了AnyCompany的管理账户。AnyCompany将这个新成员账户移动到了专门为Example Corp设立的OU下。

AnyCompany的DevOps工程师有一个IAM用户，该用户可以担任名为OrganizationAccountAccessRole的角色来访问成员账户。这个角色配置了完全访问策略。当DevOps工程师尝试使用AWS管理控制台在Example Corp的新成员账户中担任该角色时，DevOps工程师收到以下错误消息："一个或多个字段中的信息无效。请检查您的信息或联系您的管理员。"

 | **选项A：** 在管理账户中，授予DevOps工程师的IAM用户在新成员账户中担任OrganizationAccountAccessRole IAM角色的权限。
- 这个选项关注的是管理账户侧的权限配置，但问题可能不在这里，因为工程师已经能够访问其他成员账户。

**选项B：** 在管理账户中，创建一个新的SCP。在SCP中，授予DevOps工程师的IAM用户对新成员账户中所有资源的完全访问权限。将SCP附加到包含新成员账户的OU。
- SCP（服务控制策略）是用来限制权限的，不是用来授予权限的。SCP不能授予超出IAM策略的权限，这个理解是错误的。

**选项C：** 在新成员账户中，创建一个名为OrganizationAccountAccessRole的新IAM角色。将AdministratorAccess AWS托管策略附加到该角色。在角色的信任策略中，授予管理账户担任该角色的权限。
- 这是一个完整的解决方案，创建了完整的角色配置，包括权限策略和信任策略。

**选项D：** 在新成员账户中，编辑OrganizationAccountAccessRole IAM角色的信任策略。授予管理账户担任该角色的权限。
- 这个选项假设角色已经存在，只需要修改信任策略。但如果角色不存在，这个操作就无法执行。

 |  |  |  |
| 148 | A DevOps engineer is designing an application that integrates with a legacy REST API. The application has an AWS Lambda function that
reads records from an Amazon Kinesis data stream. The Lambda function sends the records to the legacy REST API.
Approximately 10% of the records that the Lambda function sends from the Kinesis data stream have data errors and must be processed
manually. The Lambda function event source conguration has an Amazon Simple Queue Service (Amazon SQS) dead-letter queue as an on-
failure destination. The DevOps engineer has congured the Lambda function to process records in batches and has implemented retries in
case of failure.
During testing, the DevOps engineer notices that the dead-letter queue contains many records that have no data errors and that already have
been processed by the legacy REST API. The DevOps engineer needs to congure the Lambda function's event source options to reduce the
number of errorless records that are sent to the dead-letter queue. | A. Increase the retry attempts.
B. Congure the setting to split the batch when an error occurs.
C. Increase the concurrent batches per shard.
D. Decrease the maximum age of record. | 一名DevOps工程师正在设计一个与传统REST API集成的应用程序。该应用程序有一个AWS Lambda函数，用于从Amazon Kinesis数据流中读取记录。Lambda函数将这些记录发送到传统REST API。

Lambda函数从Kinesis数据流发送的记录中，大约10%存在数据错误，必须手动处理。Lambda函数事件源配置有一个Amazon Simple Queue Service (Amazon SQS)死信队列作为失败时的目标。DevOps工程师已配置Lambda函数批量处理记录，并在失败时实现重试机制。

在测试过程中，DevOps工程师注意到死信队列包含许多没有数据错误且已经被传统REST API成功处理的记录。DevOps工程师需要配置Lambda函数的事件源选项，以减少发送到死信队列的无错误记录数量。

 | **A. 增加重试次数**
- 这会增加处理时间，但不能解决核心问题
- 对于批次中混合有错误和正确记录的情况，增加重试次数仍然会导致整个批次失败
- 无法减少无错误记录进入死信队列的问题

**B. 配置在发生错误时拆分批次的设置**
- 这是Kinesis触发器的`BisectBatchOnFunctionError`功能
- 当批次处理失败时，Lambda会将批次一分为二，分别重试
- 这样可以隔离有问题的记录，避免好的记录因为坏记录而被发送到死信队列
- 直接解决了题目中描述的问题

**C. 增加每个分片的并发批次数**
- 这只是提高处理吞吐量，不能解决错误记录影响正确记录的问题
- 不会减少进入死信队列的无错误记录数量

**D. 减少记录的最大存活时间**
- 这会导致记录更快过期，可能会丢失数据
- 不能解决批次中混合记录的处理问题

 |  |  |  |
| 149 | A company has microservices running in AWS Lambda that read data from Amazon DynamoD | B. Create an AWS CodeBuild conguration that triggers when the test code is pushed. Use AWS CloudFormation to trigger an AWS
CodePipeline conguration that deploys the new Lambda versions and species the trac shift percentage and interval.
A. Create an AWS CodePipeline conguration and set up a post-commit hook to trigger the pipeline after tests have passed. Use AWS
CodeDeploy and create a Canary deployment conguration that species the percentage of trac and interval.
C. Create an AWS CodePipeline conguration and set up the source code step to trigger when code is pushed. Set up the build step to use
AWS CodeBuild to run the tests. Set up an AWS CodeDeploy conguration to deploy, then select the
CodeDeployDefault.LambdaLinear10PercentEvery3Minutes option.
D. Use the AWS CLI to set up a post-commit hook that uploads the code to an Amazon S3 bucket after tests have passed Set up an S3
event trigger that runs a Lambda function that deploys the new version. Use an interval in the Lambda function to deploy the code over
time at the required percentage. | 一家公司有运行在AWS Lambda上的微服务，这些服务从Amazon DynamoDB读取数据。[题目描述似乎不完整，但从选项来看，这道题是关于如何为Lambda函数设置CI/CD管道，实现自动化测试和渐进式部署]

选项：
- A. 创建AWS CodePipeline配置，设置post-commit钩子在测试通过后触发管道。使用AWS CodeDeploy创建金丝雀部署配置，指定流量百分比和间隔。
- B. 创建AWS CodeBuild配置，在测试代码推送时触发。使用AWS CloudFormation触发AWS CodePipeline配置，部署新的Lambda版本并指定流量转移百分比和间隔。
- C. 创建AWS CodePipeline配置，设置源代码步骤在代码推送时触发。设置构建步骤使用AWS CodeBuild运行测试。设置AWS CodeDeploy配置进行部署，然后选择CodeDeployDefault.LambdaLinear10PercentEvery3Minutes选项。
- D. 使用AWS CLI设置post-commit钩子，在测试通过后将代码上传到Amazon S3存储桶。设置S3事件触发器运行Lambda函数来部署新版本。在Lambda函数中使用间隔来按要求的百分比逐步部署代码。

 | **选项A分析：**
- 使用CodePipeline和CodeDeploy的组合是正确的方向
- Post-commit钩子的使用不是最佳实践，应该让CodePipeline直接监控源代码变更
- 金丝雀部署配置对Lambda是可行的
- 缺少构建和测试阶段的明确定义

**选项B分析：**
- CodeBuild配置合理，可以运行测试
- 使用CloudFormation触发CodePipeline的架构过于复杂且不标准
- CloudFormation主要用于基础设施即代码，不是用来触发管道的最佳工具
- 架构设计不够清晰和直接

**选项C分析：**
- 完整的CI/CD管道设计：源代码触发 → 构建测试 → 部署
- CodePipeline直接监控源代码变更，这是标准做法
- CodeBuild用于运行测试，职责清晰
- CodeDeploy用于Lambda部署，并使用预定义的线性部署配置
- `CodeDeployDefault.LambdaLinear10PercentEvery3Minutes`是AWS提供的标准Lambda渐进式部署配置
- 整个流程符合AWS最佳实践

**选项D分析：**
- 使用AWS CLI和自定义Lambda函数实现部署过于复杂
- 缺少专业的CI/CD工具支持
- 自定义实现容易出错，维护成本高
- 不符合AWS推荐的托管服务优先原则

 |  |  |  |
| 150 | A company is building a web and mobile application that uses a serverless architecture powered by AWS Lambda and Amazon API Gateway.
The company wants to fully automate the backend Lambda deployment based on code that is pushed to the appropriate environment branch
in an AWS CodeCommit repository.
The deployment must have the following:
• Separate environment pipelines for testing and production
• Automatic deployment that occurs for test environments only | A. Congure a new AWS CodePipeline service. Create a CodeCommit repository for each environment. Set up CodePipeline to retrieve the
source code from the appropriate repository. Set up the deployment step to deploy the Lambda functions with AWS CloudFormation.
B. Create two AWS CodePipeline congurations for test and production environments. Congure the production pipeline to have a manual
approval step. Create a CodeCommit repository for each environment. Set up each CodePipeline to retrieve the source code from the
appropriate repository. Set up the deployment step to deploy the Lambda functions with AWS CloudFormation.
C. Create two AWS CodePipeline congurations for test and production environments. Congure the production pipeline to have a manual
approval step. Create one CodeCommit repository with a branch for each environment. Set up each CodePipeline to retrieve the source
code from the appropriate branch in the repository. Set up the deployment step to deploy the Lambda functions with AWS
CloudFormation.
D. Create an AWS CodeBuild conguration for test and production environments. Congure the production pipeline to have a manual
approval step. Create one CodeCommit repository with a branch for each environment. Push the Lambda function code to an Amazon S3
bucket. Set up the deployment step to deploy the Lambda functions from the S3 bucket. | 一家公司正在构建一个使用无服务器架构的Web和移动应用程序，该架构由AWS Lambda和Amazon API Gateway提供支持。该公司希望基于推送到AWS CodeCommit存储库中相应环境分支的代码，完全自动化后端Lambda部署。

部署必须满足以下要求：
• 为测试和生产环境分别设置独立的环境管道
• 仅对测试环境进行自动部署

 | **选项A：**
- 配置新的AWS CodePipeline服务，为每个环境创建CodeCommit存储库
- 问题：没有提到生产环境的手动批准步骤，不符合"仅测试环境自动部署"的要求
- 问题：为每个环境创建单独的存储库不是最佳实践，代码管理复杂

**选项B：**
- 创建测试和生产两个CodePipeline配置，生产管道配置手动批准步骤
- 为每个环境创建CodeCommit存储库
- 问题：多个存储库管理复杂，不利于代码版本控制和分支管理
- 优点：满足了手动批准的要求

**选项C：**
- 创建测试和生产两个CodePipeline配置，生产管道配置手动批准步骤
- 创建一个CodeCommit存储库，每个环境使用不同分支
- 每个CodePipeline从相应分支获取源代码
- 使用CloudFormation部署Lambda函数
- 优点：符合所有要求，使用分支管理是最佳实践

**选项D：**
- 使用CodeBuild而不是CodePipeline
- 问题：CodeBuild主要用于构建，不是完整的CI/CD管道解决方案
- 问题：将代码推送到S3桶的方式不够直接和高效

 |  |  |  |
| 151 | A DevOps engineer wants to nd a solution to migrate an application from on premises to AWS. The application is running on Linux and needs
to run on specic versions of Apache Tomcat, HAProxy, and Varnish Cache to function properly. The application's operating system-level
parameters require tuning. The solution must include a way to automate the deployment of new application versions. The infrastructure
should be scalable and faulty servers should be replaced automatically. | A. Upload the application as a Docker image that contains all the necessary software to Amazon ECR. Create an Amazon ECS cluster using
an AWS Fargate launch type and an Auto Scaling group. Create an AWS CodePipeline pipeline that uses Amazon ECR as a source and
Amazon ECS as a deployment provider.
B. Upload the application code to an AWS CodeCommit repository with a saved conguration le to congure and install the software.
Create an AWS Elastic Beanstalk web server tier and a load balanced-type environment that uses the Tomcat solution stack. Create an
AWS CodePipeline pipeline that uses CodeCommit as a source and Elastic Beanstalk as a deployment provider.
C. Upload the application code to an AWS CodeCommit repository with a set of .ebextensions les to congure and install the software.
Create an AWS Elastic Beanstalk worker tier environment that uses the Tomcat solution stack. Create an AWS CodePipeline pipeline that
uses CodeCommit as a source and Elastic Beanstalk as a deployment provider.
D. Upload the application code to an AWS CodeCommit repository with an appspec.yml le to congure and install the necessary software.
Create an AWS CodeDeploy deployment group associated with an Amazon EC2 Auto Scaling group. Create an AWS CodePipeline pipeline
that uses CodeCommit as a source and CodeDeploy as a deployment provider. | 一名DevOps工程师想要找到一个解决方案，将应用程序从本地迁移到AWS。该应用程序运行在Linux上，需要运行在特定版本的Apache Tomcat、HAProxy和Varnish Cache上才能正常工作。应用程序的操作系统级参数需要调优。解决方案必须包括自动化部署新应用程序版本的方法。基础设施应该是可扩展的，故障服务器应该自动替换。

 | **选项A：** 将应用程序作为包含所有必要软件的Docker镜像上传到Amazon ECR。使用AWS Fargate启动类型和Auto Scaling组创建Amazon ECS集群。创建使用Amazon ECR作为源、Amazon ECS作为部署提供商的AWS CodePipeline管道。
- **优点：** 容器化解决方案，可以包含所有特定版本的软件，支持自动扩展和故障替换
- **缺点：** Fargate对操作系统级参数调优的支持有限，无法进行深度的OS级别定制

**选项B：** 将应用程序代码上传到AWS CodeCommit存储库，包含配置文件来配置和安装软件。创建使用Tomcat解决方案堆栈的AWS Elastic Beanstalk Web服务器层和负载均衡类型环境。创建使用CodeCommit作为源、Elastic Beanstalk作为部署提供商的AWS CodePipeline管道。
- **优点：** 支持自动扩展和部署自动化
- **缺点：** Elastic Beanstalk的Tomcat堆栈不包含HAProxy和Varnish Cache，无法满足特定软件版本要求

**选项C：** 将应用程序代码上传到AWS CodeCommit存储库，包含.ebextensions文件来配置和安装软件。创建使用Tomcat解决方案堆栈的AWS Elastic Beanstalk工作层环境。创建使用CodeCommit作为源、Elastic Beanstalk作为部署提供商的AWS CodePipeline管道。
- **优点：** .ebextensions可以进行更多定制化配置
- **缺点：** Worker tier不适合Web应用程序，且仍然受限于Elastic Beanstalk的预定义堆栈

**选项D：** 将应用程序代码上传到AWS CodeCommit存储库，包含appspec.yml文件来配置和安装必要软件。创建与Amazon EC2 Auto Scaling组关联的AWS CodeDeploy部署组。创建使用CodeCommit作为源、CodeDeploy作为部署提供商的AWS CodePipeline管道。
- **优点：** 提供完全的EC2实例控制，可以安装特定版本的所有软件，支持操作系统级参数调优，Auto Scaling组提供自动扩展和故障替换
- **缺点：** 需要更多的管理开销

 |  |  |  |
| 152 | A DevOps engineer is using AWS CodeDeploy across a eet of Amazon EC2 instances in an EC2 Auto Scaling group. The associated
CodeDeploy deployment group, which is integrated with EC2 Auto Scaling, is congured to perform in-place deployments with
CodeDeployDefault.OneAtATime. During an ongoing new deployment, the engineer discovers that, although the overall deployment nished
successfully, two out of ve instances have the previous application revision deployed. The other three instances have the newest application
revision. | A. The two affected instances failed to fetch the new deployment.
B. A failed AfterInstall lifecycle event hook caused the CodeDeploy agent to roll back to the previous version on the affected instances.
C. The CodeDeploy agent was not installed in two affected instances.
D. EC2 Auto Scaling launched two new instances while the new deployment had not yet nished, causing the previous version to be
deployed on the affected instances. | 一名DevOps工程师正在使用AWS CodeDeploy在EC2 Auto Scaling组中的一组Amazon EC2实例上进行部署。与EC2 Auto Scaling集成的相关CodeDeploy部署组被配置为使用CodeDeployDefault.OneAtATime策略执行就地部署。在正在进行的新部署过程中，工程师发现尽管整体部署成功完成，但五个实例中有两个仍然部署着之前的应用程序版本，而其他三个实例部署了最新的应用程序版本。

 | **A. 两个受影响的实例无法获取新部署。**
- 如果实例无法获取新部署，部署应该会失败，而不是显示为成功完成。CodeDeploy会报告部署失败状态。

**B. 失败的AfterInstall生命周期事件钩子导致CodeDeploy代理在受影响的实例上回滚到之前的版本。**
- 如果AfterInstall钩子失败，整个部署会被标记为失败，而不是成功。此外，CodeDeploy会停止部署过程，不会继续到其他实例。

**C. CodeDeploy代理没有安装在两个受影响的实例上。**
- 如果CodeDeploy代理没有安装，这些实例根本不会参与部署过程，部署会失败或跳过这些实例，但不会显示为成功。

**D. EC2 Auto Scaling在新部署尚未完成时启动了两个新实例，导致之前的版本被部署到受影响的实例上。**
- 这是最合理的解释。当Auto Scaling组启动新实例时，如果正在进行部署，新实例可能会从启动配置或启动模板中获取之前的应用程序版本，而不是正在部署的新版本。

 |  |  |  |
| 153 | A security team is concerned that a developer can unintentionally attach an Elastic IP address to an Amazon EC2 instance in production. No
developer should be allowed to attach an Elastic IP address to an instance. The security team must be notied if any production server has an
Elastic IP address at any time.
How can this task be automated? | A. Use Amazon Athena to query AWS CloudTrail logs to check for any associate-address attempts. Create an AWS Lambda function to
disassociate the Elastic IP address from the instance, and alert the security team.
B. Attach an IAM policy to the developers' IAM group to deny associate-address permissions. Create a custom AWS Cong rule to check
whether an Elastic IP address is associated with any instance tagged as production, and alert the security team.
C. Ensure that all IAM groups associated with developers do not have associate-address permissions. Create a scheduled AWS Lambda
function to check whether an Elastic IP address is associated with any instance tagged as production, and alert the security team if an
instance has an Elastic IP address associated with it.
D. Create an AWS Cong rule to check that all production instances have EC2 IAM roles that include deny associate-address permissions.
Verify whether there is an Elastic IP address associated with any instance, and alert the security team if an instance has an Elastic IP
address associated with it. | 安全团队担心开发人员可能会无意中将弹性IP地址附加到生产环境中的Amazon EC2实例上。不应允许任何开发人员将弹性IP地址附加到实例。如果任何生产服务器在任何时候都有弹性IP地址，必须通知安全团队。

如何自动化这个任务？

 | **选项A：** 使用Amazon Athena查询AWS CloudTrail日志来检查任何associate-address尝试。创建AWS Lambda函数来取消弹性IP地址与实例的关联，并警告安全团队。
- **问题：** 这个方案只是被动地检查日志，没有预防措施阻止开发人员执行associate-address操作
- **优点：** 能够检测到违规行为并自动修复
- **缺点：** 缺乏预防性控制，允许违规操作先发生

**选项B：** 为开发人员的IAM组附加IAM策略以拒绝associate-address权限。创建自定义AWS Config规则来检查是否有弹性IP地址与任何标记为生产的实例关联，并警告安全团队。
- **优点：** 
  - 预防性控制：通过IAM策略阻止开发人员执行associate-address操作
  - 检测控制：使用AWS Config规则持续监控生产实例
  - 通知机制：能够及时警告安全团队
- **完整性：** 同时提供预防和检测控制

**选项C：** 确保与开发人员关联的所有IAM组都没有associate-address权限。创建定时AWS Lambda函数来检查是否有弹性IP地址与任何标记为生产的实例关联，如果实例有关联的弹性IP地址，则警告安全团队。
- **优点：** 有预防性控制和检测机制
- **缺点：** 使用定时Lambda函数不如AWS Config规则高效，Config规则是专门为合规性检查设计的

**选项D：** 创建AWS Config规则来检查所有生产实例都有包含拒绝associate-address权限的EC2 IAM角色。验证是否有弹性IP地址与任何实例关联，如果实例有关联的弹性IP地址，则警告安全团队。
- **问题：** 将权限控制放在EC2实例角色上是不正确的方法，应该控制用户/开发人员的权限而不是实例的权限
- **概念错误：** EC2 IAM角色用于实例访问AWS服务，不用于控制谁可以操作该实例

 |  |  |  |
| 154 | A company is using AWS Organizations to create separate AWS accounts for each of its departments. The company needs to automate the
following tasks:
• Update the Linux AMIs with new patches periodically and generate a golden image
• Install a new version of Chef agents in the golden image, if available
• Provide the newly generated AMIs to the department's accounts | A. Write a script to launch an Amazon EC2 instance from the previous golden image. Apply the patch updates. Install the new version of
the Chef agent, generate a new golden image, and then modify the AMI permissions to share only the new image with the department's
accounts.
B. Use Amazon EC2 Image Builder to create an image pipeline that consists of the base Linux AMI and components to install the Chef
agent. Use AWS Resource Access Manager to share EC2 Image Builder images with the department's accounts.
C. Use an AWS Systems Manager Automation runbook to update the Linux AMI by using the previous image. Provide the URL for the script
that will update the Chef agent. Use AWS Organizations to replace the previous golden image in the department's accounts.
D. Use Amazon EC2 Image Builder to create an image pipeline that consists of the base Linux AMI and components to install the Chef
agent. Create a parameter in AWS Systems Manager Parameter Store to store the new AMI ID that can be referenced by the department's
accounts. |  |  |  |  |  |
| 155 | A company has a mission-critical application on AWS that uses automatic scaling. The company wants the deployment lifecycle to meet the
following parameters:
• The application must be deployed one instance at a time to ensure the remaining eet continues to serve trac.
• The application is CPU intensive and must be closely monitored.
• The deployment must automatically roll back if the CPU utilization of the deployment instance exceeds 85%. | A. Use AWS CloudFormation to create an AWS Step Functions state machine and Auto Scaling lifecycle hooks to move to one instance at a
time into a wait state. Use AWS Systems Manager automation to deploy the update to each instance and move it back into the Auto
Scaling group using the heartbeat timeout.
B. Use AWS CodeDeploy with Amazon EC2 Auto Scaling Congure an alarm tied to the CPU utilization metric. Use the CodeDeployDefault
OneAtAtime conguration as a deployment strategy. Congure automatic rollbacks within the deployment group to roll back the
deployment if the alarm thresholds are breached.
C. Use AWS Elastic Beanstalk for load balancing and AWS Auto Scaling. Congure an alarm tied to the CPU utilization metric. Congure
rolling deployments with a xed batch size of one instance. Enable enhanced health to monitor the status of the deployment and roll back
based on the alarm previously created.
D. Use AWS Systems Manager to perform a blue/green deployment with Amazon EC2 Auto Scaling. Congure an alarm tied to the CPU
utilization metric. Deploy updates one at a time. Congure automatic rollbacks within the Auto Scaling group to roll back the deployment
if the alarm thresholds are breached. | 一家公司在AWS上有一个关键任务应用程序，该应用程序使用自动扩展。公司希望部署生命周期满足以下参数：
• 应用程序必须一次部署一个实例，以确保剩余的实例群继续为流量提供服务。
• 应用程序是CPU密集型的，必须被密切监控。
• 如果部署实例的CPU利用率超过85%，部署必须自动回滚。

 | **选项A：** 使用AWS CloudFormation创建AWS Step Functions状态机和Auto Scaling生命周期钩子，一次将一个实例移动到等待状态。使用AWS Systems Manager自动化来部署更新到每个实例，并使用心跳超时将其移回Auto Scaling组。
- 这个方案过于复杂，涉及多个服务的协调
- 没有明确的CPU监控和自动回滚机制
- Step Functions和生命周期钩子的组合不是标准的部署模式

**选项B：** 使用AWS CodeDeploy与Amazon EC2 Auto Scaling。配置与CPU利用率指标相关的警报。使用CodeDeployDefault.OneAtATime配置作为部署策略。在部署组内配置自动回滚，以在警报阈值被突破时回滚部署。
- CodeDeploy原生支持OneAtATime部署策略，满足一次一个实例的要求
- 可以配置CloudWatch警报监控CPU利用率
- CodeDeploy有内置的自动回滚功能，可以基于警报触发
- 这是专门为应用程序部署设计的服务

**选项C：** 使用AWS Elastic Beanstalk进行负载均衡和AWS Auto Scaling。配置与CPU利用率指标相关的警报。配置固定批次大小为一个实例的滚动部署。启用增强健康监控来监控部署状态，并基于之前创建的警报进行回滚。
- Elastic Beanstalk支持滚动部署，可以设置批次大小为1
- 有增强健康监控功能
- 但Elastic Beanstalk更适合简单的应用程序部署，对于复杂的自定义回滚条件支持有限

**选项D：** 使用AWS Systems Manager执行蓝/绿部署与Amazon EC2 Auto Scaling。配置与CPU利用率指标相关的警报。一次部署一个更新。在Auto Scaling组内配置自动回滚，以在警报阈值被突破时回滚部署。
- 蓝/绿部署不符合"一次一个实例"的要求，它是创建完全独立的环境
- Auto Scaling组本身没有基于CPU警报的自动回滚功能
- Systems Manager主要用于补丁管理，不是专门的应用部署工具

 | B |  |  |
| 156 | A company has a single developer writing code for an automated deployment pipeline. The developer is storing source code in an Amazon S3
bucket for each project. The company wants to add more developers to the team but is concerned about code conicts and lost work. The
company also wants to build a test environment to deploy newer versions of code for testing and allow developers to automatically deploy to
both environments when code is changed in the repository. | A. Create an AWS CodeCommit repository for each project, use the main branch for production code, and create a testing branch for code
deployed to testing. Use feature branches to develop new features and pull requests to merge code to testing and main branches.
B. Create another S3 bucket for each project for testing code, and use an AWS Lambda function to promote code changes between testing
and production buckets. Enable versioning on all buckets to prevent code conicts.
C. Create an AWS CodeCommit repository for each project, and use the main branch for production and test code with different
deployment pipelines for each environment. Use feature branches to develop new features.
D. Enable versioning and branching on each S3 bucket, use the main branch for production code, and create a testing branch for code
deployed to testing. Have developers use each branch for developing in each environment. | 一家公司有一个开发人员为自动化部署管道编写代码。该开发人员将每个项目的源代码存储在Amazon S3存储桶中。公司希望在团队中增加更多开发人员，但担心代码冲突和工作丢失的问题。公司还希望构建一个测试环境来部署较新版本的代码进行测试，并允许开发人员在代码库中的代码发生更改时自动部署到两个环境。

 | **选项A：** 为每个项目创建AWS CodeCommit存储库，使用main分支存放生产代码，创建testing分支用于部署到测试环境的代码。使用功能分支开发新功能，使用拉取请求将代码合并到testing和main分支。
- **优点：** 使用专业的Git版本控制系统，支持完整的分支策略和合并请求工作流，能有效防止代码冲突，支持多开发人员协作
- **缺点：** 无明显缺点，符合最佳实践

**选项B：** 为每个项目创建另一个S3存储桶用于测试代码，使用AWS Lambda函数在测试和生产存储桶之间推广代码更改。在所有存储桶上启用版本控制以防止代码冲突。
- **优点：** 提供了某种程度的版本控制
- **缺点：** S3不是为源代码管理设计的，缺乏真正的分支和合并功能，Lambda函数方案过于复杂且不标准

**选项C：** 为每个项目创建AWS CodeCommit存储库，使用main分支同时存放生产和测试代码，为每个环境使用不同的部署管道。使用功能分支开发新功能。
- **优点：** 使用了专业的版本控制系统
- **缺点：** 生产和测试代码在同一分支上，无法独立管理不同环境的代码版本，可能导致测试代码意外部署到生产环境

**选项D：** 在每个S3存储桶上启用版本控制和分支，使用main分支存放生产代码，创建testing分支用于部署到测试环境的代码。让开发人员使用每个分支在各自环境中进行开发。
- **优点：** 尝试实现分支策略
- **缺点：** S3本身不支持Git风格的分支功能，这个方案在技术上不可行

 |  |  |  |
| 157 | A DevOps engineer notices that all Amazon EC2 instances running behind an Application Load Balancer in an Auto Scaling group are failing to
respond to user requests. The EC2 instances are also failing target group HTTP health checks.
Upon inspection, the engineer notices the application process was not running in any EC2 instances. There are a signicant number of out of
memory messages in the system logs. The engineer needs to improve the resilience of the application to cope with a potential application
memory leak. Monitoring and notications should be enabled to alert when there is an issue. | A. Change the Auto Scaling conguration to replace the instances when they fail the load balancer's health checks.
B. Change the target group health check HealthCheckIntervalSeconds parameter to reduce the interval between health checks.
C. Change the target group health checks from HTTP to TCP to check if the port where the application is listening is reachable.
D. Enable the available memory consumption metric within the Amazon CloudWatch dashboard for the entire Auto Scaling group. Create
an alarm when the memory utilization is high. Associate an Amazon SNS topic to the alarm to receive notications when the alarm goes
off.
E. Use the Amazon CloudWatch agent to collect the memory utilization of the EC2 instances in the Auto Scaling group. Create an alarm
when the memory utilization is high and associate an Amazon SNS topic to receive a notication. | 一名DevOps工程师注意到在Auto Scaling组中运行在Application Load Balancer后面的所有Amazon EC2实例都无法响应用户请求。这些EC2实例也无法通过目标组的HTTP健康检查。

经过检查，工程师发现应用程序进程在任何EC2实例中都没有运行。系统日志中有大量的内存不足消息。工程师需要提高应用程序的弹性以应对潜在的应用程序内存泄漏。应该启用监控和通知功能，以便在出现问题时发出警报。

 | **选项A：** 更改Auto Scaling配置，当实例未通过负载均衡器的健康检查时替换这些实例。
- 这是一个有效的解决方案，可以自动替换失败的实例
- 能够提高应用程序的弹性
- 但缺少监控和通知功能

**选项B：** 更改目标组健康检查的HealthCheckIntervalSeconds参数以减少健康检查之间的间隔。
- 这只是更频繁地检查，但不能解决根本的内存泄漏问题
- 不能提供监控和通知功能
- 治标不治本的方案

**选项C：** 将目标组健康检查从HTTP更改为TCP，以检查应用程序监听的端口是否可达。
- TCP检查可能会显示端口开放，但应用程序进程已经因内存不足而停止
- 不能有效检测应用程序的实际健康状态
- 同样缺少监控和通知功能

**选项D：** 在Amazon CloudWatch仪表板中为整个Auto Scaling组启用可用内存消耗指标。当内存利用率高时创建警报。将Amazon SNS主题关联到警报以在警报触发时接收通知。
- 描述有误：CloudWatch默认不提供内存指标
- 需要额外配置才能获取内存指标
- 概念正确但实现方式不准确

**选项E：** 使用Amazon CloudWatch代理收集Auto Scaling组中EC2实例的内存利用率。当内存利用率高时创建警报，并关联Amazon SNS主题以接收通知。
- 正确的技术实现方式：CloudWatch代理可以收集内存指标
- 提供了监控功能（内存利用率监控）
- 提供了通知功能（SNS主题）
- 能够在内存泄漏导致问题之前发出预警

 |  |  |  |
| 158 | An ecommerce company uses a large number of Amazon Elastic Block Store (Amazon EBS) backed Amazon EC2 instances. To decrease
manual work across all the instances, a DevOps engineer is tasked with automating restart actions when EC2 instance retirement events are
scheduled.
How can this be accomplished? | A. Create a scheduled Amazon EventBridge rule to run an AWS Systems Manager Automation runbook that checks if any EC2 instances are
scheduled for retirement once a week. If the instance is scheduled for retirement, the runbook will hibernate the instance.
B. Enable EC2 Auto Recovery on all of the instances. Create an AWS Cong rule to limit the recovery to occur during a maintenance
window only.
C. Reboot all EC2 instances during an approved maintenance window that is outside of standard business hours. Set up Amazon
CloudWatch alarms to send a notication in case any instance is failing EC2 instance status checks.
D. Set up an AWS Health Amazon EventBridge rule to run AWS Systems Manager Automation runbooks that stop and start the EC2 instance
when a retirement scheduled event occurs. | 一家电商公司使用大量基于Amazon弹性块存储(Amazon EBS)的Amazon EC2实例。为了减少所有实例的手动工作，DevOps工程师需要在EC2实例退役事件被安排时自动化重启操作。

如何实现这个目标？

 | **选项A：** 创建一个定时的Amazon EventBridge规则，每周运行一次AWS Systems Manager自动化运行手册，检查是否有EC2实例被安排退役。如果实例被安排退役，运行手册将休眠该实例。
- **问题：** 
  - 每周检查频率太低，可能错过紧急的退役通知
  - 休眠(hibernate)实例并不能解决退役问题，退役的实例仍然会被AWS强制停止
  - 这种方法是轮询式的，不够实时和高效

**选项B：** 在所有实例上启用EC2自动恢复。创建AWS Config规则限制恢复只在维护窗口期间发生。
- **问题：**
  - EC2自动恢复主要用于硬件故障恢复，不适用于计划性退役事件
  - AWS Config规则无法控制EC2自动恢复的时间窗口
  - 这个方案没有针对退役事件的具体处理机制

**选项C：** 在批准的维护窗口期间（标准工作时间之外）重启所有EC2实例。设置Amazon CloudWatch告警，在任何实例未通过EC2实例状态检查时发送通知。
- **问题：**
  - 定期重启所有实例会造成不必要的服务中断
  - 这种方法过于粗暴，没有针对性
  - 无法精确应对特定的退役事件

**选项D：** 设置AWS Health Amazon EventBridge规则，当退役计划事件发生时运行AWS Systems Manager自动化运行手册来停止和启动EC2实例。
- **优势：**
  - 使用AWS Health服务可以实时接收AWS基础设施事件通知
  - EventBridge规则可以精确捕获退役事件
  - 停止和启动实例可以将实例迁移到新的底层硬件
  - 完全自动化，无需人工干预
  - 只对受影响的实例进行操作，避免不必要的中断

 |  |  |  |
| 159 | A company manages AWS accounts for application teams in AWS Control Tower. Individual application teams are responsible for securing their
respective AWS accounts.
A DevOps engineer needs to enable Amazon GuardDuty for all AWS accounts in which the application teams have not already enabled
GuardDuty. The DevOps engineer is using AWS CloudFormation StackSets from the AWS Control Tower management account.
How should the DevOps engineer congure the CloudFormation template to prevent failure during the StackSets deployment? | A. Create a CloudFormation custom resource that invokes an AWS Lambda function. Congure the Lambda function to conditionally
enable GuardDuty if GuardDuty is not already enabled in the accounts.
B. Use the Conditions section of the CloudFormation template to enable GuardDuty in accounts where GuardDuty is not already enabled.
C. Use the CloudFormation Fn::GetAtt intrinsic function to check whether GuardDuty is already enabled. If GuardDuty is not already
enabled, use the Resources section of the CloudFormation template to enable GuardDuty.
D. Manually discover the list of AWS account IDs where GuardDuty is not enabled. Use the CloudFormation Fn::ImportValue intrinsic
function to import the list of account IDs into the CloudFormation template to skip deployment for the listed AWS accounts. | 一家公司在AWS Control Tower中为应用团队管理AWS账户。各个应用团队负责保护各自的AWS账户安全。

一名DevOps工程师需要为所有尚未启用Amazon GuardDuty的AWS账户启用GuardDuty。该DevOps工程师正在从AWS Control Tower管理账户使用AWS CloudFormation StackSets。

DevOps工程师应该如何配置CloudFormation模板以防止在StackSets部署过程中出现失败？

 | **选项A：** 创建一个CloudFormation自定义资源来调用AWS Lambda函数。配置Lambda函数在账户中尚未启用GuardDuty的情况下有条件地启用GuardDuty。
- **正确性：高** - 自定义资源可以执行复杂的逻辑判断，Lambda函数可以检查GuardDuty状态并有条件地启用它，避免重复启用导致的错误。

**选项B：** 使用CloudFormation模板的Conditions部分在尚未启用GuardDuty的账户中启用GuardDuty。
- **正确性：低** - CloudFormation的Conditions部分无法动态检查AWS服务的当前状态，它只能基于参数或映射进行静态条件判断。

**选项C：** 使用CloudFormation Fn::GetAtt内置函数检查GuardDuty是否已启用。如果尚未启用，则使用模板的Resources部分启用GuardDuty。
- **正确性：低** - Fn::GetAtt只能获取模板中已定义资源的属性，无法检查现有AWS服务的状态。

**选项D：** 手动发现未启用GuardDuty的AWS账户ID列表。使用CloudFormation Fn::ImportValue内置函数将账户ID列表导入CloudFormation模板，以跳过列出的AWS账户的部署。
- **正确性：低** - 这种方法需要手动操作，不够自动化，且Fn::ImportValue用于导入其他堆栈的输出值，不适用于此场景。

 |  |  |  |
| 160 | A company has an AWS Control Tower landing zone. The company's DevOps team creates a workload OU. A development OU and a production
OU are nested under the workload OU. The company grants users full access to the company's AWS accounts to deploy applications.
The DevOps team needs to allow only a specic management IAM role to manage the IAM roles and policies of any AWS accounts in only the
production OU. | A. Create an SCP that denies full access with a condition to exclude the management IAM role for the organization root.
B. Ensure that the FullAWSAccess SCP is applied at the organization root.
C. Create an SCP that allows IAM related actions. Attach the SCP to the development OU.
D. Create an SCP that denies IAM related actions with a condition to exclude the management IAM role. Attach the SCP to the workload
OU.
E. Create an SCP that denies IAM related actions with a condition to exclude the management IAM role. Attach the SCP to the production
OU. | 一家公司有一个AWS Control Tower着陆区。公司的DevOps团队创建了一个工作负载OU（组织单元）。开发OU和生产OU嵌套在工作负载OU下。公司授予用户对公司AWS账户的完全访问权限来部署应用程序。DevOps团队需要仅允许特定的管理IAM角色来管理生产OU中任何AWS账户的IAM角色和策略。

 | **A. 在组织根级别创建一个SCP，拒绝完全访问，但有条件排除管理IAM角色。**
- 不正确。这会影响整个组织的所有账户，包括开发OU，这不符合要求。要求只是限制生产OU的IAM管理权限。

**B. 确保FullAWSAccess SCP应用于组织根级别。**
- 不正确。FullAWSAccess SCP允许所有操作，这与限制IAM管理权限的需求相反。这不会解决问题。

**C. 创建一个允许IAM相关操作的SCP。将SCP附加到开发OU。**
- 不正确。这个选项是允许IAM操作而不是限制，并且附加到了错误的OU（开发OU而不是生产OU）。

**D. 创建一个拒绝IAM相关操作的SCP，但有条件排除管理IAM角色。将SCP附加到工作负载OU。**
- 不正确。虽然策略内容正确，但附加位置错误。附加到工作负载OU会影响其下的所有OU（包括开发OU和生产OU），但需求只要求限制生产OU。

**E. 创建一个拒绝IAM相关操作的SCP，但有条件排除管理IAM角色。将SCP附加到生产OU。**
- 正确。这个选项完全符合需求：
  - 拒绝IAM相关操作（限制IAM管理）
  - 有条件排除管理IAM角色（允许特定角色管理IAM）
  - 仅附加到生产OU（不影响开发环境）

 |  |  |  |
| 161 | A company hired a penetration tester to simulate an internal security breach. The tester performed port scans on the company's Amazon EC2
instances. The company's security measures did not detect the port scans.
The company needs a solution that automatically provides notication when port scans are performed on EC2 instances. The company
creates and subscribes to an Amazon Simple Notication Service (Amazon SNS) topic. | A. Ensure that Amazon GuardDuty is enabled. Create an Amazon CloudWatch alarm for detected EC2 and port scan ndings. Connect the
alarm to the SNS topic.
B. Ensure that Amazon Inspector is enabled. Create an Amazon EventBridge event for detected network reachability ndings that indicate
port scans. Connect the event to the SNS topic.
C. Ensure that Amazon Inspector is enabled. Create an Amazon EventBridge event for detected CVEs that cause open port vulnerabilities.
Connect the event to the SNS topic.
D. Ensure that AWS CloudTrail is enabled. Create an AWS Lambda function to analyze the CloudTrail logs for unusual amounts of trac
from an IP address range. Connect the Lambda function to the SNS topic. | 一家公司雇佣了一名渗透测试人员来模拟内部安全漏洞。测试人员对公司的Amazon EC2实例执行了端口扫描。公司的安全措施没有检测到这些端口扫描。

公司需要一个解决方案，当对EC2实例执行端口扫描时能够自动提供通知。公司创建并订阅了一个Amazon Simple Notification Service (Amazon SNS) 主题。

 | **选项A：确保启用Amazon GuardDuty。为检测到的EC2和端口扫描发现创建Amazon CloudWatch告警。将告警连接到SNS主题。**
- 正确。GuardDuty是AWS的威胁检测服务，专门设计用于检测恶意活动和异常行为，包括端口扫描
- GuardDuty可以检测针对EC2实例的端口扫描活动，并生成相应的发现（findings）
- 可以通过CloudWatch Events/EventBridge将GuardDuty的发现转发到SNS进行通知
- 这是检测端口扫描的最佳AWS服务

**选项B：确保启用Amazon Inspector。为检测到的网络可达性发现（表明端口扫描）创建Amazon EventBridge事件。将事件连接到SNS主题。**
- 不正确。Amazon Inspector主要用于应用程序安全评估和漏洞管理
- Inspector的网络可达性评估是评估网络配置和开放端口的静态分析，不是实时检测端口扫描活动
- Inspector不会检测正在进行的端口扫描攻击

**选项C：确保启用Amazon Inspector。为检测到的导致开放端口漏洞的CVE创建Amazon EventBridge事件。将事件连接到SNS主题。**
- 不正确。这个选项关注的是CVE（通用漏洞披露）和开放端口漏洞
- 这是静态漏洞评估，不是实时端口扫描检测
- 不能满足检测端口扫描活动的需求

**选项D：确保启用AWS CloudTrail。创建AWS Lambda函数来分析CloudTrail日志，查找来自IP地址范围的异常流量。将Lambda函数连接到SNS主题。**
- 不正确。CloudTrail记录的是API调用，不是网络流量
- 端口扫描是网络层面的活动，不会在CloudTrail中留下记录
- 这种方法无法检测到端口扫描活动

 |  |  |  |
| 162 | A company runs applications in an Amazon Elastic Kubernetes Service (Amazon EKS) cluster. The EKS cluster uses an Application Load
Balancer to route trac to the applications that run in the cluster.
A new application that was migrated to the EKS cluster is performing poorly. All the other applications in the EKS cluster maintain appropriate
operation. The new application scales out horizontally to the precongured maximum number of pods immediately upon deployment, before
any user trac routes to the web application. | A. Implement the Horizontal Pod Autoscaler in the EKS cluster.
B. Implement the Vertical Pod Autoscaler in the EKS cluster.
C. Implement the Cluster Autoscaler.
D. Implement the AWS Load Balancer Controller in the EKS cluster. | 一家公司在Amazon Elastic Kubernetes Service (Amazon EKS)集群中运行应用程序。EKS集群使用Application Load Balancer将流量路由到集群中运行的应用程序。

一个迁移到EKS集群的新应用程序性能表现不佳。EKS集群中的所有其他应用程序都保持正常运行。这个新应用程序在部署后立即水平扩展到预配置的最大pod数量，甚至在任何用户流量路由到web应用程序之前就发生了这种情况。

 | **A. 在EKS集群中实施Horizontal Pod Autoscaler (HPA)**
- HPA基于CPU使用率、内存使用率或自定义指标自动调整pod数量
- 如果应用程序在没有流量时就扩展到最大pod数，说明HPA配置可能有问题
- 这个选项可以解决问题，通过重新配置HPA的指标和阈值来防止不必要的扩展

**B. 在EKS集群中实施Vertical Pod Autoscaler (VPA)**
- VPA调整单个pod的CPU和内存资源请求/限制
- 不会解决pod数量异常扩展的问题
- VPA主要用于优化资源分配，而不是控制pod数量

**C. 实施Cluster Autoscaler**
- Cluster Autoscaler管理节点数量，而不是pod数量
- 当pod无法调度时增加节点，当节点利用率低时减少节点
- 不会解决应用程序pod数量异常扩展的问题

**D. 在EKS集群中实施AWS Load Balancer Controller**
- 管理ALB/NLB的创建和配置
- 主要用于负载均衡器的集成，不会影响pod的扩展行为
- 不会解决pod数量异常扩展的问题

 |  |  |  |
| 163 | A company has an AWS Control Tower landing zone that manages its organization in AWS Organizations. The company created an OU
structure that is based on the company's requirements. The company's DevOps team has established the core accounts for the solution and
an account for all centralized AWS CloudFormation and AWS Service Catalog solutions.
The company wants to offer a series of customizations that an account can request through AWS Control Tower. | A. Enable trusted access for CloudFormation with Organizations by using service-managed permissions.
B. Create an IAM role that is named AWSControlTowerBlueprintAccess. Congure the role with a trust policy that allows the
AWSControlTowerAdmin role in the management account to assume the role. Attach the AWSServiceCatalogAdminFullAccess IAM policy to
the AWSControlTowerBlueprintAccess role.
C. Create a Service Catalog product for each CloudFormation template.
D. Create a CloudFormation stack set for each CloudFormation template. Enable automatic deployment for each stack set. Create a
CloudFormation stack instance that targets specic OUs.
E. Deploy the Customizations for AWS Control Tower (CfCT) CloudFormation stack.
F. Create a CloudFormation template that contains the resources for each customization. |  |  |  |  |  |
| 164 | A company runs a workload on Amazon EC2 instances. The company needs a control that requires the use of Instance Metadata Service
Version 2 (IMDSv2) on all EC2 instances in the AWS account. If an EC2 instance does not prevent the use of Instance Metadata Service
Version 1 (IMDSv1), the EC2 instance must be terminated. | A. Set up AWS Cong in the account. Use a managed rule to check EC2 instances. Congure the rule to remediate the ndings by using
AWS Systems Manager Automation to terminate the instance.
B. Create a permissions boundary that prevents the ec2:RunInstance action if the ec2:MetadataHttpTokens condition key is not set to a
value of required. Attach the permissions boundary to the IAM role that was used to launch the instance.
C. Set up Amazon Inspector in the account. Congure Amazon Inspector to activate deep inspection for EC2 instances. Create an Amazon
EventBridge rule for an Inspector2 nding. Set an AWS Lambda function as the target to terminate the instance.
D. Create an Amazon EventBridge rule for the EC2 instance launch successful event. Send the event to an AWS Lambda function to
inspect the EC2 metadata and to terminate the instance. |  |  |  |  |  |
| 165 | A company builds an application that uses an Application Load Balancer in front of Amazon EC2 instances that are in an Auto Scaling group.
The application is stateless. The Auto Scaling group uses a custom AMI that is fully prebuilt. The EC2 instances do not have a custom
bootstrapping process.
The AMI that the Auto Scaling group uses was recently deleted. The Auto Scaling group's scaling activities show failures because the AMI ID
does not exist. | A. Create a new launch template that uses the new AMI.
B. Update the Auto Scaling group to use the new launch template.
C. Reduce the Auto Scaling group's desired capacity to 0.
D. Increase the Auto Scaling group's desired capacity by 1.
E. Create a new AMI from a running EC2 instance in the Auto Scaling group. | 一家公司构建了一个应用程序，该应用程序在Auto Scaling组中的Amazon EC2实例前面使用Application Load Balancer。该应用程序是无状态的。Auto Scaling组使用完全预构建的自定义AMI。EC2实例没有自定义引导过程。

Auto Scaling组使用的AMI最近被删除了。Auto Scaling组的扩展活动显示失败，因为AMI ID不存在。

 | **A. 创建一个使用新AMI的新启动模板**
- 正确。由于原AMI被删除，需要创建新的AMI并配置新的启动模板。这是解决问题的必要步骤之一。

**B. 更新Auto Scaling组以使用新的启动模板**
- 正确。在创建新启动模板后，必须更新Auto Scaling组配置以使用新的启动模板，这样才能使用新的AMI。

**C. 将Auto Scaling组的期望容量减少到0**
- 正确。这可以停止当前失败的扩展活动，为后续配置更新做准备，避免持续的失败尝试。

**D. 将Auto Scaling组的期望容量增加1**
- 错误。在AMI不存在的情况下增加容量只会导致更多的失败，因为仍然无法启动新实例。

**E. 从Auto Scaling组中正在运行的EC2实例创建新AMI**
- 正确。这是获取新AMI的有效方法，可以从现有运行的实例创建新的AMI来替代被删除的AMI。

 |  |  |  |
| 166 | A company deploys a web application on Amazon EC2 instances that are behind an Application Load Balancer (ALB). The company stores the
application code in an AWS CodeCommit repository. When code is merged to the main branch, an AWS Lambda function invokes an AWS
CodeBuild project. The CodeBuild project packages the code, stores the packaged code in AWS CodeArtifact, and invokes AWS Systems
Manager Run Command to deploy the packaged code to the EC2 instances.
Previous deployments have resulted in defects, EC2 instances that are not running the latest version of the packaged code, and
inconsistencies between instances. | A. Create a pipeline in AWS CodePipeline that uses the CodeCommit repository as a source provider. Congure pipeline stages that run
the CodeBuild project in parallel to build and test the application. In the pipeline, pass the CodeBuild project output artifact to an AWS
CodeDeploy action.
B. Create a pipeline in AWS CodePipeline that uses the CodeCommit repository as a source provider. Create separate pipeline stages that
run a CodeBuild project to build and then test the application. In the pipeline, pass the CodeBuild project output artifact to an AWS
CodeDeploy action.
C. Create an AWS CodeDeploy application and a deployment group to deploy the packaged code to the EC2 instances. Congure the ALB
for the deployment group.
D. Create individual Lambda functions that use AWS CodeDeploy instead of Systems Manager to run build, test, and deploy actions.
E. Create an Amazon S3 bucket. Modify the CodeBuild project to store the packages in the S3 bucket instead of in CodeArtifact. Use
deploy actions in CodeDeploy to deploy the artifact to the EC2 instances. |  |  |  |  |  |
| 167 | A company uses an organization in AWS Organizations to manage its AWS accounts. The company's automation account contains a CI/CD
pipeline that creates and congures new AWS accounts.
The company has a group of internal service teams that provide services to accounts in the organization. The service teams operate out of a
set of services accounts. The service teams want to receive an AWS CloudTrail event in their services accounts when the CreateAccount API
call creates a new account.
How should the company share this CloudTrail event with the service accounts? | A. Create an Amazon EventBridge rule in the automation account to send account creation events to the default event bus in the services
accounts. Update the default event bus in the services accounts to allow events from the automation account.
B. Create a custom Amazon EventBridge event bus in the services accounts. Update the custom event bus to allow events from the
automation account. Create an EventBridge rule in the services account that directly listens to CloudTrail events from the automation
account.
C. Create a custom Amazon EventBridge event bus in the automation account and the services accounts. Create an EventBridge rule and
policy that connects the custom event buses that are in the automation account and the services accounts.
D. Create a custom Amazon EventBridge event bus in the automation account. Create an EventBridge rule and policy that connects the
custom event bus to the default event buses in the services accounts. | 一家公司使用AWS Organizations中的组织来管理其AWS账户。该公司的自动化账户包含一个CI/CD管道，用于创建和配置新的AWS账户。

该公司有一组内部服务团队，为组织中的账户提供服务。服务团队在一组服务账户中运营。当CreateAccount API调用创建新账户时，服务团队希望在其服务账户中接收AWS CloudTrail事件。

公司应该如何与服务账户共享此CloudTrail事件？

 | **选项A：** 在自动化账户中创建Amazon EventBridge规则，将账户创建事件发送到服务账户中的默认事件总线。更新服务账户中的默认事件总线以允许来自自动化账户的事件。

- 这个方案技术上可行，但使用默认事件总线进行跨账户事件共享不是最佳实践
- 默认事件总线主要用于账户内部的事件处理
- 安全性和隔离性相对较差

**选项B：** 在服务账户中创建自定义Amazon EventBridge事件总线。更新自定义事件总线以允许来自自动化账户的事件。在服务账户中创建EventBridge规则，直接监听来自自动化账户的CloudTrail事件。

- 这个方案存在技术问题：EventBridge规则不能直接跨账户监听CloudTrail事件
- 需要通过事件总线进行中转，而不是直接监听
- 架构设计不合理

**选项C：** 在自动化账户和服务账户中都创建自定义Amazon EventBridge事件总线。创建EventBridge规则和策略，连接自动化账户和服务账户中的自定义事件总线。

- 这是标准的跨账户事件共享最佳实践
- 使用自定义事件总线提供更好的隔离性和安全性
- 通过适当的策略控制访问权限
- 架构清晰，便于管理和维护

**选项D：** 在自动化账户中创建自定义Amazon EventBridge事件总线。创建EventBridge规则和策略，将自定义事件总线连接到服务账户中的默认事件总线。

- 混合使用自定义和默认事件总线，架构不一致
- 虽然技术上可行，但不是最佳实践
- 管理复杂度较高

 |  |  |  |
| 168 | A DevOps engineer is building a solution that uses Amazon Simple Queue Service (Amazon SQS) standard queues. The solution also includes
an AWS Lambda function and an Amazon DynamoDB table. The Lambda function pulls content from an SQS queue event source and writes the
content to the DynamoDB table.
The solution must maximize the scalability of Lambda and must prevent successfully processed SQS messages from being processed multiple
times. | A. Decrease the batch window to 1 second when conguring the Lambda function's event source mapping.
B. Decrease the batch size to 1 when conguring the Lambda function's event source mapping.
C. Include the ReportBatchItemFailures value in the FunctionResponseTypes list in the Lambda function's event source mapping.
D. Set the queue visibility timeout on the Lambda function's event source mapping to account for invocation throttling of the Lambda
function. |  |  |  |  |  |
| 169 | A company has a new AWS account that teams will use to deploy various applications. The teams will create many Amazon S3 buckets for
application-specic purposes and to store AWS CloudTrail logs. The company has enabled Amazon Macie for the account.
A DevOps engineer needs to optimize the Macie costs for the account without compromising the account's functionality. | A. Exclude S3 buckets that contain CloudTrail logs from automated discovery.
B. Exclude S3 buckets that have public read access from automated discovery.
C. Congure scheduled daily discovery jobs for all S3 buckets in the account.
D. Congure discovery jobs to include S3 objects based on the last modied criterion.
E. Congure discovery jobs to include S3 objects that are tagged as production only. | 一家公司有一个新的AWS账户，团队将使用该账户部署各种应用程序。团队将为特定应用程序目的创建许多Amazon S3存储桶，并存储AWS CloudTrail日志。公司已为该账户启用了Amazon Macie。
DevOps工程师需要在不影响账户功能的情况下优化该账户的Macie成本。

2. | A. 从自动发现中排除包含CloudTrail日志的S3存储桶
- **正确**：CloudTrail日志通常不包含敏感的个人身份信息(PII)或敏感数据，主要是API调用记录。扫描这些存储桶不会带来安全价值，但会产生不必要的成本。排除这些存储桶可以显著降低Macie成本。

B. 从自动发现中排除具有公共读取访问权限的S3存储桶
- **错误**：具有公共读取访问权限的存储桶实际上更需要被Macie扫描，因为它们面临更高的数据泄露风险。排除这些存储桶会降低安全性。

C. 为账户中的所有S3存储桶配置每日计划发现作业
- **错误**：这会增加成本而不是优化成本。每日扫描所有存储桶会产生大量的扫描费用，特别是对于不经常变化的数据。

D. 配置发现作业以基于最后修改标准包含S3对象
- **正确**：通过只扫描最近修改的对象，可以避免重复扫描未更改的数据，从而降低成本。这是一个有效的成本优化策略。

E. 配置发现作业仅包含标记为生产环境的S3对象
- **部分正确**：这可以减少扫描范围，但可能会遗漏开发或测试环境中的敏感数据。这种方法可能会影响账户的整体安全功能。

3. | A |  |  |
| 170 | A company uses an organization in AWS Organizations to manage its AWS accounts. The company recently acquired another company that
has standalone AWS accounts. The acquiring company's DevOps team needs to consolidate the administration of the AWS accounts for both
companies and retain full administrative control of the accounts. The DevOps team also needs to collect and group ndings across all the
accounts to implement and maintain a security posture. | A. Invite the acquired company's AWS accounts to join the organization. Create an SCP that has full administrative privileges. Attach the
SCP to the management account.
B. Invite the acquired company's AWS accounts to join the organization. Create the OrganizationAccountAccessRole IAM role in the invited
accounts. Grant permission to the management account to assume the role.
C. Use AWS Security Hub to collect and group ndings across all accounts. Use Security Hub to automatically detect new accounts as the
accounts are added to the organization.
D. Use AWS Firewall Manager to collect and group ndings across all accounts. Enable all features for the organization. Designate an
account in the organization as the delegated administrator account for Firewall Manager.
E. Use Amazon Inspector to collect and group ndings across all accounts. Designate an account in the organization as the delegated
administrator account for Amazon Inspector. | 一家公司使用AWS Organizations中的组织来管理其AWS账户。该公司最近收购了另一家拥有独立AWS账户的公司。收购方的DevOps团队需要整合两家公司AWS账户的管理，并保持对账户的完全管理控制权。DevOps团队还需要收集和分组所有账户的发现结果，以实施和维护安全态势。

 | **选项A：** 邀请被收购公司的AWS账户加入组织。创建具有完全管理权限的SCP（服务控制策略）。将SCP附加到管理账户。
- **错误**：SCP是用于限制权限的，不是用于授予权限。将限制性SCP附加到管理账户会限制管理账户的能力，这与需求相反。

**选项B：** 邀请被收购公司的AWS账户加入组织。在被邀请的账户中创建OrganizationAccountAccessRole IAM角色。授权管理账户承担该角色的权限。
- **正确**：这是AWS Organizations的标准最佳实践。OrganizationAccountAccessRole允许管理账户对成员账户进行跨账户访问和管理。

**选项C：** 使用AWS Security Hub收集和分组所有账户的发现结果。使用Security Hub在账户添加到组织时自动检测新账户。
- **正确**：Security Hub是专门用于收集、整合和管理安全发现结果的服务，支持跨账户安全态势管理，并且可以与Organizations集成。

**选项D：** 使用AWS Firewall Manager收集和分组所有账户的发现结果。为组织启用所有功能。指定组织中的一个账户作为Firewall Manager的委托管理员账户。
- **错误**：Firewall Manager主要用于管理防火墙规则和WAF规则，不是用于收集和分组安全发现结果的主要工具。

**选项E：** 使用Amazon Inspector收集和分组所有账户的发现结果。指定组织中的一个账户作为Amazon Inspector的委托管理员账户。
- **部分正确但不完整**：Inspector主要专注于应用程序安全评估和漏洞管理，范围比Security Hub更窄，不能提供全面的安全态势管理。

 |  |  |  |
| 171 | A company has an application and a CI/CD pipeline. The CI/CD pipeline consists of an AWS CodePipeline pipeline and an AWS CodeBuild
project. The CodeBuild project runs tests against the application as part of the build process and outputs a test report. The company must
keep the test reports for 90 days. | A. Add a new stage in the CodePipeline pipeline after the stage that contains the CodeBuild project. Create an Amazon S3 bucket to store
the reports. Congure an S3 deploy action type in the new CodePipeline stage with the appropriate path and format for the reports.
B. Add a report group in the CodeBuild project buildspec le with the appropriate path and format for the reports. Create an Amazon S3
bucket to store the reports. Congure an Amazon EventBridge rule that invokes an AWS Lambda function to copy the reports to the S3
bucket when a build is completed. Create an S3 Lifecycle rule to expire the objects after 90 days.
C. Add a new stage in the CodePipeline pipeline. Congure a test action type with the appropriate path and format for the reports.
Congure the report expiration time to be 90 days in the CodeBuild project buildspec le.
D. Add a report group in the CodeBuild project buildspec le with the appropriate path and format for the reports. Create an Amazon S3
bucket to store the reports. Congure the report group as an artifact in the CodeBuild project buildspec le. Congure the S3 bucket as
the artifact destination. Set the object expiration to 90 days. | 一家公司有一个应用程序和一个CI/CD流水线。CI/CD流水线由AWS CodePipeline流水线和AWS CodeBuild项目组成。CodeBuild项目在构建过程中对应用程序运行测试，并输出测试报告。公司必须保留测试报告90天。

 | **选项A：** 在包含CodeBuild项目的阶段之后，在CodePipeline流水线中添加一个新阶段。创建Amazon S3存储桶来存储报告。在新的CodePipeline阶段中配置S3部署操作类型，使用适当的路径和格式来处理报告。
- **问题：** 这种方法过于复杂，需要额外的流水线阶段。CodePipeline的S3部署操作主要用于部署构件，不是专门为测试报告设计的。没有提到生命周期管理来满足90天的要求。

**选项B：** 在CodeBuild项目的buildspec文件中添加报告组，使用适当的路径和格式来处理报告。创建Amazon S3存储桶来存储报告。配置Amazon EventBridge规则，当构建完成时调用AWS Lambda函数将报告复制到S3存储桶。创建S3生命周期规则，在90天后使对象过期。
- **问题：** 这种方法过于复杂，引入了不必要的EventBridge和Lambda组件。CodeBuild已经有内置的报告功能，不需要额外的事件驱动架构。

**选项C：** 在CodePipeline流水线中添加一个新阶段。配置测试操作类型，使用适当的路径和格式来处理报告。在CodeBuild项目的buildspec文件中配置报告过期时间为90天。
- **问题：** CodePipeline没有专门的"测试操作类型"用于存储测试报告。buildspec文件中也不能直接配置报告过期时间。

**选项D：** 在CodeBuild项目的buildspec文件中添加报告组，使用适当的路径和格式来处理报告。创建Amazon S3存储桶来存储报告。在CodeBuild项目的buildspec文件中将报告组配置为构件。将S3存储桶配置为构件目标。设置对象过期时间为90天。
- **优势：** 使用CodeBuild的原生报告功能，通过buildspec中的reports部分配置报告组。利用CodeBuild的构件功能将报告存储到S3。使用S3生命周期策略管理90天的保留期。这是最直接和原生的解决方案。

 |  |  |  |
| 172 | A company uses an Amazon API Gateway regional REST API to host its application API. The REST API has a custom domain. The REST API's
default endpoint is deactivated.
The company's internal teams consume the API. The company wants to use mutual TLS between the API and the internal teams as an
additional layer of authentication. | A. 
B. Provision a client certicate that is signed by a public certicate authority (CA). Import the certicate into AWS Certicate Manager
(ACM).
C. Upload the provisioned client certicate to an Amazon S3 bucket. Congure the API Gateway mutual TLS to use the client certicate
that is stored in the S3 bucket as the trust store.
D. Upload the provisioned client certicate private key to an Amazon S3 bucket. Congure the API Gateway mutual TLS to use the private
key that is stored in the S3 bucket as the trust store.
E. Upload the root private certicate authority (CA) certicate to an Amazon S3 bucket. Congure the API Gateway mutual TLS to use the
private CA certicate that is stored in the S3 bucket as the trust store. | 一家公司使用Amazon API Gateway区域REST API来托管其应用程序API。该REST API有一个自定义域名。REST API的默认端点已被停用。
公司的内部团队使用该API。公司希望在API和内部团队之间使用双向TLS作为额外的身份验证层。

2. | A. [选项内容缺失]

B. 配置由公共证书颁发机构(CA)签名的客户端证书。将证书导入到AWS Certificate Manager(ACM)中。
- 这个选项不正确。虽然ACM可以管理证书，但对于API Gateway的双向TLS配置，客户端证书不是存储在ACM中作为信任存储使用的。ACM主要用于服务器端证书管理。

C. 将配置的客户端证书上传到Amazon S3存储桶。配置API Gateway双向TLS使用存储在S3存储桶中的客户端证书作为信任存储。
- 这个选项不正确。客户端证书本身不应该作为信任存储。信任存储应该包含的是用于验证客户端证书的CA证书，而不是客户端证书本身。

D. 将配置的客户端证书私钥上传到Amazon S3存储桶。配置API Gateway双向TLS使用存储在S3存储桶中的私钥作为信任存储。
- 这个选项完全不正确。私钥绝不应该上传到服务器端作为信任存储。私钥应该保留在客户端，用于客户端身份验证。将私钥作为信任存储是一个严重的安全错误。

E. 将根私有证书颁发机构(CA)证书上传到Amazon S3存储桶。配置API Gateway双向TLS使用存储在S3存储桶中的私有CA证书作为信任存储。
- 这个选项是正确的。在双向TLS配置中，API Gateway需要一个信任存储来验证客户端提供的证书。信任存储应该包含签发客户端证书的CA证书。将CA证书上传到S3并配置为信任存储是正确的做法。

3. | E |  |  |
| 173 | A company uses AWS Directory Service for Microsoft Active Directory as its identity provider (IdP). The company requires all infrastructure to
be dened and deployed by AWS CloudFormation.
A DevOps engineer needs to create a eet of Windows-based Amazon EC2 instances to host an application. The DevOps engineer has created
a CloudFormation template that contains an EC2 launch template, IAM role, EC2 security group, and EC2 Auto Scaling group. The DevOps
engineer must implement a solution that joins all EC2 instances to the domain of the AWS Managed Microsoft AD directory. | A. In the CloudFormation template, create an AWS::SSM::Document resource that joins the EC2 instance to the AWS Managed Microsoft AD
domain by using the parameters for the existing directory. Update the launch template to include the SSMAssociation property to use the
new SSM document. Attach the AmazonSSMManagedInstanceCore and AmazonSSMDirectoryServiceAccess AWS managed policies to the
IAM role that the EC2 instances use.
B. In the CloudFormation template, update the launch template to include specic tags that propagate on launch. Create an
AWS::SSM::Association resource to associate the AWS-JoinDirectoryServiceDomain Automation runbook with the EC2 instances that have
the specied tags. Dene the required parameters to join the AWS Managed Microsoft AD directory. Attach the
AmazonSSMManagedInstanceCore and AmazonSSMDirectoryServiceAccess AWS managed policies to the IAM role that the EC2 instances
use.
C. Store the existing AWS Managed Microsoft AD domain connection details in AWS Secrets Manager. In the CloudFormation template,
create an AWS::SSM::Association resource to associate the AWS-CreateManagedWindowsInstanceWithApproval Automation runbook with
the EC2 Auto Scaling group. Pass the ARNs for the parameters from Secrets Manager to join the domain. Attach the
AmazonSSMDirectoryServiceAccess and SecretsManagerReadWrite AWS managed policies to the IAM role that the EC2 instances use.
D. Store the existing AWS Managed Microsoft AD domain administrator credentials in AWS Secrets Manager. In the CloudFormation
template, update the EC2 launch template to include user data. Congure the user data to pull the administrator credentials from Secrets
Manager and to join the AWS Managed Microsoft AD domain. Attach the AmazonSSMManagedInstanceCore and
SecretsManagerReadWrite AWS managed policies to the IAM role that the EC2 instances use. |  |  |  |  |  |
| 174 | A company uses AWS Organizations to manage its AWS accounts. The company has a root OU that has a child OU. The root OU has an SCP
that allows all actions on all resources. The child OU has an SCP that allows all actions for Amazon DynamoDB and AWS Lambda, and denies
all other actions.
The company has an AWS account that is named vendor-data in the child OU. A DevOps engineer has an IAM user that is attached to the
Administrator Access IAM policy in the vendor-data account. The DevOps engineer attempts to launch an Amazon EC2 instance in the vendor-
data account but receives an access denied error. | A. Attach the AmazonEC2FullAccess IAM policy to the IAM user.
B. Create a new SCP that allows all actions for Amazon EC2. Attach the SCP to the vendor-data account.
C. Update the SCP in the child OU to allow all actions for Amazon EC2.
D. Create a new SCP that allows all actions for Amazon EC2. Attach the SCP to the root OU. | 一家公司使用AWS Organizations来管理其AWS账户。该公司有一个根组织单位(root OU)，根OU下有一个子OU。根OU有一个SCP(服务控制策略)，允许对所有资源执行所有操作。子OU有一个SCP，只允许对Amazon DynamoDB和AWS Lambda执行所有操作，拒绝所有其他操作。

该公司在子OU中有一个名为vendor-data的AWS账户。一名DevOps工程师拥有一个IAM用户，该用户在vendor-data账户中附加了Administrator Access IAM策略。DevOps工程师尝试在vendor-data账户中启动Amazon EC2实例，但收到访问拒绝错误。

2. | A. 将AmazonEC2FullAccess IAM策略附加到IAM用户。
- 错误。问题不在于IAM权限不足，因为用户已经有Administrator Access策略，这已经包含了EC2的完整权限。问题在于SCP的限制。

B. 创建一个新的SCP，允许对Amazon EC2执行所有操作。将SCP附加到vendor-data账户。
- 错误。SCP不能直接附加到单个账户，只能附加到组织单位(OU)。

C. 更新子OU中的SCP，允许对Amazon EC2执行所有操作。
- 正确。当前子OU的SCP只允许DynamoDB和Lambda操作，拒绝其他所有操作（包括EC2）。需要修改子OU的SCP来包含EC2权限。

D. 创建一个新的SCP，允许对Amazon EC2执行所有操作。将SCP附加到根OU。
- 错误。虽然技术上可行，但这会影响根OU下的所有账户和子OU，不是最佳实践。而且子OU的限制性SCP仍然会阻止EC2操作。

3. | C |  |  |
| 175 | A company's security policies require the use of security hardened AMIs in production environments. A DevOps engineer has used EC2 Image
Builder to create a pipeline that builds the AMIs on a recurring schedule.
The DevOps engineer needs to update the launch templates of the company's Auto Scaling groups. The Auto Scaling groups must use the
newest AMIs during the launch of Amazon EC2 instances. | A. Congure an Amazon EventBridge rule to receive new AMI events from Image Builder. Target an AWS Systems Manager Run Command
document that updates the launch templates of the Auto Scaling groups with the newest AMI I
D. Congure the Image Builder distribution settings to update the launch templates with the newest AMI ICongure the Auto Scaling
groups to use the newest version of the launch template.
B. Congure an Amazon EventBridge rule to receive new AMI events from Image Builder. Target an AWS Lambda function that updates the
launch templates of the Auto Scaling groups with the newest AMI I
C. Congure the launch template to use a value from AWS Systems Manager Parameter Store for the AMI I | 一家公司的安全策略要求在生产环境中使用经过安全加固的AMI。DevOps工程师已经使用EC2 Image Builder创建了一个管道，该管道按照定期计划构建AMI。

DevOps工程师需要更新公司Auto Scaling组的启动模板。Auto Scaling组在启动Amazon EC2实例时必须使用最新的AMI。

 | **选项A：** 配置Amazon EventBridge规则来接收来自Image Builder的新AMI事件。目标为AWS Systems Manager Run Command文档，该文档使用最新的AMI ID更新Auto Scaling组的启动模板。

- **优点：** 使用EventBridge自动化触发，Systems Manager Run Command可以执行更新操作
- **缺点：** Run Command主要用于在EC2实例上执行命令，而不是更新AWS资源配置，这不是最佳用途

**选项B：** 配置Image Builder分发设置以使用最新AMI更新启动模板。配置Auto Scaling组使用启动模板的最新版本。

- **优点：** 直接利用Image Builder的内置功能
- **缺点：** Image Builder的分发设置主要用于AMI的分发和共享，不直接支持更新启动模板的功能

**选项C：** 配置Amazon EventBridge规则来接收来自Image Builder的新AMI事件。目标为AWS Lambda函数，该函数使用最新的AMI ID更新Auto Scaling组的启动模板。

- **优点：** 
  - EventBridge可以监听Image Builder的AMI创建事件
  - Lambda函数可以灵活地调用AWS API更新启动模板
  - 完全自动化的解决方案
  - Lambda可以处理复杂的逻辑和错误处理

**选项D：** 配置启动模板使用AWS Systems Manager Parameter Store中的值作为AMI ID。

- **优点：** 通过Parameter Store实现动态配置
- **缺点：** 题目中没有提到如何自动更新Parameter Store中的值，仍需要额外的自动化机制

 |  |  |  |
| 176 | A company has congured an Amazon S3 event source on an AWS Lambda function. The company needs the Lambda function to run when a
new object is created or an existing object is modied in a particular S3 bucket. The Lambda function will use the S3 bucket name and the S3
object key of the incoming event to read the contents of the created or modied S3 object. The Lambda function will parse the contents and
save the parsed contents to an Amazon DynamoDB table.
The Lambda function's execution role has permissions to read from the S3 bucket and to write to the DynamoDB table. During testing, a
DevOps engineer discovers that the Lambda function does not run when objects are added to the S3 bucket or when existing objects are
modied. | A. Increase the memory of the Lambda function to give the function the ability to process large les from the S3 bucket.
B. Create a resource policy on the Lambda function to grant Amazon S3 the permission to invoke the Lambda function for the S3 bucket.
C. Congure an Amazon Simple Queue Service (Amazon SQS) queue as an OnFailure destination for the Lambda function.
D. Provision space in the /tmp folder of the Lambda function to give the function the ability to process large les from the S3 bucket. | 一家公司在AWS Lambda函数上配置了Amazon S3事件源。公司需要Lambda函数在特定S3存储桶中创建新对象或修改现有对象时运行。Lambda函数将使用传入事件的S3存储桶名称和S3对象键来读取已创建或修改的S3对象的内容。Lambda函数将解析内容并将解析后的内容保存到Amazon DynamoDB表中。

Lambda函数的执行角色具有从S3存储桶读取和向DynamoDB表写入的权限。在测试过程中，DevOps工程师发现当对象添加到S3存储桶或修改现有对象时，Lambda函数不会运行。

 | **A. 增加Lambda函数的内存，使函数能够处理来自S3存储桶的大文件。**
- 错误。问题描述中明确指出Lambda函数根本没有被触发运行，这不是内存不足的问题，而是权限配置问题。

**B. 在Lambda函数上创建资源策略，授予Amazon S3调用该S3存储桶的Lambda函数的权限。**
- 正确。当S3事件触发Lambda函数时，S3服务需要有权限调用Lambda函数。这需要在Lambda函数上配置资源策略（resource-based policy），明确允许S3服务调用该函数。

**C. 配置Amazon Simple Queue Service (Amazon SQS)队列作为Lambda函数的OnFailure目标。**
- 错误。OnFailure目标是用于处理异步调用失败的情况，但当前问题是Lambda函数根本没有被触发，不是执行失败的问题。

**D. 在Lambda函数的/tmp文件夹中预置空间，使函数能够处理来自S3存储桶的大文件。**
- 错误。与选项A类似，这是针对函数执行时的资源问题，但当前问题是函数没有被触发执行。

 |  |  |  |
| 177 | A company has deployed a critical application in two AWS Regions. The application uses an Application Load Balancer (ALB) in both Regions.
The company has Amazon Route 53 alias DNS records for both ALBs.
The company uses Amazon Route 53 Application Recovery Controller to ensure that the application can fail over between the two Regions.
The Route 53 ARC conguration includes a routing control for both Regions. The company uses Route 53 ARC to perform quarterly disaster
recovery (DR) tests.
During the most recent DR test, a DevOps engineer accidentally turned off both routing controls. The company needs to ensure that at least
one routing control is turned on at all times. | A. In Route 53 ARC, create a new assertion safety rule. Apply the assertion safety rule to the two routing controls. Congure the rule with
the ATLEAST type with a threshold of 1.
B. In Route 53 ARC, create a new gating safety rule. Apply the assertion safety rule to the two routing controls. Congure the rule with the
OR type with a threshold of 1.
C. In Route 53 ARC, create a new resource set. Congure the resource set with an AWS::Route53::HealthCheck resource type. Specify the
ARNs of the two routing controls as the target resource. Create a new readiness check for the resource set.
D. In Route 53 ARC, create a new resource set. Congure the resource set with an AWS::Route53RecoveryReadiness::DNSTargetResource
resource type. Add the domain names of the two Route 53 alias DNS records as the target resource. Create a new readiness check for the
resource set. | 一家公司在两个AWS区域部署了一个关键应用程序。该应用程序在两个区域都使用应用程序负载均衡器(ALB)。
公司为两个ALB都配置了Amazon Route 53别名DNS记录。
公司使用Amazon Route 53应用程序恢复控制器来确保应用程序可以在两个区域之间进行故障转移。
Route 53 ARC配置包括两个区域的路由控制。公司使用Route 53 ARC执行季度灾难恢复(DR)测试。
在最近的DR测试中，一名DevOps工程师意外地关闭了两个路由控制。公司需要确保至少有一个路由控制始终处于开启状态。

 | **选项A：在Route 53 ARC中，创建一个新的断言安全规则。将断言安全规则应用到两个路由控制上。使用ATLEAST类型配置规则，阈值为1。**
- 这是正确的方法。断言安全规则(Assertion Safety Rule)专门用于防止意外的路由控制状态更改
- ATLEAST类型确保至少有指定数量的路由控制保持开启状态
- 阈值为1意味着至少要有1个路由控制处于开启状态，这正好满足需求

**选项B：在Route 53 ARC中，创建一个新的门控安全规则。将断言安全规则应用到两个路由控制上。使用OR类型配置规则，阈值为1。**
- 门控安全规则(Gating Safety Rule)用于控制其他安全规则的启用/禁用，不是用于直接控制路由控制状态
- 描述中混淆了门控安全规则和断言安全规则的概念
- OR类型不是门控安全规则的正确配置类型

**选项C：在Route 53 ARC中，创建一个新的资源集。使用AWS::Route53::HealthCheck资源类型配置资源集。指定两个路由控制的ARN作为目标资源。为资源集创建新的就绪检查。**
- 就绪检查(Readiness Check)用于验证资源是否准备好处理流量，不是用于防止意外的配置更改
- 健康检查资源类型不适用于路由控制的保护
- 这种方法无法防止意外关闭路由控制

**选项D：在Route 53 ARC中，创建一个新的资源集。使用AWS::Route53RecoveryReadiness::DNSTargetResource资源类型配置资源集。添加两个Route 53别名DNS记录的域名作为目标资源。为资源集创建新的就绪检查。**
- 同样是就绪检查方法，无法解决防止意外关闭路由控制的问题
- DNS目标资源类型用于检查DNS解析，不是用于路由控制保护
- 这种方法不能防止DevOps工程师意外关闭路由控制

 | A |  |  |
| 178 | A healthcare services company is concerned about the growing costs of software licensing for an application for monitoring patient wellness.
The company wants to create an audit process to ensure that the application is running exclusively on Amazon EC2 Dedicated Hosts. A
DevOps engineer must create a workow to audit the application to ensure compliance. | A. Use AWS Systems Manager Conguration Compliance. Use calls to the put-compliance-items API action to scan and build a database of
noncompliant EC2 instances based on their host placement conguration. Use an Amazon DynamoDB table to store these instance IDs for
fast access. Generate a report through Systems Manager by calling the list-compliance-summaries API action.
B. Use custom Java code running on an EC2 instance. Set up EC2 Auto Scaling for the instance depending on the number of instances to
be checked. Send the list of noncompliant EC2 instance IDs to an Amazon SQS queue. Set up another worker instance to process instance
IDs from the SQS queue and write them to Amazon DynamoDUse an AWS Lambda function to terminate noncompliant instance IDs
obtained from the queue, and send them to an Amazon SNS email topic for distribution.
C. Use AWS Cong. Identify all EC2 instances to be audited by enabling Cong Recording on all Amazon EC2 resources for the region.
Create a custom AWS Cong rule that triggers an AWS Lambda function by using the "cong-rule-change -triggered" blueprint. Modify the
Lambda evaluateCompliance() function to verify host placement to return a NON_COMPLIANT result if the instance is not running on an
EC2 Dedicated Host. Use the AWS Cong report to address noncompliant instances.
D. Use AWS CloudTrail. Identify all EC2 instances to be audited by analyzing all calls to the EC2 RunCommand API action. Invoke an AWS
Lambda function that analyzes the host placement of the instance. Store the EC2 instance ID of noncompliant resources in an Amazon
RDS for MySQL DB instance. Generate a report by querying the RDS instance and exporting the query results to a CSV text le. |  |  |  |  |  |
| 179 | A DevOps engineer is planning to deploy a Ruby-based application to production. The application needs to interact with an Amazon RDS for
MySQL database and should have automatic scaling and high availability. The stored data in the database is critical and should persist
regardless of the state of the application stack.
The DevOps engineer needs to set up an automated deployment strategy for the application with automatic rollbacks. The solution also must
alert the application team when a deployment fails. | A. Deploy the application on AWS Elastic Beanstalk. Deploy an Amazon RDS for MySQL DB instance as part of the Elastic Beanstalk
conguration.
B. Deploy the application on AWS Elastic Beanstalk. Deploy a separate Amazon RDS for MySQL DB instance outside of Elastic Beanstalk.
C. Congure a notication email address that alerts the application team in the AWS Elastic Beanstalk conguration.
D. Congure an Amazon EventBridge rule to monitor AWS Health events. Use an Amazon Simple Notication Service (Amazon SNS) topic
as a target to alert the application team.
E. Use the immutable deployment method to deploy new application versions. |  |  |  |  |  |
| 180 | A company is using AWS CodePipeline to deploy an application. According to a new guideline, a member of the company's security team must
sign off on any application changes before the changes are deployed into production. The approval must be recorded and retained. | A. Congure CodePipeline to write actions to Amazon CloudWatch Logs.
B. Congure CodePipeline to write actions to an Amazon S3 bucket at the end of each pipeline stage.
C. Create an AWS CloudTrail trail to deliver logs to Amazon S3.
D. Create a CodePipeline custom action to invoke an AWS Lambda function for approval. Create a policy that gives the security team
access to manage CodePipeline custom actions.
E. Create a CodePipeline manual approval action before the deployment step. Create a policy that grants the security team access to
approve manual approval stages. |  |  |  |  |  |
| 181 | A company requires its internal business teams to launch resources through pre-approved AWS CloudFormation templates only. The security
team requires automated monitoring when resources drift from their expected state. | A. Allow users to deploy CloudFormation stacks using a CloudFormation service role only. Use CloudFormation drift detection to detect
when resources have drifted from their expected state.
B. Allow users to deploy CloudFormation stacks using a CloudFormation service role only. Use AWS Cong rules to detect when resources
have drifted from their expected state.
C. Allow users to deploy CloudFormation stacks using AWS Service Catalog only. Enforce the use of a launch constraint. Use AWS Cong
rules to detect when resources have drifted from their expected state.
D. Allow users to deploy CloudFormation stacks using AWS Service Catalog only. Enforce the use of a template constraint. Use Amazon
EventBridge notications to detect when resources have drifted from their expected state. | 一家公司要求其内部业务团队仅通过预先批准的AWS CloudFormation模板来启动资源。安全团队要求在资源偏离其预期状态时进行自动化监控。

选项：
A. 仅允许用户使用CloudFormation服务角色部署CloudFormation堆栈。使用CloudFormation漂移检测来检测资源何时偏离其预期状态。
B. 仅允许用户使用CloudFormation服务角色部署CloudFormation堆栈。使用AWS Config规则来检测资源何时偏离其预期状态。
C. 仅允许用户通过AWS Service Catalog部署CloudFormation堆栈。强制使用启动约束。使用AWS Config规则来检测资源何时偏离其预期状态。
D. 仅允许用户通过AWS Service Catalog部署CloudFormation堆栈。强制使用模板约束。使用Amazon EventBridge通知来检测资源何时偏离其预期状态。

 | **选项A：**
- 优点：CloudFormation服务角色可以控制权限，CloudFormation漂移检测可以检测配置偏移
- 缺点：无法确保用户只使用预先批准的模板，用户仍可以使用任意模板；CloudFormation漂移检测需要手动触发，不是自动化的

**选项B：**
- 优点：AWS Config规则可以提供持续的自动化监控
- 缺点：同样无法确保用户只使用预先批准的模板，缺乏模板治理机制

**选项C：**
- 优点：AWS Service Catalog专门用于管理预先批准的模板和产品组合；启动约束可以控制部署权限；AWS Config规则提供持续自动化监控
- 缺点：启动约束主要用于控制谁可以启动产品，而不是限制使用哪些模板

**选项D：**
- 优点：AWS Service Catalog确保使用预批准模板；模板约束可以限制模板参数和配置
- 缺点：EventBridge本身不能直接检测资源配置漂移，需要与其他服务配合

 |  |  |  |
| 182 | A company has multiple development groups working in a single shared AWS account. The senior manager of the groups wants to be alerted
via a third-party API call when the creation of resources approaches the service limits for the account. | A. Create an Amazon EventBridge rule that runs periodically and targets an AWS Lambda function. Within the Lambda function, evaluate
the current state of the AWS environment and compare deployed resource values to resource limits on the account. Notify the senior
manager if the account is approaching a service limit.
B. Deploy an AWS Lambda function that refreshes AWS Trusted Advisor checks, and congure an Amazon EventBridge rule to run the
Lambda function periodically. Create another EventBridge rule with an event pattern matching Trusted Advisor events and a target
Lambda function. In the target Lambda function, notify the senior manager.
C. Deploy an AWS Lambda function that refreshes AWS Health Dashboard checks, and congure an Amazon EventBridge rule to run the
Lambda function periodically. Create another EventBridge rule with an event pattern matching Health Dashboard events and a target
Lambda function. In the target Lambda function, notify the senior manager.
D. Add an AWS Cong custom rule that runs periodically, checks the AWS service limit status, and streams notications to an Amazon
Simple Notication Service (Amazon SNS) topic. Deploy an AWS Lambda function that noties the senior manager, and subscribe the
Lambda function to the SNS topic. | 一家公司有多个开发团队在单个共享的AWS账户中工作。团队的高级经理希望在资源创建接近账户服务限制时，通过第三方API调用收到警报。

 | **选项A：** 创建一个定期运行的Amazon EventBridge规则，目标为AWS Lambda函数。在Lambda函数中，评估AWS环境的当前状态，并将已部署的资源值与账户的资源限制进行比较。如果账户接近服务限制，则通知高级经理。

- **分析：** 这个方案需要手动实现所有的服务限制检查逻辑，包括获取各种AWS服务的当前使用量和限制值。这种方法复杂度高，维护困难，且容易出错。需要为每个AWS服务编写特定的检查代码。

**选项B：** 部署一个AWS Lambda函数来刷新AWS Trusted Advisor检查，并配置Amazon EventBridge规则定期运行该Lambda函数。创建另一个EventBridge规则，使用事件模式匹配Trusted Advisor事件，并以Lambda函数为目标。在目标Lambda函数中通知高级经理。

- **分析：** 这是最佳方案。AWS Trusted Advisor专门提供服务限制监控功能，包括"Service Limits"检查。它能够自动监控各种AWS服务的使用情况并与限制进行比较。通过EventBridge可以捕获Trusted Advisor的状态变化事件，实现自动化通知。

**选项C：** 部署一个AWS Lambda函数来刷新AWS Health Dashboard检查，并配置Amazon EventBridge规则定期运行该Lambda函数。创建另一个EventBridge规则，使用事件模式匹配Health Dashboard事件，并以Lambda函数为目标。在目标Lambda函数中通知高级经理。

- **分析：** AWS Health Dashboard主要关注AWS服务的健康状态和计划维护事件，而不是服务限制监控。虽然它可能包含一些限制相关的信息，但这不是它的主要功能，不适合用于服务限制监控。

**选项D：** 添加一个定期运行的AWS Config自定义规则，检查AWS服务限制状态，并将通知流式传输到Amazon SNS主题。部署一个通知高级经理的AWS Lambda函数，并将该Lambda函数订阅到SNS主题。

- **分析：** AWS Config主要用于配置合规性检查，而不是服务限制监控。虽然可以创建自定义规则来检查服务限制，但这需要大量的自定义开发工作，且不如使用专门的服务限制监控工具高效。

 |  |  |  |
| 183 | A DevOps engineer is setting up a container-based architecture. The engineer has decided to use AWS CloudFormation to automatically
provision an Amazon ECS cluster and an Amazon EC2 Auto Scaling group to launch the EC2 container instances. After successfully creating
the CloudFormation stack, the engineer noticed that, even though the ECS cluster and the EC2 instances were created successfully and the
stack nished the creation, the EC2 instances were associating with a different cluster.
How should the DevOps engineer update the CloudFormation template to resolve this issue? | A. Reference the EC2 instances in the AWS::ECS::Cluster resource and reference the ECS cluster in the AWS::ECS::Service resource.
B. Reference the ECS cluster in the AWS::AutoScaling::LaunchConguration resource of the UserData property.
C. Reference the ECS cluster in the AWS::EC2::Instance resource of the UserData property.
D. Reference the ECS cluster in the AWS::CloudFormation::CustomResource resource to trigger an AWS Lambda function that registers the
EC2 instances with the appropriate ECS cluster. | 一名DevOps工程师正在设置基于容器的架构。该工程师决定使用AWS CloudFormation自动配置Amazon ECS集群和Amazon EC2 Auto Scaling组来启动EC2容器实例。在成功创建CloudFormation堆栈后，工程师注意到，尽管ECS集群和EC2实例都成功创建且堆栈完成了创建，但EC2实例关联到了不同的集群。

DevOps工程师应该如何更新CloudFormation模板来解决这个问题？

 | **选项A：在AWS::ECS::Cluster资源中引用EC2实例，并在AWS::ECS::Service资源中引用ECS集群。**
- 这个选项不正确。AWS::ECS::Cluster资源不需要直接引用EC2实例，而且这不是解决EC2实例关联到错误集群的正确方法。ECS集群的创建和EC2实例的注册是分离的过程。

**选项B：在AWS::AutoScaling::LaunchConfiguration资源的UserData属性中引用ECS集群。**
- 这个选项是正确的。在Auto Scaling组的启动配置中，通过UserData脚本可以配置ECS代理，指定EC2实例应该加入哪个ECS集群。这是标准的做法，通过在UserData中设置ECS_CLUSTER环境变量来实现。

**选项C：在AWS::EC2::Instance资源的UserData属性中引用ECS集群。**
- 虽然技术上可行，但题目中提到使用的是Auto Scaling组，而不是单独的EC2实例。因此这个选项不符合题目描述的架构。

**选项D：在AWS::CloudFormation::CustomResource资源中引用ECS集群，触发AWS Lambda函数将EC2实例注册到适当的ECS集群。**
- 这个选项过于复杂且不必要。使用自定义资源和Lambda函数来处理这个问题是过度工程化的解决方案，当有更简单直接的方法时不应该选择。

 |  |  |  |
| 184 | A DevOps engineer is implementing governance controls for a company that requires its infrastructure to be housed within the United States.
The engineer must restrict which AWS Regions can be used, and ensure an alert is sent as soon as possible if any activity outside the
governance policy takes place. The controls should be automatically enabled on any new Region outside the United States (US). | A. Create an AWS Organizations SCP that denies access to all non-global services in non-US Regions. Attach the policy to the root of the
organization.
B. Congure AWS CloudTrail to send logs to Amazon CloudWatch Logs and enable it for all Regions. Use a CloudWatch Logs metric lter to
send an alert on any service activity in non-US Regions.
C. Use an AWS Lambda function that checks for AWS service activity and deploy it to all Regions. Write an Amazon EventBridge rule that
runs the Lambda function every hour, sending an alert if activity is found in a non-US Region.
D. Use an AWS Lambda function to query Amazon Inspector to look for service activity in non-US Regions and send alerts if any activity is
found.
E. Write an SCP using the aws:RequestedRegion condition key limiting access to US Regions. Apply the policy to all users, groups, and
roles. |  |  |  |  |  |
| 185 | A company sells products through an ecommerce web application. The company wants a dashboard that shows a pie chart of product
transaction details. The company wants to integrate the dashboard with the company's existing Amazon CloudWatch dashboards. | A. Update the ecommerce application to emit a JSON object to a CloudWatch log group for each processed transaction. Use CloudWatch
Logs Insights to query the log group and to visualize the results in a pie chart format. Attach the results to the desired CloudWatch
dashboard.
B. Create a Lambda subscription lter for the log le. Attach the
results to the desired CloudWatch dashboard.
C. Update the ecommerce application to use AWS X-Ray for instrumentation. Create a new X-Ray subsegment. Add an annotation for each
processed transaction. Use X-Ray traces to query the data and to visualize the results in a pie chart format. Attach the results to the
desired CloudWatch dashboard.
D. Update the ecommerce application to emit a JSON object to a CloudWatch log group for each processed transaction. Create an AWS
Lambda function to aggregate and write the results to Amazon DynamoD | 一家公司通过电子商务网络应用程序销售产品。该公司希望有一个仪表板，显示产品交易详情的饼图。公司希望将此仪表板与公司现有的Amazon CloudWatch仪表板集成。

 | **选项A：** 更新电子商务应用程序，为每个处理的交易向CloudWatch日志组发送JSON对象。使用CloudWatch Logs Insights查询日志组并以饼图格式可视化结果。将结果附加到所需的CloudWatch仪表板。

- ✅ **正确方案**：CloudWatch Logs Insights支持查询和聚合日志数据
- ✅ 可以直接在CloudWatch仪表板中创建饼图可视化
- ✅ 与现有CloudWatch仪表板完美集成
- ✅ 实现简单，成本效益高

**选项B：** 为日志文件创建Lambda订阅过滤器。将结果附加到所需的CloudWatch仪表板。

- ❌ **描述不完整**：选项被截断，缺少关键实现细节
- ❌ 没有说明如何处理数据聚合和可视化
- ❌ Lambda订阅过滤器主要用于实时处理，不是最佳的仪表板数据源

**选项C：** 更新电子商务应用程序使用AWS X-Ray进行仪表化。创建新的X-Ray子段。为每个处理的交易添加注释。使用X-Ray跟踪查询数据并以饼图格式可视化结果。将结果附加到CloudWatch仪表板。

- ❌ **工具用途不匹配**：X-Ray主要用于分布式跟踪和性能监控
- ❌ X-Ray不是为业务指标聚合和报告设计的
- ❌ 无法直接在CloudWatch仪表板中显示X-Ray数据的饼图
- ❌ 过度复杂化了简单的业务指标需求

**选项D：** 更新电子商务应用程序，为每个处理的交易向CloudWatch日志组发送JSON对象。创建AWS Lambda函数来聚合结果并写入Amazon DynamoDB...

- ❌ **描述不完整**：选项被截断
- ❌ 引入了不必要的复杂性（DynamoDB）
- ❌ 需要额外的组件和维护成本

 |  |  |  |
| 186 | A company is launching an application. The application must use only approved AWS services. The account that runs the application was
created less than 1 year ago and is assigned to an AWS Organizations OU.
The company needs to create a new Organizations account structure. The account structure must have an appropriate SCP that supports the
use of only services that are currently active in the AWS account. The company will use AWS Identity and Access Management (IAM) Access
Analyzer in the solution. | A. Create an SCP that allows the services that IAM Access Analyzer identies. Create an OU for the account. Move the account into the
new OU. Attach the new SCP to the new OU. Detach the default FullAWSAccess SCP from the new OU.
B. Create an SCP that denies the services that IAM Access Analyzer identies. Create an OU for the account. Move the account into the
new OU. Attach the new SCP to the new OU.
C. Create an SCP that allows the services that IAM Access Analyzer identies. Attach the new SCP to the organization's root.
D. Create an SCP that allows the services that IAM Access Analyzer identies. Create an OU for the account. Move the account into the
new OU. Attach the new SCP to the management account. Detach the default FullAWSAccess SCP from the new OU. | 一家公司正在启动一个应用程序。该应用程序必须只使用经过批准的AWS服务。运行该应用程序的账户创建时间不到1年，并被分配到一个AWS Organizations组织单元(OU)中。

公司需要创建一个新的Organizations账户结构。该账户结构必须具有适当的服务控制策略(SCP)，支持仅使用当前在AWS账户中活跃的服务。公司将在解决方案中使用AWS身份和访问管理(IAM) Access Analyzer。

 | **选项A：** 创建一个允许IAM Access Analyzer识别的服务的SCP。为账户创建一个OU。将账户移动到新的OU中。将新的SCP附加到新的OU。从新的OU中分离默认的FullAWSAccess SCP。
- ✅ 正确：创建允许策略来限制只能使用已识别的服务
- ✅ 正确：创建专门的OU进行隔离管理
- ✅ 正确：将SCP附加到OU是正确的做法
- ✅ 正确：移除FullAWSAccess SCP是必要的，否则会覆盖限制性策略

**选项B：** 创建一个拒绝IAM Access Analyzer识别的服务的SCP。为账户创建一个OU。将账户移动到新的OU中。将新的SCP附加到新的OU。
- ❌ 错误：创建拒绝策略会阻止当前正在使用的服务，这与需求相反
- ✅ 正确：OU创建和移动操作是对的
- ❌ 关键错误：没有移除FullAWSAccess SCP，意味着除了被明确拒绝的服务外，其他所有服务仍然可用

**选项C：** 创建一个允许IAM Access Analyzer识别的服务的SCP。将新的SCP附加到组织的根。
- ✅ 正确：创建允许策略
- ❌ 错误：附加到根会影响整个组织的所有账户，而不是仅针对特定账户
- ❌ 错误：没有创建专门的OU进行隔离管理

**选项D：** 创建一个允许IAM Access Analyzer识别的服务的SCP。为账户创建一个OU。将账户移动到新的OU中。将新的SCP附加到管理账户。从新的OU中分离默认的FullAWSAccess SCP。
- ✅ 正确：创建允许策略
- ✅ 正确：创建OU和移动账户
- ❌ 错误：将SCP附加到管理账户而不是目标OU，这不会对目标账户产生预期的限制效果
- ✅ 正确：移除FullAWSAccess SCP

 | A |  |  |
| 187 | A company has multiple development teams in different business units that work in a shared single AWS account. All Amazon EC2 resources
that are created in the account must include tags that specify who created the resources. The tagging must occur within the rst hour of
resource creation.
A DevOps engineer needs to add tags to the created resources that include the user ID that created the resource and the cost center I | D. Create an Amazon EventBridge rule that uses Amazon EC2 as the event source. Congure the rule to match events delivered by
CloudTrail. Congure the rule to target the Lambda function.
A. Create an S3 event notication on the S3 bucket to invoke the Lambda function for s3:ObjectTagging:Put events. Enable bucket
versioning on the S3 bucket.
B. Enable server access logging on the S3 bucket. Create an S3 event notication on the S3 bucket for s3:ObjectTagging:* events.
C. Create a recurring hourly Amazon EventBridge scheduled rule that invokes the Lambda function. Modify the Lambda function to read
the logs from the S3 bucket. |  |  |  |  |  |
| 188 | A company runs an application for multiple environments in a single AWS account. An AWS CodePipeline pipeline uses a development
Amazon Elastic Container Service (Amazon ECS) cluster to test an image for the application from an Amazon Elastic Container Registry
(Amazon ECR) repository. The pipeline promotes the image to a production ECS cluster.
The company needs to move the production cluster into a separate AWS account in the same AWS Region. The production cluster must be
able to download the images over a private connection. | A. Use Amazon ECR VPC endpoints and an Amazon S3 gateway endpoint. In the separate AWS account, create an ECR repository. Set the
repository policy to allow the production ECS tasks to pull images from the main AWS account. Congure the production ECS task
execution role to have permission to download the image from the ECR repository.
B. Set a repository policy on the production ECR repository in the main AWS account. Congure the repository policy to allow the
production ECS tasks in the separate AWS account to pull images from the main account. Congure the production ECS task execution
role to have permission to download the image from the ECR repository.
C. Congure ECR private image replication in the main AWS account. Activate cross-account replication. Dene the destination account ID
of the separate AWS account.
D. Use Amazon ECR VPC endpoints and an Amazon S3 gateway endpoint. Set a repository policy on the production ECR repository in the
main AWS account. Congure the repository policy to allow the production ECS tasks in the separate AWS account to pull images from the
main account. Congure the production ECS task execution role to have permission to download the image from the ECR repository. | 一家公司在单个AWS账户中为多个环境运行应用程序。AWS CodePipeline管道使用开发环境的Amazon Elastic Container Service (Amazon ECS)集群来测试来自Amazon Elastic Container Registry (Amazon ECR)存储库的应用程序镜像。该管道将镜像推广到生产ECS集群。

公司需要将生产集群迁移到同一AWS区域的单独AWS账户中。生产集群必须能够通过私有连接下载镜像。

 | **选项A：** 使用Amazon ECR VPC端点和Amazon S3网关端点。在单独的AWS账户中创建ECR存储库。设置存储库策略以允许生产ECS任务从主AWS账户拉取镜像。配置生产ECS任务执行角色具有从ECR存储库下载镜像的权限。
- **问题：** 在单独账户中创建新的ECR存储库没有必要，因为可以直接从主账户拉取镜像。这种方法增加了不必要的复杂性。

**选项B：** 在主AWS账户的生产ECR存储库上设置存储库策略。配置存储库策略以允许单独账户中的生产ECS任务从主账户拉取镜像。配置生产ECS任务执行角色具有从ECR存储库下载镜像的权限。
- **问题：** 缺少私有连接的配置。题目明确要求通过私有连接下载镜像，但此选项没有提及VPC端点的配置。

**选项C：** 在主AWS账户中配置ECR私有镜像复制。激活跨账户复制。定义单独账户的目标账户ID。
- **问题：** 虽然这能实现跨账户镜像访问，但ECR复制功能主要用于灾难恢复和就近访问，不是为了解决私有连接需求。且复制会产生额外的存储成本。

**选项D：** 使用Amazon ECR VPC端点和Amazon S3网关端点。在主AWS账户的生产ECR存储库上设置存储库策略。配置存储库策略以允许单独账户中的生产ECS任务从主账户拉取镜像。配置生产ECS任务执行角色具有从ECR存储库下载镜像的权限。
- **优势：** 
  - 包含了VPC端点配置，满足私有连接要求
  - 正确配置了跨账户访问权限
  - S3网关端点用于ECR底层存储访问
  - 配置了必要的IAM权限

 |  |  |  |
| 189 | A company needs to ensure that ow logs remain congured for all existing and new VPCs in its AWS account. The company uses an AWS
CloudFormation stack to manage its VPCs. The company needs a solution that will work for any VPCs that any IAM user creates. | A. Add the AWS::EC2::FlowLog resource to the CloudFormation stack that creates the VPCs.
B. Create an organization in AWS Organizations. Add the company's AWS account to the organization. Create an SCP to prevent users from
modifying VPC ow logs.
C. Turn on AWS Cong. Create an AWS Cong rule to check whether VPC ow logs are turned on. Congure automatic remediation to turn
on VPC ow logs.
D. Create an IAM policy to deny the use of API calls for VPC ow logs. Attach the IAM policy to all IAM users. | 一家公司需要确保其AWS账户中所有现有和新建的VPC都配置了流日志。该公司使用AWS CloudFormation堆栈来管理其VPC。公司需要一个解决方案，能够适用于任何IAM用户创建的任何VPC。

选项：
A. 将AWS::EC2::FlowLog资源添加到创建VPC的CloudFormation堆栈中。
B. 在AWS Organizations中创建一个组织。将公司的AWS账户添加到组织中。创建一个SCP来防止用户修改VPC流日志。
C. 启用AWS Config。创建一个AWS Config规则来检查VPC流日志是否已启用。配置自动修复来启用VPC流日志。
D. 创建一个IAM策略来拒绝使用VPC流日志的API调用。将IAM策略附加到所有IAM用户。

 | **选项A：将AWS::EC2::FlowLog资源添加到创建VPC的CloudFormation堆栈中**
- 这个方案只能覆盖通过特定CloudFormation堆栈创建的VPC
- 无法处理IAM用户通过其他方式（如控制台、CLI、其他CloudFormation模板）创建的VPC
- 不满足"适用于任何IAM用户创建的任何VPC"的要求

**选项B：在AWS Organizations中创建组织并使用SCP防止用户修改VPC流日志**
- SCP只能防止用户修改流日志，但不能自动为新VPC创建流日志
- 这是一个预防性措施，而不是主动配置流日志的解决方案
- 无法解决为现有VPC和新VPC自动配置流日志的核心需求

**选项C：启用AWS Config并创建Config规则检查VPC流日志，配置自动修复**
- AWS Config可以持续监控所有VPC的配置状态
- Config规则可以检测哪些VPC没有启用流日志
- 自动修复功能可以自动为不合规的VPC启用流日志
- 这个方案适用于所有VPC，无论是如何创建的
- 能够处理现有VPC和未来创建的VPC

**选项D：创建IAM策略拒绝VPC流日志API调用并附加到所有IAM用户**
- 这个方案会阻止用户使用流日志功能，与需求完全相反
- 目标是确保流日志被配置，而不是阻止其使用
- 这个选项明显不符合要求

 |  |  |  |
| 190 | A company's application teams use AWS CodeCommit repositories for their applications. The application teams have repositories in multiple
AWS accounts. All accounts are in an organization in AWS Organizations.
Each application team uses AWS IAM Identity Center (AWS Single Sign-On) congured with an external IdP to assume a developer IAM role.
The developer role allows the application teams to use Git to work with the code in the repositories.
A security audit reveals that the application teams can modify the main branch in any repository. A DevOps engineer must implement a
solution that allows the application teams to modify the main branch of only the repositories that they manage. | A. Update the SAML assertion to pass the user's team name. Update the IAM role's trust policy to add an access-team session tag that has
the team name.
B. Create an approval rule template for each team in the Organizations management account. Associate the template with all the
repositories. Add the developer role ARN as an approver.
C. Create an approval rule template for each account. Associate the template with all repositories. Add the "aws:ResourceTag/access-
team": "$ ;{aws:PrincipalTag/access-team}" condition to the approval rule template.
D. For each CodeCommit repository, add an access-team tag that has the value set to the name of the associated team.
E. Attach an SCP to the accounts. Include the following statement: |  |  |  |  |  |
| 191 | A company uses AWS WAF to protect its cloud infrastructure. A DevOps engineer needs to give an operations team the ability to analyze log
messages from AWS WAF. The operations team needs to be able to create alarms for specic patterns in the log output. | A. Create an Amazon CloudWatch Logs log group. Congure the appropriate AWS WAF web ACL to send log messages to the log group.
Instruct the operations team to create CloudWatch metric lters.
B. Create an Amazon OpenSearch Service cluster and appropriate indexes. Congure an Amazon Kinesis Data Firehose delivery stream to
stream log data to the indexes. Use OpenSearch Dashboards to create lters and widgets.
C. Create an Amazon S3 bucket for the log output. Congure AWS WAF to send log outputs to the S3 bucket. Instruct the operations team
to create AWS Lambda functions that detect each desired log message pattern. Congure the Lambda functions to publish to an Amazon
Simple Notication Service (Amazon SNS) topic.
D. Create an Amazon S3 bucket for the log output. Congure AWS WAF to send log outputs to the S3 bucket. Use Amazon Athena to create
an external table denition that ts the log message pattern. Instruct the operations team to write SQL queries and to create Amazon
CloudWatch metric lters for the Athena queries. | 一家公司使用AWS WAF来保护其云基础设施。DevOps工程师需要为运维团队提供分析AWS WAF日志消息的能力。运维团队需要能够为日志输出中的特定模式创建告警。

选项：
A. 创建Amazon CloudWatch Logs日志组。配置相应的AWS WAF web ACL将日志消息发送到日志组。指导运维团队创建CloudWatch指标过滤器。

B. 创建Amazon OpenSearch Service集群和相应的索引。配置Amazon Kinesis Data Firehose传输流将日志数据流式传输到索引。使用OpenSearch Dashboards创建过滤器和小部件。

C. 为日志输出创建Amazon S3存储桶。配置AWS WAF将日志输出发送到S3存储桶。指导运维团队创建AWS Lambda函数来检测每个所需的日志消息模式。配置Lambda函数发布到Amazon Simple Notification Service (Amazon SNS)主题。

D. 为日志输出创建Amazon S3存储桶。配置AWS WAF将日志输出发送到S3存储桶。使用Amazon Athena创建符合日志消息模式的外部表定义。指导运维团队编写SQL查询并为Athena查询创建Amazon CloudWatch指标过滤器。

 | **选项A分析：**
- ✅ AWS WAF支持直接将日志发送到CloudWatch Logs
- ✅ CloudWatch指标过滤器可以基于日志模式创建自定义指标
- ✅ 可以基于这些指标轻松创建CloudWatch告警
- ✅ 解决方案简单、直接，符合AWS最佳实践
- ✅ 成本效益高，无需额外的复杂服务

**选项B分析：**
- ✅ 技术上可行，OpenSearch提供强大的日志分析能力
- ❌ 过于复杂，需要管理OpenSearch集群
- ❌ 成本较高，OpenSearch集群需要持续运行
- ❌ 对于简单的模式匹配和告警需求来说过度设计
- ❌ 需要额外配置Kinesis Data Firehose

**选项C分析：**
- ✅ AWS WAF可以将日志发送到S3
- ❌ 需要自定义Lambda函数来处理日志分析
- ❌ 实现复杂，需要编写和维护Lambda代码
- ❌ 不是实时分析，S3存储有延迟
- ❌ 维护成本高，需要管理多个组件

**选项D分析：**
- ✅ AWS WAF可以将日志发送到S3
- ❌ Athena主要用于批量查询，不适合实时告警
- ❌ CloudWatch无法直接为Athena查询创建指标过滤器
- ❌ 架构复杂，不适合实时监控需求
- ❌ 查询成本可能较高

 |  |  |  |
| 192 | A software team is using AWS CodePipeline to automate its Java application release pipeline. The pipeline consists of a source stage, then a
build stage, and then a deploy stage. Each stage contains a single action that has a runOrder value of 1.
The team wants to integrate unit tests into the existing release pipeline. The team needs a solution that deploys only the code changes that
pass all unit tests. | A. Modify the build stage. Add a test action that has a runOrder value of 1. Use AWS CodeDeploy as the action provider to run unit tests.
B. Modify the build stage. Add a test action that has a runOrder value of 2. Use AWS CodeBuild as the action provider to run unit tests.
C. Modify the deploy stage. Add a test action that has a runOrder value of 1. Use AWS CodeDeploy as the action provider to run unit tests.
D. Modify the deploy stage. Add a test action that has a runOrder value of 2. Use AWS CodeBuild as the action provider to run unit tests. | 一个软件团队正在使用AWS CodePipeline来自动化其Java应用程序发布管道。该管道包含一个源代码阶段，然后是构建阶段，最后是部署阶段。每个阶段都包含一个runOrder值为1的单一操作。

团队希望将单元测试集成到现有的发布管道中。团队需要一个解决方案，只部署通过所有单元测试的代码更改。

 | **选项A：修改构建阶段。添加一个runOrder值为1的测试操作。使用AWS CodeDeploy作为操作提供者来运行单元测试。**
- ❌ 错误：AWS CodeDeploy是用于应用程序部署的服务，不是用于运行单元测试的
- ❌ runOrder值为1意味着与现有构建操作并行执行，这可能导致测试在构建完成前就开始运行

**选项B：修改构建阶段。添加一个runOrder值为2的测试操作。使用AWS CodeBuild作为操作提供者来运行单元测试。**
- ✅ 正确：AWS CodeBuild是执行构建和测试任务的正确服务
- ✅ runOrder值为2确保测试在构建完成后执行
- ✅ 在构建阶段进行测试符合CI/CD最佳实践，确保只有通过测试的代码才会进入部署阶段

**选项C：修改部署阶段。添加一个runOrder值为1的测试操作。使用AWS CodeDeploy作为操作提供者来运行单元测试。**
- ❌ 错误：AWS CodeDeploy不适合运行单元测试
- ❌ 在部署阶段运行测试违背了CI/CD原则，应该在部署前进行测试

**选项D：修改部署阶段。添加一个runOrder值为2的测试操作。使用AWS CodeBuild作为操作提供者来运行单元测试。**
- ❌ 错误：虽然使用CodeBuild是正确的，但在部署阶段运行单元测试不符合最佳实践
- ❌ 这种方式意味着代码会先部署，然后才进行测试，这与需求不符

 |  |  |  |
| 193 | A company uses an organization in AWS Organizations to manage several AWS accounts that the company's developers use. The company
requires all data to be encrypted in transit.
Multiple Amazon S3 buckets that were created in developer accounts allow unencrypted connections. A DevOps engineer must enforce
encryption of data in transit for all existing S3 buckets that are created in accounts in the organization. | A. Use AWS CloudFormation StackSets to deploy an AWS Network Firewall rewall to each account. Route all outbound requests from the
AWS environment through the rewall. Deploy a policy to block access to all outbound requests on port 80.
B. Use AWS CloudFormation StackSets to deploy an AWS Network Firewall rewall to each account. Route all inbound requests to the AWS
environment through the rewall. Deploy a policy to block access to all inbound requests on port 80.
C. Turn on AWS Cong for the organization. Deploy a conformance pack that uses the s3-bucket-ssl-requests-only managed rule and an
AWS Systems Manager Automation runbook. Use a runbook that adds a bucket policy statement to deny access to an S3 bucket when the
value of the aws:SecureTransport condition key is false.
D. Turn on AWS Cong for the organization. Deploy a conformance pack that uses the s3-bucket-ssl-requests-only managed rule and an
AWS Systems Manager Automation runbook. Use a runbook that adds a bucket policy statement to deny access to an S3 bucket when the
value of the s3:x-amz-server-side-encryption-aws-kms-key-id condition key is null. |  |  |  |  |  |
| 194 | A company is reviewing its IAM policies. One policy written by the DevOps engineer has been agged as too permissive. The policy is used by
an AWS Lambda function that issues a stop command to Amazon EC2 instances tagged with Environment: NonProduction over the weekend.
The current policy is: | A. Add the following conditional expression:
B. Change "Resource": "*"to "Resource": "arn:aws:ec2:*:*:instance/*"
C. Add the following conditional expression:
D. Add the following conditional expression:
E. Change "Action": "ec2:*"to "Action": "ec2:StopInstances"
F. Add the following conditional expression: | 一家公司正在审查其IAM策略。DevOps工程师编写的一个策略被标记为权限过于宽泛。该策略被一个AWS Lambda函数使用，该函数在周末向标记为Environment: NonProduction的Amazon EC2实例发出停止命令。当前策略是：[策略内容未完整提供]

 | 基于题目描述和常见的IAM权限收紧最佳实践，我可以分析可能的选项：

**A, C, D, F选项** - 添加条件表达式：
- 这些选项可能包含基于标签的条件限制，如限制只能操作Environment: NonProduction标签的实例
- 条件表达式是限制权限范围的有效方法

**B选项** - 将"Resource": "*"改为"Resource": "arn:aws:ec2:*:*:instance/*"：
- 这确实会限制资源范围，从所有AWS资源缩小到只有EC2实例
- 这是一个有效的权限收紧措施

**E选项** - 将"Action": "ec2:*"改为"Action": "ec2:StopInstances"：
- 这将操作权限从所有EC2操作缩小到仅停止实例操作
- 符合最小权限原则，是很好的改进

 |  |  |  |
| 195 | A company is developing an application that will generate log events. The log events consist of ve distinct metrics every one tenth of a
second and produce a large amount of data.
The company needs to congure the application to write the logs to Amazon Timestream. The company will congure a daily query against
the Timestream table. | A. Use batch writes to write multiple log events in a single write operation.
B. Write each log event as a single write operation.
C. Treat each log as a single-measure record.
D. Treat each log as a multi-measure record.
E. Congure the memory store retention period to be longer than the magnetic store retention period.
F. Congure the memory store retention period to be shorter than the magnetic store retention period. |  |  |  |  |  |
| 196 | A DevOps engineer has created an AWS CloudFormation template that deploys an application on Amazon EC2 instances. The EC2 instances
run Amazon Linux. The application is deployed to the EC2 instances by using shell scripts that contain user data. The EC2 instances have an
IAM instance prole that has an IAM role with the AmazonSSMManagedinstanceCore managed policy attached.
The DevOps engineer has modied the user data in the CloudFormation template to install a new version of the application. The engineer has
also applied the stack update. However, the application was not updated on the running EC2 instances. The engineer needs to ensure that the
changes to the application are installed on the running EC2 instances. | A. Congure the user data content to use the Multipurpose Internet Mail Extensions (MIME) multipart format. Set the scripts-user
parameter to always in the text/cloud-cong section.
B. Refactor the user data commands to use the cfn-init helper script. Update the user data to install and congure the cfn-hup and cfn-init
helper scripts to monitor and apply the metadata changes.
C. Congure an EC2 launch template for the EC2 instances. Create a new EC2 Auto Scaling group. Associate the Auto Scaling group with
the EC2 launch template. Use the AutoScalingScheduledAction update policy for the Auto Scaling group.
D. Refactor the user data commands to use an AWS Systems Manager document (SSM document). Add an AWS CLI command in the user
data to use Systems Manager Run Command to apply the SSM document to the EC2 instances.
E. Refactor the user data command to use an AWS Systems Manager document (SSM document). Use Systems Manager State Manager to
create an association between the SSM document and the EC2 instances. | 一名DevOps工程师创建了一个AWS CloudFormation模板，该模板在Amazon EC2实例上部署应用程序。EC2实例运行Amazon Linux。应用程序通过包含用户数据的shell脚本部署到EC2实例上。EC2实例具有IAM实例配置文件，该配置文件有一个附加了AmazonSSMManagedInstanceCore托管策略的IAM角色。

DevOps工程师已修改了CloudFormation模板中的用户数据以安装新版本的应用程序。工程师也已应用了堆栈更新。但是，应用程序并未在运行的EC2实例上更新。工程师需要确保应用程序的更改安装在运行的EC2实例上。

 | **A. 配置用户数据内容使用多用途互联网邮件扩展(MIME)多部分格式。在text/cloud-config部分将scripts-user参数设置为always。**
- 这个选项涉及cloud-init配置，scripts-user设置为always可以让脚本在每次启动时运行
- 但这只在实例重启时有效，对于已运行的实例无法解决问题
- 不是最佳解决方案

**B. 重构用户数据命令以使用cfn-init辅助脚本。更新用户数据以安装和配置cfn-hup和cfn-init辅助脚本来监控和应用元数据更改。**
- cfn-init用于处理CloudFormation元数据
- cfn-hup是一个守护进程，可以监控CloudFormation元数据的更改并自动应用
- 这是CloudFormation的标准解决方案，可以在不重启实例的情况下应用更新
- 非常适合这个场景

**C. 为EC2实例配置EC2启动模板。创建新的EC2 Auto Scaling组。将Auto Scaling组与EC2启动模板关联。为Auto Scaling组使用AutoScalingScheduledAction更新策略。**
- 这需要重新创建实例架构，过于复杂
- AutoScalingScheduledAction是用于计划扩展的，不适用于应用程序更新
- 不是针对现有实例的解决方案

**D. 重构用户数据命令以使用AWS Systems Manager文档(SSM文档)。在用户数据中添加AWS CLI命令，使用Systems Manager Run Command将SSM文档应用到EC2实例。**
- 虽然可以工作，但在用户数据中使用Run Command不是最佳实践
- 用户数据主要在实例启动时执行，不适合持续管理
- 比较复杂且不够优雅

**E. 重构用户数据命令以使用AWS Systems Manager文档(SSM文档)。使用Systems Manager State Manager在SSM文档和EC2实例之间创建关联。**
- State Manager可以确保实例保持所需状态
- 但这改变了整个架构，从CloudFormation转向SSM
- 虽然是有效解决方案，但不是最直接的

 | B |  |  |
| 197 | A company is refactoring applications to use AWS. The company identies an internal web application that needs to make Amazon S3 API
calls in a specic AWS account.
The company wants to use its existing identity provider (IdP) auth.company.com for authentication. The IdP supports only OpenID Connect
(OIDC). A DevOps engineer needs to secure the web application's access to the AWS account. | A. Congure AWS IAM Identity Center (AWS Single Sign-On). Congure an IdP. Upload the IdP metadata from the existing IdP.
B. Create an IAM IdP by using the provider URL, audience, and signature from the existing IP.
C. Create an IAM role that has a policy that allows the necessary S3 actions. Congure the role's trust policy to allow the OIDC IP to
assume the role if the sts.amazon.com:aud context key is appid_from_idp.
D. Create an IAM role that has a policy that allows the necessary S3 actions. Congure the role's trust policy to allow the OIDC IP to
assume the role if the auth.company.com:aud context key is appid_from_idp.
E. Congure the web application to use the AssumeRoleWithWebIdentity API operation to retrieve temporary credentials. Use the
temporary credentials to make the S3 API calls. | 一家公司正在重构应用程序以使用AWS。该公司识别出一个内部Web应用程序需要在特定AWS账户中进行Amazon S3 API调用。

该公司希望使用其现有的身份提供商(IdP) auth.company.com进行身份验证。该IdP仅支持OpenID Connect (OIDC)。DevOps工程师需要保护Web应用程序对AWS账户的访问。

 | **选项A：** 配置AWS IAM Identity Center (AWS Single Sign-On)。配置IdP。从现有IdP上传IdP元数据。
- **分析：** IAM Identity Center主要用于SAML联合身份验证，而题目明确说明IdP仅支持OIDC。这种方法不适用于OIDC场景。

**选项B：** 使用现有IdP的提供商URL、受众和签名创建IAM IdP。
- **分析：** 这是配置OIDC身份提供商的正确步骤。需要在AWS IAM中创建OIDC身份提供商，使用IdP的URL、受众等信息。这是必要的配置步骤。

**选项C：** 创建具有允许必要S3操作策略的IAM角色。配置角色的信任策略，允许OIDC IdP在sts.amazon.com:aud上下文键为appid_from_idp时承担该角色。
- **分析：** 信任策略中的条件键不正确。sts.amazon.com:aud不是OIDC联合身份验证的正确条件键格式。

**选项D：** 创建具有允许必要S3操作策略的IAM角色。配置角色的信任策略，允许OIDC IdP在auth.company.com:aud上下文键为appid_from_idp时承担该角色。
- **分析：** 这是正确的信任策略配置。对于OIDC IdP，条件键应该使用IdP的域名格式（auth.company.com:aud），这与题目中提到的IdP域名一致。

**选项E：** 配置Web应用程序使用AssumeRoleWithWebIdentity API操作来检索临时凭证。使用临时凭证进行S3 API调用。
- **分析：** 这是OIDC联合身份验证的正确实现方式。应用程序需要使用AssumeRoleWithWebIdentity API来获取临时AWS凭证。

 |  |  |  |
| 198 | A company uses Amazon RDS for all databases in its AWS accounts. The company uses AWS Control Tower to build a landing zone that has an
audit and logging account. All databases must be encrypted at rest for compliance reasons. The company's security engineer needs to receive
notication about any noncompliant databases that are in the company’s accounts. | A. Use AWS Control Tower to activate the optional detective control (guardrail) to determine whether the RDS storage is encrypted. Create
an Amazon Simple Notication Service (Amazon SNS) topic in the company's audit account. Create an Amazon EventBridge rule to lter
noncompliant events from the AWS Control Tower control (guardrail) to notify the SNS topic. Subscribe the security engineer's email
address to the SNS topic.
B. Use AWS CloudFormation StackSets to deploy AWS Lambda functions to every account. Write the Lambda function code to determine
whether the RDS storage is encrypted in the account the function is deployed to. Send the ndings as an Amazon CloudWatch metric to
the management account. Create an Amazon Simple Notication Service (Amazon SNS) topic. Create a CloudWatch alarm that noties the
SNS topic when metric thresholds are met. Subscribe the security engineer's email address to the SNS topic.
C. Create a custom AWS Cong rule in every account to determine whether the RDS storage is encrypted. Create an Amazon Simple
Notication Service (Amazon SNS) topic in the audit account. Create an Amazon EventBidge rule to lter noncompliant events from the
AWS Control Tower control (guardrail) to notify the SNS topic. Subscribe the security engineer's email address to the SNS topic.
D. Launch an Amazon C2 instance. Run an hourly cron job by using the AWS CLI to determine whether the RDS storage is encrypted in each
AWS account. Store the results in an RDS database. Notify the security engineer by sending email messages from the EC2 instance when
noncompliance is detected | 一家公司在其AWS账户中的所有数据库都使用Amazon RDS。该公司使用AWS Control Tower构建了一个包含审计和日志记录账户的着陆区。出于合规要求，所有数据库都必须进行静态加密。公司的安全工程师需要接收关于公司账户中任何不合规数据库的通知。

 | **选项A：** 使用AWS Control Tower激活可选的检测控制（护栏）来确定RDS存储是否加密。在公司的审计账户中创建Amazon SNS主题。创建Amazon EventBridge规则来过滤来自AWS Control Tower控制（护栏）的不合规事件，以通知SNS主题。将安全工程师的电子邮件地址订阅到SNS主题。

- **优点：** 利用AWS Control Tower的原生功能，架构简洁，集中管理
- **缺点：** AWS Control Tower的检测控制主要用于预防性控制，对于现有资源的检测能力有限

**选项B：** 使用AWS CloudFormation StackSets将AWS Lambda函数部署到每个账户。编写Lambda函数代码来确定函数部署到的账户中RDS存储是否加密。将发现结果作为Amazon CloudWatch指标发送到管理账户。创建Amazon SNS主题。创建CloudWatch告警，当达到指标阈值时通知SNS主题。将安全工程师的电子邮件地址订阅到SNS主题。

- **优点：** 可以实现跨账户监控
- **缺点：** 架构复杂，需要自定义开发，维护成本高，不是最佳实践

**选项C：** 在每个账户中创建自定义AWS Config规则来确定RDS存储是否加密。在审计账户中创建Amazon SNS主题。创建Amazon EventBridge规则来过滤来自AWS Control Tower控制（护栏）的不合规事件，以通知SNS主题。将安全工程师的电子邮件地址订阅到SNS主题。

- **优点：** AWS Config是专门用于合规性检查的服务，非常适合这种场景
- **缺点：** 描述中提到EventBridge过滤来自Control Tower的事件，但实际应该是Config的事件

**选项D：** 启动Amazon EC2实例。使用AWS CLI运行每小时的cron作业来确定每个AWS账户中RDS存储是否加密。将结果存储在RDS数据库中。当检测到不合规时，通过从EC2实例发送电子邮件消息来通知安全工程师。

- **优点：** 无
- **缺点：** 不是云原生解决方案，需要管理基础设施，安全性差，不符合最佳实践

 |  |  |  |
| 199 | A company is migrating from its on-premises data center to AWS. The company currently uses a custom on-premises Cl/CD pipeline solution
to build and package software.
The company wants its software packages and dependent public repositories to be available in AWS CodeArtifact to facilitate the creation of
application-specic pipelines. | A. Update the C1ICD pipeline to create a VM image that contains newly packaged software. Use AWS Import/Export to make the VM image
available as an Amazon EC2 AMI. Launch the AMI with an attached IAM instance prole that allows CodeArtifact actions. Use AWS CLI
commands to publish the packages to a CodeArtifact repository.
B. Create an AWS Identity and Access Management Roles Anywhere trust anchor. Create an IAM role that allows CodeArtifact actions and
that has a trust relationship on the trust anchor. Update the on-premises CI/CD pipeline to assume the new IAM role and to publish the
packages to CodeArtifact.
C. Create a new Amazon S3 bucket. Generate a presigned URL that allows the PutObject request. Update the on-premises CI/CD pipeline
to use the presigned URL to publish the packages from the on-premises location to the S3 bucket. Create an AWS Lambda function that
runs when packages are created in the bucket through a put command. Congure the Lambda function to publish the packages to
CodeArtifact.
D. For each public repository, create a CodeArutact repository that is congured with an external connection. Congure the dependent
repositories as upstream public repositories.
E. Create a Codeartitact repository that is congured with a set of external connections to the public repositories. Congure the external
connections to be downstream of the repository. | 一家公司正在从其本地数据中心迁移到AWS。该公司目前使用自定义的本地CI/CD管道解决方案来构建和打包软件。

该公司希望其软件包和依赖的公共仓库能够在AWS CodeArtifact中可用，以便于创建特定应用程序的管道。

 | **选项A：** 更新CI/CD管道创建包含新打包软件的VM镜像。使用AWS Import/Export使VM镜像作为Amazon EC2 AMI可用。启动带有允许CodeArtifact操作的IAM实例配置文件的AMI。使用AWS CLI命令将包发布到CodeArtifact仓库。
- **分析：** 这个方案过于复杂且不必要。创建VM镜像和AMI只是为了发布包到CodeArtifact是过度设计的解决方案，不符合最佳实践。

**选项B：** 创建AWS Identity and Access Management Roles Anywhere信任锚点。创建一个允许CodeArtifact操作并与信任锚点有信任关系的IAM角色。更新本地CI/CD管道以承担新的IAM角色并将包发布到CodeArtifact。
- **分析：** 这是一个很好的解决方案。IAM Roles Anywhere允许本地工作负载安全地承担AWS IAM角色，无需长期凭证。这是AWS推荐的本地到云集成方式。

**选项C：** 创建新的Amazon S3存储桶。生成允许PutObject请求的预签名URL。更新本地CI/CD管道使用预签名URL将包从本地位置发布到S3存储桶。创建AWS Lambda函数，当通过put命令在存储桶中创建包时运行。配置Lambda函数将包发布到CodeArtifact。
- **分析：** 这个方案可行但过于复杂，增加了不必要的中间步骤（S3和Lambda），增加了延迟和复杂性。

**选项D：** 为每个公共仓库创建配置了外部连接的CodeArtifact仓库。将依赖仓库配置为上游公共仓库。
- **分析：** 这个选项正确地描述了如何处理公共依赖项。CodeArtifact的外部连接功能允许连接到公共仓库（如npm、PyPI、Maven Central等），上游配置是正确的。

**选项E：** 创建配置了一组到公共仓库外部连接的CodeArtifact仓库。将外部连接配置为仓库的下游。
- **分析：** 配置错误。外部连接应该是上游的，而不是下游的。下游配置在这种情况下是不正确的。

 |  |  |  |
| 200 | A DevOps team uses AWS CodePipeline, AWS CodeBuild, and AWS CodeDeploy to deploy an application. The application is a REST API that
uses AWS Lambda functions and Amazon API Gateway. Recent deployments have introduced errors that have affected many customers.
The DevOps team needs a solution that reverts to the most recent stable version of the application when an error is detected. The solution
must affect the fewest customers possible. | A. Set the deployment conguration in CodeDeploy to LambdaAllAtOnce. Congure automatic rollbacks on the deployment group. Create
an Amazon CloudWatch alarm that detects HTTP Bad Gateway errors on API Gateway. Congure the deployment group to roll back when
the number of alarms meets the alarm threshold.
B. Set the deployment conguration in CodeDeploy to LambdaCanary10Percent10Minutes. Congure automatic rollbacks on the
deployment group. Create an Amazon CloudWatch alarm that detects HTTP Bad Gateway errors on API Gateway. Congure the
deployment group to roll back when the number of alarms meets the alarm threshold.
C. Set the deployment conguration in CodeDeploy to LambdaAllAtOnce. Congure manual rollbacks on the deployment group. Create an
Amazon Simple Notication Service (Amazon SNS) topic to send notications every time a deployment fails. Congure the SNS topic to
invoke a new Lambda function that stops the current deployment and starts the most recent successful deployment.
D. Set the deployment conguration in CodeDeploy to LambdaCanary10Percent10Minutes. Congure manual rollbacks on the deployment
group. Create a metric lter on an Amazon CloudWatch log group for API Gateway to monitor HTTP Bad Gateway errors. Congure the
metric lter to invoke a new Lambda function that stops the current deployment and starts the most recent successful deployment. |  |  |  |  |  |
| 201 | A company recently deployed its web application on AWS. The company is preparing for a large-scale sales event and must ensure that the
web application can scale to meet the demand.
The application's frontend infrastructure includes an Amazon CloudFront distribution that has an Amazon S3 bucket as an origin. The backend
infrastructure includes an Amazon API Gateway API, several AWS Lambda functions, and an Amazon Aurora DB cluster.
The company's DevOps engineer conducts a load test and identies that the Lambda functions can full the peak number of requests.
However, the DevOps engineer notices request latency during the initial burst of requests. Most of the requests to the Lambda functions
produce queries to the database. A large portion of the invocation time is used to establish database connections. | A. Congure a higher reserved concurrency for the Lambda functions.
B. Congure a higher provisioned concurrency for the Lambda functions.
C. Convert the DB cluster to an Aurora global database. Add additional Aurora Replicas in AWS Regions based on the locations of the
company's customers.
D. Refactor the Lambda functions. Move the code blocks that initialize database connections into the function handlers. | 一家公司最近在AWS上部署了其Web应用程序。该公司正在为大规模销售活动做准备，必须确保Web应用程序能够扩展以满足需求。

应用程序的前端基础设施包括一个以Amazon S3存储桶为源的Amazon CloudFront分发。后端基础设施包括一个Amazon API Gateway API、几个AWS Lambda函数和一个Amazon Aurora数据库集群。

公司的DevOps工程师进行了负载测试，发现Lambda函数可以满足峰值请求数量。但是，DevOps工程师注意到在初始请求突发期间存在请求延迟。大部分对Lambda函数的请求都会产生对数据库的查询。大部分调用时间都用于建立数据库连接。

 | **A. 为Lambda函数配置更高的预留并发性**
- 预留并发性(Reserved Concurrency)只是限制函数的最大并发执行数，并不能解决冷启动和数据库连接建立的延迟问题
- 这个选项不能解决数据库连接建立时间长的核心问题

**B. 为Lambda函数配置更高的预置并发性**
- 预置并发性(Provisioned Concurrency)会预先初始化Lambda函数实例，包括执行初始化代码
- 这可以显著减少冷启动时间，如果数据库连接在初始化阶段建立，可以有效解决延迟问题
- 直接针对"初始突发请求延迟"这个问题

**C. 将数据库集群转换为Aurora全球数据库，在基于客户位置的AWS区域中添加额外的Aurora副本**
- 这主要解决的是地理分布和读取性能问题
- 不能解决数据库连接建立时间的问题
- 过度复杂，且成本较高

**D. 重构Lambda函数，将初始化数据库连接的代码块移动到函数处理程序中**
- 这实际上会使问题变得更糟
- 将连接初始化移到处理程序中意味着每次函数调用都要建立新连接
- 这与Lambda最佳实践相反，应该将连接初始化放在处理程序外部以便重用

 |  |  |  |
| 202 | A company runs a web application that extends across multiple Availability Zones. The company uses an Application Load Balancer (ALB) for
routing, AWS Fargate for the application, and Amazon Aurora for the application data. The company uses AWS CloudFormation templates to
deploy the application. The company stores all Docker images in an Amazon Elastic Container Registry (Amazon ECR) repository in the same
AWS account and AWS Region.
A DevOps engineer needs to establish a disaster recovery (DR) process in another Region. The solution must meet an RPO of 8 hours and an
RTO of 2 hours. The company sometimes needs more than 2 hours to build the Docker images from the Dockerle. | A. Copy the CloudFormation templates and the Dockerle to an Amazon S3 bucket in the DR Region. Use AWS Backup to congure
automated Aurora cross-Region hourly snapshots. In case of DR, build the most recent Docker image and upload the Docker image to an
ECR repository in the DR Region. Use the CloudFormation template that has the most recent Aurora snapshot and the Docker image from
the ECR repository to launch a new CloudFormation stack in the DR Region. Update the application DNS records to point to the new AL
B. 
C. Copy the CloudFormation templates to an Amazon S3 bucket in the DR Region. Use Amazon EventBridge to schedule an AWS Lambda
function to take an hourly snapshot of the Aurora database and of the most recent Docker image in the ECR repository. Copy the snapshot
and the Docker image to the DR Region. In case of DR, use the CloudFormation template with the most recent Aurora snapshot and the
Docker image from the local ECR repository to launch a new CloudFormation stack in the DR Region.
D. Copy the CloudFormation templates to an Amazon S3 bucket in the DR Region. Deploy a second application CloudFormation stack in the
DR Region. Recongure Aurora to be a global database. Update both CloudFormation stacks when a new application release in the current
Region is needed. In case of DR, update the application DNS records to point to the new AL | 一家公司运行一个跨多个可用区的Web应用程序。该公司使用应用负载均衡器(ALB)进行路由，使用AWS Fargate运行应用程序，使用Amazon Aurora存储应用程序数据。公司使用AWS CloudFormation模板部署应用程序。公司将所有Docker镜像存储在同一AWS账户和区域的Amazon弹性容器注册表(Amazon ECR)存储库中。

DevOps工程师需要在另一个区域建立灾难恢复(DR)流程。解决方案必须满足8小时的RPO(恢复点目标)和2小时的RTO(恢复时间目标)。公司有时需要超过2小时来从Dockerfile构建Docker镜像。

 | **选项A：** 
将CloudFormation模板和Dockerfile复制到DR区域的S3存储桶。使用AWS Backup配置自动化Aurora跨区域每小时快照。在DR情况下，构建最新的Docker镜像并上传到DR区域的ECR存储库。使用包含最新Aurora快照和ECR存储库中Docker镜像的CloudFormation模板在DR区域启动新的CloudFormation堆栈。更新应用程序DNS记录指向新的ALB。

**问题：** 在DR时构建Docker镜像需要超过2小时，无法满足2小时RTO要求。

**选项B：** 
将CloudFormation模板复制到DR区域的S3存储桶。使用Amazon EventBridge调度AWS Lambda函数每小时对Aurora数据库和ECR存储库中最新Docker镜像进行快照。将快照和Docker镜像复制到DR区域。在DR情况下，使用包含最新Aurora快照和本地ECR存储库中Docker镜像的CloudFormation模板在DR区域启动新的CloudFormation堆栈。

**优势：** 预先复制Docker镜像到DR区域，避免了DR时的构建时间，能满足RTO要求。

**选项C：** 
将CloudFormation模板复制到DR区域的S3存储桶。在DR区域部署第二个应用程序CloudFormation堆栈。重新配置Aurora为全球数据库。当当前区域需要新应用程序发布时，更新两个CloudFormation堆栈。在DR情况下，更新应用程序DNS记录指向新的ALB。

**优势：** 使用Aurora全球数据库提供最佳的数据复制，预部署的基础设施能快速切换。

 |  |  |  |
| 203 | A company's application runs on Amazon EC2 instances. The application writes to a log le that records the username, date, time, and source
IP address of the login. The log is published to a log group in Amazon CloudWatch Logs.
The company is performing a root cause analysis for an event that occurred on the previous day. The company needs to know the number of
logins for a specic user from the past 7 days. | A. Create a CloudWatch Logs metric lter on the log group. Use a lter pattern that matches the username. Publish a CloudWatch metric
that sums the number of logins over the past 7 days.
B. Create a CloudWatch Logs subscription on the log group. Use a lter pattern that matches the username. Publish a CloudWatch metric
that sums the number of logins over the past 7 days.
C. Create a CloudWatch Logs Insights query that uses an aggregation function to count the number of logins for the username over the
past 7 days. Run the query against the log group.
D. Create a CloudWatch dashboard. Add a number widget that has a lter pattern that counts the number of logins for the username over
the past 7 days directly from the log group. | 一家公司的应用程序运行在Amazon EC2实例上。该应用程序写入一个日志文件，记录登录的用户名、日期、时间和源IP地址。该日志发布到Amazon CloudWatch Logs中的一个日志组。
公司正在对前一天发生的事件进行根本原因分析。公司需要知道过去7天内特定用户的登录次数。

2. | A. 在日志组上创建CloudWatch Logs指标过滤器。使用匹配用户名的过滤器模式。发布一个CloudWatch指标，汇总过去7天的登录次数。
- 指标过滤器可以从日志中提取指标数据
- 可以设置过滤器模式匹配特定用户名
- 可以创建指标来统计匹配的日志条目数量
- 这是一个可行的解决方案

B. 在日志组上创建CloudWatch Logs订阅。使用匹配用户名的过滤器模式。发布一个CloudWatch指标，汇总过去7天的登录次数。
- CloudWatch Logs订阅主要用于将日志数据流式传输到其他服务（如Kinesis、Lambda等）
- 订阅本身不直接创建指标
- 这不是解决当前问题的最直接方法

C. 创建一个CloudWatch Logs Insights查询，使用聚合函数统计过去7天内该用户名的登录次数。对日志组运行该查询。
- CloudWatch Logs Insights是专门用于日志分析和查询的服务
- 支持SQL类似的查询语法和聚合函数
- 可以直接查询特定时间范围内的数据
- 非常适合一次性分析和根本原因分析
- 这是最直接和高效的解决方案

D. 创建一个CloudWatch仪表板。添加一个数字小部件，该小部件具有过滤器模式，直接从日志组统计过去7天内该用户名的登录次数。
- CloudWatch仪表板主要用于可视化指标数据
- 仪表板小部件通常显示CloudWatch指标，而不是直接查询日志
- 不能直接从日志组进行复杂的过滤和计数操作

3. | C |  |  |
| 204 | A company has an AWS CodeDeploy application. The application has a deployment group that uses a single tag group to identify instances for
the deployment of Application. The single tag group conguration identies instances that have Environment=Production and
Name=ApplicationA tags for the deployment of Application | A. Change the current single tag group to include only the Environment=Production tag. Add another single tag group that includes only
the Name=ApplicationA tag.
B. Change the current single tag group to include the Department=Marketing, Environment=production, and Name=ApplicationA tags.
C. Add another single tag group that includes only the Department=Marketing tag. Keep the Environment=Production and
Name=ApplicationA tags with the current single tag group.
D. Change the current single tag group to include only the Environment=Production tag. Add another single tag group that includes only
the Department=Marketing tag. | 一家公司有一个AWS CodeDeploy应用程序。该应用程序有一个部署组，使用单个标签组来识别用于应用程序部署的实例。当前的单个标签组配置识别具有Environment=Production和Name=ApplicationA标签的实例来部署应用程序。

现在公司希望将应用程序部署到具有Environment=Production、Name=ApplicationA和Department=Marketing标签的实例上。

2. | **选项A：** 将当前的单个标签组更改为仅包含Environment=Production标签。添加另一个单个标签组，仅包含Name=ApplicationA标签。
- 这种配置会使用OR逻辑，意味着只要实例有Environment=Production标签OR Name=ApplicationA标签就会被选中
- 这会选择过多的实例，不符合要求（需要同时满足三个条件）

**选项B：** 将当前的单个标签组更改为包含Department=Marketing、Environment=Production和Name=ApplicationA标签。
- 在单个标签组内，所有标签都必须同时存在（AND逻辑）
- 这正好满足题目要求：实例必须同时具有这三个标签才会被选中进行部署
- 这是最直接和准确的解决方案

**选项C：** 添加另一个单个标签组，仅包含Department=Marketing标签。保持当前单个标签组的Environment=Production和Name=ApplicationA标签。
- 这会创建两个标签组，使用OR逻辑
- 意味着实例只需要有Department=Marketing标签OR同时有Environment=Production和Name=ApplicationA标签
- 这会选择不符合要求的实例

**选项D：** 将当前的单个标签组更改为仅包含Environment=Production标签。添加另一个单个标签组，仅包含Department=Marketing标签。
- 这种配置使用OR逻辑
- 会选择所有有Environment=Production标签或Department=Marketing标签的实例
- 不能确保实例同时具有所有三个必需的标签

3. | B |  |  |
| 205 | A company is launching an application that stores raw data in an Amazon S3 bucket. Three applications need to access the data to generate
reports. The data must be redacted differently for each application before the applications can access the data. | A. Create an S3 bucket for each application. Congure S3 Same-Region Replication (SRR) from the raw data's S3 bucket to each
application's S3 bucket. Congure each application to consume data from its own S3 bucket.
B. Create an Amazon Kinesis data stream. Create an AWS Lambda function that is invoked by object creation events in the raw data’s S3
bucket. Program the Lambda function to redact data for each application. Publish the data on the Kinesis data stream. Congure each
application to consume data from the Kinesis data stream.
C. For each application, create an S3 access point that uses the raw data's S3 bucket as the destination. Create an AWS Lambda function
that is invoked by object creation events in the raw data's S3 bucket. Program the Lambda function to redact data for each application.
Store the data in each application's S3 access point. Congure each application to consume data from its own S3 access point.
D. Create an S3 access point that uses the raw data’s S3 bucket as the destination. For each application, create an S3 Object Lambda
access point that uses the S3 access point. Congure the AWS Lambda function for each S3 Object Lambda access point to redact data
when objects are retrieved. Congure each application to consume data from its own S3 Object Lambda access point | 一家公司正在启动一个应用程序，该应用程序将原始数据存储在Amazon S3存储桶中。三个应用程序需要访问这些数据来生成报告。在应用程序能够访问数据之前，必须为每个应用程序以不同的方式对数据进行脱敏处理。

 | **选项A：** 为每个应用程序创建一个S3存储桶。配置从原始数据S3存储桶到每个应用程序S3存储桶的S3同区域复制(SRR)。配置每个应用程序从其自己的S3存储桶消费数据。
- **问题：** S3 SRR只是简单的数据复制，无法在复制过程中进行数据脱敏处理
- **缺陷：** 不能满足"数据必须为每个应用程序进行不同脱敏"的要求

**选项B：** 创建一个Amazon Kinesis数据流。创建一个由原始数据S3存储桶中对象创建事件触发的AWS Lambda函数。编程Lambda函数为每个应用程序脱敏数据。将数据发布到Kinesis数据流上。配置每个应用程序从Kinesis数据流消费数据。
- **问题：** 所有应用程序都从同一个Kinesis流消费数据，无法为不同应用程序提供不同的脱敏数据
- **缺陷：** 不能满足每个应用程序需要不同脱敏数据的要求

**选项C：** 为每个应用程序创建一个以原始数据S3存储桶为目标的S3访问点。创建一个由原始数据S3存储桶中对象创建事件触发的AWS Lambda函数。编程Lambda函数为每个应用程序脱敏数据。将数据存储在每个应用程序的S3访问点中。配置每个应用程序从其自己的S3访问点消费数据。
- **问题：** S3访问点不能存储数据，它只是访问现有S3存储桶的网络端点
- **技术错误：** 误解了S3访问点的功能

**选项D：** 创建一个以原始数据S3存储桶为目标的S3访问点。为每个应用程序创建一个使用该S3访问点的S3 Object Lambda访问点。为每个S3 Object Lambda访问点配置AWS Lambda函数，在检索对象时对数据进行脱敏。配置每个应用程序从其自己的S3 Object Lambda访问点消费数据。
- **优势：** 正确使用了S3 Object Lambda功能，可以在数据检索时实时进行脱敏处理
- **符合要求：** 每个应用程序有独立的Object Lambda访问点，可以应用不同的脱敏逻辑

 |  |  |  |
| 206 | A company uses AWS Control Tower and AWS CloudFormation to manage its AWS accounts and to create AWS resources. The company
requires all Amazon S3 buckets to be encrypted with AWS Key Management Service (AWS KMS) when the S3 buckets are created in a
CloudFormation stack. | A. Use AWS Organizations. Attach an SCP that denies the s3:PutObject permission if the request does not include an x-amz-server-side-
encryption header that requests server-side encryption with AWS KMS keys (SSE-KMS).
B. Use AWS Control Tower with a multi-account environment. Congure and enable proactive AWS Control Tower controls on all OUs with
CloudFormation hooks.
C. Use AWS Control Tower with a multi-account environment. Congure and enable detective AWS Control Tower controls on all OUs with
CloudFormation hooks.
D. Use AWS Organizations. Create an AWS Cong organizational rule to check whether a KMS encryption key is enabled for all S3 buckets.
Deploy the rule. Create and apply an SCP to prevent users from stopping and deleting AWS Cong across all AWS accounts, | 一家公司使用AWS Control Tower和AWS CloudFormation来管理其AWS账户并创建AWS资源。该公司要求在CloudFormation堆栈中创建Amazon S3存储桶时，所有S3存储桶都必须使用AWS密钥管理服务(AWS KMS)进行加密。

 | **选项A：** 使用AWS Organizations。附加一个SCP策略，如果请求不包含要求使用AWS KMS密钥进行服务器端加密(SSE-KMS)的x-amz-server-side-encryption标头，则拒绝s3:PutObject权限。
- 这个方案只能控制对象上传时的加密，但无法确保S3存储桶本身在创建时就配置了默认加密
- SCP控制的是对象级别的操作，而题目要求的是存储桶级别的加密配置
- 不能完全满足题目要求

**选项B：** 使用AWS Control Tower的多账户环境。在所有OU上配置并启用主动式AWS Control Tower控制，配合CloudFormation钩子。
- 主动式(Proactive)控制可以在资源创建之前进行检查和阻止
- 可以通过CloudFormation钩子在堆栈部署时强制执行加密要求
- 能够在S3存储桶创建时就确保KMS加密配置
- 完全符合题目要求的预防性控制需求

**选项C：** 使用AWS Control Tower的多账户环境。在所有OU上配置并启用检测式AWS Control Tower控制，配合CloudFormation钩子。
- 检测式(Detective)控制是在资源创建后进行检查
- 无法阻止不合规的S3存储桶创建，只能在创建后发现问题
- 不符合题目要求的预防性控制需求

**选项D：** 使用AWS Organizations。创建AWS Config组织规则来检查所有S3存储桶是否启用了KMS加密密钥。部署规则。创建并应用SCP以防止用户在所有AWS账户中停止和删除AWS Config。
- AWS Config规则是检测式控制，在资源创建后才能发现不合规
- 无法在CloudFormation部署时阻止创建不加密的S3存储桶
- 不能满足预防性控制的要求

 |  |  |  |
| 207 | A DevOps engineer has developed an AWS Lambda function. The Lambda function starts an AWS CloudFormation drift detection operation on
all supported resources for a specic CloudFormation stack. The Lambda function then exits its invocation.
The DevOps engineer has created an Amazon EventBridge scheduled rule that invokes the Lambda function every hour. An Amazon Simple
Notication Service (Amazon SNS) topic already exists in the AWS account. The DevOps engineer has subscribed to the SNS topic to receive
notications.
The DevOps engineer needs to receive a notication as soon as possible when drift is detected in this specic stack conguration. | A. Congure the existing EventBridge rule to also target the SNS topic. Congure an SNS subscription lter policy to match the
CloudFormation stack. Attach the subscription lter policy to the SNS topic.
B. Create a second Lambda function to query the CloudFormation API for the drift detection results for the stack. Congure the second
Lambda function to publish a message to the SNS topic if drift is detected. Adjust the existing EventBridge rule to also target the second
Lambda function.
C. Congure Amazon GuardDuty in the account with drift detection for all CloudFormation stacks. Create a second EventBridge rule that
reacts to the GuardDuty drift detection event nding for the specic CloudFormation stack. Congure the SNS topic as a target of the
second EventBridge rule.
D. Congure AWS Cong in the account. Use the cloudformation-stack-drift-detection-check managed rule. Create a second EventBridge
rule that reacts to a compliance change event for the CloudFormation stack. Congure the SNS topic as a target of the second
EventBridge rule. | 一名DevOps工程师开发了一个AWS Lambda函数。该Lambda函数对特定CloudFormation堆栈的所有支持资源启动AWS CloudFormation漂移检测操作。Lambda函数然后退出其调用。

DevOps工程师创建了一个Amazon EventBridge定时规则，每小时调用一次Lambda函数。AWS账户中已经存在一个Amazon Simple Notification Service (Amazon SNS)主题。DevOps工程师已订阅该SNS主题以接收通知。

DevOps工程师需要在检测到此特定堆栈配置中的漂移时尽快收到通知。

 | **选项A：** 配置现有的EventBridge规则也以SNS主题为目标。配置SNS订阅过滤策略以匹配CloudFormation堆栈。将订阅过滤策略附加到SNS主题。
- **错误**：这种方法不会检测实际的漂移，只是在定时规则触发时发送通知，无法提供漂移检测结果。

**选项B：** 创建第二个Lambda函数来查询CloudFormation API以获取堆栈的漂移检测结果。配置第二个Lambda函数在检测到漂移时向SNS主题发布消息。调整现有的EventBridge规则也以第二个Lambda函数为目标。
- **部分正确但不是最佳方案**：虽然技术上可行，但需要额外的Lambda函数来轮询结果，不是最优的事件驱动架构。

**选项C：** 在账户中配置Amazon GuardDuty，为所有CloudFormation堆栈启用漂移检测。创建第二个EventBridge规则，响应特定CloudFormation堆栈的GuardDuty漂移检测事件发现。将SNS主题配置为第二个EventBridge规则的目标。
- **错误**：GuardDuty主要用于安全威胁检测，不提供CloudFormation堆栈漂移检测功能。

**选项D：** 在账户中配置AWS Config。使用cloudformation-stack-drift-detection-check托管规则。创建第二个EventBridge规则，响应CloudFormation堆栈的合规性变更事件。将SNS主题配置为第二个EventBridge规则的目标。
- **正确**：AWS Config的cloudformation-stack-drift-detection-check规则专门用于检测CloudFormation堆栈漂移，当检测到漂移时会生成合规性变更事件，可以通过EventBridge规则捕获并触发SNS通知。

 |  |  |  |
| 208 | A company has deployed a complex container-based workload on AWS. The workload uses Amazon Managed Service for Prometheus for
monitoring. The workload runs in an Amazon
Elastic Kubernetes Service (Amazon EKS) cluster in an AWS account.
The company’s DevOps team wants to receive workload alerts by using the company’s Amazon Simple Notication Service (Amazon SNS)
topic. The SNS topic is in the same AWS account as the EKS cluster. | A. Use the Amazon Managed Service for Prometheus remote write URL to send alerts to the SNS topic
B. Create an alerting rule that checks the availability of each of the workload’s containers.
C. Create an alert manager conguration for the SNS topic.
D. Modify the access policy of the SNS topic. Grant the aps.amazonaws.com service principal the sns:Publish permission and the
sns:GetTopicAttributes permission for the SNS topic.
E. Modify the IAM role that Amazon Managed Service for Prometheus uses. Grant the role the sns:Publish permission and the
sns:GetTopicAttributes permission for the SNS topic. |  |  |  |  |  |
| 209 | A company's organization in AWS Organizations has a single OU. The company runs Amazon EC2 instances in the OU accounts. The company
needs to limit the use of each EC2 instance’s credentials to the specic EC2 instance that the credential is assigned to. A DevOps engineer
must congure security for the EC2 instances. | A. Create an SCP that species the VPC CIDR block. Congure the SCP to check whether the value of the aws:VpcSourcelp condition key is
in the specied block. In the same SCP check, check whether the values of the aws:EC2InstanceSourcePrivatelPv4 and aws:SourceVpc
condition keys are the same. Deny access if either condition is false. Apply the SCP to the OU.
B. Create an SCP that checks whether the values of the aws:EC2InstanceSourceVPC and aws:SourceVpc condition keys are the same.
Deny access if the values are not the same. In the same SCP check, check whether the values of the aws:EC2InstanceSourcePrivateIPv4
and aws:VpcSourceIp condition keys are the same. Deny access if the values are not the same. Apply the SCP to the OU.
C. Create an SCP that includes a list of acceptable VPC values and checks whether the value of the aws:SourceVpc condition key is in the
list. In the same SCP check, dene a list of acceptable IP address values and check whether the value of the aws:VpcSourceIp condition
key is in the list. Deny access if either condition is false. Apply the SCP to each account in the organization.
D. Create an SCP that checks whether the values of the aws:EC2InstanceSourceVPC and aws:VpcSourceIp condition keys are the same.
Deny access if the values are not the same. In the same SCP check, check whether the values of the aws:EC2InstanceSourcePrivateIPv4
and aws:SourceVpc condition keys are the same. Deny access if the values are not the same. Apply the SCP to each account in the
organization. | 一家公司在AWS Organizations中的组织有一个单独的OU（组织单元）。该公司在OU账户中运行Amazon EC2实例。公司需要限制每个EC2实例的凭证使用，确保凭证只能被分配给它的特定EC2实例使用。DevOps工程师必须为EC2实例配置安全性。

 | **选项A：**
- 创建SCP指定VPC CIDR块，检查aws:VpcSourceIp条件键值是否在指定块内
- 同时检查aws:EC2InstanceSourcePrivateIPv4和aws:SourceVpc条件键值是否相同
- 问题：aws:EC2InstanceSourcePrivateIPv4与aws:SourceVpc比较没有意义（一个是IP地址，一个是VPC ID）

**选项B：**
- 检查aws:EC2InstanceSourceVPC和aws:SourceVpc条件键值是否相同
- 检查aws:EC2InstanceSourcePrivateIPv4和aws:VpcSourceIp条件键值是否相同
- 这个逻辑是正确的：确保请求来自正确的VPC和正确的EC2实例IP
- 应用到OU级别

**选项C：**
- 创建可接受的VPC值列表，检查aws:SourceVpc是否在列表中
- 创建可接受的IP地址值列表，检查aws:VpcSourceIp是否在列表中
- 问题：需要维护静态列表，不够灵活，且应用到每个账户而非OU

**选项D：**
- 检查aws:EC2InstanceSourceVPC和aws:VpcSourceIp条件键值是否相同
- 检查aws:EC2InstanceSourcePrivateIPv4和aws:SourceVpc条件键值是否相同
- 问题：比较的条件键类型不匹配（VPC ID与IP地址比较，IP地址与VPC ID比较）

 |  |  |  |
| 210 | A company has a eet of Amazon EC2 instances that run Linux in a single AWS account. The company is using an AWS Systems Manager
Automation task across the EC2 instances.
During the most recent patch cycle, several EC2 instances went into an error state because of insucient available disk space. A DevOps
engineer needs to ensure that the EC2 instances have sucient available disk space during the patching process in the future. | A. Ensure that the Amazon CloudWatch agent is installed on all EC2 instances.
B. Create a cron job that is installed on each EC2 instance to periodically delete temporary les.
C. Create an Amazon CloudWatch log group for the EC2 instances. Congure a cron job that is installed on each EC2 instance to write the
available disk space to a CloudWatch log stream for the relevant EC2 instance.
D. Create an Amazon CloudWatch alarm to monitor available disk space on all EC2 instances. Add the alarm as a safety control to the
Systems Manager Automation task.
E. Create an AWS Lambda function to periodically check for sucient available disk space on all EC2 instances by evaluating each EC2
instance's respective Amazon CloudWatch log stream. | 一家公司在单个AWS账户中拥有一组运行Linux的Amazon EC2实例。该公司正在跨EC2实例使用AWS Systems Manager自动化任务。

在最近的补丁周期中，由于可用磁盘空间不足，几个EC2实例进入了错误状态。DevOps工程师需要确保EC2实例在未来的补丁过程中有足够的可用磁盘空间。

 | **A. 确保在所有EC2实例上安装Amazon CloudWatch代理。**
- 这是一个必要的基础步骤，CloudWatch代理可以收集磁盘空间等系统指标
- 但仅安装代理并不能解决问题，还需要配置监控和告警机制
- 这个选项不够完整

**B. 创建一个cron作业，安装在每个EC2实例上以定期删除临时文件。**
- 这是一个预防性措施，可以帮助维护磁盘空间
- 但这种方法是被动的，无法在补丁过程中实时检测磁盘空间不足的情况
- 不能作为Systems Manager自动化任务的安全控制

**C. 为EC2实例创建Amazon CloudWatch日志组。配置安装在每个EC2实例上的cron作业，将可用磁盘空间写入相关EC2实例的CloudWatch日志流。**
- 这种方法过于复杂，需要自定义脚本和日志解析
- 不是实时监控，依赖cron作业的执行频率
- 无法直接与Systems Manager自动化任务集成

**D. 创建Amazon CloudWatch告警来监控所有EC2实例的可用磁盘空间。将告警作为安全控制添加到Systems Manager自动化任务中。**
- 这是最佳解决方案，提供实时监控和主动告警
- CloudWatch告警可以直接集成到Systems Manager自动化任务中作为安全控制
- 当磁盘空间不足时，可以暂停或停止自动化任务，防止实例进入错误状态
- 符合AWS最佳实践

**E. 创建AWS Lambda函数，通过评估每个EC2实例各自的Amazon CloudWatch日志流来定期检查所有EC2实例上的足够可用磁盘空间。**
- 过度工程化的解决方案，增加了不必要的复杂性
- 依赖于选项C中提到的日志流方法，效率低下
- 无法与Systems Manager自动化任务直接集成

 |  |  |  |
| 211 | A DevOps engineer is building an application that uses an AWS Lambda function to query an Amazon Aurora MySQL DB cluster. The Lambda
function performs only read queries. Amazon EventBridge events invoke the Lambda function.
As more events invoke the Lambda function each second, the database's latency increases and the database's throughput decreases. The
DevOps engineer needs to improve the performance of the application. | A. Use Amazon RDS Proxy to create a proxy. Connect the proxy to the Aurora cluster reader endpoint. Set a maximum connections
percentage on the proxy.
B. Implement database connection pooling inside the Lambda code. Set a maximum number of connections on the database connection
pool.
C. Implement the database connection opening outside the Lambda event handler code.
D. Implement the database connection opening and closing inside the Lambda event handler code.
E. Connect to the proxy endpoint from the Lambda function. | 一名DevOps工程师正在构建一个应用程序，该应用程序使用AWS Lambda函数来查询Amazon Aurora MySQL数据库集群。Lambda函数只执行读取查询。Amazon EventBridge事件调用Lambda函数。

随着每秒调用Lambda函数的事件增多，数据库的延迟增加，数据库的吞吐量下降。DevOps工程师需要改善应用程序的性能。

 | **A. 使用Amazon RDS Proxy创建代理。将代理连接到Aurora集群读取器端点。在代理上设置最大连接百分比。**
- ✅ 正确。RDS Proxy专门设计用于解决Lambda函数的数据库连接问题
- RDS Proxy可以管理连接池，减少数据库连接开销
- 可以设置最大连接数限制，防止数据库过载
- 支持连接复用，提高性能

**B. 在Lambda代码内部实现数据库连接池。在数据库连接池上设置最大连接数。**
- ❌ 不理想。Lambda的无服务器特性使得传统连接池效果有限
- Lambda实例的生命周期不可预测，连接池管理复杂
- 无法有效控制全局连接数

**C. 在Lambda事件处理程序代码外部实现数据库连接开启。**
- ⚠️ 部分正确但不完整。虽然在handler外部建立连接是好实践
- 但这只是优化的一部分，无法解决高并发时的连接数问题
- 不能根本解决数据库性能瓶颈

**D. 在Lambda事件处理程序代码内部实现数据库连接的开启和关闭。**
- ❌ 错误。这是最差的做法
- 每次调用都建立新连接会大大增加延迟
- 会加剧数据库连接数问题

**E. 从Lambda函数连接到代理端点。**
- ⚠️ 不完整。虽然连接代理是正确的，但缺少创建和配置代理的步骤
- 单独这个选项无法解决问题

 |  |  |  |
| 212 | A company has an AWS CloudFormation stack that is deployed in a single AWS account. The company has congured the stack to send event
notications to an Amazon Simple Notication Service (Amazon SNS) topic.
A DevOps engineer must implement an automated solution that applies a tag to the specic CloudFormation stack instance only after a
successful stack update occurs. The DevOps engineer has created an AWS Lambda function that applies and updates this tag for the specic
stack instance. | A. Run the AWS-UpdateCloudFormationStack AWS Systems ManagerAutomation runbook when Systems Manager detects an
UPDATE_COMPLETE event for the instance status of the CloudFormation stack. Congure the runbook to invoke the Lambda function.
B. Create a custom AWS Cong rule that produces a compliance change event if the CloudFormation stack has an UPDATE_COMPLETE
instance status. Congure AWS Cong to directly invoke the Lambda function to automatically remediate the change event.
C. Create an Amazon EventBridge rule that matches the UPDATE_COMPLETE event pattern for the instance status of the CloudFormation
stack. Congure the rule to invoke the Lambda function.
D. Adjust the conguration of the CloudFormation stack to send notications for only an UPDATE_COMPLETE instance status event to the
SNS topic. Subscribe the Lambda function to the SNS topic. | 一家公司有一个部署在单个AWS账户中的AWS CloudFormation堆栈。该公司已配置堆栈将事件通知发送到Amazon Simple Notification Service (Amazon SNS)主题。

DevOps工程师必须实现一个自动化解决方案，该解决方案仅在成功的堆栈更新发生后，为特定的CloudFormation堆栈实例应用标签。DevOps工程师已经创建了一个AWS Lambda函数，用于为特定堆栈实例应用和更新此标签。

 | **选项A：** 当Systems Manager检测到CloudFormation堆栈实例状态的UPDATE_COMPLETE事件时，运行AWS-UpdateCloudFormationStack AWS Systems Manager自动化运行手册。配置运行手册调用Lambda函数。
- 分析：Systems Manager Automation主要用于运维自动化，但它不是专门为监听CloudFormation事件而设计的。这种方法过于复杂，且不是最直接的事件响应机制。

**选项B：** 创建一个自定义AWS Config规则，如果CloudFormation堆栈具有UPDATE_COMPLETE实例状态，则产生合规性变更事件。配置AWS Config直接调用Lambda函数以自动修复变更事件。
- 分析：AWS Config主要用于资源配置合规性监控，不是为实时事件响应而设计的。Config规则评估可能有延迟，且这不是Config的典型用例。

**选项C：** 创建一个Amazon EventBridge规则，匹配CloudFormation堆栈实例状态的UPDATE_COMPLETE事件模式。配置规则调用Lambda函数。
- 分析：EventBridge是AWS的事件驱动架构服务，专门设计用于捕获和路由事件。CloudFormation会自动向EventBridge发送状态变更事件，包括UPDATE_COMPLETE事件。这是最直接和高效的解决方案。

**选项D：** 调整CloudFormation堆栈的配置，仅为UPDATE_COMPLETE实例状态事件向SNS主题发送通知。将Lambda函数订阅到SNS主题。
- 分析：虽然这个方案可行，但需要修改现有的CloudFormation堆栈配置，可能影响其他依赖SNS通知的系统。相比之下，EventBridge提供了更灵活和解耦的解决方案。

 |  |  |  |
| 213 | A company deploys an application to two AWS Regions. The application creates and stores objects in an Amazon S3 bucket that is in the same
Region as the application. Both deployments of the application need to have access to all the objects and their metadata from both Regions.
The company has congured two-way replication between the S3 buckets and has enabled S3 Replication metrics on each S3 bucket.
A DevOps engineer needs to implement a solution that retries the replication process if an object fails to replicate. | A. Create an Amazon EventBridge rule that listens to S3 event notications for failed replication events. Create an AWS Lambda function
that downloads the failed replication object and then runs a PutObject command for the object to the destination bucket. Congure the
EventBridge rule to invoke the Lambda function to handle the object that failed to replicate.
B. Create an Amazon Simple Queue Service (Amazon SQS) queue. Congure S3 event notications to send failed replication notications
to the SQS queue. Create an AWS Lambda function that downloads the failed replication object and then runs a PutObject command for
the object to the destination bucket. Congure the Lambda function to poll the queue for notications to process.
C. Create an Amazon EventBridge rule that listens to S3 event notications for failed replications. Create an AWS Lambda function that
downloads the failed replication object and then runs a PutObject command for the object to the destination bucket.
D. Create an AWS Lambda function that will use S3 batch operations to retry the replication on the existing object for a failed replication.
Congure S3 event notications to send failed replication notications to the Lambda function. | 一家公司将应用程序部署到两个AWS区域。应用程序在与应用程序相同区域的Amazon S3存储桶中创建和存储对象。两个应用程序部署都需要访问来自两个区域的所有对象及其元数据。公司已在S3存储桶之间配置了双向复制，并在每个S3存储桶上启用了S3复制指标。

DevOps工程师需要实现一个解决方案，当对象复制失败时重试复制过程。

 | **选项A：** 创建Amazon EventBridge规则监听S3复制失败事件通知。创建AWS Lambda函数下载失败的复制对象，然后对目标存储桶运行PutObject命令。配置EventBridge规则调用Lambda函数处理复制失败的对象。
- **分析：** 这个方案技术上可行，EventBridge可以处理S3事件，Lambda可以执行重试逻辑。但是手动下载和重新上传对象的方式不是最优的，因为这样会丢失原始的复制元数据和版本信息。

**选项B：** 创建Amazon SQS队列。配置S3事件通知将复制失败通知发送到SQS队列。创建AWS Lambda函数下载失败的复制对象，然后对目标存储桶运行PutObject命令。配置Lambda函数轮询队列处理通知。
- **分析：** 使用SQS作为缓冲是一个好的架构模式，可以确保消息不丢失。但同样存在手动下载重新上传的问题，且增加了架构复杂性。

**选项C：** 创建Amazon EventBridge规则监听S3复制失败事件通知。创建AWS Lambda函数下载失败的复制对象，然后对目标存储桶运行PutObject命令。
- **分析：** 与选项A类似，但描述不够完整，没有明确说明如何触发Lambda函数。

**选项D：** 创建AWS Lambda函数使用S3批处理操作对失败的复制重试现有对象的复制。配置S3事件通知将复制失败通知发送到Lambda函数。
- **分析：** 这个方案使用S3批处理操作来重试复制，这是处理S3复制失败的最佳实践。S3批处理操作可以直接重试复制过程，保持原始的元数据和复制配置。

 |  |  |  |
| 214 | A company needs to implement failover for its application. The application includes an Amazon CloudFront distribution and a public
Application Load Balancer (ALB) in an AWS Region. The company has congured the ALB as the default origin for the distribution.
After some recent application outages, the company wants a zero-second RTO. The company deploys the application to a secondary Region in
a warm standby conguration. A DevOps engineer needs to automate the failover of the application to the secondary Region so that HTTP
GET requests meet the desired RTO. | A. Create a second CloudFront distribution that has the secondary ALB as the default origin. Create Amazon Route 53 alias records that
have a failover policy and Evaluate Target Health set to Yes for both CloudFront distributions. Update the application to use the new
record set.
B. Create a new origin on the distribution for the secondary ALCreate a new origin group. Set the original ALB as the primary origin.
Congure the origin group to fail over for HTTP 5xx status codes. Update the default behavior to use the origin group.
C. Create Amazon Route 53 alias records that have a failover policy and Evaluate Target Health set to Yes for both ALBs. Set the TTL of
both records to 0. Update the distribution's origin to use the new record set.
D. Create a CloudFront function that detects HTTP 5xx status codes. Congure the function to return a 307 Temporary Redirect error
response to the secondary ALB if the function detects 5xx status codes. Update the distribution's default behavior to send origin
responses to the function. |  |  |  |  |  |
| 215 | A cloud team uses AWS Organizations and AWS IAM Identity Center (AWS Single Sign-On) to manage a company's AWS accounts. The company
recently established a research team. The research team requires the ability to fully manage the resources in its account. The research team
must not be able to create IAM users.
The cloud team creates a Research Administrator permission set in IAM Identity Center for the research team. The permission set has the
AdministratorAccess AWS managed policy attached. The cloud team must ensure that no one on the research team can create IAM users. | A. Create an IAM policy that denies the iam:CreateUser action. Attach the IAM policy to the Research Administrator permission set.
B. Create an IAM policy that allows all actions except the iam:CreateUser action. Use the IAM policy to set the permissions boundary for
the Research Administrator permission set.
C. Create an SCP that denies the iam:CreateUser action. Attach the SCP to the research team's AWS account.
D. Create an AWS Lambda function that deletes IAM users. Create an Amazon EventBridge rule that detects the IAM CreateUser event.
Congure the rule to invoke the Lambda function. | 一个云团队使用AWS Organizations和AWS IAM Identity Center（AWS Single Sign-On）来管理公司的AWS账户。公司最近成立了一个研究团队。研究团队需要能够完全管理其账户中的资源。研究团队不得创建IAM用户。

云团队在IAM Identity Center中为研究团队创建了一个Research Administrator权限集。该权限集附加了AdministratorAccess AWS托管策略。云团队必须确保研究团队中的任何人都不能创建IAM用户。

 | **选项A：创建一个拒绝iam:CreateUser操作的IAM策略。将IAM策略附加到Research Administrator权限集。**
- 这个方法在技术上可行，但存在问题
- 当同时有允许（AdministratorAccess）和拒绝策略时，拒绝策略会优先生效
- 但这种方法只在权限集级别生效，如果用户通过其他方式获得权限可能被绕过

**选项B：创建一个允许除iam:CreateUser操作外所有操作的IAM策略。使用该IAM策略为Research Administrator权限集设置权限边界。**
- 权限边界（Permissions Boundary）是一个高级功能，用于设置用户或角色的最大权限
- 但在IAM Identity Center的权限集中，权限边界的应用方式与传统IAM用户不同
- 这个方法复杂且不是最佳实践

**选项C：创建一个拒绝iam:CreateUser操作的SCP。将SCP附加到研究团队的AWS账户。**
- SCP（Service Control Policy）是AWS Organizations的功能
- SCP在账户级别生效，无论用户通过什么方式获得权限都会受到限制
- SCP的拒绝策略具有最高优先级，无法被绕过
- 这是组织级别的控制，符合最佳实践

**选项D：创建一个删除IAM用户的AWS Lambda函数。创建一个Amazon EventBridge规则来检测IAM CreateUser事件。配置规则调用Lambda函数。**
- 这是一个响应式的解决方案，而不是预防性的
- 虽然能删除已创建的用户，但无法阻止创建行为本身
- 增加了系统复杂性，不是最佳实践
- 可能存在时间延迟和安全风险

 |  |  |  |
| 216 | A company releases a new application in a new AWS account. The application includes an AWS Lambda function that processes messages
from an Amazon Simple Queue Service (Amazon SQS) standard queue. The Lambda function stores the results in an Amazon S3 bucket for
further downstream processing. The Lambda function needs to process the messages within a specic period of time after the messages are
published. The Lambda function has a batch size of 10 messages and takes a few seconds to process a batch of messages.
As load increases on the application's rst day of service, messages in the queue accumulate at a greater rate than the Lambda function can
process the messages. Some messages miss the required processing timelines. The logs show that many messages in the queue have data
that is not valid. The company needs to meet the timeline requirements for messages that have valid data. | A. Increase the Lambda function's batch size. Change the SQS standard queue to an SQS FIFO queue. Request a Lambda concurrency
increase in the AWS Region.
B. Reduce the Lambda function's batch size. Increase the SQS message throughput quota. Request a Lambda concurrency increase in the
AWS Region.
C. Increase the Lambda function's batch size. Congure S3 Transfer Acceleration on the S3 bucket. Congure an SQS dead-letter queue.
D. Keep the Lambda function's batch size the same. Congure the Lambda function to report failed batch items. Congure an SQS dead-
letter queue. |  |  |  |  |  |
| 217 | A company has an application that runs on AWS Lambda and sends logs to Amazon CloudWatch Logs. An Amazon Kinesis data stream is
subscribed to the log groups in CloudWatch Logs. A single consumer Lambda function processes the logs from the data stream and stores the
logs in an Amazon S3 bucket.
The company’s DevOps team has noticed high latency during the processing and ingestion of some logs. | A. Create a data stream consumer with enhanced fan-out. Set the Lambda function that processes the logs as the consumer.
B. Increase the ParallelizationFactor setting in the Lambda event source mapping.
C. Congure reserved concurrency for the Lambda function that processes the logs.
D. Increase the batch size in the Kinesis data stream.
E. Turn off the ReportBatchItemFailures setting in the Lambda event source mapping.
F. Increase the number of shards in the Kinesis data stream. |  |  |  |  |  |
| 218 | A company operates sensitive workloads across the AWS accounts that are in the company's organization in AWS Organizations. The company
uses an IP address range to delegate IP addresses for Amazon VPC CIDR blocks and all non-cloud hardware.
The company needs a solution that prevents principals that are outside the company’s IP address range from performing AWS actions in the
organization's accounts. | A. Congure AWS Firewall Manager for the organization. Create an AWS Network Firewall policy that allows only source trac from the
company's IP address range. Set the policy scope to all accounts in the organization.
B. In Organizations, create an SCP that denies source IP addresses that are outside of the company’s IP address range. Attach the SCP to
the organization's root.
C. Congure Amazon GuardDuty for the organization. Create a GuardDuty trusted IP address list for the company's IP range. Activate the
trusted IP list for the organization.
D. In Organizations, create an SCP that allows source IP addresses that are inside of the company’s IP address range. Attach the SCP to
the organization's root. |  |  |  |  |  |
| 219 | A company deploys an application in two AWS Regions. The application currently uses an Amazon S3 bucket in the primary Region to store
data.
A DevOps engineer needs to ensure that the application is highly available in both Regions. The DevOps engineer has created a new S3
bucket in the secondary Region. All existing and new objects must be in both S3 buckets. The application must fail over between the Regions
with no data loss. | A. Create a new IAM role that allows the Amazon S3 and S3 Batch Operations service principals to assume the role that has the necessary
permissions for S3 replication.
B. Create a new IAM role that allows the AWS Batch service principal to assume the role that has the necessary permissions for S3
replication.
C. Create an S3 Cross-Region Replication (CRR) rule on the source S3 bucket. Congure the rule to use the IAM role for Amazon S3 to
replicate to the target S3 bucket.
D. Create a two-way replication rule on the source S3 bucket. Congure the rule to use the IAM role for Amazon S3 to replicate to the
target S3 bucket.
E. Create an AWS Batch job that has an AWS Fargate orchestration type. Congure the job to use the IAM role for AWS Batch. Specify a
Bash command to use the AWS CLI to synchronize the contents of the source S3 bucket and the target S3 bucket
F. Create an operation in S3 Batch Operations to replicate the contents of the source S3 bucket to the target S3 bucket. Congure the
operation to use the IAM role for Amazon S3. | 一家公司在两个AWS区域部署应用程序。该应用程序目前使用主区域中的Amazon S3存储桶来存储数据。

DevOps工程师需要确保应用程序在两个区域都具有高可用性。DevOps工程师已在辅助区域创建了一个新的S3存储桶。所有现有和新的对象都必须存在于两个S3存储桶中。应用程序必须能够在区域之间进行故障转移且不丢失数据。

 | **选项A：** 创建一个新的IAM角色，允许Amazon S3和S3 Batch Operations服务主体承担该角色，该角色具有S3复制的必要权限。
- 这是正确的IAM角色配置，S3复制需要S3服务主体权限
- S3 Batch Operations用于处理现有对象的批量复制

**选项B：** 创建一个新的IAM角色，允许AWS Batch服务主体承担该角色，该角色具有S3复制的必要权限。
- 错误，AWS Batch不是S3复制的正确服务，应该是S3服务主体

**选项C：** 在源S3存储桶上创建S3跨区域复制(CRR)规则。配置规则使用Amazon S3的IAM角色复制到目标S3存储桶。
- 正确，CRR是实现跨区域复制的标准方法
- 但只能处理新对象，不能处理现有对象

**选项D：** 在源S3存储桶上创建双向复制规则。配置规则使用Amazon S3的IAM角色复制到目标S3存储桶。
- 错误，S3 CRR不支持双向复制
- 需要在两个存储桶上分别配置单向复制规则

**选项E：** 创建具有AWS Fargate编排类型的AWS Batch作业。配置作业使用AWS Batch的IAM角色。指定Bash命令使用AWS CLI同步源S3存储桶和目标S3存储桶的内容。
- 这是一个可行但复杂的解决方案
- 不是AWS推荐的最佳实践，维护成本高

**选项F：** 在S3 Batch Operations中创建操作，将源S3存储桶的内容复制到目标S3存储桶。配置操作使用Amazon S3的IAM角色。
- 正确，S3 Batch Operations是处理现有对象批量复制的标准方法

 |  |  |  |
| 220 | A company uses an organization in AWS Organizations to manage multiple AWS accounts. The company needs an automated process across
all AWS accounts to isolate any compromised Amazon EC2 instances when the instances receive a specic tag. | A. Use AWS CloudFormation StackSets to deploy the CloudFormation stacks in all AWS accounts.
B. Create an SCP that has a Deny statement for the ec2:* action with a condition of "aws:RequestTag/isolation": false.
C. Attach the SCP to the root of the organization.
D. Create an AWS CloudFormation template that creates an EC2 instance role that has no IAM policies attached. Congure the template to
have a security group that has an explicit Deny rule on all trac. Use the CloudFormation template to create an AWS Lambda function
that attaches the IAM role to instances. Congure the Lambda function to add a network ACL. Set up an Amazon EventBridge rule to
invoke the Lambda function when a specic tag is applied to a compromised EC2 instance.
E. Create an AWS CloudFormation template that creates an EC2 instance role that has no IAM policies attached. Congure the template to
have a security group that has no inbound rules or outbound rules. Use the CloudFormation template to create an AWS Lambda function
that attaches the IAM role to instances. Congure the Lambda function to replace any existing security groups with the new security
group. Set up an Amazon EventBridge rule to invoke the Lambda function when a specic tag is applied to a compromised EC2 instance. | 一家公司使用AWS Organizations中的组织来管理多个AWS账户。该公司需要一个跨所有AWS账户的自动化流程，当Amazon EC2实例收到特定标签时，能够隔离任何被入侵的EC2实例。

 | **选项A：使用AWS CloudFormation StackSets在所有AWS账户中部署CloudFormation堆栈。**
- 这只是一个部署方法，没有具体说明要部署什么资源来实现隔离功能
- 单独使用StackSets无法解决自动化隔离的需求
- 不完整的解决方案

**选项B：创建一个SCP（服务控制策略），包含对ec2:*操作的拒绝声明，条件为"aws:RequestTag/isolation": false。**
- SCP用于限制账户权限，但这里的逻辑有问题
- 这个策略会阻止没有isolation标签的EC2操作，而不是隔离已标记的实例
- 无法实现题目要求的隔离功能

**选项C：将SCP附加到组织的根部。**
- 这只是选项B的延续，同样无法解决问题
- 仅仅是策略附加位置的说明

**选项D：创建CloudFormation模板，包含没有IAM策略的EC2实例角色和显式拒绝所有流量的安全组。使用模板创建Lambda函数来附加IAM角色，配置Lambda函数添加网络ACL。设置EventBridge规则在特定标签应用到被入侵的EC2实例时调用Lambda函数。**
- 安全组不能有"显式拒绝"规则，安全组只支持允许规则
- 网络ACL的配置复杂且可能影响整个子网
- 技术实现上有错误

**选项E：创建CloudFormation模板，包含没有IAM策略的EC2实例角色和没有入站/出站规则的安全组。使用模板创建Lambda函数来附加IAM角色，配置Lambda函数用新安全组替换现有安全组。设置EventBridge规则在特定标签应用到被入侵的EC2实例时调用Lambda函数。**
- 技术实现正确：没有入站/出站规则的安全组可以有效隔离实例
- 使用EventBridge监控标签变化是正确的自动化方法
- Lambda函数可以自动执行隔离操作
- CloudFormation StackSets可以跨账户部署此解决方案

 |  |  |  |
| 221 | A company manages multiple AWS accounts by using AWS Organizations with OUs for the different business divisions. The company is
updating their corporate network to use new IP address ranges. The company has 10 Amazon S3 buckets in different AWS accounts. The S3
buckets store reports for the different divisions. The S3 bucket congurations allow only private corporate network IP addresses to access the
S3 buckets.
A DevOps engineer needs to change the range of IP addresses that have permission to access the contents of the S3 buckets. The DevOps
engineer also needs to revoke the permissions of two OUs in the company. | A. Create a new SCP that has two statements, one that allows access to the new range of IP addresses for all the S3 buckets and one that
denies access to the old range of IP addresses for all the S3 buckets. Set a permissions boundary for the OrganizationAccountAccessRole
role in the two OUs to deny access to the S3 buckets.
B. Create a new SCP that has a statement that allows only the new range of IP addresses to access the S3 buckets. Create another SCP
that denies access to the S3 buckets. Attach the second SCP to the two OUs.
C. On all the S3 buckets, congure resource-based policies that allow only the new range of IP addresses to access the S3 buckets. Create
a new SCP that denies access to the S3 buckets. Attach the SCP to the two OUs.
D. On all the S3 buckets, congure resource-based policies that allow only the new range of IP addresses to access the S3 buckets. Set a
permissions boundary for the OrganizationAccountAccessRole role in the two OUs to deny access to the S3 buckets. | 一家公司使用AWS Organizations管理多个AWS账户，为不同的业务部门设置了组织单位(OUs)。该公司正在更新其企业网络以使用新的IP地址范围。该公司在不同AWS账户中有10个Amazon S3存储桶，这些S3存储桶存储不同部门的报告。S3存储桶配置仅允许私有企业网络IP地址访问S3存储桶。

一名DevOps工程师需要更改有权访问S3存储桶内容的IP地址范围。该DevOps工程师还需要撤销公司中两个OUs的权限。

2. | **选项A：** 创建一个新的SCP，包含两个语句：一个允许新IP地址范围访问所有S3存储桶，一个拒绝旧IP地址范围访问所有S3存储桶。为两个OUs中的OrganizationAccountAccessRole角色设置权限边界以拒绝访问S3存储桶。
- 问题：SCP不能直接控制基于IP地址的访问，这是资源级别的控制
- 权限边界的使用场景不正确，且只针对特定角色

**选项B：** 创建一个新的SCP，包含仅允许新IP地址范围访问S3存储桶的语句。创建另一个SCP拒绝访问S3存储桶，并将第二个SCP附加到两个OUs。
- 问题：SCP无法直接控制基于IP地址的访问策略
- SCP主要用于限制权限，而不是配置资源访问策略

**选项C：** 在所有S3存储桶上配置基于资源的策略，仅允许新IP地址范围访问S3存储桶。创建一个新的SCP拒绝访问S3存储桶，并将SCP附加到两个OUs。
- 正确：使用S3存储桶策略控制IP地址访问是正确的方法
- 正确：使用SCP在组织级别拒绝特定OUs的访问权限
- 这种方法结合了资源级别和组织级别的控制

**选项D：** 在所有S3存储桶上配置基于资源的策略，仅允许新IP地址范围访问S3存储桶。为两个OUs中的OrganizationAccountAccessRole角色设置权限边界以拒绝访问S3存储桶。
- 部分正确：S3存储桶策略配置正确
- 问题：权限边界只影响特定角色，不能全面控制OU级别的访问
- 权限边界的应用范围有限

3. | C |  |  |
| 222 | A company has started using AWS across several teams. Each team has multiple accounts and unique security proles. The company
manages the accounts in an organization in AWS Organizations. Each account has its own conguration and security controls.
The company's DevOps team wants to use preventive and detective controls to govern all accounts. The DevOps team needs to ensure the
security of accounts now and in the future as the company creates new accounts in the organization. | A. Use Organizations to create OUs that have appropriate SCPs attached for each team. Place team accounts in the appropriate OUs to
apply security controls. Create any new team accounts in the appropriate OUs.
B. Create an AWS Control Tower landing zone. Congure OUs and appropriate controls in AWS Control Tower for the existing teams.
Congure trusted access for AWS Control Tower. Enroll the existing accounts in the appropriate OUs that match the appropriate security
policies for each team. Use AWS Control Tower to provision any new accounts.
C. Create AWS CloudFormation stack sets in the organization's management account. Congure a stack set that deploys AWS Cong with
conguration rules and remediation actions for all controls to each account in the organization. Update the stack sets to deploy to new
accounts as the accounts are created.
D. Congure AWS Cong to manage the AWS Cong rules across all AWS accounts in the organization. Deploy conformance packs that
provide AWS Cong rules and remediation actions across the organization. | 一家公司已经开始在多个团队中使用AWS。每个团队都有多个账户和独特的安全配置文件。公司在AWS Organizations中的组织内管理这些账户。每个账户都有自己的配置和安全控制。

公司的DevOps团队希望使用预防性和检测性控制来治理所有账户。DevOps团队需要确保账户现在和未来的安全性，因为公司会在组织中创建新账户。

 | **选项A：** 使用Organizations创建具有适当SCP（服务控制策略）的OU（组织单位），为每个团队附加相应的SCP。将团队账户放置在适当的OU中以应用安全控制。在适当的OU中创建任何新的团队账户。
- 优点：提供了预防性控制（SCP）
- 缺点：缺乏检测性控制，没有自动化的合规监控和修复机制

**选项B：** 创建AWS Control Tower着陆区。在AWS Control Tower中为现有团队配置OU和适当的控制。为AWS Control Tower配置可信访问。将现有账户注册到与每个团队适当安全策略匹配的相应OU中。使用AWS Control Tower来配置任何新账户。
- 优点：提供预防性和检测性控制的完整解决方案，自动化账户配置，内置合规监控
- 缺点：实施复杂度较高

**选项C：** 在组织的管理账户中创建AWS CloudFormation堆栈集。配置一个堆栈集，将AWS Config与配置规则和修复操作部署到组织中的每个账户。更新堆栈集以在创建新账户时部署到新账户。
- 优点：提供检测性控制和自动修复
- 缺点：缺乏预防性控制，需要手动管理堆栈集更新

**选项D：** 配置AWS Config来管理组织中所有AWS账户的AWS Config规则。部署提供AWS Config规则和修复操作的合规包。
- 优点：提供检测性控制和合规监控
- 缺点：缺乏预防性控制，没有提及新账户的自动化处理

 |  |  |  |
| 223 | A company uses an AWS CodeCommit repository to store its source code and corresponding unit tests. The company has congured an AWS
CodePipeline pipeline that includes an AWS CodeBuild project that runs when code is merged to the main branch of the repository.
The company wants the CodeBuild project to run the unit tests. If the unit tests pass, the CodeBuild project must tag the most recent commit.
How should the company congure the CodeBuild project to meet these requirements? | A. Congure the CodeBuild project to use native Git to done the CodeCommit repository. Congure the project to run the unit tests.
Congure the project to use native Git to create a tag and to push the Git tag to the repository if the code passes the unit tests.
B. Congure the CodeBuild projed to use native Git to done the CodeCommit repository. Congure the project to run the unit tests.
Congure the project to use AWS CLI commands to create a new repository tag in the repository if the code passes the unit tests.
C. Congure the CodeBuild project to use AWS CLI commands to copy the code from the CodeCommit repository. Congure the project to
run the unit tests. Congure the project to use AWS CLI commands to create a new Git tag in the repository if the code passes the unit
tests.
D. Congure the CodeBuild project to use AWS CLI commands to copy the code from the CodeCommit repository. Congure the project to
run the unit tests. Congure the project to use AWS CLI commands to create a new repository tag in the repository if the code passes the
unit tests. | 一家公司使用AWS CodeCommit存储库来存储其源代码和相应的单元测试。该公司已配置了一个AWS CodePipeline管道，其中包含一个AWS CodeBuild项目，当代码合并到存储库的主分支时会运行该项目。

公司希望CodeBuild项目运行单元测试。如果单元测试通过，CodeBuild项目必须为最近的提交打标签。

公司应该如何配置CodeBuild项目来满足这些要求？

 | **选项A：** 配置CodeBuild项目使用原生Git克隆CodeCommit存储库。配置项目运行单元测试。如果代码通过单元测试，配置项目使用原生Git创建标签并将Git标签推送到存储库。
- 使用原生Git克隆存储库是正确的方法
- 使用原生Git创建和推送标签是标准做法
- 这种方法简单直接，符合Git最佳实践

**选项B：** 配置CodeBuild项目使用原生Git克隆CodeCommit存储库。配置项目运行单元测试。如果代码通过单元测试，配置项目使用AWS CLI命令在存储库中创建新的存储库标签。
- 使用原生Git克隆是正确的
- 但混合使用原生Git和AWS CLI来处理标签不是最佳实践
- AWS CLI的"存储库标签"与Git标签是不同的概念

**选项C：** 配置CodeBuild项目使用AWS CLI命令从CodeCommit存储库复制代码。配置项目运行单元测试。如果代码通过单元测试，配置项目使用AWS CLI命令在存储库中创建新的Git标签。
- 使用AWS CLI复制代码不如Git克隆高效
- 表述中"创建新的Git标签"在AWS CLI上下文中不准确

**选项D：** 配置CodeBuild项目使用AWS CLI命令从CodeCommit存储库复制代码。配置项目运行单元测试。如果代码通过单元测试，配置项目使用AWS CLI命令在存储库中创建新的存储库标签。
- 使用AWS CLI复制代码效率较低
- "存储库标签"指的是AWS资源标签，不是Git标签
- 不符合Git版本控制的最佳实践

 |  |  |  |
| 224 | A DevOps engineer manages a company's Amazon Elastic Container Service (Amazon ECS) cluster. The cluster runs on several Amazon EC2
instances that are in an Auto Scaling group. The DevOps engineer must implement a solution that logs and reviews all stopped tasks for
errors. | A. Create an Amazon EventBridge rule to capture task state changes. Send the event to Amazon CloudWatch Logs. Use CloudWatch Logs
Insights to investigate stopped tasks.
B. Congure tasks to write log data in the embedded metric format. Store the logs in Amazon CloudWatch Logs. Monitor the
ContainerInstanceCount metric for changes.
C. Congure the EC2 instances to store logs in Amazon CloudWatch Logs. Create a CloudWatch Contributor Insights rule that uses the EC2
instance log data. Use the Contributor Insights rule to investigate stopped tasks.
D. Congure an EC2 Auto Scaling lifecycle hook for the EC2_INSTANCE_TERMINATING scale-in event. Write the SystemEventLog le to
Amazon S3. Use Amazon Athena to query the log le for errors. |  |  |  |  |  |
| 225 | A company wants to deploy a workload on several hundred Amazon EC2 instances. The company will provision the EC2 instances in an Auto
Scaling group by using a launch template.
The workload will pull les from an Amazon S3 bucket, process the data, and put the results into a different S3 bucket. The EC2 instances
must have least-privilege permissions and must use temporary security credentials. | A. Create an IAM role that has the appropriate permissions for S3 buckets Add the IAM role to an instance prole.
B. Update the launch template to include the IAM instance prole.
C. Create an IAM user that has the appropriate permissions for Amazon S3 Generate a secret key and token.
D. Create a trust anchor and prole Attach the IAM role to the prole.
E. Update the launch template Modify the user data to use the new secret key and token. |  |  |  |  |  |
| 226 | A company is using AWS CodeDeploy to automate software deployment. The deployment must meet these requirements:
• A number of instances must be available to serve trac during the deployment. Trac must be balanced across those instances, and the
instances must automatically heal in the event of failure. • A new eet of instances must be launched for deploying a new revision
automatically, with no manual provisioning.
• Trac must be rerouted to the new environment to half of the new instances at a time. The deployment should succeed if trac is rerouted
to at least half of the instances: otherwise, it should fail.
• Before routing trac to the new eet of instances, the temporary les generated during the deployment process must be deleted.
• At the end of a successful deployment, the original instances in the deployment group must be deleted immediately to reduce costs.
How can a DevOps engineer meet these requirements? | A. Use an Application Load Balancer and an in-place deployment. Associate the Auto Scaling group with the deployment group. Use the
Automatically copy Auto Scaling group option, and use CodeDeployDefault.OneAtAtime as the deployment conguration. Instruct AWS
CodeDeploy to terminate the original instances in the deployment group, and use the AllowTrac hook within appspec.yml to delete the
temporary les.
B. Use an Application Load Balancer and a blue/green deployment. Associate the Auto Scaling group and Application Load Balancer
target group with the deployment group. Use the Automatically copy Auto Scaling group option, create a custom deployment conguration
with minimum healthy hosts dened as 50%, and assign the conguration to the deployment group. Instruct AWS CodeDeploy to terminate
the original instances in the deployment group, and use the BeforeBlockTrac hook within appspec.yml to delete the temporary les.
C. Use an Application Load Balancer and a blue/green deployment. Associate the Auto Scaling group and the Application Load Balancer
target group with the deployment group. Use the Automatically copy Auto Scaling group option, and use CodeDeployDefault.HalfAtAtime
as the deployment conguration. Instruct AWS CodeDeploy to terminate the original instances in the deployment group, and use the
BeforeAllowTrac hook within appspec.yml to delete the temporary les.
D. Use an Application Load Balancer and an in-place deployment. Associate the Auto Scaling group and Application Load Balancer target
group with the deployment group. Use the Automatically copy Auto Scaling group option, and use CodeDeployDefault.AllatOnce as a
deployment conguration. Instruct AWS CodeDeploy to terminate the original instances in the deployment group, and use the BlockTrac
hook within appspec.yml to delete the temporary les. |  |  |  |  |  |
| 227 | A company needs to adopt a multi-account strategy to deploy its applications and the associated CI/CD infrastructure. The company has
created an organization in AWS Organizations that has all features enabled. The company has congured AWS Control Tower and has set up a
landing zone.
The company needs to use AWS Control Tower controls (guardrails) in all AWS accounts in the organization. The company must create the
accounts for a multi-environment application and must ensure that all accounts are congured to an initial baseline. | A. Create an AWS Control Tower Account Factory Customization (AFC) blueprint that uses the baseline conguration. Use AWS Control
Tower Account Factory to provision a dedicated AWS account for each environment and a CI/CD account by using the blueprint.
B. Use AWS Control Tower Account Factory to provision a dedicated AWS account for each environment and a CI/CD account. Use AWS
CloudFormation StackSets to apply the baseline conguration to the new accounts.
C. Use Organizations to provision a multi-environment AWS account and a CI/CD account. In the Organizations management account,
create an AWS Lambda function that assumes the Organizations access role to apply the baseline conguration to the new accounts.
D. Use Organizations to provision a dedicated AWS account for each environment, an audit account, and a CI/CD account. Use AWS
CloudFormation StackSets to apply the baseline conguration to the new accounts. | 一家公司需要采用多账户策略来部署其应用程序和相关的CI/CD基础设施。该公司已在AWS Organizations中创建了一个启用了所有功能的组织。公司已配置了AWS Control Tower并设置了着陆区。

公司需要在组织中的所有AWS账户中使用AWS Control Tower控制措施（护栏）。公司必须为多环境应用程序创建账户，并确保所有账户都配置为初始基线。

 | **选项A：创建一个使用基线配置的AWS Control Tower Account Factory Customization (AFC)蓝图。使用AWS Control Tower Account Factory通过该蓝图为每个环境和CI/CD账户提供专用的AWS账户。**
- 正确使用了AWS Control Tower Account Factory来创建账户
- AFC（Account Factory Customization）是Control Tower的原生功能，专门用于在账户创建时应用自定义配置
- 能够确保所有新账户自动应用基线配置和Control Tower护栏
- 完全符合Control Tower的最佳实践

**选项B：使用AWS Control Tower Account Factory为每个环境和CI/CD账户提供专用的AWS账户。使用AWS CloudFormation StackSets将基线配置应用到新账户。**
- 使用Control Tower Account Factory创建账户是正确的
- 但使用CloudFormation StackSets来应用基线配置不是最佳实践
- 这种方法需要额外的步骤和管理开销
- 没有充分利用Control Tower的原生自动化功能

**选项C：使用Organizations提供多环境AWS账户和CI/CD账户。在Organizations管理账户中，创建一个AWS Lambda函数，该函数承担Organizations访问角色以将基线配置应用到新账户。**
- 直接使用Organizations而不是Control Tower Account Factory
- 这种方法绕过了Control Tower的护栏和自动化功能
- 需要自定义Lambda函数，增加了复杂性和维护成本
- 不符合题目要求使用Control Tower控制措施的需求

**选项D：使用Organizations为每个环境、审计账户和CI/CD账户提供专用的AWS账户。使用AWS CloudFormation StackSets将基线配置应用到新账户。**
- 直接使用Organizations而不是Control Tower
- 同样绕过了Control Tower的功能
- 虽然提到了审计账户，但没有利用Control Tower的集成审计功能
- 不符合题目明确要求使用Control Tower的需求

 |  |  |  |
| 228 | A DevOps team has created a Custom Lambda rule in AWS Cong. The rule monitors Amazon Elastic Container Repository (Amazon ECR)
policy statements for ecr:* actions. When a noncompliant repository is detected, Amazon EventBridge uses Amazon Simple Notication
Service (Amazon SNS) to route the notication to a security team.
When the custom AWS Cong rule is evaluated, the AWS Lambda function fails to run. | A. Modify the Lambda function's resource policy to grant AWS Cong permission to invoke the function.
B. Modify the SNS topic policy to include conguration changes for EventBridge to publish to the SNS topic.
C. Modify the Lambda function's execution role to include conguration changes for custom AWS Cong rules.
D. Modify all the ECR repository policies to grant AWS Cong access to the necessary ECR API actions. |  |  |  |  |  |
| 229 | A developer is creating a proof of concept for a new software as a service (SaaS) application. The application is in a shared development AWS
account that is part of an organization in AWS Organizations.
The developer needs to create service-linked IAM roles for the AWS services that are being considered for the proof of concept. The solution
needs to give the developer the ability to create and congure the service-linked roles only. | A. Create an IAM user for the developer in the organization's management account. Congure a cross-account role in the development
account for the developer to use. Limit the scope of the cross-account role to common services.
B. Add the developer to an IAM group. Attach the PowerUserAccess managed policy to the IAM group. Enforce multi-factor authentication
(MFA) on the user account.
C. Add an SCP to the development account in Organizations. Congure the SCP with a Deny rule for iam:* to limit the developer's access.
D. Create an IAM role that has the necessary IAM access to allow the developer to create policies and roles. Create and attach a
permissions boundary to the role. Grant the developer access to assume the role. |  |  |  |  |  |
| 230 | A company uses AWS Organizations to manage its AWS accounts. The company wants its monitoring system to receive an alert when a root
user logs in. The company also needs a dashboard to display any log activity that the root user generates. | A. Enable AWS Cong with a multi-account aggregator. Congure log forwarding to Amazon CloudWatch Logs.
B. Create an Amazon QuickSight dashboard that uses an Amazon CloudWatch Logs query.
C. Create an Amazon CloudWatch Logs metric lter to match root user login events. Congure a CloudWatch alarm and an Amazon Simple
Notication Service (Amazon SNS) topic to send alerts to the company's monitoring system.
D. Create an Amazon CloudWatch Logs subscription lter to match root user login events. Congure the lter to forward events to an
Amazon Simple Notication Service (Amazon SNS) topic. Congure the SNS topic to send alerts to the company's monitoring system.
E. Create an AWS CloudTrail organization trail. Congure the organization trail to send events to Amazon CloudWatch Logs. |  |  |  |  |  |
| 231 | A company uses AWS Organizations to manage its AWS accounts. A DevOps engineer must ensure that all users who access the AWS
Management Console are authenticated through the company’s corporate identity provider (IdP). | A. Use Amazon GuardDuty with a delegated administrator account Use GuardDuty to enforce denial of IAM user logins.
B. Use AWS IAM Identity Center to congure identity federation with SAML 2.0.
C. Create a permissions boundary in AWS IAM Identity Center to deny password logins for IAM users.
D. Create IAM groups in the Organizations management account to apply consistent permissions for all IAM users.
E. Create an SCP in Organizations to deny password creation for IAM users. | 一家公司使用AWS Organizations来管理其AWS账户。DevOps工程师必须确保所有访问AWS管理控制台的用户都通过公司的企业身份提供商(IdP)进行身份验证。

 | **A. 使用Amazon GuardDuty与委托管理员账户，使用GuardDuty强制拒绝IAM用户登录。**
- 不正确。GuardDuty是威胁检测服务，用于监控恶意活动和未授权行为，不是用于强制身份验证策略的工具。它无法阻止IAM用户登录或强制使用企业IdP。

**B. 使用AWS IAM Identity Center配置SAML 2.0身份联合。**
- 正确。IAM Identity Center（前身为AWS SSO）专门设计用于与企业身份提供商集成，支持SAML 2.0联合身份验证。这是实现企业IdP统一身份验证的标准解决方案。

**C. 在AWS IAM Identity Center中创建权限边界来拒绝IAM用户的密码登录。**
- 不正确。权限边界用于定义用户或角色的最大权限，不是用于控制身份验证方式的工具。此外，这种方法不能强制使用企业IdP。

**D. 在Organizations管理账户中创建IAM组，为所有IAM用户应用一致的权限。**
- 不正确。创建IAM组只是权限管理，不能解决身份验证问题。用户仍然可以使用IAM用户凭证直接登录，而不通过企业IdP。

**E. 在Organizations中创建SCP来拒绝IAM用户的密码创建。**
- 部分正确但不完整。虽然SCP可以阻止创建IAM用户密码，但这只是消极的控制措施，不能提供通过企业IdP的积极身份验证解决方案。

 |  |  |  |
| 232 | A company has deployed a new platform that runs on Amazon Elastic Kubernetes Service (Amazon EKS). The new platform hosts web
applications that users frequently update. The application developers build the Docker images for the applications and deploy the Docker
images manually to the platform.
The platform usage has increased to more than 500 users every day. Frequent updates, building the updated Docker images for the
applications, and deploying the Docker images on the platform manually have all become dicult to manage.
The company needs to receive an Amazon Simple Notication Service (Amazon SNS) notication if Docker image scanning returns any HIGH
or CRITICAL ndings for operating system or programming language package vulnerabilities. | A. Create an AWS CodeCommit repository to store the Dockerle and Kubernetes deployment les. Create a pipeline in AWS CodePipeline.
Use an Amazon S3 event to invoke the pipeline when a newer version of the Dockerle is committed. Add a step to the pipeline to initiate
the AWS CodeBuild project.
B. Create an AWS CodeCommit repository to store the Dockerle and Kubernetes deployment les. Create a pipeline in AWS CodePipeline.
Use an Amazon EventBridge event to invoke the pipeline when a newer version of the Dockerle is committed. Add a step to the pipeline
to initiate the AWS CodeBuild project.
C. Create an AWS CodeBuild project that builds the Docker images and stores the Docker images in an Amazon Elastic Container Registry
(Amazon ECR) repository. Turn on basic scanning for the ECR repository. Create an Amazon EventBridge rule that monitors Amazon
GuardDuty events. Congure the EventBridge rule to send an event to an SNS topic when the nding-severity-counts parameter is more
than 0 at a CRITICAL or HIGH level.
D. Create an AWS CodeBuild project that builds the Docker images and stores the Docker images in an Amazon Elastic Container Registry
(Amazon ECR) repository. Turn on enhanced scanning for the ECR repository. Create an Amazon EventBridge rule that monitors ECR image
scan events. Congure the EventBridge rule to send an event to an SNS topic when the nding-severity-counts parameter is more than 0
at a CRITICAL or HIGH level.
E. Create an AWS CodeBuild project that scans the Dockerle. Congure the project to build the Docker images and store the Docker
images in an Amazon Elastic Container Registry (Amazon ECR) repository if the scan is successful. Congure an SNS topic to provide
notication if the scan returns any vulnerabilities. |  |  |  |  |  |
| 233 | A company groups its AWS accounts in OUs in an organization in AWS Organizations. The company has deployed a set of Amazon API Gateway
APIs in one of the Organizations accounts. The APIs are bound to the account's VPC and have no existing authentication mechanism. Only
principals in a specic OU can have permissions to invoke the APIs.
The company applies the following policy to the API Gateway interface VPC endpoint:
The company also updates the API Gateway resource policies to deny invocations that do not come through the interface VPC endpoint. After
the updates, the following error message appears during attempts to use the interface VPC endpoint URL to invoke an API: "User: anonymous
is not authorized." | A. Enable IAM authentication on all API methods by setting AWS JAM as the authorization method.
B. Create a token-based AWS Lambda authorizer that passes the caller's identity in a bearer token.
C. Create a request parameter-based AWS Lambda authorizer that passes the caller's identity in a combination of headers, query string
parameters, stage variables, and $cortext variables.
D. Use Amazon Cognito user pools as the authorizer to control access to the API.
E. Verify the identity of the requester by using Signature Version 4 to sign client requests by using AWS credentials. | 一家公司在AWS Organizations中将其AWS账户分组到组织单位(OU)中。该公司在其中一个Organizations账户中部署了一组Amazon API Gateway API。这些API绑定到账户的VPC，并且没有现有的身份验证机制。只有特定OU中的主体才能拥有调用这些API的权限。

公司将以下策略应用到API Gateway接口VPC端点：
公司还更新了API Gateway资源策略，拒绝不通过接口VPC端点的调用。更新后，在尝试使用接口VPC端点URL调用API时出现以下错误消息："User: anonymous is not authorized."

 | **A. 通过设置AWS IAM作为授权方法，在所有API方法上启用IAM身份验证。**
- 正确选项。错误消息"User: anonymous is not authorized"表明API Gateway无法识别调用者的身份。启用IAM身份验证可以确保请求包含有效的AWS凭证，从而解决匿名用户问题。

**B. 创建基于令牌的AWS Lambda授权器，在bearer token中传递调用者的身份。**
- 不适合此场景。Lambda授权器通常用于自定义身份验证逻辑，但这里的问题是缺乏基本的身份验证机制，而不是需要复杂的自定义授权。

**C. 创建基于请求参数的AWS Lambda授权器，通过headers、查询字符串参数、stage变量和$context变量的组合传递调用者身份。**
- 过于复杂且不必要。同样是自定义授权方案，但问题的根本原因是缺乏身份验证，不是需要复杂的参数处理。

**D. 使用Amazon Cognito用户池作为授权器来控制对API的访问。**
- 不适合此场景。Cognito用户池主要用于应用程序用户身份验证，而这里需要的是AWS账户/角色级别的身份验证。

**E. 通过使用AWS凭证的Signature Version 4签名客户端请求来验证请求者的身份。**
- 这是IAM身份验证的底层实现机制，但选项A更直接地描述了解决方案。

 |  |  |  |
| 234 | A company wants to decrease the time it takes to develop new features. The company uses AWS CodeBuild and AWS CodeDeploy to build and
deploy its applications. The company uses AWS CodePipeline to deploy each microservice with its own CI/CD pipeline.
The company needs more visibility into the average time between the release of new features and the average time to recover after a failed
deployment. | A. Program an AWS Lambda function that creates Amazon CloudWatch custom metrics with information about successful runs and failed
runs for each pipeline. Create an Amazon EventBridge rule to invoke the Lambda function every 5 minutes. Use the metrics to build a
CloudWatch dashboard.
B. 
C. Program an AWS Lambda function that writes information about successful runs and failed runs to Amazon DynamoD
D. Program an AWS Lambda function that writes information about successful runs and failed runs to Amazon DynamoD | 一家公司希望减少开发新功能所需的时间。该公司使用AWS CodeBuild和AWS CodeDeploy来构建和部署应用程序。公司使用AWS CodePipeline为每个微服务部署各自的CI/CD管道。

公司需要更好地了解新功能发布的平均时间以及部署失败后的平均恢复时间。

 | **选项A：** 编写一个AWS Lambda函数，使用每个管道的成功运行和失败运行信息创建Amazon CloudWatch自定义指标。创建Amazon EventBridge规则每5分钟调用一次Lambda函数。使用这些指标构建CloudWatch仪表板。

- ✅ **正确方案**：这是一个完整且有效的解决方案
- 使用CloudWatch自定义指标来跟踪部署成功/失败情况
- EventBridge定期触发Lambda函数收集数据
- CloudWatch仪表板提供可视化监控界面
- 能够有效测量平均发布时间和故障恢复时间

**选项B：** [选项内容缺失]

**选项C：** 编写一个AWS Lambda函数，将成功运行和失败运行的信息写入Amazon DynamoDB...

- ❌ **不完整**：选项描述被截断
- 虽然DynamoDB可以存储数据，但缺少可视化和分析组件
- 没有提到如何计算平均时间或创建仪表板

**选项D：** 编写一个AWS Lambda函数，将成功运行和失败运行的信息写入Amazon DynamoDB...

- ❌ **不完整**：选项描述被截断
- 与选项C存在相同问题

 |  |  |  |
| 235 | A company has developed a static website hosted on an Amazon S3 bucket. The website is deployed using AWS CloudFormation. The
CloudFormation template denes an S3 bucket and a custom resource that copies content into the bucket from a source location.
The company has decided that it needs to move the website to a new location, so the existing CloudFormation stack must be deleted and re-
created. However, CloudFormation reports that the stack could not be deleted cleanly. | A. Deletion has failed because the S3 bucket has an active website conguration. Modify the CloudFormation template to remove the
WebsiteConguration property from the S3 bucket resource.
B. Deletion has failed because the S3 bucket is not empty. Modify the custom resource's AWS Lambda function code to recursively empty
the bucket when RequestType is Delete.
C. Deletion has failed because the custom resource does not dene a deletion policy. Add a DeletionPolicy property to the custom
resource denition with a value of RemoveOnDeletion.
D. Deletion has failed because the S3 bucket is not empty. Modify the S3 bucket resource in the CloudFormation template to add a
DeletionPolicy property with a value of Empty. | 一家公司开发了一个托管在Amazon S3存储桶上的静态网站。该网站使用AWS CloudFormation进行部署。CloudFormation模板定义了一个S3存储桶和一个自定义资源，该自定义资源将内容从源位置复制到存储桶中。

公司决定需要将网站迁移到新位置，因此必须删除并重新创建现有的CloudFormation堆栈。但是，CloudFormation报告无法正常删除堆栈。

 | **选项A：** 删除失败是因为S3存储桶有活跃的网站配置。修改CloudFormation模板以从S3存储桶资源中移除WebsiteConfiguration属性。
- **分析：** 这是错误的。S3存储桶的网站配置不会阻止CloudFormation删除堆栈。网站配置只是存储桶的一个属性，不会影响删除操作。

**选项B：** 删除失败是因为S3存储桶不为空。修改自定义资源的AWS Lambda函数代码，在RequestType为Delete时递归清空存储桶。
- **分析：** 这是正确的。CloudFormation无法删除非空的S3存储桶，这是AWS的安全机制。当自定义资源接收到删除请求时，Lambda函数应该清空存储桶中的所有对象，然后CloudFormation才能成功删除存储桶。

**选项C：** 删除失败是因为自定义资源没有定义删除策略。在自定义资源定义中添加DeletionPolicy属性，值为RemoveOnDeletion。
- **分析：** 这是错误的。首先，"RemoveOnDeletion"不是有效的DeletionPolicy值。其次，自定义资源的删除行为是由Lambda函数代码控制的，而不是DeletionPolicy。

**选项D：** 删除失败是因为S3存储桶不为空。修改CloudFormation模板中的S3存储桶资源，添加值为Empty的DeletionPolicy属性。
- **分析：** 这是错误的。"Empty"不是有效的DeletionPolicy值。S3存储桶的有效DeletionPolicy值包括Delete、Retain和Snapshot（但S3不支持Snapshot）。

 |  |  |  |
| 236 | A company uses Amazon EC2 as its primary compute platform. A DevOps team wants to audit the company's EC2 instances to check whether
any prohibited applications have been installed on the EC2 instances. | A. Congure AWS Systems Manager on each instance. Use AWS Systems Manager Inventory. Use Systems Manager resource data sync to
synchronize and store ndings in an Amazon S3 bucket. Create an AWS Lambda function that runs when new objects are added to the S3
bucket. Congure the Lambda function to identify prohibited applications.
B. Congure AWS Systems Manager on each instance. Use Systems Manager Inventory Create AWS Cong rules that monitor changes
from Systems Manager Inventory to identify prohibited applications.
C. Congure AWS Systems Manager on each instance. Use Systems Manager Inventory. Filter a trail in AWS CloudTrail for Systems
Manager Inventory events to identify prohibited applications.
D. Designate Amazon CloudWatch Logs as the log destination for all application instances. Run an automated script across all instances
to create an inventory of installed applications. Congure the script to forward the results to CloudWatch Logs. Create a CloudWatch
alarm that uses lter patterns to search log data to identify prohibited applications. | 一家公司使用Amazon EC2作为其主要计算平台。DevOps团队希望审计公司的EC2实例，以检查是否在EC2实例上安装了任何禁用的应用程序。

 | **选项A：** 在每个实例上配置AWS Systems Manager。使用AWS Systems Manager Inventory。使用Systems Manager资源数据同步将发现结果同步并存储在Amazon S3存储桶中。创建一个AWS Lambda函数，当新对象添加到S3存储桶时运行。配置Lambda函数来识别禁用的应用程序。

- **优点：** 这是一个完整的解决方案，使用了正确的服务组合
- **分析：** Systems Manager Inventory可以收集软件清单，Resource Data Sync可以将数据集中存储到S3，Lambda可以处理和分析数据来识别禁用应用程序
- **可行性：** 高度可行且符合AWS最佳实践

**选项B：** 在每个实例上配置AWS Systems Manager。使用Systems Manager Inventory。创建AWS Config规则来监控Systems Manager Inventory的变化，以识别禁用的应用程序。

- **优点：** 使用了正确的清单服务
- **缺点：** AWS Config主要用于配置合规性监控，不是专门设计用来处理软件清单数据和识别特定应用程序的
- **可行性：** 技术上可能，但不是最佳方案

**选项C：** 在每个实例上配置AWS Systems Manager。使用Systems Manager Inventory。在AWS CloudTrail中过滤Systems Manager Inventory事件的跟踪来识别禁用的应用程序。

- **缺点：** CloudTrail记录的是API调用和管理事件，而不是实际的软件清单内容
- **问题：** CloudTrail无法提供应用程序安装的详细信息，只能显示Inventory服务的调用记录
- **可行性：** 不可行，方向错误

**选项D：** 指定Amazon CloudWatch Logs作为所有应用程序实例的日志目标。在所有实例上运行自动化脚本来创建已安装应用程序的清单。配置脚本将结果转发到CloudWatch Logs。创建CloudWatch告警，使用过滤模式搜索日志数据来识别禁用的应用程序。

- **缺点：** 需要自定义脚本开发和维护，增加了复杂性
- **问题：** 没有利用AWS原生的清单管理服务，重新发明轮子
- **可行性：** 可行但不是最佳实践

 |  |  |  |
| 237 | A company has an event-driven JavaScript application. The application uses decoupled AWS managed services that publish, consume, and
route events. During application testing, events are not delivered to the target that is specied by an Amazon EventBridge rule.
A DevOps team must provide application testers with additional functionality to view, troubleshoot, and prevent the loss of events without
redeployment of the application. | A. Launch AWS Device Farm with a standard test environment and project to run a specic build of the application.
B. Create an Amazon S3 bucket. Enable AWS CloudTrail. Create a CloudTrail trail that species the S3 bucket as the storage location.
C. Congure the EventBridge rule to use an Amazon Simple Queue Service (Amazon SQS) standard queue as a dead-letter queue.
D. Congure the EventBridge rule to use an Amazon Simple Queue Service (Amazon SQS) FIFO queue as a dead-letter queue.
E. Create a log group in Amazon CloudWatch Logs Specify the log group as an additional target of the EventBridge rule.
F. Update the application code base to use the AWS X-Ray SDK tracing feature to instrument the code with support for the X-Amzn-Trace-Id
header. | 一家公司有一个事件驱动的JavaScript应用程序。该应用程序使用解耦的AWS托管服务来发布、消费和路由事件。在应用程序测试期间，事件没有被传递到Amazon EventBridge规则指定的目标。

DevOps团队必须为应用程序测试人员提供额外的功能来查看、故障排除和防止事件丢失，且不需要重新部署应用程序。

 | **A. 启动AWS Device Farm，使用标准测试环境和项目来运行应用程序的特定构建版本。**
- 不正确。AWS Device Farm主要用于移动应用程序的测试，不适用于EventBridge事件传递问题的故障排除。

**B. 创建Amazon S3存储桶。启用AWS CloudTrail。创建一个CloudTrail跟踪，指定S3存储桶作为存储位置。**
- 部分有用但不完整。CloudTrail可以记录EventBridge的API调用，但无法防止事件丢失或提供实时故障排除能力。

**C. 配置EventBridge规则使用Amazon Simple Queue Service (Amazon SQS)标准队列作为死信队列。**
- 正确。死信队列可以捕获未能成功传递到目标的事件，防止事件丢失，并允许测试人员查看和分析失败的事件。

**D. 配置EventBridge规则使用Amazon Simple Queue Service (Amazon SQS) FIFO队列作为死信队列。**
- 技术上可行，但通常标准队列就足够了，FIFO队列会增加不必要的复杂性和成本。

**E. 在Amazon CloudWatch Logs中创建日志组。将日志组指定为EventBridge规则的附加目标。**
- 正确。将CloudWatch Logs作为附加目标可以记录所有事件，提供查看和故障排除功能，且不需要重新部署应用程序。

**F. 更新应用程序代码库以使用AWS X-Ray SDK跟踪功能，通过支持X-Amzn-Trace-Id头来检测代码。**
- 不正确。这需要重新部署应用程序，违反了题目要求的"不需要重新部署"的约束。

 |  |  |  |
| 238 | A company is migrating its container-based workloads to an AWS Organizations multi-account environment. The environment consists of
application workload accounts that the company uses to deploy and run the containerized workloads. The company has also provisioned a
shared services account for shared workloads in the organization.
The company must follow strict compliance regulations. All container images must receive security scanning before they are deployed to any
environment. Images can be consumed by downstream deployment mechanisms after the images pass a scan with no critical vulnerabilities.
Pre-scan and post-scan images must be isolated from one another so that a deployment can never use pre-scan images.
A DevOps engineer needs to create a strategy to centralize this process. | A. Create Amazon Elastic Container Registry (Amazon ECR) repositories in the shared services account: one repository for each pre-scan
image and one repository for each post-scan image. Congure Amazon ECR image scanning to run on new image pushes to the pre-scan
repositories. Use resource-based policies to grant the organization write access to the pre-scan repositories and read access to the post-
scan repositories.
B. Create pre-scan Amazon Elastic Container Registry (Amazon ECR) repositories in each account that publishes container images. Create
repositories for post-scan images in the shared services account. Congure Amazon ECR image scanning to run on new image pushes to
the pre-scan repositories. Use resource-based policies to grant the organization read access to the post-scan repositories.
C. Congure image replication for each image from the image's pre-scan repository to the image's post-scan repository.
D. Create a pipeline in AWS CodePipeline for each pre-scan repository. Create a source stage that runs when new images are pushed to
the pre-scan repositories. Create a stage that uses AWS CodeBuild as the action provider. Write a buildspec.yaml denition that
determines the image scanning status and pushes images without critical vulnerabilities to the post-scan repositories.
E. Create an AWS Lambda function. Create an Amazon EventBridge rule that reacts to image scanning completed events and invokes the
Lambda function. Write function code that determines the image scanning status and pushes images without critical vulnerabilities to the
post-scan repositories. |  |  |  |  |  |
| 239 | A company uses an Amazon Elastic Kubernetes Service (Amazon EKS) cluster to deploy its web applications on containers. The web
applications contain condential data that cannot be decrypted without specic credentials.
A DevOps engineer has stored the credentials in AWS Secrets Manager. The secrets are encrypted by an AWS Key Management Service (AWS
KMS) customer managed key. A Kubernetes service account for a third-party tool makes the secrets available to the applications. The service
account assumes an IAM role that the company created to access the secrets.
The service account receives an Access Denied (403 Forbidden) error while trying to retrieve the secrets from Secrets Manager. | A. The IAM role that is attached to the EKS cluster does not have access to retrieve the secrets from Secrets Manager.
B. The key policy for the customer managed key does not allow the Kubernetes service account IAM role to use the key.
C. The key policy for the customer managed key does not allow the EKS cluster IAM role to use the key.
D. The IAM role that is assumed by the Kubernetes service account does not have permission to access the EKS cluster. | 一家公司使用Amazon Elastic Kubernetes Service (Amazon EKS)集群在容器上部署其Web应用程序。这些Web应用程序包含机密数据，如果没有特定的凭证就无法解密。

一名DevOps工程师已将凭证存储在AWS Secrets Manager中。这些密钥由AWS Key Management Service (AWS KMS)客户管理密钥加密。第三方工具的Kubernetes服务账户使这些密钥对应用程序可用。该服务账户承担公司创建的IAM角色来访问这些密钥。

该服务账户在尝试从Secrets Manager检索密钥时收到Access Denied (403 Forbidden)错误。

 | **A. 附加到EKS集群的IAM角色没有从Secrets Manager检索密钥的访问权限。**
- 这个选项不正确。题目明确说明是Kubernetes服务账户承担IAM角色来访问密钥，而不是EKS集群的IAM角色直接访问Secrets Manager。

**B. 客户管理密钥的密钥策略不允许Kubernetes服务账户IAM角色使用该密钥。**
- 这个选项很可能正确。当使用客户管理的KMS密钥加密Secrets Manager中的密钥时，访问者不仅需要Secrets Manager的权限，还需要KMS密钥的使用权限。如果密钥策略没有授权给服务账户的IAM角色，就会出现403错误。

**C. 客户管理密钥的密钥策略不允许EKS集群IAM角色使用该密钥。**
- 这个选项不正确。访问Secrets Manager的是Kubernetes服务账户承担的IAM角色，而不是EKS集群的IAM角色。

**D. 由Kubernetes服务账户承担的IAM角色没有访问EKS集群的权限。**
- 这个选项不正确。如果IAM角色没有访问EKS集群的权限，服务账户根本无法运行，更不会到达尝试访问Secrets Manager的步骤。

 |  |  |  |
| 240 | A company is migrating its product development teams from an on-premises data center to a hybrid environment. The new environment will
add four AWS Regions and will give the developers the ability to use the Region that is geographically closest to them.
All the development teams use a shared set of Linux applications. The on-premises data center stores the applications on a NetApp ONTAP
storage device. The storage volume is mounted read-only on the development on-premises VMs. The company updates the applications on
the shared volume once a week.
A DevOps engineer needs to replicate the data to all the new Regions. The DevOps engineer must ensure that the data is always up to date
with deduplication. The data also must not be dependent on the availability of the on-premises storage device. | A. Create an Amazon S3 File Gateway in the on-premises data center. Create S3 buckets in each Region. Set up a cron job to copy the data
from the storage device to the S3 File Gateway. Set up S3 Cross-Region Replication (CRR) to the S3 buckets in each Region.
B. Create an Amazon FSx File Gateway in one Region. Create le servers in Amazon FSx for Windows File Server in each Region. Set up a
cron job to copy the data from the storage device to the FSx File Gateway.
C. Create Multi-AZ Amazon FSx for NetApp ONTAP instances and volumes in each Region. Congure a scheduled SnapMirror relationship
between the on-premises storage device and the FSx for ONTAP instances.
D. Create an Amazon Elastic File System (Amazon EFS) le system in each Region. Deploy an AWS DataSync agent in the on-premises data
center. Congure a schedule for DataSync to copy the data to Amazon EFS daily. |  |  |  |  |  |
| 241 | A company has an application that stores data that includes personally identiable information (PII) in an Amazon S3 bucket. All data is
encrypted with AWS Key Management Service (AWS KMS) customer managed keys. All AWS resources are deployed from an AWS
CloudFormation template.
A DevOps engineer needs to set up a development environment for the application in a different AWS account. The data in the development
environment's S3 bucket needs to be updated once a week from the production environment's S3 bucket.
The company must not move PII from the production environment without anonymizing the PII rst. The data in each environment must be
encrypted with different KMS customer managed keys. | A. Activate Amazon Macie on the S3 bucket in the production account. Create an AWS Step Functions state machine to initiate a discovery
job and redact all PII before copying les to the S3 bucket in the development account. Give the state machine tasks decrypt permissions
on the KMS key in the production account. Give the state machine tasks encrypt permissions on the KMS key in the development account.
B. Set up S3 replication between the production S3 bucket and the development S3 bucket. Activate Amazon Macie on the development
S3 bucket. Create an AWS Step Functions state machine to initiate a discovery job and redact all PII as the les are copied to the
development S3 bucket. Give the state machine tasks encrypt and decrypt permissions on the KMS key in the development account.
C. Set up an S3 Batch Operations job to copy les from the production S3 bucket to the development S3 bucket. In the development
account, congure an AWS Lambda function to redact ail PII. Congure S3 Object Lambda to use the Lambda function for S3 GET requests.
Give the Lambda function's IAM role encrypt and decrypt permissions on the KMS key in the development account.
D. Create a development environment from the CloudFormation template in the development account. Schedule an Amazon EventBridge
rule to start the AWS Step Functions state machine once a week.
E. Create a development environment from the CloudFormation template in the development account. Schedule a cron job on an Amazon
EC2 instance to run once a week to start the S3 Batch Operations job. |  |  |  |  |  |
| 242 | A company uses an Amazon Elastic Kubernetes Service (Amazon EKS) cluster to host its machine learning (ML) application. As the ML model
and the container image size grow, the time that new pods take to start up has increased to several minutes.
A DevOps engineer needs to reduce the startup time to seconds. The solution must also reduce the startup time to seconds when the pod
runs on nodes that were recently added to the cluster.
The DevOps engineer creates an Amazon EventBridge rule that invokes an automation in AWS Systems Manager. The automation prefetches
the container images from an Amazon Elastic Container Registry (Amazon ECR) repository when new images are pushed to the repository. The
DevOps engineer also congures tags to be applied to the cluster and the node groups. | A. Create an IAM role that has a policy that allows EventBridge to use Systems Manager to run commands in the EKS cluster's control
plane nodes. Create a Systems Manager State Manager association that uses the control plane nodes' tags to prefetch corresponding
container images.
B. Create an IAM role that has a policy that allows EventBridge to use Systems Manager to run commands in the EKS cluster's nodes.
Create a Systems Manager State Manager association that uses the nodes' machine size to prefetch corresponding container images.
C. Create an IAM role that has a policy that allows EventBridge to use Systems Manager to run commands in the EKS cluster's nodes.
Create a Systems Manager State Manager association that uses the nodes' tags to prefetch corresponding container images.
D. Create an IAM role that has a policy that allows EventBridge to use Systems Manager to run commands in the EKS cluster's control
plane nodes. Create a Systems Manager State Manager association that uses the nodes' tags to prefetch corresponding container
images. |  |  |  |  |  |
| 243 | A company's application has an API that retrieves workload metrics. The company needs to audit, analyze, and visualize these metrics from
the application to detect issues at scale. | A. Congure an Amazon EventBridge schedule to invoke an AWS Lambda function that calls the API to retrieve workload metrics. Store the
workload metric data in an Amazon S3 bucket.
B. Congure an Amazon EventBridge schedule to invoke an AWS Lambda function that calls the API to retrieve workload metrics. Store the
workload metric data in an Amazon DynamoDB table that has a DynamoDB stream enabled.
C. Create an AWS Glue crawler to catalog the workload metric data in the Amazon S3 bucket. Create views in Amazon Athena for the
cataloged data.
D. Connect an AWS Glue crawler to the Amazon DynamoDB stream to catalog the workload metric data. Create views in Amazon Athena for
the cataloged data.
E. Create Amazon QuickSight datasets from the Amazon Athena views. Create a QuickSight analysis to visualize the workload metric data
as a dashboard.
F. Create an Amazon CloudWatch dashboard that has custom widgets that invoke AWS Lambda functions. Congure the Lambda functions
to query the workload metrics data from the Amazon Athena views. |  |  |  |  |  |
| 244 | A DevOps engineer is building the infrastructure for an application. The application needs to run on an Amazon Elastic Kubernetes Service
(Amazon EKS) cluster that includes Amazon EC2 instances. The EC2 instances need to use an Amazon Elastic File System (Amazon EFS) le
system as a storage backend. The Amazon EFS Container Storage Interface (CSI) driver is installed on the EKS cluster.
When the DevOps engineer starts the application, the EC2 instances do not mount the EFS le system. | A. Switch the EKS nodes from Amazon EC2 to AWS Fargate.
B. Add an inbound rule to the EFS le system’s security group to allow NFS trac from the EKS cluster.
C. Create an IAM role that allows the Amazon EFS CSI driver to interact with the le system
D. Set up AWS DataSync to congure le transfer between the EFS le system and the EKS nodes.
E. Create a mount target for the EFS le system in the subnet of the EKS nodes. | 一名DevOps工程师正在为应用程序构建基础设施。该应用程序需要运行在包含Amazon EC2实例的Amazon Elastic Kubernetes Service (Amazon EKS) 集群上。EC2实例需要使用Amazon Elastic File System (Amazon EFS) 文件系统作为存储后端。Amazon EFS Container Storage Interface (CSI) 驱动程序已安装在EKS集群上。

当DevOps工程师启动应用程序时，EC2实例无法挂载EFS文件系统。

 | **A. 将EKS节点从Amazon EC2切换到AWS Fargate**
- 错误。切换到Fargate并不能解决EFS挂载问题，而且题目明确要求使用EC2实例。Fargate也支持EFS，但这不是解决当前问题的方案。

**B. 在EFS文件系统的安全组中添加入站规则，允许来自EKS集群的NFS流量**
- 正确。EFS使用NFS协议（端口2049），如果安全组没有正确配置允许NFS流量，EC2实例就无法访问EFS文件系统。这是一个常见的网络连接问题。

**C. 创建一个IAM角色，允许Amazon EFS CSI驱动程序与文件系统交互**
- 部分正确，但通常EFS CSI驱动程序需要的IAM权限主要用于创建和管理访问点等操作，而不是基本的文件系统挂载。基本挂载更多依赖于网络连接。

**D. 设置AWS DataSync来配置EFS文件系统和EKS节点之间的文件传输**
- 错误。DataSync是用于数据迁移和同步的服务，不是用于解决实时文件系统挂载问题的。

**E. 在EKS节点的子网中为EFS文件系统创建挂载目标**
- 正确。EFS需要在每个可用区创建挂载目标，如果EKS节点所在的子网没有对应的EFS挂载目标，节点就无法访问EFS文件系统。

 |  |  |  |
| 245 | A company deploys an application on on-premises devices in the company’s on-premises data center. The company uses an AWS Direct
Connect connection between the data center and the company's AWS account. During initial setup of the on-premises devices and during
application updates, the application needs to retrieve conguration les from an Amazon Elastic File System (Amazon EFS) le system.
All trac from the on-premises devices to Amazon EFS must remain private and encrypted. The on-premises devices must follow the principle
of least privilege for AWS access. The company's DevOps team needs the ability to revoke access from a single device without affecting the
access of the other devices. | A. Create an IAM role that trust IAM Roles Anywhere. Attach the
AmazonElasticFileSystemClientReadWriteAccess to the role. Create an IAM Roles Anywhere prole for the IAM role. Congure the AWS CLI
on the on-premises devices to use the aws_signing_helper command to obtain credentials.
B. Generate certicates for each on-premises device in AWS Private Certicate Authority. Create a trust anchor in IAM Roles Anywhere that
references an AWS Private C
C. Create an IAM user that has an access key and a secret key for all devices. Attach the AmazonElasticFileSystemClientReadWriteAccess
policy to the IAM user. Congure the AWS CLI on the on-premises devices to use the IAM user's access key and secret key.
D. Use the amazon-efs-utils package to mount the EFS le system.
E. Use the native Linux NFS client to mount the EFS le system. | 一家公司在其本地数据中心的本地设备上部署应用程序。该公司在数据中心和其AWS账户之间使用AWS Direct Connect连接。在本地设备的初始设置期间和应用程序更新期间，应用程序需要从Amazon Elastic File System (Amazon EFS)文件系统检索配置文件。从本地设备到Amazon EFS的所有流量必须保持私有和加密。本地设备必须遵循AWS访问的最小权限原则。公司的DevOps团队需要能够撤销单个设备的访问权限而不影响其他设备的访问。

 | **选项A：** 创建一个信任IAM Roles Anywhere的IAM角色。将AmazonElasticFileSystemClientReadWriteAccess附加到该角色。为IAM角色创建IAM Roles Anywhere配置文件。在本地设备上配置AWS CLI使用aws_signing_helper命令获取凭证。
- 这个选项使用了IAM Roles Anywhere，这是正确的方向，但描述不完整，缺少证书管理部分。

**选项B：** 在AWS Private Certificate Authority中为每个本地设备生成证书。在IAM Roles Anywhere中创建一个引用AWS Private CA的信任锚点。
- 这个选项描述了正确的架构，使用AWS Private CA为每个设备生成独立证书，通过IAM Roles Anywhere实现临时凭证访问，满足最小权限和单独撤销的要求。

**选项C：** 创建一个具有访问密钥和秘密密钥的IAM用户供所有设备使用。将AmazonElasticFileSystemClientReadWriteAccess策略附加到IAM用户。在本地设备上配置AWS CLI使用IAM用户的访问密钥和秘密密钥。
- 这违反了最小权限原则和单独撤销要求，所有设备共享同一凭证，无法单独管理。

**选项D：** 使用amazon-efs-utils包挂载EFS文件系统。
- 这只是挂载方法，不涉及身份验证和授权机制。

**选项E：** 使用原生Linux NFS客户端挂载EFS文件系统。
- 同样只是挂载方法，且原生NFS客户端不支持加密传输。

 |  |  |  |
| 246 | A DevOps engineer is setting up an Amazon Elastic Container Service (Amazon ECS) blue/green deployment for an application by using AWS
CodeDeploy and AWS CloudFormation. During the deployment window, the application must be highly available and CodeDeploy must shift
10% of trac to a new version of the application every minute until all trac is shifted. | A. Add an AppSpec le with the CodeDeployDefault.ECSLinearl OPercentEveryl Minutes deployment conguration.
B. Add the AWS::CodeDeployBlueGreen transform and the AWS::CodeDeploy::BlueGreen hook parameter with the
CodeDeployDefault.ECSLinear10PercentEvery1Minutes deployment conguration.
C. Add an AppSpec le with the ECSCanary10Percent5Minutes deployment conguration.
D. Add the AWS::CodeDeployBlueGreen transform and the AWS::CodeDepioy::BlueGreen hook parameter with the
ECSCanary10Percent5Minutes deployment conguration. | 一名DevOps工程师正在使用AWS CodeDeploy和AWS CloudFormation为应用程序设置Amazon弹性容器服务(Amazon ECS)蓝/绿部署。在部署窗口期间，应用程序必须保持高可用性，并且CodeDeploy必须每分钟将10%的流量转移到应用程序的新版本，直到所有流量都转移完成。

选项：
A. 添加一个AppSpec文件，使用CodeDeployDefault.ECSLinear10PercentEvery1Minutes部署配置。
B. 添加AWS::CodeDeployBlueGreen转换和AWS::CodeDeploy::BlueGreen钩子参数，使用CodeDeployDefault.ECSLinear10PercentEvery1Minutes部署配置。
C. 添加一个AppSpec文件，使用ECSCanary10Percent5Minutes部署配置。
D. 添加AWS::CodeDeployBlueGreen转换和AWS::CodeDeploy::BlueGreen钩子参数，使用ECSCanary10Percent5Minutes部署配置。

 | **选项A：** 
- 使用AppSpec文件配置部署策略是正确的方法
- CodeDeployDefault.ECSLinear10PercentEvery1Minutes是正确的部署配置名称，符合题目要求（每分钟转移10%流量）
- Linear部署策略会逐步增加流量直到100%，符合题目要求

**选项B：**
- AWS::CodeDeployBlueGreen转换主要用于CloudFormation模板中的蓝/绿部署
- 部署配置名称正确
- 但这种方法更适合通过CloudFormation直接管理部署，而不是通过CodeDeploy服务

**选项C：**
- 使用AppSpec文件是正确的方法
- 但ECSCanary10Percent5Minutes是金丝雀部署策略，只会转移10%流量并保持5分钟，然后需要手动决定是否继续
- 不符合题目要求的"每分钟转移10%直到全部转移完成"

**选项D：**
- 使用CloudFormation转换方法
- 但部署配置是金丝雀策略，不符合题目要求

 |  |  |  |
| 247 | A company uses an organization in AWS Organizations to manage its AWS accounts. The company's DevOps team has developed an AWS
Lambda function that calls the Organizations API to create new AWS accounts.
The Lambda function runs in the organization's management account. The DevOps team needs to move the Lambda function from the
management account to a dedicated AWS account. The DevOps team must ensure that the Lambda function has the ability to create new AWS
accounts only in Organizations before the team deploys the Lambda function to the new account. | A. In the management account, create a new IAM role that has the necessary permission to create new accounts in Organizations. Allow
the role to be assumed by the Lambda execution role in the new AWS account. Update the Lambda function code to assume the role when
the Lambda function creates new AWS accounts. Update the Lambda execution role to ensure that it has permission to assume the new
role.
B. In the management account, turn on delegated administration for Organizations. Create a new delegation policy that grants the new
AWS account permission to create new AWS accounts in Organizations. Ensure that the Lambda execution role has the
organizations:CreateAccount permission.
C. In the management account, create a new IAM role that has the necessary permission to create new accounts in Organizations. Allow
the role to be assumed by the Lambda service principal. Update the Lambda function code to assume the role when the Lambda function
creates new AWS accounts. Update the Lambda execution role to ensure that it has permission to assume the new role.
D. In the management account, enable AWS Control Tower. Turn on delegated administration for AWS Control Tower. Create a resource
policy that allows the new AWS account to create new AWS accounts in AWS Control Tower. Update the Lambda function code to use the
AWS Control Tower API in the new AWS account. Ensure that the Lambda execution role has the controltower:CreateManagedAccount
permission. |  |  |  |  |  |
| 248 | A company has deployed an application in a single AWS Region. The application backend uses Amazon DynamoDB tables and Amazon S3
buckets.
The company wants to deploy the application in a secondary Region. The company must ensure that the data in the DynamoDB tables and the
S3 buckets persists across both Regions. The data must also immediately propagate across Regions. | A. Implement two-way S3 bucket replication between the primary Region's S3 buckets and the secondary Region’s S3 buckets. Convert the
DynamoDB tables into global tables. Set the secondary Region as the additional Region.
B. Implement S3 Batch Operations copy jobs between the primary Region and the secondary Region for all S3 buckets. Convert the
DynamoDB tables into global tables. Set the secondary Region as the additional Region.
C. Implement two-way S3 bucket replication between the primary Region's S3 buckets and the secondary Region's S3 buckets. Enable
DynamoDB streams on the DynamoDB tables in both Regions. In each Region, create an AWS Lambda function that subscribes to the
DynamoDB streams. Congure the Lambda function to copy new records to the DynamoDB tables in the other Region.
D. Implement S3 Batch Operations copy jobs between the primary Region and the secondary Region for all S3 buckets. Enable DynamoDB
streams on the DynamoDB tables in both Regions. In each Region, create an AWS Lambda function that subscribes to the DynamoDB
streams. Congure the Lambda function to copy new records to the DynamoDB tables in the other Region. | 一家公司已在单个AWS区域部署了应用程序。应用程序后端使用Amazon DynamoDB表和Amazon S3存储桶。

该公司希望在辅助区域部署应用程序。公司必须确保DynamoDB表和S3存储桶中的数据在两个区域之间持久化。数据还必须立即在区域之间传播。

 | **选项A：** 在主区域的S3存储桶和辅助区域的S3存储桶之间实施双向S3存储桶复制。将DynamoDB表转换为全局表。将辅助区域设置为附加区域。
- ✅ S3双向复制可以确保数据在两个区域间同步
- ✅ DynamoDB全局表是AWS原生的多区域复制解决方案，提供自动、实时的数据同步
- ✅ 满足"立即传播"的要求
- ✅ 这是AWS推荐的最佳实践

**选项B：** 在主区域和辅助区域之间为所有S3存储桶实施S3批处理操作复制作业。将DynamoDB表转换为全局表。将辅助区域设置为附加区域。
- ❌ S3批处理操作是手动/计划任务，不能提供实时同步
- ✅ DynamoDB全局表部分正确
- ❌ 不满足"立即传播"的要求

**选项C：** 在主区域的S3存储桶和辅助区域的S3存储桶之间实施双向S3存储桶复制。在两个区域的DynamoDB表上启用DynamoDB流。在每个区域创建AWS Lambda函数订阅DynamoDB流。配置Lambda函数将新记录复制到另一个区域的DynamoDB表。
- ✅ S3双向复制正确
- ❌ 使用Lambda和DynamoDB Streams进行跨区域复制是自定义解决方案，复杂且容易出错
- ❌ 不如DynamoDB全局表可靠和高效

**选项D：** 在主区域和辅助区域之间为所有S3存储桶实施S3批处理操作复制作业。在两个区域的DynamoDB表上启用DynamoDB流。在每个区域创建AWS Lambda函数订阅DynamoDB流。配置Lambda函数将新记录复制到另一个区域的DynamoDB表。
- ❌ S3批处理操作不提供实时同步
- ❌ Lambda自定义复制方案复杂且不可靠
- ❌ 完全不满足"立即传播"的要求

 |  |  |  |
| 249 | A company has congured Amazon RDS storage autoscaling for its RDS DB instances. A DevOps team needs to visualize the autoscaling
events on an Amazon CloudWatch dashboard. | A. Create an Amazon EventBridge rule that reacts to RDS storage autoscaling events from RDS events. Create an AWS Lambda function
that publishes a CloudWatch custom metric. Congure the EventBridge rule to invoke the Lambda function. Visualize the custom metric
by using the CloudWatch dashboard.
B. Create a trail by using AWS CloudTrail with management events congured. Congure the trail to send the management events to
Amazon CloudWatch Logs. Create a metric lter in CloudWatch Logs to match the RDS storage autoscaling events. Visualize the metric
lter by using the CloudWatch dashboard.
C. Create an Amazon EventBridge rule that reacts to RDS storage autoscaling events from the RDS events. Create a CloudWatch alarm.
Congure the EventBridge rule to change the status of the CloudWatch alarm. Visualize the alarm status by using the CloudWatch
dashboard.
D. Create a trail by using AWS CloudTrail with data events congured. Congure the trail to send the data events to Amazon CloudWatch
Logs. Create a metric lter in CloudWatch Logs to match the RDS storage autoscaling events. Visualize the metric lter by using the
CloudWatch dashboard. | 一家公司已经为其RDS数据库实例配置了Amazon RDS存储自动扩展功能。DevOps团队需要在Amazon CloudWatch仪表板上可视化自动扩展事件。

 | **选项A：** 创建一个Amazon EventBridge规则来响应来自RDS事件的RDS存储自动扩展事件。创建一个AWS Lambda函数来发布CloudWatch自定义指标。配置EventBridge规则来调用Lambda函数。使用CloudWatch仪表板可视化自定义指标。

- **正确性：高** - RDS存储自动扩展事件会发布到RDS事件流中，EventBridge可以捕获这些事件。通过Lambda函数创建自定义指标是一个有效的可视化方法。

**选项B：** 使用AWS CloudTrail创建一个配置了管理事件的跟踪。配置跟踪将管理事件发送到Amazon CloudWatch Logs。在CloudWatch Logs中创建指标过滤器来匹配RDS存储自动扩展事件。使用CloudWatch仪表板可视化指标过滤器。

- **正确性：低** - RDS存储自动扩展事件不是CloudTrail管理事件。CloudTrail主要记录API调用，而自动扩展是RDS服务内部的自动化操作，不会作为管理事件记录在CloudTrail中。

**选项C：** 创建一个Amazon EventBridge规则来响应来自RDS事件的RDS存储自动扩展事件。创建一个CloudWatch告警。配置EventBridge规则来改变CloudWatch告警的状态。使用CloudWatch仪表板可视化告警状态。

- **正确性：中等** - 虽然技术上可行，但使用告警状态来可视化事件不是最佳实践。告警主要用于监控和通知，而不是用作事件可视化的主要方法。

**选项D：** 使用AWS CloudTrail创建一个配置了数据事件的跟踪。配置跟踪将数据事件发送到Amazon CloudWatch Logs。在CloudWatch Logs中创建指标过滤器来匹配RDS存储自动扩展事件。使用CloudWatch仪表板可视化指标过滤器。

- **正确性：低** - RDS存储自动扩展事件也不是CloudTrail数据事件。数据事件主要记录对象级别的操作（如S3对象访问），不包括RDS自动扩展事件。

 |  |  |  |
| 250 | A company uses containers for its applications. The company learns that some container images are missing required security congurations.
A DevOps engineer needs to implement a solution to create a standard base image. The solution must publish the base image weekly to the
us-west-2 Region, us-east-2 Region, and eu-central-1 Region. | A. Create an EC2 Image Builder pipeline that uses a container recipe to build the image. Congure the pipeline to distribute the image to
an Amazon Elastic Container Registry (Amazon ECR) repository in us-west-2. Congure ECR replication from us-west-2 to us-east-2 and
from us-east-2 to eu-central-1. Congure the pipeline to run weekly.
B. Create an AWS CodePipeline pipeline that uses an AWS CodeBuild project to build the image. Use AWS CodeDeploy to publish the
image to an Amazon Elastic Container Registry (Amazon ECR) repository in us-west-2. Congure ECR replication from us-west-2 to us-east-
2 and from us-east-2 to eu-central-1. Congure the pipeline to run weekly.
C. Create an EC2 Image Builder pipeline that uses a container recipe to build the image. Congure the pipeline to distribute the image to
Amazon Elastic Container Registry (Amazon ECR) repositories in all three Regions. Congure the pipeline to run weekly.
D. Create an AWS CodePipeline pipeline that uses an AWS CodeBuild project to build the image. Use AWS CodeDeploy to publish the
image to Amazon Elastic Container Registry (Amazon ECR) repositories in all three Regions. Congure the pipeline to run weekly. |  |  |  |  |  |
| 251 | A DevOps engineer needs to implement a solution to install antivirus software on all the Amazon EC2 instances in an AWS account. The EC2
instances run the most recent version of Amazon Linux.
The solution must detect all instances and must use an AWS Systems Manager document to install the software if the software is not present. | A. Create an association in Systems Manager State Manager. Target all the managed nodes. Include the software in the association.
Congure the association to use the Systems Manager document.
B. Set up AWS Cong to record all the resources in the account. Create an AWS Cong custom rule to determine if the software is installed
on all the EC2 instances. Congure an automatic remediation action that uses the Systems Manager document for noncompliant EC2
instances.
C. Activate Amazon EC2 scanning on Amazon Inspector to determine if the software is installed on all the EC2 instances. Associate the
ndings with the Systems Manager document.
D. Create an Amazon EventBridge rule that uses AWS CloudTrail to detect the Runinstances API call. Congure inventory collection in
Systems Manager Inventory to determine if the software is installed on the EC2 instances. Associate the Systems Manager inventory with
the Systems Manager document. | 一名DevOps工程师需要实施一个解决方案，在AWS账户中的所有Amazon EC2实例上安装防病毒软件。这些EC2实例运行最新版本的Amazon Linux。

该解决方案必须能够检测所有实例，并且必须使用AWS Systems Manager文档来安装软件（如果软件尚未安装）。

 | **选项A：在Systems Manager State Manager中创建关联。目标为所有托管节点。在关联中包含软件。配置关联使用Systems Manager文档。**
- 这是正确的方法。State Manager专门用于维护EC2实例的期望状态
- 可以自动检测所有托管节点并确保软件始终安装
- 如果软件被卸载，State Manager会自动重新安装
- 直接使用Systems Manager文档执行安装任务

**选项B：设置AWS Config记录账户中的所有资源。创建AWS Config自定义规则来确定软件是否安装在所有EC2实例上。为不合规的EC2实例配置使用Systems Manager文档的自动修复操作。**
- 技术上可行，但过于复杂
- 需要创建自定义Config规则来检测软件安装状态
- 增加了不必要的复杂性和成本
- 不是最直接的解决方案

**选项C：在Amazon Inspector上激活Amazon EC2扫描，以确定软件是否安装在所有EC2实例上。将发现结果与Systems Manager文档关联。**
- Inspector主要用于安全漏洞评估，不是用于软件安装管理
- 无法直接与Systems Manager文档关联进行自动修复
- 不适合这个用例

**选项D：创建Amazon EventBridge规则，使用AWS CloudTrail检测RunInstances API调用。在Systems Manager Inventory中配置库存收集，以确定软件是否安装在EC2实例上。将Systems Manager库存与Systems Manager文档关联。**
- 过于复杂，涉及多个不必要的服务
- EventBridge + CloudTrail只能检测新实例创建，无法管理现有实例
- Inventory可以收集信息但不能直接触发修复操作
- 无法实现自动化的持续合规性

 |  |  |  |
| 252 | A company needs to increase the security of the container images that run in its production environment. The company wants to integrate
operating system scanning and programming language package vulnerability scanning for the containers in its CI/CD pipeline. The CI/CD
pipeline is an AWS CodePipeline pipeline that includes an AWS CodeBuild build project, AWS CodeDeploy actions, and an Amazon Elastic
Container Registry (Amazon ECR) repository.
A DevOps engineer needs to add an image scan to the CI/CD pipeline. The CI/CD pipeline must deploy only images without CRITICAL and
HIGH ndings into production. | A. Use Amazon ECR basic scanning.
B. Use Amazon ECR enhanced scanning.
C. Congure Amazon ECR to submit a Rejected status to the CI/CD pipeline when the image scan returns CRITICAL or HIGH ndings.
D. Congure an Amazon EventBridge rule to invoke an AWS Lambda function when the image scan is completed. Congure the Lambda
function to consume the Amazon Inspector scan status and to submit an Approved or Rejected status to the CI/CD pipeline.
E. Congure an Amazon EventBridge rule to invoke an AWS Lambda function when the image scan is completed. Congure the Lambda
function to consume the Clair scan status and to submit an Approved or Rejected status to the CI/CD pipeline. | 一家公司需要提高在其生产环境中运行的容器镜像的安全性。该公司希望在其CI/CD管道中集成操作系统扫描和编程语言包漏洞扫描功能。该CI/CD管道是一个AWS CodePipeline管道，包括AWS CodeBuild构建项目、AWS CodeDeploy操作和Amazon弹性容器注册表(Amazon ECR)存储库。

DevOps工程师需要向CI/CD管道添加镜像扫描功能。CI/CD管道必须仅将没有CRITICAL(严重)和HIGH(高危)发现的镜像部署到生产环境。

 | **A. 使用Amazon ECR基础扫描**
- ECR基础扫描只提供操作系统级别的漏洞扫描
- 不包括编程语言包的漏洞扫描
- 不满足题目要求的完整扫描需求

**B. 使用Amazon ECR增强扫描**
- ECR增强扫描基于Amazon Inspector v2
- 提供操作系统和编程语言包的漏洞扫描
- 满足题目的扫描需求，但单独使用无法自动阻止部署

**C. 配置Amazon ECR在镜像扫描返回CRITICAL或HIGH发现时向CI/CD管道提交拒绝状态**
- ECR本身不具备直接向CodePipeline提交状态的功能
- 这不是ECR的原生功能
- 技术上不可行

**D. 配置Amazon EventBridge规则在镜像扫描完成时调用AWS Lambda函数。配置Lambda函数消费Amazon Inspector扫描状态并向CI/CD管道提交批准或拒绝状态**
- EventBridge可以监听ECR扫描完成事件
- Lambda可以处理Amazon Inspector的扫描结果
- 可以根据扫描结果向CodePipeline提交状态
- 技术上可行且符合AWS最佳实践

**E. 配置Amazon EventBridge规则在镜像扫描完成时调用AWS Lambda函数。配置Lambda函数消费Clair扫描状态并向CI/CD管道提交批准或拒绝状态**
- Clair不是ECR增强扫描使用的扫描引擎
- ECR增强扫描使用Amazon Inspector，不是Clair
- 技术细节错误

 |  |  |  |
| 253 | A company's DevOps team manages a set of AWS accounts that are in an organization in AWS Organizations.
The company needs a solution that ensures that all Amazon EC2 instances use approved AM Is that the DevOps team manages. The solution
also must remediate the usage of AMIs that are not approved. The individual account administrators must not be able to remove the
restriction to use approved AMIs. | A. Use AWS CloudFormation StackSets to deploy an Amazon EventBridge rule to each account. Congure the rule to react to AWS
CloudTrail events for Amazon EC2 and to send a notication to an Amazon Simple Notication Service (Amazon SNS) topic. Subscribe the
DevOps team to the SNS topic.
B. Use AWS CloudFormation StackSets to deploy the approved-amis-by-id AWS Cong managed rule to each account. Congure the rule
with the list of approved AMIs. Congure the rule to run the AWS-StopEC2Instance AWS Systems Manager Automation runbook for the
noncompliant EC2 instances.
C. Create an AWS Lambda function that processes AWS CloudTrail events for Amazon EC2. Congure the Lambda function to send a
notication to an Amazon Simple Notication Service (Amazon SNS) topic. Subscribe the DevOps team to the SNS topic. Deploy the
Lambda function in each account in the organization. Create an Amazon EventBridge rule in each account. Congure the EventBridge
rules to react to AWS CloudTrail events for Amazon EC2 and to invoke the Lambda function.
D. Enable AWS Cong across the organization. Create a conformance pack that uses the approved-amis-by-id AWS Cong managed rule
with the list of approved AMIs. Deploy the conformance pack across the organization. Congure the rule to run the AWS-StopEC2lnstance
AWS Systems Manager Automation runbook for the noncompliant EC2 instances. |  |  |  |  |  |
| 254 | A company gives its employees limited rights to AWS. DevOps engineers have the ability to assume an administrator role. For tracking
purposes, the security team wants to receive a near-real-time notication when the administrator role is assumed.
How should this be accomplished? | A. Congure AWS Cong to publish logs to an Amazon S3 bucket. Use Amazon Athena to query the logs and send a notication to the
security team when the administrator role is assumed.
B. Congure Amazon GuardDuty to monitor when the administrator role is assumed and send a notication to the security team.
C. Create an Amazon EventBridge event rule using an AWS Management Console sign-in events event pattern that publishes a message to
an Amazon SNS topic if the administrator role is assumed.
D. Create an Amazon EventBridge events rule using an AWS API call that uses an AWS CloudTrail event pattern to invoke an AWS Lambda
function that publishes a message to an Amazon SNS topic if the administrator role is assumed. | 一家公司给员工有限的AWS权限。DevOps工程师有能力承担管理员角色。出于跟踪目的，安全团队希望在管理员角色被承担时收到近实时通知。

应该如何实现这一点？

 | **选项A：配置AWS Config将日志发布到Amazon S3存储桶。使用Amazon Athena查询日志，当管理员角色被承担时向安全团队发送通知。**
- 不正确。AWS Config主要用于配置合规性监控，不是用于实时监控角色承担事件的最佳选择
- Athena是用于批量查询分析的服务，无法提供近实时通知
- 这种方案延迟较高，不符合"近实时"的要求

**选项B：配置Amazon GuardDuty监控管理员角色被承担的情况，并向安全团队发送通知。**
- 不正确。GuardDuty主要用于威胁检测和异常行为识别
- 虽然GuardDuty可能会检测到异常的角色承担行为，但它不是专门用于监控正常的角色承担事件
- 不是针对此需求的最直接解决方案

**选项C：使用AWS管理控制台登录事件的事件模式创建Amazon EventBridge事件规则，如果管理员角色被承担，则向Amazon SNS主题发布消息。**
- 不正确。这个选项只监控管理控制台登录事件
- 角色承担(AssumeRole)可能通过API调用发生，不一定涉及控制台登录
- 事件模式不够全面，可能遗漏通过编程方式的角色承担

**选项D：使用AWS API调用创建Amazon EventBridge事件规则，该规则使用AWS CloudTrail事件模式调用AWS Lambda函数，如果管理员角色被承担，则向Amazon SNS主题发布消息。**
- 正确。CloudTrail记录所有AWS API调用，包括AssumeRole事件
- EventBridge可以基于CloudTrail事件创建规则，实现近实时监控
- Lambda函数可以处理事件并通过SNS发送通知
- 这是一个完整的、实时的监控解决方案

 |  |  |  |
| 255 | A company needs a strategy for failover and disaster recovery of its data and application. The application uses a MySQL database and
Amazon EC2 instances. The company requires a maximum RPO of 2 hours and a maximum RTO of 10 minutes for its data and application at
all times. | A. Create an Amazon Aurora Single-AZ cluster in multiple AWS Regions as the data store. Use Aurora's automatic recovery capabilities in
the event of a disaster.
B. Create an Amazon Aurora global database in two AWS Regions as the data store. In the event of a failure, promote the secondary
Region to the primary for the application. Update the application to use the Aurora cluster endpoint in the secondary Region.
C. Create an Amazon Aurora cluster in multiple AWS Regions as the data store. Use a Network Load Balancer to balance the database
trac in different Regions.
D. Set up the application in two AWS Regions. Use Amazon Route 53 failover routing that points to Application Load Balancers in both
Regions. Use health checks and Auto Scaling groups in each Region.
E. Set up the application in two AWS Regions. Congure AWS Global Accelerator to point to Application Load Balancers (ALBs) in both
Regions. Add both ALBs to a single endpoint group. Use health checks and Auto Scaling groups in each Region. | 一家公司需要制定其数据和应用程序的故障转移和灾难恢复策略。该应用程序使用MySQL数据库和Amazon EC2实例。公司要求其数据和应用程序在任何时候的最大RPO为2小时，最大RTO为10分钟。

 | **选项A：** 在多个AWS区域创建Amazon Aurora Single-AZ集群作为数据存储。在发生灾难时使用Aurora的自动恢复功能。
- **问题：** Single-AZ集群不提供跨区域的灾难恢复能力，无法满足灾难恢复要求
- **缺陷：** 只解决了数据库层面，没有涉及应用程序的故障转移策略

**选项B：** 在两个AWS区域创建Amazon Aurora全球数据库作为数据存储。在发生故障时，将辅助区域提升为应用程序的主区域。更新应用程序以使用辅助区域中的Aurora集群端点。
- **优点：** Aurora全球数据库提供跨区域复制，RPO通常在1秒内
- **缺陷：** 只涉及数据库层面的灾难恢复，没有完整的应用程序故障转移解决方案

**选项C：** 在多个AWS区域创建Amazon Aurora集群作为数据存储。使用网络负载均衡器来平衡不同区域的数据库流量。
- **问题：** 数据库不应该使用负载均衡器进行跨区域流量分配，这会导致数据一致性问题
- **缺陷：** 架构设计不合理，没有考虑应用程序层面的故障转移

**选项D：** 在两个AWS区域设置应用程序。使用Amazon Route 53故障转移路由，指向两个区域的应用程序负载均衡器。在每个区域使用健康检查和Auto Scaling组。
- **优点：** 提供完整的应用程序层故障转移解决方案
- **缺陷：** 没有明确说明数据库的灾难恢复策略

**选项E：** 在两个AWS区域设置应用程序。配置AWS Global Accelerator指向两个区域的应用程序负载均衡器。将两个ALB添加到单个端点组中。在每个区域使用健康检查和Auto Scaling组。
- **优点：** 提供应用程序层的高可用性和故障转移
- **缺陷：** 同样没有涉及数据库层面的灾难恢复策略

 |  |  |  |
| 256 | A developer is using the AWS Serverless Application Model (AWS SAM) to create a prototype for an AWS Lambda function. The AWS SAM
template contains an AWS::Serverless::Function resource that has the CodeUri property that points to an Amazon S3 location. The developer
wants to identify the correct commands for deployment before creating a CI/CD pipeline.
The developer creates an archive of the Lambda function code named package.zip. The developer uploads the .zip le archive to the S3
location specied in the CodeUri property. The developer runs the sam deploy command and deploys the Lambda function. The developer
updates the Lambda function code and uses the same steps to deploy the new version of the Lambda function. The sam deploy command
fails and returns an error of no changes to deploy. | A. Use the aws cloudformation update-stack command instead of the sam deploy command.
B. Use the aws cloudformation update-stack-instances command instead of the sam deploy command.
C. Update the CodeUri property to reference the local application code folder. Use the sam deploy command.
D. Update the CodeUri property to reference the local application code folder. Use the aws cloudformation create-change-set command
and the aws cloudformation execute-change-set command.
E. Update the CodeUri property to reference the local application code folder. Use the aws cloudformation package command and the aws
cloudformation deploy command. | 一个开发者正在使用AWS无服务器应用程序模型(AWS SAM)为AWS Lambda函数创建原型。AWS SAM模板包含一个AWS::Serverless::Function资源，该资源的CodeUri属性指向Amazon S3位置。开发者想要在创建CI/CD流水线之前确定正确的部署命令。

开发者创建了一个名为package.zip的Lambda函数代码归档文件。开发者将.zip文件归档上传到CodeUri属性中指定的S3位置。开发者运行sam deploy命令并部署Lambda函数。开发者更新Lambda函数代码并使用相同的步骤部署新版本的Lambda函数。sam deploy命令失败并返回"no changes to deploy"错误。

 | **A. 使用aws cloudformation update-stack命令替代sam deploy命令**
- 不正确。这不会解决根本问题。CloudFormation无法检测到S3中代码的变化，因为模板本身没有改变，只是S3中的文件内容变了。

**B. 使用aws cloudformation update-stack-instances命令替代sam deploy命令**
- 不正确。这个命令用于StackSets，与当前场景无关。

**C. 更新CodeUri属性以引用本地应用程序代码文件夹。使用sam deploy命令**
- 部分正确但不完整。虽然指向本地代码是正确的方向，但缺少了sam build步骤，这是SAM工作流程的重要组成部分。

**D. 更新CodeUri属性以引用本地应用程序代码文件夹。使用aws cloudformation create-change-set命令和aws cloudformation execute-change-set命令**
- 不正确。这些是原生CloudFormation命令，不适用于SAM应用程序的部署。SAM需要先进行构建和打包过程。

**E. 更新CodeUri属性以引用本地应用程序代码文件夹。使用aws cloudformation package命令和aws cloudformation deploy命令**
- 正确。这是传统的CloudFormation方式处理SAM模板的正确方法。`aws cloudformation package`会处理本地代码的打包和上传，然后`aws cloudformation deploy`进行部署。

 |  |  |  |
| 257 | A company runs its container workloads in AWS App Runner. A DevOps engineer manages the company's container repository in Amazon
Elastic Container Registry (Amazon ECR).
The DevOps engineer must implement a solution that continuously monitors the container repository. The solution must create a new
container image when the solution detects an operating system vulnerability or language package vulnerability. | A. Use EC2 Image Builder to create a container image pipeline. Use Amazon ECR as the target repository. Turn on enhanced scanning on
the ECR repository. Create an Amazon EventBridge rule to capture an Inspector? nding event. Use the event to invoke the image pipeline.
Re-upload the container to the repository.
B. Use EC2 Image Builder to create a container image pipeline. Use Amazon ECR as the target repository. Enable Amazon GuardDuty
Malware Protection on the container workload. Create an Amazon EventBridge rule to capture a GuardDuty nding event. Use the event to
invoke the image pipeline.
C. Create an AWS CodeBuild project to create a container image. Use Amazon ECR as the target repository. Turn on basic scanning on the
repository. Create an Amazon EventBridge rule to capture an ECR image action event. Use the event to invoke the CodeBuild project. Re-
upload the container to the repository.
D. Create an AWS CodeBuild project to create a container image. Use Amazon ECR as the target repository. Congure AWS Systems
Manager Compliance to scan all managed nodes. Create an Amazon EventBridge rule to capture a conguration compliance state change
event. Use the event to invoke the CodeBuild project. | 一家公司在AWS App Runner中运行其容器工作负载。DevOps工程师管理公司在Amazon弹性容器注册表(Amazon ECR)中的容器仓库。

DevOps工程师必须实施一个解决方案，持续监控容器仓库。当解决方案检测到操作系统漏洞或语言包漏洞时，必须创建一个新的容器镜像。

 | **选项A：** 使用EC2 Image Builder创建容器镜像管道。使用Amazon ECR作为目标仓库。在ECR仓库上启用增强扫描。创建Amazon EventBridge规则来捕获Inspector发现事件。使用该事件调用镜像管道。重新上传容器到仓库。

- ✅ **正确**：ECR增强扫描使用Amazon Inspector来检测操作系统和语言包漏洞
- ✅ **正确**：Inspector发现漏洞时会生成EventBridge事件
- ✅ **正确**：EC2 Image Builder可以构建容器镜像
- ✅ **正确**：完整的自动化流程符合要求

**选项B：** 使用EC2 Image Builder创建容器镜像管道。使用Amazon ECR作为目标仓库。在容器工作负载上启用Amazon GuardDuty恶意软件保护。创建Amazon EventBridge规则来捕获GuardDuty发现事件。使用该事件调用镜像管道。

- ❌ **错误**：GuardDuty恶意软件保护主要检测恶意软件，不是专门用于检测操作系统或语言包漏洞
- ❌ **错误**：不符合题目要求的漏洞检测需求

**选项C：** 创建AWS CodeBuild项目来创建容器镜像。使用Amazon ECR作为目标仓库。在仓库上启用基础扫描。创建Amazon EventBridge规则来捕获ECR镜像操作事件。使用该事件调用CodeBuild项目。重新上传容器到仓库。

- ❌ **错误**：基础扫描功能有限，不如增强扫描全面
- ❌ **错误**：ECR镜像操作事件不是漏洞发现事件，无法触发基于漏洞的自动修复

**选项D：** 创建AWS CodeBuild项目来创建容器镜像。使用Amazon ECR作为目标仓库。配置AWS Systems Manager Compliance来扫描所有托管节点。创建Amazon EventBridge规则来捕获配置合规状态变更事件。使用该事件调用CodeBuild项目。

- ❌ **错误**：Systems Manager Compliance主要用于EC2实例合规性检查，不适用于容器镜像漏洞扫描
- ❌ **错误**：不符合容器镜像漏洞检测的需求

 |  |  |  |
| 258 | A company wants to use AWS Systems Manager documents to bootstrap physical laptops for developers. The bootstrap code is stored in
GitHub. A DevOps engineer has already created a Systems Manager activation, installed the Systems Manager agent with the registration
code, and installed an activation ID on all the laptops. | A. Congure the Systems Manager document to use the AWS-RunShellScript command to copy the les from GitHub to Amazon S3, then
use the aws-downloadContent plugin with a sourceType of S3.
B. Congure the Systems Manager document to use the aws-congurePackage plugin with an install action and point to the Git repository.
C. Congure the Systems Manager document to use the aws-downloadContent plugin with a sourceType of GitHub and sourceInfo with the
repository details.
D. Congure the Systems Manager document to use the aws:softwareInventory plugin and run the script from the Git repository. | 一家公司想要使用AWS Systems Manager文档来引导开发人员的物理笔记本电脑。引导代码存储在GitHub中。DevOps工程师已经创建了Systems Manager激活，在所有笔记本电脑上安装了带有注册代码的Systems Manager代理，并安装了激活ID。

 | **选项A：** 配置Systems Manager文档使用AWS-RunShellScript命令从GitHub复制文件到Amazon S3，然后使用aws-downloadContent插件，sourceType为S3。
- 这种方法过于复杂，需要额外的S3存储步骤
- 虽然技术上可行，但不是最直接的解决方案
- 增加了不必要的中间步骤和成本

**选项B：** 配置Systems Manager文档使用aws-configurePackage插件，执行安装操作并指向Git仓库。
- aws-configurePackage插件主要用于管理预打包的软件包
- 不直接支持从Git仓库下载和执行代码
- 这个插件更适合处理已经打包好的应用程序

**选项C：** 配置Systems Manager文档使用aws-downloadContent插件，sourceType为GitHub，sourceInfo包含仓库详细信息。
- aws-downloadContent插件专门设计用于从各种源下载内容
- 直接支持GitHub作为源类型
- 可以通过sourceInfo参数指定具体的仓库信息
- 这是最直接和高效的方法

**选项D：** 配置Systems Manager文档使用aws:softwareInventory插件并从Git仓库运行脚本。
- aws:softwareInventory插件主要用于收集软件清单信息
- 不是用于下载和执行代码的插件
- 功能不匹配题目需求

 |  |  |  |
| 259 | A company's development team uses AWS CloudFormation to deploy its application resources. The team must use CloudFormation for all
changes to the environment. The team cannot use the AWS Management Console or the AWS CLI to make manual changes directly.
The team uses a developer IAM role to access the environment. The role is congured with the AdministratorAccess managed IAM policy. The
company has created a new CloudFormationDeployment IAM role that has the following policy attached:
The company wants to ensure that only CloudFormation can use the new role. The development team cannot make any manual changes to
the deployed resources. | A. Remove the AdministratorAccess policy. Assign the ReadOnlyAccess managed IAM policy to the developer role. Instruct the developers
to use the CloudFormationDeployment role as a CloudFormation service role when the developers deploy new stacks.
B. Update the trust policy of the CloudFormationDeployment role to allow the developer IAM role to assume the
CloudFormationDeployment role.
C. Congure the developer IAM role to be able to get and pass the CloudFormationDeployment role if iam:PassedToService equals .
Congure the CloudFormationDeployment role to allow all cloudformation actions for all resources.
D. Update the trust policy of the CloudFormationDeployment role to allow the cloudformation.amazonaws.com AWS principal to perform
the iam:AssumeRole action.
E. Remove the AdministratorAccess policy. Assign the ReadOnlyAccess managed IAM policy to the developer role. Instruct the developers
to assume the CloudFormationDeployment role when the developers deploy new stacks.
F. Add an IAM policy to the CloudFormationDeployment role to allow cloudformation:* on all resources. Add a policy that allows the
iam:PassRole action for the ARN of the CloudFormationDeployment role if iam:PassedToService equals cloudformation.amazonaws.com. |  |  |  |  |  |
| 260 | A company is developing a web application's infrastructure using AWS CloudFormation. The database engineering team maintains the
database resources in a CloudFormation template, and the software development team maintains the web application resources in a separate
CloudFormation template. As the scope of the application grows, the software development team needs to use resources maintained by the
database engineering team. However, both teams have their own review and lifecycle management processes that they want to keep. Both
teams also require resource-level change-set reviews. The software development team would like to deploy changes to this template using
their CI/CD pipeline. | A. Create a stack export from the database CloudFormation template and import those references into the web application
CloudFormation template.
B. Create a CloudFormation nested stack to make cross-stack resource references and parameters available in both stacks.
C. Create a CloudFormation stack set to make cross-stack resource references and parameters available in both stacks.
D. Create input parameters in the web application CloudFormation template and pass resource names and IDs from the database stack. | 一家公司正在使用AWS CloudFormation开发Web应用程序的基础设施。数据库工程团队在一个CloudFormation模板中维护数据库资源，软件开发团队在另一个独立的CloudFormation模板中维护Web应用程序资源。随着应用程序范围的扩大，软件开发团队需要使用数据库工程团队维护的资源。然而，两个团队都有各自的审查和生命周期管理流程，他们希望保持这些流程。两个团队还都需要资源级别的变更集审查。软件开发团队希望使用他们的CI/CD管道来部署对此模板的更改。

 | **选项A：从数据库CloudFormation模板创建堆栈导出，并将这些引用导入到Web应用程序CloudFormation模板中。**
- 这是正确的方法。使用CloudFormation的Export/Import功能可以实现跨堆栈资源共享
- 数据库团队可以在其模板中使用Outputs和Export导出资源
- 软件开发团队可以使用ImportValue函数引用这些导出的资源
- 保持了两个团队独立的生命周期管理和审查流程
- 支持CI/CD管道部署

**选项B：创建CloudFormation嵌套堆栈，使跨堆栈资源引用和参数在两个堆栈中都可用。**
- 嵌套堆栈需要一个父堆栈来管理子堆栈
- 这会破坏两个团队独立的审查和生命周期管理流程
- 不符合题目要求的保持独立管理的需求

**选项C：创建CloudFormation堆栈集，使跨堆栈资源引用和参数在两个堆栈中都可用。**
- 堆栈集主要用于跨多个账户和区域部署相同的堆栈
- 不是用于解决跨堆栈资源引用的问题
- 不适合这个场景

**选项D：在Web应用程序CloudFormation模板中创建输入参数，并从数据库堆栈传递资源名称和ID。**
- 这种方法需要手动传递参数值
- 增加了操作复杂性和出错可能性
- 不如Export/Import方法自动化程度高
- 虽然可行，但不是最佳实践

 |  |  |  |
| 261 | A company has an organization in AWS Organizations. A DevOps engineer needs to maintain multiple AWS accounts that belong to different
OUs in the organization. All resources, including IAM policies and Amazon S3 policies within an account, are deployed through AWS
CloudFormation. All templates and code are maintained in an AWS CodeCommit repository. Recently, some developers have not been able to
access an S3 bucket from some accounts in the organization.
The following policy is attached to the S3 bucket: | A. Modify the S3 bucket policy. Turn off the S3 Block Public Access setting on the S3 bucket. In the S3 policy, add the aws:SourceAccount
condition. Add the AWS account IDs of all developers who are experiencing the issue.
B. Verify that no IAM permissions boundaries are denying developers access to the S3 bucket. Make the necessary changes to IAM
permissions boundaries. Use an AWS Cong recorder in the individual developer accounts that are experiencing the issue to revert any
changes that are blocking access. Commit the x back into the CodeCommit repository. Invoke deployment through CloudFormation to
apply the changes.
C. Congure an SCP that stops anyone from modifying IAM resources in developer OUs. In the S3 policy, add the aws:SourceAccount
condition. Add the AWS account IDs of all developers who are experiencing the issue. Commit the x back into the CodeCommit repository.
Invoke deployment through CloudFormation to apply the changes.
D. Ensure that no SCP is blocking access for developers to the S3 bucket. Ensure that no IAM policy permissions boundaries are denying
access to developer IAM users. Make the necessary changes to the SCP and IAM policy permissions boundaries in the CodeCommit
repository. Invoke deployment through CloudFormation to apply the changes. | 一家公司在AWS Organizations中有一个组织。DevOps工程师需要维护属于组织中不同OU（组织单元）的多个AWS账户。账户内的所有资源，包括IAM策略和Amazon S3策略，都通过AWS CloudFormation部署。所有模板和代码都维护在AWS CodeCommit存储库中。最近，一些开发人员无法从组织中的某些账户访问S3存储桶。

以下策略附加到S3存储桶上：（注：题目中似乎缺少了具体的策略内容）

 | **选项A：** 修改S3存储桶策略。关闭S3存储桶上的S3 Block Public Access设置。在S3策略中，添加aws:SourceAccount条件。添加所有遇到问题的开发人员的AWS账户ID。
- **问题：** 关闭Block Public Access设置会带来安全风险，这不是解决内部访问问题的正确方法。这个方案没有遵循最小权限原则。

**选项B：** 验证没有IAM权限边界拒绝开发人员访问S3存储桶。对IAM权限边界进行必要更改。在遇到问题的个别开发人员账户中使用AWS Config记录器来恢复任何阻止访问的更改。将修复提交回CodeCommit存储库。通过CloudFormation调用部署以应用更改。
- **问题：** 这个方案过于复杂，且使用Config记录器来"恢复更改"的方法不正确。Config记录器用于监控配置变化，不是用来恢复访问权限的工具。

**选项C：** 配置一个SCP（服务控制策略），阻止任何人修改开发人员OU中的IAM资源。在S3策略中，添加aws:SourceAccount条件。添加所有遇到问题的开发人员的AWS账户ID。将修复提交回CodeCommit存储库。通过CloudFormation调用部署以应用更改。
- **问题：** 虽然SCP可以防止未来的修改，但这不能解决当前的访问问题。重点应该是识别和解决现有的访问限制。

**选项D：** 确保没有SCP阻止开发人员访问S3存储桶。确保没有IAM策略权限边界拒绝开发人员IAM用户的访问。在CodeCommit存储库中对SCP和IAM策略权限边界进行必要更改。通过CloudFormation调用部署以应用更改。
- **优点：** 这个方案系统性地检查了可能阻止访问的两个主要层面：组织级别的SCP和账户级别的IAM权限边界。然后通过既定的CI/CD流程进行修复。

 | D |  |  |
| 262 | A company has an organization in AWS Organizations for its multi-account environment. A DevOps engineer is developing an AWS
CodeArtifact based strategy for application package management across the organization. Each application team at the company has its own
account in the organization. Each application team also has limited access to a centralized shared services account.
Each application team needs full access to download, publish, and grant access to its own packages. Some common library packages that the
application teams use must also be shared with the entire organization. | A. Create a domain in each application team's account. Grant each application team's account full read access and write access to the
application team's domain.
B. Create a domain in the shared services account. Grant the organization read access and CreateRepository access.
C. Create a repository in each application team’s account. Grant each application team’s account full read access and write access to its
own repository.
D. Create a repository in the shared services account. Grant the organization read access to the repository in the shared services account
Set the repository as the upstream repository in each application team's repository.
E. For teams that require shared packages, create resource-based policies that allow read access to the repository from other application
teams' accounts.
F. Set the other application teams' repositories as upstream repositories. |  |  |  |  |  |
| 263 | A company deploys an application to Amazon EC2 instances. The application runs Amazon Linux 2 and uses AWS CodeDeploy. The application
has the following le structure for its code repository:
The appspec.yml le has the following contents in the les section: | A. The cong.txt le will be deployed to only /var/www/html/cong/cong.txt.
B. The cong.txt le will be deployed to /usr/local/src/cong.txt and to /var/www/html/cong/cong.txt.
C. The cong.txt le will be deployed to only /usr/local/src/cong.txt.
D. The cong.txt le will be deployed to /usr/local/src/cong.txt and to /var/www/html/application/web/cong.txt. | 一家公司将应用程序部署到Amazon EC2实例上。该应用程序运行Amazon Linux 2并使用AWS CodeDeploy。应用程序的代码仓库具有以下文件结构：
appspec.yml文件在files部分包含以下内容：

[注：题目中似乎缺少了关键的文件结构图和appspec.yml的具体内容，这些信息对于回答问题至关重要]

2. | 由于题目中缺少了appspec.yml文件的具体内容和文件结构，我无法看到完整的配置信息。但基于AWS CodeDeploy的工作原理，我可以分析各选项的可能性：

A. config.txt文件将仅部署到/var/www/html/config/config.txt
- 这表示只有一个目标位置的部署

B. config.txt文件将部署到/usr/local/src/config.txt和/var/www/html/config/config.txt
- 这表示同一个文件被部署到两个不同的目标位置

C. config.txt文件将仅部署到/usr/local/src/config.txt
- 这表示只部署到一个目标位置

D. config.txt文件将部署到/usr/local/src/config.txt和/var/www/html/application/web/config.txt
- 这也表示部署到两个不同的目标位置

3. |  |  |  |
| 264 | A company has set up AWS CodeArtifact repositories with public upstream repositories. The company's development team consumes open
source dependencies from the repositories in the company's internal network.
The company's security team recently discovered a critical vulnerability in the most recent version of a package that the development team
consumes. The security team has produced a patched version to x the vulnerability. The company needs to prevent the vulnerable version
from being downloaded. The company also needs to allow the security team to publish the patched version. | A. Update the status of the affected CodeArtifact package version to unlisted.
B. Update the status of the affected CodeArtifact package version to deleted.
C. Update the status of the affected CodeArtifact package version to archived.
D. Update the CodeArtifact package origin control settings to allow direct publishing and to block upstream operations.
E. Update the CodeArtifact package origin control settings to block direct publishing and to allow upstream operations. |  |  |  |  |  |
| 265 | A company is running a custom-built application that processes records. All the components run on Amazon EC2 instances that run in an Auto
Scaling group. Each record's processing is a multistep sequential action that is compute-intensive. Each step is always completed in 5
minutes or less.
A limitation of the current system is that if any steps fail, the application has to reprocess the record from the beginning. The company wants
to update the architecture so that the application must reprocess only the failed steps. | A. Create a web application to write records to Amazon S3. Use S3 Event Notications to publish to an Amazon Simple Notication Service
(Amazon SNS) topic. Use an EC2 instance to poll Amazon SNS and start processing. Save intermediate results to Amazon S3 to pass on to
the next step.
B. Perform the processing steps by using logic in the application. Convert the application code to run in a container. Use AWS Fargate to
manage the container instances. Congure the container to invoke itself to pass the state from one step to the next.
C. Create a web application to pass records to an Amazon Kinesis data stream. Decouple the processing by using the Kinesis data stream
and AWS Lambda functions.
D. Create a web application to pass records to AWS Step Functions. Decouple the processing into Step Functions tasks and AWS Lambda
functions. |  |  |  |  |  |
| 266 | A company is migrating its on-premises Windows applications and Linux applications to AWS. The company will use automation to launch
Amazon EC2 instances to mirror the on-premises congurations. The migrated applications require access to shared storage that uses SMB
for Windows and NFS for Linux.
The company is also creating a pilot light disaster recovery (DR) environment in another AWS Region. The company will use automation to
launch and congure the EC2 instances in the DR Region. The company needs to replicate the storage to the DR Region. | A. Use Amazon S3 for the application storage. Create an S3 bucket in the primary Region and an S3 bucket in the DR Region. Congure S3
Cross-Region Replication (CRR) from the primary Region to the DR Region.
B. Use Amazon Elastic Block Store (Amazon EBS) for the application storage. Create a backup plan in AWS Backup that creates snapshots
of the EBS volumes that are in the primary Region and replicates the snapshots to the DR Region.
C. Use a Volume Gateway in AWS Storage Gateway for the application storage. Congure Cross-Region Replication (CRR) of the Volume
Gateway from the primary Region to the DR Region.
D. Use Amazon FSx for NetApp ONTAP for the application storage. Create an FSx for ONTAP instance in the DR Region. Congure NetApp
SnapMirror replication from the primary Region to the DR Region. | 一家公司正在将其本地Windows应用程序和Linux应用程序迁移到AWS。该公司将使用自动化来启动Amazon EC2实例以镜像本地配置。迁移的应用程序需要访问共享存储，Windows使用SMB协议，Linux使用NFS协议。

该公司还在另一个AWS区域创建试点灯（pilot light）灾难恢复（DR）环境。公司将使用自动化在DR区域启动和配置EC2实例。公司需要将存储复制到DR区域。

 | **选项A：使用Amazon S3作为应用程序存储**
- S3是对象存储服务，不直接支持SMB或NFS协议
- 应用程序无法直接通过SMB/NFS协议访问S3存储
- 虽然S3支持跨区域复制，但不满足协议要求
- **不正确**

**选项B：使用Amazon EBS作为应用程序存储**
- EBS是块存储，主要用于单个EC2实例
- EBS不支持多个实例同时访问（除了Multi-Attach，但有限制）
- 不能直接提供SMB/NFS共享存储功能
- AWS Backup可以跨区域复制快照，但无法解决共享存储需求
- **不正确**

**选项C：使用AWS Storage Gateway的Volume Gateway**
- Volume Gateway主要提供iSCSI协议访问
- 不直接支持SMB和NFS协议
- 虽然提到跨区域复制，但Volume Gateway的CRR配置复杂
- 不是最佳的SMB/NFS解决方案
- **不正确**

**选项D：使用Amazon FSx for NetApp ONTAP**
- FSx for NetApp ONTAP同时支持SMB和NFS协议
- 可以为Windows和Linux应用程序提供共享存储
- NetApp SnapMirror是成熟的复制技术，支持跨区域复制
- 完全满足多协议访问和灾难恢复要求
- 支持自动化部署和管理
- **正确**

 |  |  |  |
| 267 | A company's application uses a eet of Amazon EC2 On-Demand Instances to analyze and process data. The EC2 instances are in an Auto
Scaling group. The Auto Scaling group is a target group for an Application Load Balancer (ALB). The application analyzes critical data that
cannot tolerate interruption. The application also analyzes noncritical data that can withstand interruption.
The critical data analysis requires quick scalability in response to real-time application demand. The noncritical data analysis involves
memory consumption. A DevOps engineer must implement a solution that reduces scale-out latency for the critical data. The solution also
must process the noncritical data. | A. For the critical data, modify the existing Auto Scaling group. Create a warm pool instance in the stopped state. Dene the warm pool
size. Create a new version of the launch template that has detailed monitoring enabled. Use Spot Instances.
B. Modify the application to use
two target groups for critical data and noncritical data.
C. For the critical data, modify the existing Auto Scaling group. Create a lifecycle hook to ensure that bootstrap scripts are completed
successfully. Ensure that the application on the instances is ready to accept trac before the instances are registered. Create a new
version of the launch template that has detailed monitoring enabled.
D. For the noncritical data, create a second Auto Scaling group that uses a launch template. Congure the launch template to install the
unied Amazon CloudWatch agent and to congure the CloudWatch agent with a custom memory utilization metric. Use Spot Instances.
Add the new Auto Scaling group as the target group for the AL
E. For the noncritical data, create a second Auto Scaling group. Choose the predened memory utilization metric type for the target
tracking scaling policy. Use Spot Instances. Add the new Auto Scaling group as the target group for the AL |  |  |  |  |  |
| 268 | A company recently migrated its application to an Amazon Elastic Kubernetes Service (Amazon EKS) cluster that uses Amazon EC2 instances.
The company congured the application to automatically scale based on CPU utilization.
The application produces memory errors when it experiences heavy loads. The application also does not scale out enough to handle the
increased load. The company needs to collect and analyze memory metrics for the application over time. | A. Attach the CloudWatchAgentServerPolicy managed IAM policy to the IAM instance prole that the cluster uses.
B. Attach the CloudWatchAgentServerPolicy managed IAM policy to a service account role for the cluster.
C. Collect performance metrics by deploying the unied Amazon CloudWatch agent to the existing EC2 instances in the cluster. Add the
agent to the AMI for any new EC2 instances that are added to the cluster.
D. Collect performance logs by deploying the AWS Distro for OpenTelemetry collector as a DaemonSet.
E. Analyze the pod_memory_utilization Amazon CloudWatch metric in the ContainerInsights namespace by using the Service dimension. |  |  |  |  |  |
| 269 | A company's video streaming platform usage has increased from 10,000 users each day to 50,000 users each day in multiple countries. The
company deploys the streaming platform on Amazon Elastic Kubernetes Service (Amazon EKS). The EKS workload scales up to thousands of
nodes during peak viewing time.
The company's users report occurrences of unauthorized logins. Users also report sudden interruptions and logouts from the platform.
The company wants additional security measures for the entire platform. The company also needs a summarized view of the resource
behaviors and interactions across the company's entire AWS environment. The summarized view must show login attempts, API calls, and
network trac. The solution must permit network trac analysis while minimizing the overhead of managing logs. The solution must also
quickly investigate any potential malicious behavior that is associated with the EKS workload. | A. Enable Amazon GuardDuty for EKS Audit Log Monitoring. Enable AWS CloudTrail logs. Store the EKS audit logs and CloudTrail log les in
an Amazon S3 bucket. Use Amazon Athena to create an external table. Use Amazon QuickSight to create a dashboard.
B. Enable Amazon GuardDuty for EKS Audit Log Monitoring. Enable Amazon Detective in the company's AWS account. Enable EKS audit
logs from optional source packages in Detective.
C. Enable Amazon CloudWatch Container Insights. Enable AWS CloudTrail logs. Store the EKS audit logs and CloudTrail log les in an
Amazon S3 bucket. Use Amazon Athena to create an external table. Use Amazon QuickSight to create a dashboard.
D. Enable Amazon GuardDuty for EKS Audit Log Monitoring. Enable Amazon CloudWatch Container Insights and VPC Flow Logs. Enable
AWS CloudTrail logs. | 一家公司的视频流媒体平台使用量从每天10,000用户增长到多个国家每天50,000用户。该公司在Amazon Elastic Kubernetes Service (Amazon EKS)上部署流媒体平台。EKS工作负载在高峰观看时间会扩展到数千个节点。

公司用户报告出现未经授权的登录情况。用户还报告平台出现突然中断和登出。

公司希望为整个平台增加额外的安全措施。公司还需要一个汇总视图来显示整个AWS环境中资源行为和交互。汇总视图必须显示登录尝试、API调用和网络流量。解决方案必须允许网络流量分析，同时最小化管理日志的开销。解决方案还必须能够快速调查与EKS工作负载相关的任何潜在恶意行为。

 | **选项A：** 启用Amazon GuardDuty的EKS审计日志监控。启用AWS CloudTrail日志。将EKS审计日志和CloudTrail日志文件存储在Amazon S3存储桶中。使用Amazon Athena创建外部表。使用Amazon QuickSight创建仪表板。
- 优点：提供了基本的安全监控和可视化
- 缺点：需要手动管理日志存储和分析，增加了管理开销，不符合"最小化管理日志开销"的要求

**选项B：** 启用Amazon GuardDuty的EKS审计日志监控。在公司AWS账户中启用Amazon Detective。在Detective中启用来自可选源包的EKS审计日志。
- 优点：GuardDuty提供威胁检测，Detective提供自动化的安全调查和可视化
- 缺点：缺少网络流量分析和API调用监控，不能完全满足需求

**选项C：** 启用Amazon CloudWatch Container Insights。启用AWS CloudTrail日志。将EKS审计日志和CloudTrail日志文件存储在Amazon S3存储桶中。使用Amazon Athena创建外部表。使用Amazon QuickSight创建仪表板。
- 优点：提供容器监控和API调用跟踪
- 缺点：缺少专门的安全威胁检测，需要手动管理日志，不符合快速调查恶意行为的要求

**选项D：** 启用Amazon GuardDuty的EKS审计日志监控。启用Amazon CloudWatch Container Insights和VPC Flow Logs。启用AWS CloudTrail日志。
- 优点：
  - GuardDuty提供EKS特定的威胁检测和快速恶意行为调查
  - CloudWatch Container Insights提供容器性能监控
  - VPC Flow Logs提供网络流量分析
  - CloudTrail提供API调用跟踪
  - 所有服务都是托管服务，最小化日志管理开销

 | D |  |  |
| 270 | A company uses AWS Organizations to manage hundreds of AWS accounts. The company has a team that is responsible for AWS Identity and
Access Management (IAM).
The IAM team wants to implement AWS IAM Identity Center (AWS Single Sign-On). The IAM team must have only the minimum needed
permissions to manage IAM Identity Center. The IAM team must not be able to gain unneeded access to the Organizations management
account. The IAM team must be able to provision new IAM Identity Center permission sets and assignments for existing and new member
accounts. | A. Create a new AWS account for the IAM team. In the new account, enable IAM Identity Center. In the Organizations management
account, register the new account as a delegated administrator for IAM Identity Center.
B. Create a new AWS account for the IAM team. In the Organizations management account, enable IAM Identity Center. In the
Organizations management account, register the new account as a delegated administrator for IAM Identity Center.
C. In IAM Identity Center, create users and a group for the IAM team. Add the users to the group. Create a new permission set. Attach the
AWSSSODirectoryAdministrator managed IAM policy to the group.
D. In IAM Identity Center, create users and a group for the IAM team. Add the users to the group. Create a new permission set. Attach the
AWSSSOMemberAccountAdministrator managed IAM policy to the group.
E. Assign the permission set to the Organizations management account. Allow the IAM team group to use the permission set.
F. Assign the permission set to the new AWS account. Allow the IAM team group to use the permission set. |  |  |  |  |  |
| 271 | A company uses an organization in AWS Organizations that has all features enabled. The company uses AWS Backup in a primary account and
uses an AWS Key Management Service (AWS KMS) key to encrypt the backups.
The company needs to automate a cross-account backup of the resources that AWS Backup backs up in the primary account. The company
congures cross-account backup in the Organizations management account. The company creates a new AWS account in the organization and
congures an AWS Backup backup vault in the new account. The company creates a KMS key in the new account to encrypt the backups.
Finally, the company congures a new backup plan in the primary account. The destination for the new backup plan is the backup vault in the
new account.
When the AWS Backup job in the primary account is invoked, the job creates backups in the primary account. However, the backups are not
copied to the new account's backup vault. | A. Edit the backup vault access policy in the new account to allow access to the primary account.
B. Edit the backup vault access policy in the primary account to allow access to the new account.
C. Edit the backup vault access policy in the primary account to allow access to the KMS key in the new account.
D. Edit the key policy of the KMS key in the primary account to share the key with the new account.
E. Edit the key policy of the KMS key in the new account to share the key with the primary account. |  |  |  |  |  |
| 272 | A company runs an application that uses an Amazon S3 bucket to store images. A DevOps engineer needs to implement a multi-Region
strategy for the objects that are stored in the S3 bucket. The company needs to be able to fail over to an S3 bucket in another AWS Region.
When an image is added to either S3 bucket, the image must be replicated to the other S3 bucket within 15 minutes.
The DevOps engineer enables two-way replication between the S3 buckets. | A. Enable S3 Replication Time Control (S3 RTC) on each replication rule.
B. Create an S3 Multi-Region Access Point in an active-passive conguration.
C. Call the SubmitMultiRegionAccessPointRoutes operation in the AWS API when the company needs to fail over to the S3 bucket in the
other Region.
D. Enable S3 Transfer Acceleration on both S3 buckets.
E. Congure a routing control in Amazon Route 53 Recovery Controller. Add the S3 buckets in an active-passive conguration.
F. Call the UpdateRoutingControlStates operation in the AWS API when the company needs to fail over to the S3 bucket in the other
Region. | **
一家公司运行一个使用Amazon S3存储桶来存储图像的应用程序。DevOps工程师需要为存储在S3存储桶中的对象实施多区域策略。公司需要能够故障转移到另一个AWS区域的S3存储桶。当图像添加到任一S3存储桶时，图像必须在15分钟内复制到另一个S3存储桶。DevOps工程师在S3存储桶之间启用了双向复制。

2. ** | **

**A. 在每个复制规则上启用S3复制时间控制(S3 RTC)**
- 正确。S3 RTC确保99.99%的对象在15分钟内完成复制，正好满足题目要求的15分钟复制时间要求。

**B. 创建一个主动-被动配置的S3多区域访问点**
- 部分正确。多区域访问点可以提供故障转移功能，但主动-被动配置不是最佳选择，因为题目已经设置了双向复制。

**C. 当公司需要故障转移到另一个区域的S3存储桶时，调用AWS API中的SubmitMultiRegionAccessPointRoutes操作**
- 正确。这是用于控制多区域访问点路由的API操作，可以实现故障转移。

**D. 在两个S3存储桶上启用S3传输加速**
- 不正确。传输加速主要用于提高上传速度，不能解决复制时间控制或故障转移问题。

**E. 在Amazon Route 53恢复控制器中配置路由控制。以主动-被动配置添加S3存储桶**
- 不正确。Route 53恢复控制器主要用于应用程序级别的故障转移，不直接管理S3存储桶的故障转移。

**F. 当公司需要故障转移到另一个区域的S3存储桶时，调用AWS API中的UpdateRoutingControlStates操作**
- 不正确。这个API与Route 53恢复控制器相关，不适用于S3存储桶的直接故障转移。

3. ** |  |  |  |
| 273 | A company uses the AWS Cloud Development Kit (AWS CDK) to dene its application. The company uses a pipeline that consists of AWS
CodePipeline and AWS CodeBuild to deploy the CDK application.
The company wants to introduce unit tests to the pipeline to test various infrastructure components. The company wants to ensure that a
deployment proceeds if no unit tests result in a failure. | A. Update the CodeBuild build phase commands to run the tests then to deploy the application. Set the OnFailure phase property to
ABORT.
B. Update the CodeBuild build phase commands to run the tests then to deploy the application. Add the --rollback true ag to the cdk
deploy command.
C. Update the CodeBuild build phase commands to run the tests then to deploy the application. Add the --require-approval any-change ag
to the cdk deploy command.
D. Create a test that uses the AWS CDK assertions module. Use the template.hasResourceProperties assertion to test that resources have
the expected properties.
E. Create a test that uses the cdk diff command. Congure the test to fail if any resources have changed. | 一家公司使用AWS云开发工具包(AWS CDK)来定义其应用程序。该公司使用由AWS CodePipeline和AWS CodeBuild组成的管道来部署CDK应用程序。

该公司希望在管道中引入单元测试来测试各种基础设施组件。公司希望确保如果没有单元测试失败，部署就会继续进行。

 | **选项A：** 更新CodeBuild构建阶段命令以运行测试然后部署应用程序。将OnFailure阶段属性设置为ABORT。
- 这个选项提到了正确的流程（先测试后部署），但OnFailure设置为ABORT意味着测试失败时会中止部署，这符合题目要求。但这个选项没有具体说明如何实现单元测试。

**选项B：** 更新CodeBuild构建阶段命令以运行测试然后部署应用程序。在cdk deploy命令中添加--rollback true标志。
- --rollback true标志用于部署失败时的回滚，但这不是关于单元测试的配置，也不能确保测试失败时阻止部署。

**选项C：** 更新CodeBuild构建阶段命令以运行测试然后部署应用程序。在cdk deploy命令中添加--require-approval any-change标志。
- --require-approval any-change标志要求对任何更改进行手动批准，这与自动化单元测试的目标不符。

**选项D：** 创建使用AWS CDK assertions模块的测试。使用template.hasResourceProperties断言来测试资源是否具有预期的属性。
- 这是正确的CDK单元测试方法。CDK assertions模块专门用于测试CDK应用程序的基础设施组件，template.hasResourceProperties可以验证生成的CloudFormation模板中的资源属性。

**选项E：** 创建使用cdk diff命令的测试。配置测试在任何资源发生更改时失败。
- cdk diff用于比较当前部署和新版本的差异，但让测试在任何更改时都失败是不合理的，这会阻止所有的基础设施更新。

 |  |  |  |
| 274 | A company has an application that runs on Amazon EC2 instances behind an Application Load Balancer (ALB). The EC2 instances are in
multiple Availability Zones. The application was miscongured in a single Availability Zone, which caused a partial outage of the application.
A DevOps engineer made changes to ensure that the unhealthy EC2 instances in one Availability Zone do not affect the healthy EC2 instances
in the other Availability Zones. The DevOps engineer needs to test the application's failover and shift where the ALB sends trac. During
failover, the ALB must avoid sending trac to the Availability Zone where the failure has occurred. | A. Turn off cross-zone load balancing on the AL
B. Start a zonal shift for
the resource set away from the Availability Zone.
C. Create an Amazon Route 53 Application Recovery Controller resource set that uses the DNS hostname of the AL
D. Create an Amazon Route 53 Application Recovery Controller resource set that uses the ARN of the ALB’s target group. Create a
readiness check that uses the ElbV2TargetGroupsCanServeTrac rule. | 一家公司有一个应用程序运行在应用负载均衡器(ALB)后面的Amazon EC2实例上。这些EC2实例分布在多个可用区中。应用程序在单个可用区中配置错误，导致应用程序部分中断。DevOps工程师进行了更改，以确保一个可用区中的不健康EC2实例不会影响其他可用区中的健康EC2实例。DevOps工程师需要测试应用程序的故障转移并改变ALB发送流量的位置。在故障转移期间，ALB必须避免向发生故障的可用区发送流量。

 | **选项A：关闭ALB上的跨区负载均衡**
- 关闭跨区负载均衡只是改变了流量分配方式，但不能主动避免向特定故障可用区发送流量
- 这不能满足"测试故障转移"和"主动避免向故障可用区发送流量"的需求
- 不正确

**选项B：为资源集启动区域转移(zonal shift)，远离该可用区**
- Zonal shift是AWS的一个功能，允许主动将流量从特定可用区转移走
- 这正好满足测试故障转移的需求，可以模拟可用区故障
- 可以确保ALB避免向指定的可用区发送流量
- 符合题目要求

**选项C：创建使用ALB的DNS主机名的Amazon Route 53 Application Recovery Controller资源集**
- Route 53 ARC主要用于跨区域的故障转移控制
- 使用DNS主机名不是正确的配置方式
- 题目场景是同一区域内的可用区级别故障转移，不是区域级别
- 不正确

**选项D：创建使用ALB目标组ARN的Amazon Route 53 Application Recovery Controller资源集，并创建使用ElbV2TargetGroupsCanServeTraffic规则的就绪检查**
- Route 53 ARC更适用于区域级别的故障转移
- 虽然技术上可行，但对于可用区级别的流量转移来说过于复杂
- 不是最直接有效的解决方案

 | A |  |  |
| 275 | A company sends its AWS Network Firewall ow logs to an Amazon S3 bucket. The company then analyzes the ow logs by using Amazon
Athena.
The company needs to transform the ow logs and add additional data before the ow logs are delivered to the existing S3 bucket.
Which solution will meet these requirements? | A. Create an AWS Lambda function to transform the data and to write a new object to the existing S3 bucket. Congure the Lambda
function with an S3 trigger for the existing S3 bucket. Specify all object create events for the event type. Acknowledge the recursive
invocation.
B. Enable Amazon EventBridge notications on the existing S3 bucket. Create a custom EventBridge event bus. Create an EventBridge rule
that is associated with the custom event bus. Congure the rule to react to all object create events for the existing S3 bucket and to
invoke an AWS Step Functions workow. Congure a Step Functions task to transform the data and to write the data into a new S3 bucket.
C. Create an Amazon EventBridge rule that is associated with the default EventBridge event bus. Congure the rule to react to all object
create events for the existing S3 bucket. Dene a new S3 bucket as the target for the rule. Create an EventBridge input transformation to
customize the event before passing the event to the rule target.
D. Create an Amazon Kinesis Data Firehose delivery stream that is congured with an AWS Lambda transformer. Specify the existing S3
bucket as the destination. Change the Network Firewall logging destination from Amazon S3 to Kinesis Data Firehose. | 一家公司将其AWS Network Firewall流日志发送到Amazon S3存储桶。然后公司使用Amazon Athena分析流日志。
公司需要在流日志传递到现有S3存储桶之前转换流日志并添加额外数据。 | A. 创建AWS Lambda函数转换数据并写入现有S3桶。为Lambda函数配置现有S3桶的S3触发器，指定所有对象创建事件类型。确认递归调用。
❌ 严重问题：会导致无限递归循环
❌ Lambda被S3对象创建触发→Lambda处理数据→写入同一S3桶→再次触发Lambda
❌ 虽然提到"确认递归调用"，但这不是好的架构设计
B. 在现有S3桶启用EventBridge通知。创建自定义EventBridge事件总线。配置EventBridge规则响应对象创建事件并调用Step Functions工作流。配置Step Functions任务转换数据并写入新S3桶。
❌ 过于复杂：涉及EventBridge、自定义事件总线、Step Functions等多个服务
❌ 改变目标：写入新S3桶可能影响现有Athena分析流程
❌ 架构冗余：简单的数据转换不需要这么复杂的架构
C. 创建与默认EventBridge事件总线关联的规则。配置规则响应现有S3桶的对象创建事件。定义新S3桶作为规则目标。创建EventBridge输入转换。
❌ 功能限制：EventBridge输入转换主要用于转换事件元数据，不能转换实际的日志数据内容
❌ 不满足需求：无法实现流日志数据的转换和附加数据添加
D. 创建配置了AWS Lambda转换器的Amazon Kinesis Data Firehose交付流。指定现有S3桶作为目标。将Network Firewall日志目标从Amazon S3更改为Kinesis Data Firehose。
✅ 专门设计：Kinesis Data Firehose专为流数据转换和传输而设计
✅ 内置转换：支持Lambda转换器进行数据转换和添加额外数据
✅ 无递归问题：数据流是单向的，不会产生循环
✅ 保持目标：仍然传递到现有S3桶，不影响Athena分析
✅ 架构简洁：最少的组件实现最大的功能 | D |  |  |
| 276 | A DevOps engineer needs to implement integration tests into an existing AWS CodePipeline CI/CD workow for an Amazon Elastic Container
Service (Amazon ECS) service. The CI/CD workow retrieves new application code from an AWS CodeCommit repository and builds a container
image. The Cl/CD workow then uploads the container image to Amazon Elastic Container Registry (Amazon ECR) with a new image tag
version.
The integration tests must ensure that new versions of the service endpoint are reachable and that various API methods return successful
response data. The DevOps engineer has already created an ECS cluster to test the service.
Which combination of steps will meet these requirements with the LEAST management overhead? (Choose three.) | A. Add a deploy stage to the pipeline. Congure Amazon ECS as the action provider. Most Voted
B. Add a deploy stage to the pipeline. Congure AWS CodeDeploy as the action provider.
C. Add an appspec.yml le to the CodeCommit repository.
D. Update the image build pipeline stage to output an imagedenitions.json le that references the new image tag. Most Voted
E. Create an AWS Lambda function that runs connectivity checks and API calls against the service. Integrate the Lambda function with
CodePipeline by using a Lambda action stage. Most Voted
F. Write a script that runs integration tests against the service. Upload the script to an Amazon S3 bucket. Integrate the script in the S3
bucket with CodePipeline by using an S3 action stage. | DevOps工程师需要在现有的AWS CodePipeline CI/CD工作流中为Amazon ECS服务实现集成测试。CI/CD工作流从AWS CodeCommit仓库检索新应用代码并构建容器镜像。然后工作流将容器镜像上传到Amazon ECR并使用新的镜像标签版本。
集成测试必须确保服务端点的新版本可达，并且各种API方法返回成功的响应数据。DevOps工程师已经创建了一个ECS集群来测试服务。 | A. 向管道添加部署阶段。配置Amazon ECS作为操作提供者。
✅ 必需步骤：需要部署阶段将新构建的容器部署到测试ECS集群
✅ 直接简单：ECS作为action provider是最直接的部署方式
✅ 管理开销最少：无需额外的部署工具
B. 向管道添加部署阶段。配置AWS CodeDeploy作为操作提供者。
❌ 增加复杂性：CodeDeploy增加了额外的配置和管理开销
❌ 不必要：对于简单的测试部署，直接ECS部署更合适
C. 向CodeCommit仓库添加appspec.yml文件。
❌ 仅适用于CodeDeploy：如果选择直接ECS部署(选项A)，则不需要appspec.yml
❌ 增加管理开销：需要维护额外的配置文件
D. 更新镜像构建管道阶段以输出引用新镜像标签的imagedefinitions.json文件。
✅ ECS部署标准：imagedefinitions.json是ECS action的标准输入格式
✅ 必需组件：定义要部署的容器镜像版本
✅ 自动化：管道自动生成，无额外管理开销
E. 创建AWS Lambda函数进行连接性检查和API调用。通过Lambda操作阶段将Lambda函数与CodePipeline集成。
✅ 完美适配：Lambda专门用于运行集成测试
✅ 无服务器：最少的管理开销，无需管理服务器
✅ 灵活性：可以进行各种API测试和连接性检查
✅ 原生集成：CodePipeline对Lambda有原生支持
F. 编写集成测试脚本并上传到S3桶。通过S3操作阶段与CodePipeline集成。
❌ 不适用：S3 action主要用于artifact存储，不是执行环境
❌ 需要额外计算资源：脚本需要在某处执行，增加管理开销 |  |  |  |
| 277 | A company runs applications on Windows and Linux Amazon EC2 instances. The instances run across multiple Availability Zones in an AWS
Region. The company uses Auto Scaling groups for each application.
The company needs a durable storage solution for the instances. The solution must use SMB for Windows and must use NFS for Linux. The
solution must also have sub-millisecond latencies. All instances will read and write the data.
Which combination of steps will meet these requirements? (Choose three.) | A company runs applications on Windows and Linux Amazon EC2 instances. The instances run across multiple Availability Zones in an AWS
Region. The company uses Auto Scaling groups for each application.
The company needs a durable storage solution for the instances. The solution must use SMB for Windows and must use NFS for Linux. The
solution must also have sub-millisecond latencies. All instances will read and write the data.
Which combination of steps will meet these requirements? (Choose three.) | 一家公司在AWS区域的多个可用区中运行Windows和Linux Amazon EC2实例上的应用程序。公司为每个应用程序使用Auto Scaling组。
公司需要为实例提供持久存储解决方案。解决方案必须为Windows使用SMB，为Linux使用NFS。解决方案还必须具有亚毫秒级延迟。所有实例都将读写数据。 | A. 创建在多个可用区有目标的Amazon EFS文件系统。
❌ 协议限制：EFS只支持NFS协议，不支持SMB
❌ 延迟性能：EFS通常是毫秒级延迟，不是亚毫秒级
❌ 不满足Windows需求：无法为Windows提供SMB访问
B. 创建Amazon FSx for NetApp ONTAP Multi-AZ文件系统。
✅ 双协议支持：同时支持SMB (Windows) 和NFS (Linux)
✅ 高性能：可提供亚毫秒级延迟
✅ 多AZ部署：支持跨可用区的高可用性
✅ 共享访问：支持多实例同时读写
C. 创建通用SSD (gp3) Amazon EBS卷用于共享存储。
❌ 共享限制：EBS卷不能直接在多个实例间共享
❌ 协议不支持：EBS不是文件系统，不支持SMB/NFS协议
❌ 架构不匹配：块存储不适合这种用例
D. 更新每个应用程序启动模板的用户数据以挂载文件系统。
✅ 自动化挂载：通过用户数据脚本实现自动挂载
✅ Auto Scaling兼容：新启动的实例自动配置
✅ 标准做法：这是配置Auto Scaling实例的标准方法
E. 在每个Auto Scaling组执行实例刷新。
✅ 应用新配置：将新的启动模板配置应用到现有实例
✅ 完整更新：确保所有实例都有最新配置
✅ 零停机：滚动更新方式
F. 更新EC2实例以在新实例启动时挂载文件系统。
❌ 不够具体：没有说明具体实现方法
❌ 手动操作：暗示需要手动配置，不如用户数据自动化 | BDE |  |  |
| 278 | A company uses an organization in AWS Organizations that a security team and a DevOps team manage. Both teams access the accounts by
using AWS IAM Identity Center.
A dedicated group has been created for each team. The DevOps team's group has been assigned a permission set named DevOps. The
permission set has the AdministratorAccess managed IAM policy attached. The permission set has been applied to all accounts in the
organization.
The security team wants to ensure that the DevOps team does not have access to IAM Identity Center in the organization's management
account. The security team has attached the following SCP to the organization root:
After implementing the policy, the security team discovers that the DevOps team can still access IAM Identity Center. | A. In the organization's management account, create a new OU. Move the organization's management account to the new OU. Detach the
SCP from the organization root. Attach the SCP to the new OU.
B. In the organization's management account, update the SCP condition reference to the ARN of the DevOps team's group role to include
the AWS account ID of the organization's management account.
C. In IAM Identity Center, create a new permission set. Ensure that the assigned policy has full access but explicitly denies permission for
the sso:* action and the sso-directory:* action. Update the assigned permission set for the DevOps team's group role in the organization's
management account. Delete the SCP.
D. In IAM Identity Center, update the DevOps permission set. Ensure that the assigned policy has full access but explicitly denies
permission for the sso:* action and the sso-directory:* action. In the Deny statement, add a StringEquals condition that compares the
aws:SourceAccount global condition context key with the organization's management account IDelete the SCP. | 一家公司使用AWS Organizations中的组织，由安全团队和DevOps团队管理。两个团队都通过AWS IAM Identity Center访问账户。

为每个团队创建了专用组。DevOps团队的组被分配了名为DevOps的权限集。该权限集附加了AdministratorAccess托管IAM策略。该权限集已应用于组织中的所有账户。

安全团队希望确保DevOps团队无法访问组织管理账户中的IAM Identity Center。安全团队已将以下SCP附加到组织根：

实施策略后，安全团队发现DevOps团队仍然可以访问IAM Identity Center。

 | **选项A：** 在组织的管理账户中创建新的OU，将组织的管理账户移动到新的OU，从组织根分离SCP，将SCP附加到新的OU。
- **错误**：管理账户不能移动到OU中。管理账户始终位于组织根级别，这是AWS Organizations的基本限制。

**选项B：** 在组织的管理账户中，更新SCP条件引用，将DevOps团队组角色的ARN包含组织管理账户的AWS账户ID。
- **部分正确但不完整**：虽然题目中没有显示具体的SCP内容，但这个选项暗示需要修改SCP的条件来正确识别管理账户中的DevOps角色。

**选项C：** 在IAM Identity Center中创建新的权限集，确保分配的策略具有完全访问权限但明确拒绝sso:*和sso-directory:*操作。为管理账户中的DevOps团队组角色更新分配的权限集。删除SCP。
- **可行但复杂**：创建新权限集是一种解决方案，但增加了管理复杂性。

**选项D：** 在IAM Identity Center中更新DevOps权限集，确保分配的策略具有完全访问权限但明确拒绝sso:*和sso-directory:*操作。在Deny语句中添加StringEquals条件，将aws:SourceAccount全局条件上下文键与组织的管理账户ID进行比较。删除SCP。
- **最佳选择**：直接修改现有权限集，添加特定的拒绝条件，只在管理账户中生效。这是最直接和高效的解决方案。

 |  |  |  |
| 279 | An Amazon EC2 Auto Scaling group manages EC2 instances that were created from an AMI. The AMI has the AWS Systems Manager Agent
installed. When an EC2 instance is launched into the Auto Scaling group, tags are applied to the EC2 instance.
EC2 instances that are launched by the Auto Scaling group must have the correct operating system conguration. | A. Create a Systems Manager Run Command document that congures the desired instance conguration. Set up Systems Manager
Compliance to invoke the Run Command document when the EC2 instances are not in compliance with the most recent patches.
B. Create a Systems Manager State Manager association that links to the Systems Manager command document. Create a tag query that
runs immediately.
C. Create a Systems Manager Run Command task that species the desired instance conguration. Create a maintenance window in
Systems Manager Maintenance Windows that runs daily. Register the Run Command task against the maintenance window. Designate the
targets.
D. Create a Systems Manager Patch Manager patch baseline and a patch group that use the same tags that the Auto Scaling group
applies. Register the patch group with the patch baseline. Dene a Systems Manager command document to patch the instances Invoke
the document by using Systems Manager Run Command. |  |  |  |  |  |
| 280 | A company uses AWS Organizations to manage its AWS accounts. The organization root has a child OU that is named Department. The
Department OU has a child OU that is named Engineering. The default FullAWSAccess policy is attached to the root, the Department OU, and
the Engineering OU.
The company has many AWS accounts in the Engineering OU. Each account has an administrative IAM role with the AdministratorAccess IAM
policy attached. The default FullAWSAccessPolicy is also attached to each account.
A DevOps engineer plans to remove the FullAWSAccess policy from the Department OU. The DevOps engineer will replace the policy with a
policy that contains an Allow statement for all Amazon EC2 API operations. | A. All API actions on all resources will be allowed.
B. All API actions on EC2 resources will be allowed. All other API actions will be denied.
C. All API actions on all resources will be denied.
D. All API actions on EC2 resources will be denied. All other API actions will be allowed. |  |  |  |  |  |
| 281 | A company manages AWS accounts in AWS Organizations. The company needs a solution to send Amazon CloudWatch Logs data to an
Amazon S3 bucket in a dedicated AWS account. The solution must support all existing and future CloudWatch Logs log groups. | A. Enable Organizations backup policies to back up all log groups to a dedicated S3 bucket. Add an S3 bucket policy that allows access
from all accounts that belong to the company.
B. Create a backup plan in AWS Backup. Specify a dedicated S3 bucket as a backup vault. Assign all CloudWatch Logs log group resources
to the backup plan. Create resource assignments in the backup plan for all accounts that belong to the company.
C. Create a backup plan in AWS Backup. Specify a dedicated S3 bucket as a backup vault. Assign all existing log groups to the backup
plan. Create resource assignments in the backup plan for all accounts that belong to the company. Create an AWS Systems Manager
Automation runbook to assign log groups to a backup plan. Create an AWS Cong rule that has an automatic remediation action for all
noncompliant log groups. Specify the runbook as the rule's target.
D. Create a CloudWatch Logs destination and an Amazon Kinesis Data Firehose delivery stream in the dedicated AWS account. Specify the
S3 bucket as the destination of the delivery stream. Create subscription lters for all existing log groups in all accounts. Create an AWS
Lambda function to call the CloudWatch Logs PutSubscriptionFilter API operation. Create an Amazon EventBridge rule to invoke the
Lambda function when a CreateLogGroup event occurs. |  |  |  |  |  |
| 282 | A DevOps engineer manages a Java-based application that runs in an Amazon Elastic Container Service (Amazon ECS) cluster on AWS
Fargate. Auto scaling has not been congured for the application.
The DevOps engineer has determined that the Java Virtual Machine (JVM) thread count is a good indicator of when to scale the application.
The application serves customer trac on port 8080 and makes JVM metrics available on port 9404.
Application use has recently increased. The DevOps engineer needs to congure auto scaling for the application. | A. Deploy the Amazon CloudWatch agent as a container sidecar. Congure the CloudWatch agent to retrieve JVM metrics from port 9404.
Create CloudWatch alarms on the JVM thread count metric to scale the application. Add a step scaling policy in Fargate to scale up and
scale down based on the CloudWatch alarms.
B. Deploy the Amazon CloudWatch agent as a container sidecar. Congure a metric lter for the JVM thread count metric on the
CloudWatch log group for the CloudWatch agent. Add a target tracking policy in Fargate. Select the metric from the metric lter as a scale
target.
C. Create an Amazon Managed Service for Prometheus workspace. Deploy AWS Distro for OpenTelemetry as a container sidecar to publish
the JVM metrics from port 9404 to the Prometheus workspace. Congure rules for the workspace to use the JVM thread count metric to
scale the application. Add a step scaling policy in Fargate. Select the Prometheus rules to scale up and scaling down.
D. Create an Amazon Managed Service for Prometheus workspace. Deploy AWS Distro for OpenTelemetry as a container sidecar to retrieve
JVM metrics from port 9404 to publish the JVM metrics from port 9404 to the Prometheus workspace. Add a target tracking policy in
Fargate. Select the Prometheus metric as a scale target. | 一名DevOps工程师管理着一个基于Java的应用程序，该应用程序运行在AWS Fargate上的Amazon Elastic Container Service (Amazon ECS)集群中。该应用程序尚未配置自动扩缩容。

DevOps工程师已确定Java虚拟机(JVM)线程数是决定何时扩缩容应用程序的良好指标。该应用程序在端口8080上为客户提供流量服务，并在端口9404上提供JVM指标。

应用程序使用量最近有所增加。DevOps工程师需要为应用程序配置自动扩缩容。

 | **选项A：** 将Amazon CloudWatch代理部署为容器边车。配置CloudWatch代理从端口9404检索JVM指标。在JVM线程数指标上创建CloudWatch告警来扩缩容应用程序。在Fargate中添加步进扩缩容策略，基于CloudWatch告警进行扩容和缩容。

- **正确性：高** - CloudWatch代理可以收集自定义指标，CloudWatch告警可以触发ECS服务的自动扩缩容
- **技术可行性：** ECS支持基于CloudWatch指标的自动扩缩容，步进扩缩容策略是有效的扩缩容方式

**选项B：** 将Amazon CloudWatch代理部署为容器边车。在CloudWatch代理的CloudWatch日志组上为JVM线程数指标配置指标过滤器。在Fargate中添加目标跟踪策略。选择指标过滤器中的指标作为扩缩容目标。

- **正确性：低** - 指标过滤器主要用于从日志中提取指标，而不是直接从应用程序端点收集指标
- **技术问题：** 这种方法过于复杂且不是收集JVM指标的最佳实践

**选项C：** 创建Amazon Managed Service for Prometheus工作空间。部署AWS Distro for OpenTelemetry作为容器边车，将端口9404的JVM指标发布到Prometheus工作空间。为工作空间配置规则，使用JVM线程数指标来扩缩容应用程序。在Fargate中添加步进扩缩容策略。选择Prometheus规则进行扩容和缩容。

- **正确性：低** - Prometheus工作空间不能直接触发ECS自动扩缩容
- **技术问题：** ECS自动扩缩容需要CloudWatch指标，不能直接使用Prometheus规则

**选项D：** 创建Amazon Managed Service for Prometheus工作空间。部署AWS Distro for OpenTelemetry作为容器边车，从端口9404检索JVM指标并发布到Prometheus工作空间。在Fargate中添加目标跟踪策略。选择Prometheus指标作为扩缩容目标。

- **正确性：低** - 类似选项C，ECS自动扩缩容不能直接使用Prometheus指标
- **技术问题：** 需要额外的集成将Prometheus指标转换为CloudWatch指标

 |  |  |  |
| 283 | A company has an application that runs in a single AWS Region. The application runs on an Amazon Elastic Kubernetes Service (Amazon EKS)
cluster and connects to an Amazon Aurora MySQL cluster. The application is built in an AWS CodeBuild project. The container images are
published to Amazon Elastic Container Registry (Amazon ECR).
The company needs to replicate the state of the application for the container images and the database to a second Region. | A. Turn on Amazon S3 Cross-Region Replication (CRR) on the bucket that holds the ECR container images. Deploy the application to an EKS
cluster in the second Region by referencing the new S3 bucket object URL for the container image in a Kubernetes deployment le.
Congure a cross-Region Aurora Replica in the second Region. Congure the new application deployment to use the endpoints for the
cross-Region Aurora Replica.
B. Create an Amazon EventBridge rule that reacts to image pushes to the ECR repository. Congure the EventBridge rule to invoke an AWS
Lambda function to replicate the image to a new ECR repository in the second Region. Deploy the application to an EKS cluster in the
second Region by referencing the new ECR repository in a Kubernetes deployment le. Congure a cross-Region Aurora Replica in the
second Region. Congure the new application deployment to use the endpoints for the cross-Region Aurora Replica.
C. Turn on Cross-Region Replication to replicate the ECR repository to the second Region. Deploy the application to an EKS cluster in the
second Region by referencing the new ECR repository in a Kubernetes deployment le. Congure an Aurora global database with clusters
in the initial Region and the second Region. Congure the new application deployment to use the endpoints for the second Region's
cluster in the Aurora global database.
D. Congure the CodeBuild project to also push the container image to an ECR repository in the second Region. Deploy the application to
an EKS cluster in the second Region by referencing the new ECR repository in a Kubernetes deployment le. Congure an Aurora MySQL
cluster in the second Region as the target for binary log replication from the Aurora MySQL cluster in the initial Region. Congure the new
application deployment to use the endpoints for the second Region's cluster. | 一家公司有一个在单个AWS区域运行的应用程序。该应用程序运行在Amazon Elastic Kubernetes Service (Amazon EKS)集群上，并连接到Amazon Aurora MySQL集群。应用程序在AWS CodeBuild项目中构建。容器镜像发布到Amazon Elastic Container Registry (Amazon ECR)。

公司需要将应用程序的状态（包括容器镜像和数据库）复制到第二个区域。

 | **选项A：**
- 错误：ECR容器镜像不存储在S3存储桶中，而是存储在ECR服务中
- ECR有自己的存储机制，不能通过S3 CRR来复制
- Kubernetes部署文件不能直接引用S3对象URL作为容器镜像
- Aurora跨区域副本配置是正确的

**选项B：**
- 正确：使用EventBridge监听ECR推送事件是可行的方案
- Lambda函数可以实现ECR镜像的跨区域复制
- EKS集群可以正确引用新区域的ECR仓库
- Aurora跨区域副本配置正确
- 这是一个可行但相对复杂的解决方案

**选项C：**
- 错误：ECR本身没有内置的"Cross-Region Replication"功能
- Aurora Global Database配置是正确且更优的选择
- 其他部分配置合理

**选项D：**
- 正确：修改CodeBuild项目同时推送到两个区域的ECR是直接有效的方法
- Aurora MySQL的二进制日志复制是可行的数据库复制方案
- 配置简单，易于实施和维护
- 这是最直接和实用的解决方案

 |  |  |  |
| 284 | A company is building a serverless application that uses AWS Lambda functions to process data.
A BeginResponse Lambda function initializes data in response to specic application events. The company needs to ensure that a large
number of Lambda functions are invoked after the BeginResponse Lambda function runs. Each Lambda function must be invoked in parallel
and depends on only the outputs of the BeginResponse Lambda function. Each Lambda function has retry logic for invocation and must be
able to ne-tune concurrency without losing data. | A. Create an Amazon Simple Notication Service (Amazon SNS) topic. Modify the BeginResponse Lambda function to publish to the SNS
topic before the BeginResponse Lambda function nishes running. Subscribe all Lambda functions that need to invoke after the
BeginResponse Lambda function runs to the SNS topic. Subscribe any new Lambda functions to the SNS topic.
B. Create an Amazon Simple Queue Service (Amazon SQS) queue for each Lambda function that needs to run after the BeginResponse
Lambda function runs. Subscribe each Lambda function to its own SQS queue. Create an Amazon Simple Notication Service (Amazon
SNS) topic. Subscribe each SQS queue to the SNS topic. Modify the BeginResponse function to publish to the SNS topic when it nishes
running.
C. Create an Amazon Simple Queue Service (Amazon SQS) queue for each Lambda function that needs to run after the BeginResponse
Lambda function runs. Subscribe the Lambda function to the SQS queue. Create an Amazon Simple Notication Service (Amazon SNS)
topic for each SQS queue. Subscribe the SQS queues to the SNS topics. Modify the BeginResponse function to publish to the SNS topics
when the function nishes running.
D. Create an AWS Step Functions Standard Workow. Congure states in the workow to invoke the Lambda functions sequentially. Create
an Amazon Simple Notication Service (Amazon SNS) topic. Modify the BeginResponse Lambda function to publish to the SNS topic
before the Lambda function nishes running. Create a new Lambda function that is subscribed to the SNS topic and that invokes the Step
Functions workow. |  |  |  |  |  |
| 285 | A company operates a globally deployed product out of multiple AWS Regions. The company's DevOps team needs to use Amazon API
Gateway to deploy an API to support the product.
The API must be deployed redundantly. The deployment must provide independent availability from each company location. The deployment
also must respond to a custom domain URL and must optimize performance for the API user requests. | A. Deploy an API Gateway edge-optimized API endpoint in the us-east-1 Region. Create an API Gateway custom domain for the API. Create
an Amazon Route 53 record set with a geoproximity routing policy for the API's custom domain. Increase the geographic bias to the
maximum allowed value.
B. Deploy an API Gateway regional API endpoint in the us-east-1 Region. Integrate the API Gateway API with a public Application Load
Balancer (ALB). Create an AWS Global Accelerator standard accelerator. Associate the endpoint with the ALCreate an Amazon Route 53
alias record set that points the custom domain name to the DNS name that is assigned to the accelerator.
C. Deploy an API Gateway regional API endpoint in every AWS Region where the company's product is deployed. Create an API Gateway
custom domain in each Region for the deployed API Gateway API. Create an Amazon Route 53 record set that has a latency routing policy
for every deployed API Gateway custom domain.
D. Deploy an API Gateway edge-optimized API endpoint in the us-east-1 Region. Create an Amazon CloudFront distribution. Congure the
CloudFront distribution with an alternate domain name. Specify the API Gateway Invoke URL as the origin domain. Create an Amazon
Route 53 alias record set with a simple routing policy. Point the routing policy to the CloudFront distribution domain name. |  |  |  |  |  |
| 286 | A DevOps engineer uses AWS CodeBuild to frequently produce software packages. The CodeBuild project builds large Docker images that the
DevOps engineer can use across multiple builds.
The DevOps engineer wants to improve build performance and minimize costs. | A. Store the Docker images in an Amazon Elastic Container Registry (Amazon ECR) repository. Implement a local Docker layer cache for
CodeBuild.
B. Cache the Docker images in an Amazon S3 bucket that is available across multiple build hosts. Expire the cache by using an S3
Lifecycle policy.
C. Store the Docker images in an Amazon Elastic Container Registry (Amazon ECR) repository. Modify the CodeBuild project runtime
conguration to always use the most recent image version.
D. Create custom AMIs that contain the cached Docker images. In the CodeBuild build, launch Amazon EC2 instances from the custom
AMIs. | 一名DevOps工程师使用AWS CodeBuild来频繁生产软件包。CodeBuild项目构建大型Docker镜像，这些镜像可以在多个构建中重复使用。
DevOps工程师希望提高构建性能并最小化成本。

 | **选项A：将Docker镜像存储在Amazon Elastic Container Registry (Amazon ECR)仓库中。为CodeBuild实现本地Docker层缓存。**
- ✅ **正确选择**
- ECR是AWS原生的容器镜像仓库服务，专为Docker镜像设计
- CodeBuild支持本地Docker层缓存，可以缓存Docker镜像层，避免重复下载相同的层
- 显著提高构建性能，减少网络传输时间和成本
- 符合AWS最佳实践

**选项B：将Docker镜像缓存在可跨多个构建主机使用的Amazon S3存储桶中。使用S3生命周期策略使缓存过期。**
- ❌ **不正确**
- S3不是为Docker镜像存储设计的，缺乏容器镜像的原生支持
- 没有Docker镜像层的去重和优化功能
- 需要额外的脚本来管理镜像的上传/下载
- 不如ECR高效

**选项C：将Docker镜像存储在Amazon Elastic Container Registry (Amazon ECR)仓库中。修改CodeBuild项目运行时配置以始终使用最新的镜像版本。**
- ❌ **不正确**
- 虽然使用ECR是正确的，但始终拉取最新版本会导致每次构建都需要下载完整镜像
- 没有利用缓存机制，无法提高性能或降低成本
- 与题目要求的性能优化目标相反

**选项D：创建包含缓存Docker镜像的自定义AMI。在CodeBuild构建中，从自定义AMI启动Amazon EC2实例。**
- ❌ **不正确**
- CodeBuild是托管服务，不需要也不建议管理底层EC2实例
- 创建和维护自定义AMI增加了复杂性和成本
- 违背了使用托管服务的初衷
- AMI更新和版本管理会带来额外开销

 |  |  |  |
| 287 | A large company recently acquired a small company. The large company invited the small company to join the large company's existing
organization in AWS Organizations as a new OU.
A DevOps engineer determines that the small company needs to launch t3.small Amazon EC2 instance types for the company's application
workloads. The small company needs to deploy the instances only within US-based AWS Regions.
The DevOps engineer needs to use an SCP in the small company's new OU to ensure that the small company can launch only the required
instance types. | A. Congure a statement to deny the ec2:RunInstances action for all EC2 instance resources when the ec2:InstanceType condition is not
equal to t3.small.
Congure another statement to deny the ec2:RunInstances action for all EC2 instance resources when the aws:RequestedRegion condition
is not equal to us-*.
B. Congure a statement to allow the ec2:RunInstances action for all EC2 instance resources when the ec2:InstanceType condition is not
equal to t3.small.
Congure another statement to allow the ec2:RunInstances action for all EC2 instance resources when the aws:RequestedRegion
condition is not equal to us-*.
C. Congure a statement to deny the ec2:RunInstances action for all EC2 instance resources when the ec2:InstanceType condition is equal
to t3.small.
Congure another statement to deny the ec2:RunInstances action for all EC2 instance resources when the aws:RequestedRegion condition
is equal to us-*.
D. Congure a statement to allow the ec2:RunInstances action for all EC2 instance resources when the ec2:InstanceType condition is
equal to t3.small.
Congure another statement to allow the ec2:RunInstances action for all EC2 instance resources when the aws:RequestedRegion
condition is equal to us-*. | 一家大公司最近收购了一家小公司。大公司邀请小公司作为新的组织单元(OU)加入大公司在AWS Organizations中的现有组织。

一名DevOps工程师确定小公司需要为其应用程序工作负载启动t3.small Amazon EC2实例类型。小公司需要仅在美国境内的AWS区域部署实例。

DevOps工程师需要在小公司的新OU中使用服务控制策略(SCP)来确保小公司只能启动所需的实例类型。

 | **选项A：** 
- 配置一个语句，当ec2:InstanceType条件不等于t3.small时，拒绝对所有EC2实例资源执行ec2:RunInstances操作
- 配置另一个语句，当aws:RequestedRegion条件不等于us-*时，拒绝对所有EC2实例资源执行ec2:RunInstances操作
- **分析：** 这个选项使用拒绝(deny)策略，正确地限制了只能使用t3.small实例类型和美国区域

**选项B：**
- 配置一个语句，当ec2:InstanceType条件不等于t3.small时，允许对所有EC2实例资源执行ec2:RunInstances操作
- 配置另一个语句，当aws:RequestedRegion条件不等于us-*时，允许对所有EC2实例资源执行ec2:RunInstances操作
- **分析：** 这个选项使用允许(allow)策略，但逻辑错误。它允许非t3.small实例类型和非美国区域，这与需求相反

**选项C：**
- 配置一个语句，当ec2:InstanceType条件等于t3.small时，拒绝对所有EC2实例资源执行ec2:RunInstances操作
- 配置另一个语句，当aws:RequestedRegion条件等于us-*时，拒绝对所有EC2实例资源执行ec2:RunInstances操作
- **分析：** 这个选项拒绝了我们想要允许的内容（t3.small和美国区域），逻辑完全错误

**选项D：**
- 配置一个语句，当ec2:InstanceType条件等于t3.small时，允许对所有EC2实例资源执行ec2:RunInstances操作
- 配置另一个语句，当aws:RequestedRegion条件等于us-*时，允许对所有EC2实例资源执行ec2:RunInstances操作
- **分析：** SCP主要用于设置权限边界，通常使用拒绝策略而不是允许策略。此外，这种配置可能不会有效限制其他实例类型

 | A |  |  |
| 288 | A DevOps team manages infrastructure for an application. The application uses long-running processes to process items from an Amazon
Simple Queue Service (Amazon SQS) queue. The application is deployed to an Auto Scaling group.
The application recently experienced an issue where items were taking signicantly longer to process. The queue exceeded the expected size,
which prevented various business processes from functioning properly. The application records all logs to a third-party tool.
The team is currently subscribed to an Amazon Simple Notication Service (Amazon SNS) topic that the team uses for alerts. The team needs
to be alerted if the queue exceeds the expected size. | A. Create an Amazon CloudWatch metric alarm with a period of 1 hour and a static threshold to alarm if the average of the
ApproximateNumberOfMessagesDelayed metric is greater than the expected value. Congure the alarm to notify the SNS topic.
B. Create an Amazon CloudWatch metric alarm with a period of 1 hour and a static threshold to alarm if the sum of the
ApproximateNumberOfMessagesVisible metric is greater than the expected value. Congure the alarm to notify the SNS topic.
C. Create an AWS Lambda function that retrieves the ApproximateNumberOfMessages SQS queue attribute value and publishes the value
as a new CloudWatch custom metric. Create an Amazon EventBridge rule that is scheduled to run every 5 minutes and that invokes the
Lambda function. Congure a CloudWatch metrics alarm with a period of 1 hour and a static threshold to alarm if the sum of the new
custom metric is greater than the expected value.
D. Create an AWS Lambda function that checks the ApproximateNumberOfMessagesDelayed SQS queue attribute and compares the value
to a dened expected size in the function. Create an Amazon EventBridge rule that is scheduled to run every 5 minutes and that invokes
the Lambda function. When the ApproximateNumberOfMessagesDelayed SQS queue attribute exceeds the expected size, send a
notication the SNS topic. | 一个DevOps团队管理应用程序的基础设施。该应用程序使用长时间运行的进程来处理Amazon Simple Queue Service (Amazon SQS)队列中的项目。应用程序部署在Auto Scaling组中。

该应用程序最近遇到了一个问题，项目处理时间显著延长。队列超过了预期大小，这阻止了各种业务流程正常运行。应用程序将所有日志记录到第三方工具中。

团队目前订阅了一个Amazon Simple Notification Service (Amazon SNS)主题，用于接收警报。团队需要在队列超过预期大小时收到警报。

 | **选项A：** 创建Amazon CloudWatch指标警报，周期为1小时，使用静态阈值，当ApproximateNumberOfMessagesDelayed指标的平均值大于预期值时触发警报。配置警报通知SNS主题。
- **问题：** ApproximateNumberOfMessagesDelayed指标表示的是延迟消息数量（通常用于FIFO队列的延迟传递），不是队列中总消息数量。对于监控队列大小来说，这不是合适的指标。

**选项B：** 创建Amazon CloudWatch指标警报，周期为1小时，使用静态阈值，当ApproximateNumberOfMessagesVisible指标的总和大于预期值时触发警报。配置警报通知SNS主题。
- **优点：** ApproximateNumberOfMessagesVisible是监控队列大小的正确指标，表示队列中可见消息的数量。使用原生CloudWatch指标，简单直接。
- **注意：** 使用"sum"统计可能不太合适，通常应该使用"average"或"maximum"。

**选项C：** 创建AWS Lambda函数检索ApproximateNumberOfMessages SQS队列属性值，并将其发布为新的CloudWatch自定义指标。创建Amazon EventBridge规则，每5分钟运行一次并调用Lambda函数。配置CloudWatch指标警报，周期为1小时，使用静态阈值。
- **问题：** 过度复杂化。SQS已经提供了原生的CloudWatch指标，不需要创建自定义指标。增加了不必要的Lambda函数和EventBridge规则。

**选项D：** 创建AWS Lambda函数检查ApproximateNumberOfMessagesDelayed SQS队列属性，并与函数中定义的预期大小进行比较。创建Amazon EventBridge规则，每5分钟运行一次并调用Lambda函数。当ApproximateNumberOfMessagesDelayed超过预期大小时，发送通知到SNS主题。
- **问题：** 同选项A，使用了错误的指标（ApproximateNumberOfMessagesDelayed）。同时过度复杂化，不需要自定义Lambda解决方案。

 |  |  |  |
| 289 | A large company runs critical workloads in multiple AWS accounts. The AWS accounts are managed under AWS Organizations with all features
enabled. The company stores condential customer data in an Amazon S3 bucket. Access to the S3 bucket requires multiple levels of
approval.
The company wants to monitor when the S3 bucket is accessed by using the AWS CLI. The company also wants insights into the various
activities performed by other users on all other S3 buckets in the AWS accounts to detect any issues. | A. Create an AWS CloudTrail trail that is delivered to Amazon CloudWatch in each AWS account. Enable data events logs for all S3 buckets.
Use Amazon GuardDuty for anomaly detection in all the AWS accounts. Use Amazon Athena to perform SQL queries on the custom metrics
created from the CloudTrail logs.
B. Create an AWS CloudTrail organization trail that is delivered to Amazon CloudWatch in the Organizations management account. Enable
data events logs for all S3 buckets. Use Amazon CloudWatch anomaly detection in all the AWS accounts. Use Amazon Athena to perform
SQL queries on the custom metrics created from the CloudTrail logs.
C. Create an AWS CloudTrail organization trail that is delivered to Amazon CloudWatch in the Organizations management account. Enable
data events logs for all S3 buckets. Use Amazon CloudWatch anomaly detection in all the AWS accounts. Use Amazon CloudWatch Metrics
Insights to perform SQL queries on the custom metrics created from the CloudTrail logs.
D. Create an AWS CloudTrail trail that is delivered to Amazon CloudWatch in each AWS account. Enable data events logs for all S3 buckets.
Use a custom solution for anomaly detection in all the AWS accounts. Use Amazon CloudWatch Metrics Insights to perform SQL queries on
the custom metrics created from the CloudTrail logs. |  |  |  |  |  |
| 290 | A DevOps team is deploying microservices for an application on an Amazon Elastic Kubernetes Service (Amazon EKS) cluster. The cluster uses
managed node groups. The DevOps team wants to enable auto scaling for the microservice Pods based on a specic CPU utilization
percentage. The DevOps team has already installed the Kubernetes Metrics Server on the cluster. | A. Edit the Auto Scaling group that is associated with the worker nodes of the EKS cluster. Congure the Auto Scaling group to use a
target tracking scaling policy to scale when the average CPU utilization of the Auto Scaling group reaches a specic percentage.
B. Deploy the Kubernetes Horizontal Pod Autoscaler (HPA) and the Kubernetes Vertical Pod Autoscaler (VPA) in the cluster. Congure the
HPA to scale based on the target CPU utilization percentage. Congure the VPA to use the recommender mode setting.
C. Run the AWS Systems Manager AWS-UpdateEKSManagedNodeGroup Automation document. Modify the values for
NodeGroupDesiredSize, NodeGroupMaxSize, and NodeGroupMinSize to be based on an estimate for the required node size.
D. Deploy the Kubernetes Horizontal Pod Autoscaler (HPA) and the Kubernetes Cluster Autoscaler in the cluster. Congure the HPA to
scale based on the target CPU utilization percentage. Congure the Cluster Autoscaler to use the auto-discovery setting. | 一个DevOps团队正在Amazon Elastic Kubernetes Service (Amazon EKS)集群上为应用程序部署微服务。该集群使用托管节点组。DevOps团队希望基于特定的CPU利用率百分比为微服务Pod启用自动扩缩容。DevOps团队已经在集群上安装了Kubernetes Metrics Server。

 | **选项A：** 编辑与EKS集群工作节点关联的Auto Scaling组。配置Auto Scaling组使用目标跟踪扩缩容策略，当Auto Scaling组的平均CPU利用率达到特定百分比时进行扩缩容。
- **错误**：这种方法只能扩缩容节点，而不能扩缩容Pod。题目要求的是基于CPU利用率对微服务Pod进行自动扩缩容，而不是对节点进行扩缩容。

**选项B：** 在集群中部署Kubernetes水平Pod自动扩缩容器(HPA)和Kubernetes垂直Pod自动扩缩容器(VPA)。配置HPA基于目标CPU利用率百分比进行扩缩容。配置VPA使用推荐器模式设置。
- **部分正确但不完整**：HPA确实可以基于CPU利用率扩缩容Pod，这满足了题目要求。但是VPA主要用于调整Pod的资源请求和限制，而不是扩缩容Pod数量。更重要的是，这个选项没有考虑到当Pod扩容时可能需要更多节点的情况。

**选项C：** 运行AWS Systems Manager AWS-UpdateEKSManagedNodeGroup自动化文档。修改NodeGroupDesiredSize、NodeGroupMaxSize和NodeGroupMinSize的值，基于所需节点大小的估算。
- **错误**：这是手动调整节点组大小，不是自动扩缩容解决方案。题目要求的是基于CPU利用率的自动扩缩容，而不是手动调整。

**选项D：** 在集群中部署Kubernetes水平Pod自动扩缩容器(HPA)和Kubernetes集群自动扩缩容器。配置HPA基于目标CPU利用率百分比进行扩缩容。配置集群自动扩缩容器使用自动发现设置。
- **正确**：这是完整的解决方案。HPA负责基于CPU利用率自动扩缩容Pod数量，集群自动扩缩容器负责在需要更多节点时自动添加节点，在节点利用率低时自动移除节点。两者配合使用可以实现完整的自动扩缩容解决方案。

 |  |  |  |
| 291 | A company has multiple AWS accounts. The company uses AWS IAM Identity Center that is integrated with a third-party SAML 2.0 identity
provider (IdP).
The attributes for access control feature is enabled in IAM Identity Center. The attribute mapping list maps the department key from the IdP
to the ${path:enterprise.department} attribute. All existing Amazon EC2 instances have a d1, d2, d3 department tag that corresponds to three
company’s departments.
A DevOps engineer must create policies based on the matching attributes. The policies must grant each user access to only the EC2 instances
that are tagged with the user’s respective department name. | A. 
B. 
C. 
D.  | 一家公司拥有多个AWS账户。该公司使用与第三方SAML 2.0身份提供商(IdP)集成的AWS IAM Identity Center。

IAM Identity Center中启用了访问控制属性功能。属性映射列表将IdP中的department键映射到${path:enterprise.department}属性。所有现有的Amazon EC2实例都有d1、d2、d3部门标签，对应公司的三个部门。

DevOps工程师必须基于匹配属性创建策略。这些策略必须授予每个用户仅访问标记有用户各自部门名称的EC2实例的权限。

 | 由于选项内容为空，我无法逐一分析具体选项。但基于题目要求，正确的解决方案应该包含以下要素：

**需要的解决方案特征：**
- 使用基于属性的访问控制(ABAC)
- 利用${path:enterprise.department}属性
- 创建条件策略匹配EC2实例的department标签
- 确保用户只能访问其部门对应的EC2实例

**可能的策略示例：**
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeInstances",
        "ec2:StartInstances",
        "ec2:StopInstances"
      ],
      "Resource": "*",
      "Condition": {
        "StringEquals": {
          "ec2:ResourceTag/department": "${path:enterprise.department}"
        }
      }
    }
  ]
}
```

 |  |  |  |
| 292 | A security team wants to use AWS CloudTrail to monitor all actions and API calls in multiple accounts that are in the same organization in
AWS Organizations. The security team needs to ensure that account users cannot turn off CloudTrail in the accounts. | A. Apply an SCP to all OUs to deny the cloudtrail:StopLogging action and the cloudtrail:DeleteTrail action.
B. Create IAM policies in each account to deny the cloudtrail:StopLogging action and the cloudtrail:DeleteTrail action.
C. Set up Amazon CloudWatch alarms to notify the security team when a user disables CloudTrail in an account.
D. Use AWS Cong to automatically re-enable CloudTrail if a user disables CloudTrail in an account. | 安全团队希望使用AWS CloudTrail来监控AWS Organizations中同一组织内多个账户中的所有操作和API调用。安全团队需要确保账户用户无法在这些账户中关闭CloudTrail。

 | **A. 对所有OU应用SCP来拒绝cloudtrail:StopLogging操作和cloudtrail:DeleteTrail操作。**
- 这是最有效的解决方案
- SCP（Service Control Policy）在组织级别工作，可以强制限制所有成员账户的权限
- 即使账户管理员也无法绕过SCP的限制
- 直接阻止了关闭CloudTrail的两个关键操作

**B. 在每个账户中创建IAM策略来拒绝cloudtrail:StopLogging操作和cloudtrail:DeleteTrail操作。**
- 这种方法存在重大缺陷
- 账户管理员可以修改或删除这些IAM策略
- 无法提供真正的强制保护
- 管理复杂度高，需要在每个账户中单独配置

**C. 设置Amazon CloudWatch告警，当用户在账户中禁用CloudTrail时通知安全团队。**
- 这只是监控和通知机制，不能预防问题发生
- 无法阻止用户关闭CloudTrail
- 属于事后响应而非预防措施

**D. 使用AWS Config在用户禁用CloudTrail时自动重新启用CloudTrail。**
- 题目中"AWS Con g"应该是"AWS Config"的错误拼写
- 这是补救措施而非预防措施
- 存在时间窗口，CloudTrail可能会被暂时关闭
- 无法完全满足"确保用户无法关闭"的要求

 |  |  |  |
| 293 | A DevOps engineer needs to congure a blue/green deployment for an existing three-tier application. The application runs on Amazon EC2
instances and uses an Amazon RDS database. The EC2 instances run behind an Application Load Balancer (ALB) and are in an Auto Scaling
group.
The DevOps engineer has created launch templates, Auto Scaling groups, and ALB target groups for the blue environment and the green
environment. Each target group species which application version, blue or green, will be loaded on the EC2 instances. An Amazon Route 53
record for www.example.com points to the AL | B. 
A. Starta rolling restart of the Auto Scaling group for the green environment to deploy the new application version to the green
environment's EC2 instances. When the rolling restart is complete, use an AWS CLI command to update the ALB to send trac to the
green environment's target group.
C. Update the launch template to deploy the green environment's application version to the blue environment's EC2 instances. Do not
change the target groups or the Auto Scaling groups in either environment. Perform a rolling restart of the blue environments EC2
instances.
D. Starta rolling restart of the Auto Scaling group for the green environment to deploy the new application version to the green
environment's EC2 instances. When the rolling restart is complete, update Route 53 to point to the green environment's endpoint on the
AL | 一名DevOps工程师需要为现有的三层应用程序配置蓝/绿部署。该应用程序运行在Amazon EC2实例上，并使用Amazon RDS数据库。EC2实例运行在应用程序负载均衡器(ALB)后面，并位于Auto Scaling组中。

DevOps工程师已经为蓝环境和绿环境创建了启动模板、Auto Scaling组和ALB目标组。每个目标组指定将在EC2实例上加载哪个应用程序版本（蓝色或绿色）。Amazon Route 53记录www.example.com指向ALB。

 | **选项A：** （题目中未完整显示）

**选项B：** 启动绿环境Auto Scaling组的滚动重启，将新应用程序版本部署到绿环境的EC2实例。当滚动重启完成后，使用AWS CLI命令更新ALB，将流量发送到绿环境的目标组。
- 这个方案有问题，因为在ALB层面切换流量不是标准的蓝/绿部署做法
- 直接修改ALB配置可能导致流量中断
- 不符合蓝/绿部署的最佳实践

**选项C：** 更新启动模板，将绿环境的应用程序版本部署到蓝环境的EC2实例。不更改任一环境中的目标组或Auto Scaling组。对蓝环境的EC2实例执行滚动重启。
- 这实际上是滚动部署，而不是蓝/绿部署
- 违背了蓝/绿部署的核心原则（保持两个独立环境）
- 没有利用已创建的绿环境基础设施

**选项D：** 启动绿环境Auto Scaling组的滚动重启，将新应用程序版本部署到绿环境的EC2实例。当滚动重启完成后，更新Route 53指向ALB上的绿环境端点。
- 符合蓝/绿部署的标准流程
- 在DNS层面进行流量切换，更加安全可控
- 保持了两个独立环境的完整性
- 允许快速回滚（通过DNS切换回蓝环境）

 |  |  |  |
| 294 | A company has an application that runs on Amazon EC2 instances in an Auto Scaling group. The application processes a high volume of
messages from an Amazon Simple Queue Service (Amazon SQS) queue.
A DevOps engineer noticed that the application took several hours to process a group of messages from the SQS queue. The average CPU
utilization of the Auto Scaling group did not cross the threshold of a target tracking scaling policy when processing the messages. The
application that processes the SQS queue publishes logs to ‘Amazon CloudWatch Logs.
The DevOps engineer needs to ensure that the queue is processed quickly. | A. Create an AWS Lambda function. Congure the Lambda function to publish a custom metric by using the
ApproximateNumberOfMessagesVisible SQS queue attribute and the GroupInServiceInstances Auto Scaling group attribute to publish the
queue messages for each instance. Schedule an Amazon EventBridge rule to run the Lambda function every hour. Create a target tracking
scaling policy for the Auto Scaling group that uses the custom metric to scale in and out.
B. Create an AWS Lambda function. Congure the Lambda function to publish a custom metric by using the
ApproximateNumberOfMessagesVisible SQS queue attribute and the GroupInServiceInstances Auto Scaling group attribute to publish the
queue messages for each instance. Create a CloudWatch subscription lter for the application logs with the Lambda function as the
target. Create a target tracking scaling policy for the Auto Scaling group that uses the custom metric to scale in and out.
C. Create a target tracking scaling policy for the Auto Scaling group. In the target tracking policy, use the
ApproximateNumberOfMessagesVisible SQS queue attribute and the GroupInServiceInstances Auto Scaling group attribute to calculate
how many messages are in the queue for each number of instances by using metric math. Use the calculated attribute to scale in and out.
D. Create an AWS Lambda function that logs the ApproximateNumberOfMessagesVisible attribute of the SQS queue to a CloudWatch Logs
log group. Schedule an Amazon EventBridge rule to run the Lambda function every 5 minutes. Create a metric ler to count the number of
log events from a CloudWatch logs group. Create a target tracking scaling policy for the Auto Scaling group that uses the custom metric to
scale in and out. | 一家公司有一个运行在Auto Scaling组中Amazon EC2实例上的应用程序。该应用程序处理来自Amazon Simple Queue Service (Amazon SQS)队列的大量消息。

一位DevOps工程师注意到，应用程序花费了几个小时来处理SQS队列中的一组消息。在处理消息时，Auto Scaling组的平均CPU利用率没有超过目标跟踪扩展策略的阈值。处理SQS队列的应用程序将日志发布到Amazon CloudWatch Logs。

DevOps工程师需要确保队列能够快速处理。

 | **选项A：** 创建AWS Lambda函数，配置Lambda函数使用ApproximateNumberOfMessagesVisible SQS队列属性和GroupInServiceInstances Auto Scaling组属性发布自定义指标，计算每个实例的队列消息数。安排Amazon EventBridge规则每小时运行Lambda函数。为Auto Scaling组创建使用自定义指标进行扩缩的目标跟踪扩展策略。
- **问题：** 每小时运行一次频率太低，无法及时响应队列消息的变化，不能满足快速处理的需求。

**选项B：** 创建AWS Lambda函数，配置Lambda函数使用ApproximateNumberOfMessagesVisible SQS队列属性和GroupInServiceInstances Auto Scaling组属性发布自定义指标，计算每个实例的队列消息数。为应用程序日志创建CloudWatch订阅过滤器，以Lambda函数为目标。为Auto Scaling组创建使用自定义指标进行扩缩的目标跟踪扩展策略。
- **问题：** 使用日志订阅过滤器触发Lambda函数的逻辑不合理，这种方式无法准确反映队列消息数量的变化。

**选项C：** 为Auto Scaling组创建目标跟踪扩展策略。在目标跟踪策略中，使用ApproximateNumberOfMessagesVisible SQS队列属性和GroupInServiceInstances Auto Scaling组属性，通过指标数学计算每个实例对应的队列消息数量。使用计算出的属性进行扩缩。
- **优势：** 直接使用CloudWatch指标数学功能，无需额外的Lambda函数，实时性好，架构简单高效。

**选项D：** 创建AWS Lambda函数，将SQS队列的ApproximateNumberOfMessagesVisible属性记录到CloudWatch Logs日志组。安排Amazon EventBridge规则每5分钟运行Lambda函数。创建指标过滤器统计CloudWatch日志组中的日志事件数量。为Auto Scaling组创建使用自定义指标进行扩缩的目标跟踪扩展策略。
- **问题：** 架构过于复杂，通过日志记录再创建指标过滤器的方式效率低下，且5分钟的间隔仍然可能导致响应延迟。

 |  |  |  |
| 295 | A company has a single AWS account that runs hundreds of Amazon EC2 instances in a single AWS Region. The company launches and
terminates new EC2 instances every hour. The account includes existing EC2 instances that have been running for longer than a week.
The company's security policy requires all running EC2 instances to have an EC2 instance prole attached. The company has created a default
EC2 instance prole. The default EC2 instance prole must be attached to any EC2 instances that do not have a prole attached. | A. Congure an Amazon EventBridge rule that matches the Amazon EC2 RunInstances API calls. Congure the rule to invoke an AWS
Lambda function to attach the default instance prole to the EC2 instances.
B. Congure AWS Cong. Deploy an AWS Cong ec2-instance-prole-attached managed rule. Congure an automatic remediation action
that invokes an AWS Systems Manager Automation runbook to attach the default instance prole to the EC2 instances.
C. Congure an Amazon EventBridge rule that matches the Amazon EC2 StartInstances API calls. Congure the rule to invoke an AWS
Systems Manager Automation runbook to attach the default instance prole to the EC2 instances.
D. Congure AWS Cong. Deploy an AWS Cong iam-role-managed-policy-check managed rule. Congure an automatic remediation action
that invokes an AWS Lambda function to attach the default instance prole to the EC2 instances. |  |  |  |  |  |
| 296 | A company uses AWS Organizations to manage hundreds of AWS accounts. The company has a team that is responsible for AWS Identity and
Access Management (IAM).
The IAM team wants to implement AWS IAM Identity Center. The IAM team must have only the minimum required permissions to manage IAM
Identity Center. The IAM team must not be able to gain unnecessary access to the Organizations management account. The IAM team must
be able to provision new IAM Identity Center permission sets and assignments for new and existing member accounts. | A. Create a new AWS account for the IAM team. Enable IAM Identity Center in the new account. In the Organizations management
account, register the new account as a delegated administrator for IAM Identity Center.
B. Create a new AWS account for the IAM team. Enable IAM Identity Center in the Organizations management account. In the
Organizations management account, register the new account as a delegated administrator for IAM Identity Center.
C. Create an SCP in Organizations. Create a new OU for the Organizations management account, and link the new SCP to the OU.
Congure the SCP to deny all access to IAM Identity Center.
D. Create IAM users and an IAM group for the IAM team in IAM Identity Center. Add the users to the group. Create a new permission set.
Attach the AWSSSOMemberAccountAdministrator managed IAM policy to the group.
E. Assign the new permission set to the Organizations management account. Allow the IAM team's group to use the permission set.
F. Assign the new permission set to the new AWS account. Allow the IAM team's group to use the permission set. |  |  |  |  |  |
| 297 | A company uses an Amazon Aurora PostgreSQL global database that has two secondary AWS Regions. A DevOps engineer has congured the
database parameter group to guarantee an RPO of 60 seconds. Write operations on the primary cluster are occasionally blocked because of
the RPO setting.
The DevOps engineer needs to reduce the frequency of blocked write operations. | A. Add an additional secondary cluster to the global database.
B. Enable write forwarding for the global database.
C. Remove one of the secondary clusters from the global database.
D. Congure synchronous replication for the global database. | 一家公司使用Amazon Aurora PostgreSQL全球数据库，该数据库有两个辅助AWS区域。DevOps工程师已配置数据库参数组以保证60秒的RPO（恢复点目标）。由于RPO设置，主集群上的写操作偶尔会被阻塞。

DevOps工程师需要减少写操作被阻塞的频率。

 | **A. 向全球数据库添加额外的辅助集群**
- 错误。增加更多辅助集群实际上会增加复制的复杂性和延迟
- 更多的辅助集群意味着主集群需要等待更多区域的确认，这会增加而不是减少写操作被阻塞的频率
- 这与解决问题的目标相反

**B. 为全球数据库启用写转发功能**
- 错误。写转发（write forwarding）允许辅助集群接收写请求并转发到主集群
- 这个功能主要是为了改善应用程序的写入体验，但不会解决RPO导致的写阻塞问题
- 写转发不会改变底层的复制机制和RPO约束

**C. 从全球数据库中移除一个辅助集群**
- 正确。减少辅助集群数量可以减少复制延迟和复杂性
- 较少的辅助集群意味着主集群需要等待确认的区域更少
- 这可以减少因RPO设置而导致的写操作阻塞频率
- 虽然会降低一些灾难恢复能力，但可以改善写性能

**D. 为全球数据库配置同步复制**
- 错误。同步复制会使情况变得更糟
- 同步复制要求所有写操作必须在所有辅助区域确认后才能提交
- 这会显著增加延迟和写操作被阻塞的频率，而不是减少

 |  |  |  |
| 298 | A company has a web application that is hosted on an Amazon Elastic Kubernetes Service (Amazon EKS) cluster. The EKS cluster runs on AWS
Fargate that is available through an internet-facing Application Load Balancer.
The application is experiencing stability issues that lead to longer response times. A DevOps engineer needs to congure observability in
Amazon CloudWatch to troubleshoot the issue. The solution must provide only the minimum necessary permissions. | A. Deploy the CloudWatch agent as a Kubernetes StatefulSet to the EKS cluster.
B. Deploy the AWS Distro for OpenTelemetry Collector as a Kubernetes DaemonSet to the EKS cluster.
C. Associate a Kubernetes service account with an IAM role by using IAM roles for service accounts in Amazon EKS. Use the
CloudWatchAgentServerPolicy AWS managed policy.
D. Associate a Kubernetes service account with an IAM role by using IAM roles for service accounts in Amazon EKS. Use the
CloudWatchAgentAdminPolicy AWS managed policy.
E. Congure an IAM OpenID Connect (OIDC) provider for the EKS cluster.
F. Enable EKS control plane logging for the EKS cluster. |  |  |  |  |  |
| 299 | A company stores its Python-based application code in AWS CodeCommit. The company uses AWS CodePipeline to deploy the application. The
CodeCommit repository and the CodePipeline pipeline are deployed to the same AWS account.
The company's security team requires all code to be scanned for vulnerabilities before the code is deployed to production. If any
vulnerabilities are found, the deployment must stop. | A. Create a new CodeBuild project. Congure the project to run a security scan on the code by using Amazon CodeGuru Security. Congure
the CodeBuild project to raise an error if CodeGuru Security nds vulnerabilities. Create a new IAM role that has sucient permissions to
run CodeGuru Security scans. Assign the role to the CodeBuild project. In the CodePipeline pipeline, add a new stage before the
deployment stage. Select AWS CodeBuild as the action provider for the new stage. Use the source artifact from the CodeCommit
repository. Congure the action to use the CodeBuild project.
B. Create a new CodeBuild project. Congure the project to run a security scan on the code by using Amazon Inspector. Congure the
CodeBuild project to raise an error if Amazon Inspector nds vulnerabilities. Create a new IAM role that has sucient permissions to run
Amazon Inspector scans. Assign the role to the CodeBuild project. In the CodePipeline pipeline, add a new stage before the deployment
stage. Select AWS CodeBuild as the action provider for the new stage. Use the source artifact from the CodeCommit repository. Congure
the action to use the CodeBuild project.
C. Update the IAM role that is attached to CodePipeline to include sucient permissions to invoke Amazon DevOps Guru. In the
CodePipeline pipeline, add a new stage before the deployment stage. Select DevOps Guru as the action provider for the new stage. Use
the source artifact from the CodeCommit repository.
D. Update the IAM role that is attached to CodePipeline to include sucient permissions to invoke Amazon DevOps Guru. In the
CodePipeline pipeline, add a new stage before the deployment stage. Select CodeGuru Security as the action provider for the new stage.
Use the source artifact from the CodeCommit repository. | 一家公司将其基于Python的应用程序代码存储在AWS CodeCommit中。该公司使用AWS CodePipeline来部署应用程序。CodeCommit存储库和CodePipeline管道部署在同一个AWS账户中。

公司的安全团队要求在代码部署到生产环境之前，必须对所有代码进行漏洞扫描。如果发现任何漏洞，部署必须停止。

 | **选项A：** 创建一个新的CodeBuild项目，配置项目使用Amazon CodeGuru Security对代码进行安全扫描。如果CodeGuru Security发现漏洞，配置CodeBuild项目抛出错误。创建一个具有足够权限运行CodeGuru Security扫描的新IAM角色，并将该角色分配给CodeBuild项目。在CodePipeline管道中，在部署阶段之前添加一个新阶段，选择AWS CodeBuild作为新阶段的操作提供者，使用来自CodeCommit存储库的源工件，配置操作使用CodeBuild项目。

**选项B：** 创建一个新的CodeBuild项目，配置项目使用Amazon Inspector对代码进行安全扫描。如果Amazon Inspector发现漏洞，配置CodeBuild项目抛出错误。创建一个具有足够权限运行Amazon Inspector扫描的新IAM角色，并将该角色分配给CodeBuild项目。在CodePipeline管道中，在部署阶段之前添加一个新阶段，选择AWS CodeBuild作为新阶段的操作提供者，使用来自CodeCommit存储库的源工件，配置操作使用CodeBuild项目。

**选项C：** 更新附加到CodePipeline的IAM角色，包含足够的权限来调用Amazon DevOps Guru。在CodePipeline管道中，在部署阶段之前添加一个新阶段，选择DevOps Guru作为新阶段的操作提供者，使用来自CodeCommit存储库的源工件。

**选项D：** 更新附加到CodePipeline的IAM角色，包含足够的权限来调用Amazon DevOps Guru。在CodePipeline管道中，在部署阶段之前添加一个新阶段，选择CodeGuru Security作为新阶段的操作提供者，使用来自CodeCommit存储库的源工件。

 |  |  |  |
| 300 | A DevOps engineer deploys an application to a eet of Amazon Linux EC2 instances. The DevOps engineer needs to monitor system metrics
across the eet. The DevOps engineer wants to monitor the relationship between network trac and memory utilization for the application
code. The DevOps engineer wants to track the data on a 60 second interval. | A. Use Amazon CloudWatch basic monitoring to collect the NetworkIn metric and the MemoryBytesUsed metric. Graph the metrics in
CloudWatch.
B. Use Amazon CloudWatch detailed monitoring to collect the NetworkIn metric and the MemoryBytesUsed metric. Graph the metrics in
CloudWatch.
C. Use Amazon CloudWatch detailed monitoring to collect the NetworkIn metric. Install the CloudWatch agent on the EC2 instances to
collect the mem_used metric. Graph the metrics in CloudWatch.
D. Use Amazon CloudWatch basic monitoring to collect the built-in NetworkIn metric. Install the CloudWatch agent on the EC2 instances to
collect the mem_used metric. Graph the metrics in CloudWatch. | 一名DevOps工程师将应用程序部署到一组Amazon Linux EC2实例上。该DevOps工程师需要监控整个实例组的系统指标。DevOps工程师希望监控应用程序代码的网络流量和内存利用率之间的关系。DevOps工程师希望以60秒的间隔跟踪数据。

 | **选项A：使用Amazon CloudWatch基础监控收集NetworkIn指标和MemoryBytesUsed指标。在CloudWatch中绘制指标图表。**
- 错误：CloudWatch基础监控不提供MemoryBytesUsed指标
- 错误：基础监控的数据收集间隔是5分钟，不符合60秒要求
- NetworkIn指标确实是CloudWatch的内置指标

**选项B：使用Amazon CloudWatch详细监控收集NetworkIn指标和MemoryBytesUsed指标。在CloudWatch中绘制指标图表。**
- 错误：即使是详细监控，CloudWatch也不提供MemoryBytesUsed作为内置指标
- 正确：详细监控可以提供1分钟间隔的数据收集，符合60秒要求
- 正确：NetworkIn是CloudWatch的内置指标

**选项C：使用Amazon CloudWatch详细监控收集NetworkIn指标。在EC2实例上安装CloudWatch代理来收集mem_used指标。在CloudWatch中绘制指标图表。**
- 正确：详细监控提供1分钟间隔的NetworkIn指标
- 正确：CloudWatch代理可以收集自定义内存指标（mem_used）
- 正确：CloudWatch代理可以配置为1分钟间隔收集数据
- 正确：两个指标都可以在CloudWatch中绘制图表

**选项D：使用Amazon CloudWatch基础监控收集内置的NetworkIn指标。在EC2实例上安装CloudWatch代理来收集mem_used指标。在CloudWatch中绘制指标图表。**
- 错误：基础监控的数据收集间隔是5分钟，不符合60秒要求
- 正确：CloudWatch代理可以收集mem_used指标
- 问题：基础监控和代理收集的数据间隔不匹配

 |  |  |  |
| 301 | A company uses AWS Systems Manager to manage a eet of Amazon Linux EC2 instances that have SSM Agent installed. All EC2 instances
are congured to use Instance Metadata Service Version 2 (IMDSv2) and are running in the same AWS account and AWS Region. Company
policy requires developers to use only Amazon Linux.
The company wants to ensure that all new EC2 instances are automatically managed by Systems Manager after creation. | A. Create an IAM role that has a trust policy that allows Systems Manager to assume the role. Attach the
AmazonSSMManagedEC2InstanceDefaultPolicy policy to the role. Congure the default-ec2-instance-management-role SSM service
setting to use the role.
B. Ensure that AWS Cong is set up. Create an AWS Cong rule that validates if an EC2 instance has SSM Agent installed. Congure the
rule to run on EC2 conguration changes. Congure automatic remediation for the rule to run the AWS-InstallSSMAgent SSM document to
install SSM Agent.
C. Congure Systems Manager Patch Manager. Create a patch baseline that automatically installs SSM Agent on all new EC2 instances.
Create a patch group for all EC2 instances. Attach the patch baseline to the patch group. Create a maintenance window and maintenance
window task to start installing SSM Agent daily.
D. Create an EC2 instance role that has a trust policy that allows Amazon EC2 to assume the role. Attach the
AmazonSSMManagedInstanceCore policy to the role. Ensure that AWS Cong is set up. Use the ec2-instance-prole-attached managed
AWS Cong rule to validate if an EC2 instance has the role attached. Congure the rule to run on EC2 conguration changes. Congure
automatic remediation for the rule to run the AWS-SetupManagedRoleOnEc2Instance SSM document to attach the role to the EC2
instance. | 一家公司使用AWS Systems Manager来管理一组已安装SSM Agent的Amazon Linux EC2实例。所有EC2实例都配置为使用实例元数据服务版本2（IMDSv2），并在同一个AWS账户和AWS区域中运行。公司政策要求开发人员只能使用Amazon Linux。

该公司希望确保所有新的EC2实例在创建后都能自动被Systems Manager管理。

 | **选项A：** 创建一个IAM角色，该角色具有允许Systems Manager承担该角色的信任策略。将AmazonSSMManagedEC2InstanceDefaultPolicy策略附加到该角色。配置default-ec2-instance-management-role SSM服务设置以使用该角色。

- 这个选项利用了Systems Manager的默认实例管理功能
- default-ec2-instance-management-role是一个有效的SSM服务设置
- 但是AmazonSSMManagedEC2InstanceDefaultPolicy策略名称不正确，应该是AmazonSSMManagedInstanceCore
- 信任策略也应该允许EC2服务而不是Systems Manager服务承担角色

**选项B：** 确保设置了AWS Config。创建一个AWS Config规则来验证EC2实例是否安装了SSM Agent。配置规则在EC2配置更改时运行。为规则配置自动修复，运行AWS-InstallSSMAgent SSM文档来安装SSM Agent。

- 题目已经说明所有EC2实例都已安装SSM Agent
- 问题不在于安装SSM Agent，而在于确保实例能被Systems Manager管理
- 这需要正确的IAM角色和权限，而不仅仅是安装Agent

**选项C：** 配置Systems Manager Patch Manager。创建一个补丁基线，自动在所有新EC2实例上安装SSM Agent。为所有EC2实例创建补丁组。将补丁基线附加到补丁组。创建维护窗口和维护窗口任务，每天开始安装SSM Agent。

- Patch Manager用于补丁管理，不是用来安装SSM Agent的
- 题目已说明实例已安装SSM Agent
- 这个方案不能解决自动管理新实例的问题

**选项D：** 创建一个EC2实例角色，该角色具有允许Amazon EC2承担该角色的信任策略。将AmazonSSMManagedInstanceCore策略附加到该角色。确保设置了AWS Config。使用ec2-instance-profile-attached托管AWS Config规则来验证EC2实例是否附加了该角色。配置规则在EC2配置更改时运行。为规则配置自动修复，运行AWS-SetupManagedRoleOnEc2Instance SSM文档将角色附加到EC2实例。

- 正确创建了EC2实例角色，信任策略允许EC2服务承担角色
- 使用了正确的AmazonSSMManagedInstanceCore策略
- 使用AWS Config规则监控实例是否有正确的角色
- 通过自动修复确保新实例自动获得必要的角色

 | D |  |  |
| 302 | A company congured an Amazon S3 event source for an AWS Lambda function. The company needs the Lambda function to run when a new
object is created or an existing object is modied in a specic S3 bucket. The Lambda function will use the S3 bucket name and the S3 object
key of the incoming event to read the contents of the new or modied S3 object. The Lambda function will parse the contents and save the
parsed contents to an Amazon DynamoDB table.
The Lambda function's execution role has permissions to read from the S3 bucket and to write to the DynamoDB table. During testing, a
DevOps engineer discovers that the Lambda function does not run when objects are added to the S3 bucket or when existing objects are
modied. | A. Create an S3 bucket policy for the S3 bucket that grants the S3 bucket permission to invoke the Lambda function.
B. Create a resource policy for the Lambda function to grant Amazon S3 permission to invoke the Lambda function on the S3 bucket.
C. Congure an Amazon Simple Queue Service (Amazon SQS) queue as an OnFailure destination for the Lambda function. Update the
Lambda function to process messages from the SQS queue and the S3 event notications.
D. Congure an Amazon Simple Queue Service (Amazon SQS) queue as the destination for the S3 bucket event notications. Update the
Lambda function's execution role to have permission to read from the SQS queue. Update the Lambda function to consume messages
from the SQS queue. | 一家公司为AWS Lambda函数配置了Amazon S3事件源。公司需要Lambda函数在特定S3存储桶中创建新对象或修改现有对象时运行。Lambda函数将使用传入事件的S3存储桶名称和S3对象键来读取新建或修改的S3对象内容。Lambda函数将解析内容并将解析后的内容保存到Amazon DynamoDB表中。

Lambda函数的执行角色具有从S3存储桶读取和写入DynamoDB表的权限。在测试过程中，DevOps工程师发现当对象添加到S3存储桶或修改现有对象时，Lambda函数不会运行。

 | **选项A：为S3存储桶创建S3存储桶策略，授予S3存储桶调用Lambda函数的权限。**
- 错误。S3存储桶策略主要用于控制对存储桶和对象的访问权限，而不是用于授予调用Lambda函数的权限。这不是正确的权限配置方式。

**选项B：为Lambda函数创建资源策略，授予Amazon S3调用该S3存储桶上Lambda函数的权限。**
- 正确。当S3事件触发Lambda函数时，需要在Lambda函数上配置资源策略（resource-based policy），明确允许S3服务调用该Lambda函数。这是S3事件触发Lambda的标准配置要求。

**选项C：配置Amazon SQS队列作为Lambda函数的OnFailure目标。更新Lambda函数以处理来自SQS队列和S3事件通知的消息。**
- 错误。OnFailure目标是用于处理Lambda函数执行失败的情况，与解决S3事件无法触发Lambda函数的问题无关。这个选项没有解决根本问题。

**选项D：配置Amazon SQS队列作为S3存储桶事件通知的目标。更新Lambda函数的执行角色以具有从SQS队列读取的权限。更新Lambda函数以消费来自SQS队列的消息。**
- 这是一个可行的替代方案，但不是解决当前问题的最直接方法。这种方法改变了整个架构，从直接的S3-Lambda触发改为S3-SQS-Lambda的间接触发模式，增加了复杂性。

 |  |  |  |
| 303 | A company recently congured AWS Control Tower in its organization in AWS Organizations. The company enrolled all existing AWS accounts
in AWS Control Tower. The company wants to ensure that all new AWS accounts are automatically enrolled in AWS Control Tower.
The company has an existing AWS Step Functions workow that creates new AWS accounts and performs any actions required as part of
account creation. The Step Functions workow is dened in the same AWS account as AWS Control Tower. | A. Create an Amazon EventBridge event that has an aws.controltower source and a CreateManagedAccount detail-type. Add the details of
the new AWS account to the detail eld of the event.
B. Create an Amazon EventBridge event that has an aws.controltower source and a SetupLandingZone detail-type. Add the details of the
new AWS account to the detail eld of the event.
C. Create an AWSControlTowerExecution role in the new AWS account. Congure the role to allow the AWS Control Tower administrator
account to assume the role.
D. Call the AWS Service Catalog ProvisionProduct API operation with the details of the new AWS account.
E. Call the Organizations EnableAWSServiceAccess API operation with the controltower.amazonaws.com service name and the details of
the new AWS account. | 一家公司最近在其AWS Organizations组织中配置了AWS Control Tower。该公司将所有现有的AWS账户都注册到了AWS Control Tower中。公司希望确保所有新的AWS账户都能自动注册到AWS Control Tower中。

该公司有一个现有的AWS Step Functions工作流，用于创建新的AWS账户并执行账户创建过程中所需的任何操作。该Step Functions工作流定义在与AWS Control Tower相同的AWS账户中。

 | **选项A：** 创建一个Amazon EventBridge事件，该事件具有aws.controltower源和CreateManagedAccount详细类型。将新AWS账户的详细信息添加到事件的detail字段中。
- **错误**：这是在尝试创建一个EventBridge事件来触发Control Tower操作，但这不是正确的方法。CreateManagedAccount是Control Tower发出的事件类型，而不是我们应该创建的事件。

**选项B：** 创建一个Amazon EventBridge事件，该事件具有aws.controltower源和SetupLandingZone详细类型。将新AWS账户的详细信息添加到事件的detail字段中。
- **错误**：SetupLandingZone是用于设置Landing Zone的操作，不是用于注册新账户的。而且同样地，这些是Control Tower发出的事件，不是我们应该创建的。

**选项C：** 在新AWS账户中创建AWSControlTowerExecution角色。配置该角色以允许AWS Control Tower管理员账户承担该角色。
- **部分正确但不完整**：虽然AWSControlTowerExecution角色确实是Control Tower管理账户所需的，但仅创建角色并不能自动将账户注册到Control Tower中。

**选项D：** 使用新AWS账户的详细信息调用AWS Service Catalog ProvisionProduct API操作。
- **正确**：AWS Control Tower使用AWS Service Catalog来管理账户创建。Control Tower将账户创建作为Service Catalog产品提供，通过调用ProvisionProduct API可以创建并自动注册新账户到Control Tower。

**选项E：** 使用controltower.amazonaws.com服务名称和新AWS账户的详细信息调用Organizations EnableAWSServiceAccess API操作。
- **错误**：EnableAWSServiceAccess用于在组织级别启用AWS服务访问，但这不会自动注册特定账户到Control Tower。

 |  |  |  |
| 304 | A company's web application uses an Application Load Balancer (ALB) to direct trac to Amazon EC2 instances across three Availability
Zones.
The company has deployed a newer version of the application to one Availability Zone for testing. If a problem is detected with the
application, the company wants to direct trac away from the affected Availability Zone until the deployment has been rolled back. The
application must remain available and maintain static stability during the rollback. | A. Disable cross-zone load balancing on the ALB's target group. Initiate a zonal shift on the ALB to direct trac away from the affected
Availability Zone.
B. Remove the subnet that is associated
with the affected Availability Zone.
C. Congure cross-zone load balancing on the ALB's target group to inherit settings from the AL
D. Congure cross-zone load balancing on the ALB's target group to inherit settings from the AL | **
一家公司的Web应用程序使用应用负载均衡器(ALB)将流量分发到跨三个可用区的Amazon EC2实例。
该公司已将应用程序的新版本部署到一个可用区进行测试。如果检测到应用程序存在问题，公司希望将流量从受影响的可用区转移开，直到部署回滚完成。在回滚过程中，应用程序必须保持可用并维持静态稳定性。

2. ** | **

**选项A：** 在ALB的目标组上禁用跨区负载均衡。在ALB上启动区域转移(zonal shift)以将流量从受影响的可用区转移开。
- 这是正确的方法。区域转移(zonal shift)是AWS提供的一个功能，允许临时将流量从特定可用区转移开
- 禁用跨区负载均衡确保流量不会意外路由到受影响的区域
- 这种方法可以快速响应问题，同时保持应用程序的可用性

**选项B：** 移除与受影响可用区关联的子网。
- 这种方法过于激进，会导致该可用区的所有资源立即不可用
- 移除子网是一个重大的基础设施变更，可能影响其他服务
- 不符合"静态稳定性"的要求

**选项C和D：** 配置跨区负载均衡从ALB继承设置。
- 这两个选项内容不完整，似乎被截断了
- 仅配置跨区负载均衡继承设置并不能解决将流量从特定可用区转移的问题
- 没有提供具体的流量转移机制

3. ** |  |  |  |
| 305 | A company has several AWS accounts. An Amazon Connect instance runs in each account. The company uses an Amazon EventBridge default
event bus in each account for event handling.
A DevOps team needs to receive all the Amazon Connect events in a single DevOps account. | A. Update the resource-based policy of the default event bus in each account to allow the DevOps account to replay events. Congure an
EventBridge rule in the DevOps account that matches Amazon Connect events and has a target of the default event bus in the other
accounts.
B. Update the resource-based policy of the default event bus in each account to allow the DevOps account to receive events. Congure an
EventBridge rule in the DevOps account that matches Amazon Connect events and has a target of the default event bus in the other
accounts.
C. Update the resource-based policy of the default event bus in the DevOps account. Update the policy to allow events to be received from
the accounts. Congure an EventBridge rule in each account that matches Amazon Connect events and has a target of the DevOps
account's default event bus.
D. Update the resource-based policy of the default event bus in the DevOps account. Update the policy to allow events to be replayed by
the accounts. Congure an EventBridge rule in each account that matches Amazon Connect events and has a target of the DevOps
account's default event bus. | 一家公司有多个AWS账户。每个账户中都运行着一个Amazon Connect实例。公司在每个账户中使用Amazon EventBridge默认事件总线进行事件处理。

DevOps团队需要在单个DevOps账户中接收所有的Amazon Connect事件。

 | **选项A：** 
- 更新每个账户中默认事件总线的基于资源的策略，允许DevOps账户重放事件
- 在DevOps账户中配置EventBridge规则，匹配Amazon Connect事件，目标为其他账户的默认事件总线
- **错误**：这个配置方向相反，且使用了"重放事件"概念，不符合跨账户事件转发的需求

**选项B：**
- 更新每个账户中默认事件总线的基于资源的策略，允许DevOps账户接收事件
- 在DevOps账户中配置EventBridge规则，匹配Amazon Connect事件，目标为其他账户的默认事件总线
- **错误**：配置方向错误，DevOps账户无法直接从其他账户的事件总线中"拉取"事件

**选项C：**
- 更新DevOps账户中默认事件总线的基于资源的策略，允许从其他账户接收事件
- 在每个账户中配置EventBridge规则，匹配Amazon Connect事件，目标为DevOps账户的默认事件总线
- **正确**：这是标准的跨账户事件转发配置方式

**选项D：**
- 更新DevOps账户中默认事件总线的基于资源的策略，允许其他账户重放事件
- 在每个账户中配置EventBridge规则，匹配Amazon Connect事件，目标为DevOps账户的默认事件总线
- **错误**：使用了"重放事件"概念，这不是跨账户事件转发的正确术语

 |  |  |  |
| 306 | A company has deployed an Amazon Elastic Kubernetes Service (Amazon EKS) cluster with Amazon EC2 node groups. The company's DevOps
team uses the Kubernetes Horizontal Pod Autoscaler and recently installed a supported EKS cluster Autoscaler.
The DevOps team needs to implement a solution to collect metrics and logs of the EKS cluster to establish a baseline for performance. The
DevOps team will create an initial set of thresholds for specic metrics and will update the thresholds over time as the cluster is used. The
DevOps team must receive an Amazon Simple Notication Service (Amazon SNS) email notication if the initial set of thresholds is exceeded
or if the EKS cluster Autoscaler is not functioning properly.
The solution must collect cluster, node, and pod metrics. The solution also must capture logs in Amazon CloudWatch. | A. Deploy the CloudWatch agent and Fluent Bit to the cluster. Ensure that the EKS cluster has appropriate permissions to send metrics
and logs to CloudWatch.
B. Deploy AWS Distro for OpenTelemetry to the cluster. Ensure that the EKS cluster has appropriate permissions to send metrics and logs
to CloudWatch.
C. Create CloudWatch alarms to monitor the CPU, memory, and node failure metrics of the cluster. Congure the alarms to send an SNS
email notication to the DevOps team if thresholds are exceeded.
D. Create a CloudWatch composite alarm to monitor a metric log lter of the CPU, memory, and node metrics of the cluster. Congure the
alarm to send an SNS email notication to the DevOps team when anomalies are detected.
E. Create a CloudWatch alarm to monitor the logs of the Autoscaler deployments for errors. Congure the alarm to send an SNS email
notication to the DevOps team if thresholds are exceeded.
F. Create a CloudWatch alarm to monitor a metric log lter of the Autoscaler deployments for errors. Congure the alarm to send an SNS
email notication to the DevOps team if thresholds are exceeded. | 一家公司已经部署了一个带有Amazon EC2节点组的Amazon Elastic Kubernetes Service (Amazon EKS)集群。公司的DevOps团队使用Kubernetes水平Pod自动扩缩器，并且最近安装了一个受支持的EKS集群自动扩缩器。

DevOps团队需要实施一个解决方案来收集EKS集群的指标和日志，以建立性能基线。DevOps团队将为特定指标创建一组初始阈值，并随着集群的使用逐步更新这些阈值。如果超过初始阈值或EKS集群自动扩缩器运行不正常，DevOps团队必须收到Amazon Simple Notification Service (Amazon SNS)邮件通知。

解决方案必须收集集群、节点和Pod指标。解决方案还必须在Amazon CloudWatch中捕获日志。

 | **选项A：** 将CloudWatch代理和Fluent Bit部署到集群。确保EKS集群具有向CloudWatch发送指标和日志的适当权限。
- **正确性：高** - CloudWatch代理可以收集节点级指标，Fluent Bit是AWS推荐的日志收集工具，可以收集容器日志并发送到CloudWatch。这个组合可以满足收集集群、节点和Pod指标以及日志的需求。

**选项B：** 将AWS Distro for OpenTelemetry部署到集群。确保EKS集群具有向CloudWatch发送指标和日志的适当权限。
- **正确性：高** - AWS Distro for OpenTelemetry (ADOT)是AWS的可观测性解决方案，可以收集指标、跟踪和日志，并将其发送到CloudWatch。它是一个现代化的、统一的可观测性解决方案。

**选项C：** 创建CloudWatch告警来监控集群的CPU、内存和节点故障指标。配置告警在超过阈值时向DevOps团队发送SNS邮件通知。
- **正确性：高** - 这直接满足了监控特定指标并在超过阈值时发送通知的需求。

**选项D：** 创建CloudWatch复合告警来监控集群CPU、内存和节点指标的指标日志过滤器。配置告警在检测到异常时向DevOps团队发送SNS邮件通知。
- **正确性：中等** - 复合告警可以监控多个指标，但题目要求的是基于特定阈值的告警，而不是异常检测。

**选项E：** 创建CloudWatch告警来监控自动扩缩器部署的日志错误。配置告警在超过阈值时向DevOps团队发送SNS邮件通知。
- **正确性：高** - 这满足了监控EKS集群自动扩缩器是否正常运行的需求。

**选项F：** 创建CloudWatch告警来监控自动扩缩器部署错误的指标日志过滤器。配置告警在超过阈值时向DevOps团队发送SNS邮件通知。
- **正确性：高** - 通过指标日志过滤器监控自动扩缩器错误是一个有效的方法，可以将日志转换为指标进行监控。

 |  |  |  |
| 307 | A company discovers that its production environment and disaster recovery (DR) environment are deployed to the same AWS Region. All the
production applications run on Amazon EC2 instances and are deployed by AWS CloudFormation. The applications use an Amazon FSx for
NetApp ONTAP volume for application storage. No application data resides on the EC2 instances.
A DevOps engineer copies the required AMIs to a new DR Region. The DevOps engineer also updates the CloudFormation code to accept a
Region as a parameter. The storage needs to have an RPO of 10 minutes in the DR Region. | A. Create an Amazon S3 bucket in both Regions. Congure S3 Cross-Region Replication (CRR) for the S3 buckets. Create a scheduled AWS
Lambda function to copy any new content from the FSx for ONTAP volume to the S3 bucket in the production Region.
B. Use AWS Backup to create a backup vault and a custom backup plan that has a 10-minute frequency. Specify the DR Region as the
target Region. Assign the EC2 instances in the production Region to the backup plan.
C. Create an AWS Lambda function to create snapshots of the instance store volumes that are attached to the EC2 instances. Congure
the Lambda function to copy the snapshots to the DR Region and to remove the previous copies. Create an Amazon EventBridge
scheduled rule that invokes the Lambda function every 10 minutes.
D. Create an FSx for ONTAP instance in the DR Region. Congure a 5-minute schedule for a volume-level NetApp SnapMirror to replicate
the volume from the production Region to the DR Region. |  |  |  |  |  |
| 308 | During a security audit, a company discovered that some security groups allow SSH trac from 0.0.0.0/0. A security team must implement a
solution to detect and remediate this issue as soon as possible. The company uses one organization in AWS Organizations to manage all the
company's AWS accounts. | A. Enable AWS Cong for all AWS accounts. Use a periodic trigger to activate the vpe-sg-port-restriction-check AWS Cong rule. Create an
AWS Lambda function to remediate any noncompliant rules.
B. Create an AWS Lambda function in each AWS account to delete all the security group rules. Create an Amazon EventBridge rule to
match security group update events or creation events. Set the Lambda function in each account as a target for the rule.
C. Enable AWS Cong for all AWS accounts. Create a custom AWS Cong rule to run on the restricted-ssh conguration change trigger.
Congure the rule to invoke an AWS Lambda function to remediate any noncompliant resources.
D. Create an AWS Systems Manager Automation document in each account to inspect all security groups and to delete noncompliant
rules. Use an Amazon EventBridge rule to run the Automation document every hour. |  |  |  |  |  |
| 309 | A company's DevOps engineer must install a software package on 30 on-premises VMs and 15 Amazon EC2 instances.
The DevOps engineer needs to ensure that all VMs receive the package in a process that is auditable and that any conguration drift on the
VMs is automatically identied and alerted on. The company uses AWS Direct Connect to connect its on-premises data center to AWS. | A. Write a script that iterates through the list of VMs once a week. Congure the script to check for the package and install the package if
the package is not found. Congure the script to send an email message notication to the system administrator if the package is not
found.
B. Install the AWS Systems Manager Agent (SSM Agent) on all VMs. Use the SSM Agent to install the package. Use AWS Cong to monitor
for conguration drift. Use Amazon Simple Notication Service (Amazon SNS) to notify the system administrator if any drift is found.
C. Write a script that checks if the package is installed across the environment. Congure the script to create a list of all VMs that are
noncompliant. Congure the script to send the list to the system administrator, who will install the package on the noncompliant VMs.
D. Log in to each VM. Use a local package manager to install the package. Use AWS Cong to monitor the AWS resources for conguration
changes. Write a script to monitor the on-premises resources. |  |  |  |  |  |
| 310 | A company has an AWS CodePipeline pipeline in the eu-west-1 Region. The pipeline stores the build artifacts in an Amazon S3 bucket. The
pipeline builds and deploys an AWS Lambda function by using an AWS CloudFormation deploy action.
A DevOps engineer needs to update the existing pipeline to also deploy the Lambda function to the us-east-1 Region. The pipeline has
already been updated to create an additional artifact to deploy to us-east-1. | A. Modify the CloudFormation template to include a parameter for the Lambda function code's .zip le location. Create a new
CloudFormation deploy action for us-east-1 in the pipeline. Congure the new deploy action to pass in the us-east-1 artifact location as a
parameter override.
B. Create a new CloudFormation deploy action for us-east-1 in the pipeline. Congure the new deploy action to use the CloudFormation
template from the additional artifact that was created for us-east-1.
C. Create an S3 bucket in us-east-1. Congure the S3 bucket policy to allow CodePipeline to have read and write access.
D. Create an S3 bucket in us-east-1. Congure S3 Cross-Region Replication (CRR) from the S3 bucket in eu-west-1 to the S3 bucket in us-
east-1.
E. Modify the pipeline to include the S3 bucket for us-east-1 as an artifact store. Create a new CloudFormation deploy action for us-east-1
in the pipeline. Congure the new deploy action to use the CloudFormation template from the us-east-1 artifact. |  |  |  |  |  |
| 311 | A company uses an AWS Cloud Development Kit (AWS CDK) application for its infrastructure. The AWS CDK application creates AWS Lambda
functions and the IAM roles that are attached to the functions. The company also uses AWS Organizations. The company's developers can
assume the AWS CDK application deployment role.
The company's security team discovered that the developers and the role used to deploy the AWS CDK application have more permissions
than necessary. The security team also discovered that the roles attached to the Lambda functions that the CDK application creates have
more permissions than necessary. The developers must not have the ability to grant additional permissions. | A. Create an SCP that denies the iam:CreateRole action and the iam:UpdateRole action for the developer role and the AWS CDK
application deployment role. Centrally create new IAM roles to attach to the Lambda functions for the developers to use to provision
Lambda functions.
B. Create an IAM permission boundary policy. Dene the maximum actions that the AWS CDK application requires in the policy. Update the
account's AWS CDK bootstrapping to use the permission boundary. Update the conguration in the AWS CDK application for the default
permissions boundary to use the policy.
C. Create an IAM permission boundary policy. Dene the maximum actions that the AWS CDK application requires in the policy. Instruct
the developers to use the permission boundary policy name when they create a role in the AWS CDK application code.
D. Create an SCP that denies the iam:CreateRole action and the iam:UpdateRole action for the developer role. Give the AWS CDK
deployment role access to create roles associated with Lambda functions. Run AWS Identity and Access Management Access Analyzer to
verify that the Lambda functions role does not have permissions. | 一家公司使用AWS云开发工具包(AWS CDK)应用程序来管理其基础设施。AWS CDK应用程序创建AWS Lambda函数以及附加到这些函数的IAM角色。该公司还使用AWS Organizations。公司的开发人员可以担任AWS CDK应用程序部署角色。

公司的安全团队发现，开发人员和用于部署AWS CDK应用程序的角色拥有超出必要的权限。安全团队还发现，CDK应用程序创建的附加到Lambda函数的角色也拥有超出必要的权限。开发人员不得具有授予额外权限的能力。

 | **选项A：** 创建一个SCP，拒绝开发人员角色和AWS CDK应用程序部署角色的iam:CreateRole和iam:UpdateRole操作。集中创建新的IAM角色，供开发人员用于预置Lambda函数。
- 问题：完全阻止角色创建会破坏CDK的正常功能，因为CDK需要动态创建角色。集中管理角色会降低开发效率，不符合CDK的自动化理念。

**选项B：** 创建IAM权限边界策略。在策略中定义AWS CDK应用程序所需的最大操作。更新账户的AWS CDK引导配置以使用权限边界。更新AWS CDK应用程序中的配置，将默认权限边界设置为使用该策略。
- 优点：权限边界可以限制CDK创建的角色的最大权限，同时保持CDK的正常功能。通过CDK引导配置和默认权限边界设置，可以自动应用到所有创建的角色。这是一个系统性的解决方案。

**选项C：** 创建IAM权限边界策略。在策略中定义AWS CDK应用程序所需的最大操作。指示开发人员在CDK应用程序代码中创建角色时使用权限边界策略名称。
- 问题：依赖开发人员手动应用权限边界，容易出现人为错误或遗漏，不能保证一致性。

**选项D：** 创建一个SCP，拒绝开发人员角色的iam:CreateRole和iam:UpdateRole操作。给AWS CDK部署角色访问权限来创建与Lambda函数关联的角色。运行AWS IAM Access Analyzer来验证Lambda函数角色没有多余权限。
- 问题：虽然限制了开发人员直接创建角色，但没有限制CDK部署角色创建的角色的权限范围。Access Analyzer只是事后检查工具，不能预防权限过度授予。

 |  |  |  |
| 312 | A company uses Amazon Elastic Container Registry (Amazon ECR) private registries to store container images.
A DevOps team needs to ensure that the container images are regularly scanned for software package vulnerabilities. | A. Enable enhanced scanning for private registries in Amazon ECR.
B. Enable basic continuous scanning for private registries in Amazon ECR.
C. Create an AWS System Manager Automation document to scan images by using the AWS SDK. Congure the Automation document to
run when a new image is pushed to an ECR registry.
D. Create an AWS Lambda function that scans all images in Amazon ECR by using the AWS SDK. Create an Amazon EventBridge rule to
invoke the Lambda function each day. | 一家公司使用Amazon Elastic Container Registry (Amazon ECR) 私有注册表来存储容器镜像。
DevOps团队需要确保容器镜像定期扫描软件包漏洞。

选项：
A. 为Amazon ECR中的私有注册表启用增强扫描功能。
B. 为Amazon ECR中的私有注册表启用基本持续扫描功能。
C. 创建AWS Systems Manager自动化文档，使用AWS SDK扫描镜像。配置自动化文档在新镜像推送到ECR注册表时运行。
D. 创建AWS Lambda函数，使用AWS SDK扫描Amazon ECR中的所有镜像。创建Amazon EventBridge规则每天调用Lambda函数。

 | **选项A：为Amazon ECR中的私有注册表启用增强扫描功能**
- ✅ 正确选项。Amazon ECR提供增强扫描功能，基于Amazon Inspector
- 提供更全面的漏洞检测，包括操作系统和编程语言包漏洞
- 可以配置为持续扫描，自动扫描推送的镜像
- 原生AWS服务，无需额外开发和维护

**选项B：为Amazon ECR中的私有注册表启用基本持续扫描功能**
- ⚠️ 部分正确但不是最佳选择。基本扫描功能相对有限
- 只提供基于CVE数据库的基础漏洞扫描
- 扫描能力不如增强扫描全面
- 对于企业级需求可能不够充分

**选项C：创建AWS Systems Manager自动化文档扫描镜像**
- ❌ 不推荐。过度复杂化简单问题
- 需要自定义开发和维护扫描逻辑
- 增加了不必要的复杂性和维护成本
- 当ECR已有原生扫描功能时，这种方法不合理

**选项D：创建Lambda函数定期扫描所有镜像**
- ❌ 不推荐。同样过度复杂化
- 需要自定义开发扫描逻辑和漏洞数据库维护
- Lambda执行时间限制可能影响大量镜像的扫描
- 维护成本高，且重复造轮子

 |  |  |  |
| 313 | A security team sets up a workow that invokes an AWS Step Functions workow when Amazon EventBridge matches specic events. The
events can be generated by several AWS services. AWS CloudTrail records user activities.
The security team notices that some important events do not invoke the workow as expected. The CloudTrail logs do not indicate any direct
errors related to the missing events. | A. Enable EventBridge schema discovery on the event bus to determine whether the event patterns match the expected schema.
B. Congure Amazon CloudWatch to monitor EventBridge metrics and Step Functions metrics. Set up alerts for anomalies in event
patterns and workow invocations.
C. Congure an AWS Lambda logging function to monitor and log events from EventBridge to provide more details about the processed
events.
D. Review the Step Functions execution history for patterns of failures or timeouts that could correlate to the missing event invocations.
E. Review metrics for the EventBridge failed invocations to ensure that the IAM execution role that is attached to the rule has sucient
permissions.
F. Verify that the Step Functions workow has the correct permissions to be invoked by EventBridge. | 一个安全团队设置了一个工作流，当Amazon EventBridge匹配特定事件时会调用AWS Step Functions工作流。这些事件可以由多个AWS服务生成。AWS CloudTrail记录用户活动。

安全团队注意到一些重要事件没有按预期调用工作流。CloudTrail日志没有显示与缺失事件相关的任何直接错误。

 | **A. 在事件总线上启用EventBridge架构发现，以确定事件模式是否匹配预期的架构。**
- 正确。架构发现可以帮助验证传入事件的结构是否与EventBridge规则中定义的事件模式匹配。如果事件结构不匹配，规则就不会触发。

**B. 配置Amazon CloudWatch监控EventBridge指标和Step Functions指标。为事件模式和工作流调用中的异常设置警报。**
- 正确。CloudWatch指标可以提供关于EventBridge规则匹配、失败调用等的详细信息，有助于识别问题。

**C. 配置AWS Lambda日志记录函数来监控和记录来自EventBridge的事件，以提供有关已处理事件的更多详细信息。**
- 部分正确，但不是最直接的解决方案。虽然可以提供额外的日志记录，但增加了复杂性。

**D. 查看Step Functions执行历史，寻找可能与缺失事件调用相关的失败或超时模式。**
- 不太相关。如果事件没有触发工作流，Step Functions执行历史中不会有相关记录。

**E. 查看EventBridge失败调用的指标，确保附加到规则的IAM执行角色具有足够的权限。**
- 正确。权限问题是导致调用失败的常见原因。EventBridge需要适当的IAM权限来调用Step Functions。

**F. 验证Step Functions工作流具有被EventBridge调用的正确权限。**
- 正确。Step Functions需要资源策略或适当的IAM配置来允许EventBridge调用它。

 |  |  |  |
| 314 | A company's DevOps engineer uses AWS Systems Manager to perform maintenance tasks. The company has a few Amazon EC2 instances that
require a restart after notications from AWS Health.
The DevOps engineer must implement an automated solution that uses Amazon EventBridge to remediate the notications during the
company's scheduled maintenance windows.
How should the DevOps engineer congure an EventBridge rule to meet these requirements? | A. Congure an event source of AWS Health. Congure event types that indicate scheduled instance termination and retirement. Target
the AWS-RestartEC2Instance Systems Manager Automation runbook to restart the EC2 instances.
B. Congure an event source of Systems Manager. Congure an event type that indicates a maintenance window. Target the AWS-
RestartEC2Instance Systems Manager Automation runbook to restart the EC2 instances.
C. Congure an event source of AWS Health. Congure event types that indicate scheduled instance termination and retirement. Target a
newly created AWS Lambda function that registers a Systems Manager maintenance window task to restart the EC2 instances.
D. Congure an event source of EC2. Congure an event type that indicates instance state notication. Target a newly created AWS
Lambda function that registers a Systems Manager maintenance window task to restart the EC2 instances. |  |  |  |  |  |
| 315 | A DevOps engineer manages an AWS CodePipeline pipeline that builds and deploys a web application on AWS. The pipeline has a source
stage, a build stage, and a deploy stage. When deployed properly, the web application responds with a 200 OK HTTP response code when the
URL of the home page is requested.
The home page recently returned a 503 HTTP response code after CodePipeline deployed the application. The DevOps engineer needs to add
an automated test into the pipeline. The automated test must ensure that the application returns a 200 OK HTTP response code after the
application is deployed. The pipeline must fail if the response code is not present during the test. The DevOps engineer has added a
CheckURL stage after the deploy stage in the pipeline. | A. Congure the CheckURL stage to use an Amazon CloudWatch action. Congure the action to use a canary synthetic monitoring check
on the application URL and to report a success or failure to CodePipeline.
B. Create an AWS Lambda function to check the response code status of the URL and to report a success or failure to CodePipeline.
Congure an action in the CheckURL stage to invoke the Lambda function.
C. Congure the CheckURL stage to use an AWS CodeDeploy action. Congure the action with an input artifact that is the URL of the
application and to report a success or failure to CodePipeline.
D. Deploy an Amazon API Gateway HTTP API that checks the response code status of the URL and that reports success or failure to
CodePipeline. Congure the CheckURL stage to use the AWS Device Farm test action and to provide the API Gateway HTTP API as an input
artifact. | 一名DevOps工程师管理着一个AWS CodePipeline流水线，该流水线在AWS上构建和部署Web应用程序。该流水线包含源代码阶段、构建阶段和部署阶段。当正确部署时，Web应用程序在请求主页URL时会返回200 OK HTTP响应代码。

最近，在CodePipeline部署应用程序后，主页返回了503 HTTP响应代码。DevOps工程师需要在流水线中添加自动化测试。该自动化测试必须确保应用程序在部署后返回200 OK HTTP响应代码。如果测试期间没有出现该响应代码，流水线必须失败。DevOps工程师已经在流水线的部署阶段之后添加了一个CheckURL阶段。

 | **选项A：** 配置CheckURL阶段使用Amazon CloudWatch操作。配置该操作使用金丝雀综合监控检查应用程序URL，并向CodePipeline报告成功或失败。
- **分析：** CloudWatch Synthetics确实可以进行URL检查，但CloudWatch本身不是CodePipeline的原生操作类型。虽然技术上可行，但需要额外的集成工作，不是最直接的解决方案。

**选项B：** 创建一个AWS Lambda函数来检查URL的响应代码状态，并向CodePipeline报告成功或失败。在CheckURL阶段配置一个操作来调用Lambda函数。
- **分析：** 这是一个非常合理的解决方案。Lambda函数可以轻松检查HTTP响应代码，CodePipeline原生支持Lambda操作类型，可以根据Lambda函数的返回结果决定流水线是否继续或失败。这种方法简单、直接且符合AWS最佳实践。

**选项C：** 配置CheckURL阶段使用AWS CodeDeploy操作。配置该操作以应用程序URL作为输入工件，并向CodePipeline报告成功或失败。
- **分析：** CodeDeploy主要用于应用程序部署，不是用于URL健康检查的工具。URL不能作为CodeDeploy的输入工件，这个选项在技术上不合理。

**选项D：** 部署一个Amazon API Gateway HTTP API来检查URL的响应代码状态，并向CodePipeline报告成功或失败。配置CheckURL阶段使用AWS Device Farm测试操作，并提供API Gateway HTTP API作为输入工件。
- **分析：** 这个方案过于复杂，Device Farm主要用于移动应用测试，不适合简单的URL检查。使用API Gateway来检查另一个URL也是不必要的复杂化。

 |  |  |  |
| 316 | A company has an application that uploads access logs to an Amazon CloudWatch Logs log group. The elds in the log lines include the
response code and the application name.
The company wants to create a CloudWatch metric to track the number of requests by response code in a specic range and with a specic
application name. | A. Create a CloudWatch Logs log event lter on the CloudWatch Logs log stream to match the response code range. Congure the log
event lter to increment a metric. Set the response code and application name as dimensions.
B. Create a CloudWatch Logs metric lter on the CloudWatch Logs log group to match the response code range. Congure the metric lter
to increment a metric. Set the response code and application name as dimensions.
C. Create a CloudWatch Contributor Insights rule on the CloudWatch Logs log stream with a lter to match the response code range.
Congure the Contributor Insights rule to increment a CloudWatch metric with the response code and application name as dimensions.
D. Create a CloudWatch Logs Insights query on the CloudWatch Logs log group to match the response code range. Congure the Logs
Insights query to increment a CloudWatch metric with the response code and application name as dimensions. | 一家公司有一个应用程序，它将访问日志上传到Amazon CloudWatch Logs日志组。日志行中的字段包括响应代码和应用程序名称。

该公司希望创建一个CloudWatch指标来跟踪特定范围内响应代码和特定应用程序名称的请求数量。

 | **选项A：在CloudWatch Logs日志流上创建日志事件过滤器来匹配响应代码范围。配置日志事件过滤器来增加指标。将响应代码和应用程序名称设置为维度。**
- 错误：CloudWatch Logs中没有"日志事件过滤器"这个概念，正确的术语是"指标过滤器"(metric filter)
- 错误：指标过滤器是在日志组级别创建的，不是在日志流级别

**选项B：在CloudWatch Logs日志组上创建指标过滤器来匹配响应代码范围。配置指标过滤器来增加指标。将响应代码和应用程序名称设置为维度。**
- 正确：指标过滤器是CloudWatch Logs的标准功能，用于从日志数据创建指标
- 正确：指标过滤器在日志组级别创建
- 正确：可以配置模式匹配来筛选特定的响应代码范围
- 正确：可以将响应代码和应用程序名称设置为指标维度

**选项C：在CloudWatch Logs日志流上创建CloudWatch Contributor Insights规则，使用过滤器匹配响应代码范围。配置Contributor Insights规则来增加CloudWatch指标，将响应代码和应用程序名称作为维度。**
- 错误：Contributor Insights主要用于分析和可视化高基数数据，不是用来创建自定义指标的标准方法
- 错误：Contributor Insights规则不是在日志流级别创建的
- 过于复杂：对于这个简单的需求来说过度设计

**选项D：在CloudWatch Logs日志组上创建CloudWatch Logs Insights查询来匹配响应代码范围。配置Logs Insights查询来增加CloudWatch指标，将响应代码和应用程序名称作为维度。**
- 错误：CloudWatch Logs Insights是一个交互式查询服务，用于分析日志数据，不能直接用来创建持续的指标
- 错误：Logs Insights查询不能自动增加CloudWatch指标

 |  |  |  |
| 317 | A DevOps engineer provisioned an Amazon Elastic Kubernetes Service (Amazon EKS) cluster with managed node groups. The DevOps
engineer associated an OpenID Connect (OIDC) issuer with the cluster.
The DevOps engineer is conguring Amazon Elastic Block Store (Amazon EBS) General Purpose SSD (gp3) volumes for the cluster. The DevOps
engineer attempts to initiate a PersistentVolumeClaim (PVC) request but is unable to provision a volume. To troubleshoot the issue, the
DevOps engineer runs the kubectl describe pyc command. The DevOps engineer receives a failed to provision volume with StorageClass error
and a could not create volume in EC2:UnauthorizedOperation error. | A. Create a Kubernetes cluster role that allows the persistent volumes to perform get, list, watch, create, and delete operations. Congure
the cluster role to allow get, list, and watch operations for storage in the cluster.
B. Create an Amazon EBS Container Storage Interface (CSI) driver IAM role that has the required permissions and trust relationships.
Attach the IAM role to the Amazon EBS CSI driver add-on in the cluster.
C. Add the ebs.csi.aws.com/volumeType:gp3 annotation to the PersistentVolumeClaim object in the cluster.
D. Create a Kubernetes storage class object. Set the provisioner value to ebs.csi.aws.com. Set the volumeBindingMode value to
WaitForFirstConsumer in the luster. | 一名DevOps工程师使用托管节点组配置了Amazon Elastic Kubernetes Service (Amazon EKS)集群。该DevOps工程师将OpenID Connect (OIDC)发行者与集群关联。

该DevOps工程师正在为集群配置Amazon Elastic Block Store (Amazon EBS) General Purpose SSD (gp3)卷。DevOps工程师尝试发起PersistentVolumeClaim (PVC)请求，但无法配置卷。为了排除故障，DevOps工程师运行kubectl describe pvc命令。DevOps工程师收到"failed to provision volume with StorageClass"错误和"could not create volume in EC2:UnauthorizedOperation"错误。

 | **选项A：** 创建一个Kubernetes集群角色，允许持久卷执行get、list、watch、create和delete操作。配置集群角色以允许对集群中的存储执行get、list和watch操作。
- 这个选项涉及Kubernetes RBAC权限，但错误信息显示的是EC2:UnauthorizedOperation，这是AWS IAM权限问题，不是Kubernetes RBAC问题。

**选项B：** 创建一个具有所需权限和信任关系的Amazon EBS Container Storage Interface (CSI)驱动程序IAM角色。将IAM角色附加到集群中的Amazon EBS CSI驱动程序附加组件。
- 这个选项直接解决了EC2:UnauthorizedOperation错误。EBS CSI驱动程序需要适当的IAM权限来创建和管理EBS卷。错误信息表明缺少AWS权限。

**选项C：** 将ebs.csi.aws.com/volumeType:gp3注释添加到集群中的PersistentVolumeClaim对象。
- 这个注释用于指定卷类型，但不会解决权限问题。EC2:UnauthorizedOperation错误表明问题在于IAM权限，而不是卷类型配置。

**选项D：** 创建一个Kubernetes存储类对象。将provisioner值设置为ebs.csi.aws.com。在集群中将volumeBindingMode值设置为WaitForFirstConsumer。
- 虽然创建存储类是必要的配置，但这不会解决UnauthorizedOperation错误。问题的根本原因是权限不足。

 | B |  |  |
| 318 | A company runs a eet of Amazon EC2 instances in a VP | C. Create a ow log in VPC Flow Logs.
A. Create an Amazon EventBridge rule that reacts to EC2 Instance State-change Notication events.
B. Create an Amazon CloudWatch Logs log group. Specify the log group as a target for the EventBridge rule.
D. Create an Amazon CloudWatch Logs log group. Specify the log group as a destination for the ow log.
E. Create a log group metric lter.
F. Create a log group subscription lter. Use EventBridge as the destination. | 题目似乎不完整，但根据选项内容可以推断，这是一道关于在VPC中运行的Amazon EC2实例fleet的监控和日志管理题目。题目可能是询问如何设置监控和日志记录来跟踪EC2实例的状态变化或网络流量。

# | **A. Create an Amazon EventBridge rule that reacts to EC2 Instance State-change Notification events.**
- 正确。创建EventBridge规则来响应EC2实例状态变化通知事件
- 这是监控EC2实例状态变化（如启动、停止、终止等）的标准方法
- EventBridge可以捕获AWS服务的状态变化事件

**B. Create an Amazon CloudWatch Logs log group. Specify the log group as a target for the EventBridge rule.**
- 正确。创建CloudWatch Logs日志组，并将其指定为EventBridge规则的目标
- 这样可以将EC2状态变化事件记录到日志中，便于后续分析和审计
- 是A选项的合理后续步骤

**C. Create a flow log in VPC Flow Logs.**
- 正确。创建VPC Flow Logs中的流日志
- VPC Flow Logs用于捕获进出VPC网络接口的IP流量信息
- 对于网络监控和安全分析很有用

**D. Create an Amazon CloudWatch Logs log group. Specify the log group as a destination for the flow log.**
- 正确。创建CloudWatch Logs日志组，并将其指定为流日志的目标
- 这是C选项的合理后续步骤，将VPC流日志发送到CloudWatch Logs进行存储和分析

**E. Create a log group metric filter.**
- 部分正确。创建日志组指标过滤器
- 可以从日志数据中提取指标，但需要先有日志数据
- 是在有了日志组和日志数据后的进一步配置

**F. Create a log group subscription filter. Use EventBridge as the destination.**
- 正确。创建日志组订阅过滤器，使用EventBridge作为目标
- 可以将日志数据实时流式传输到EventBridge进行进一步处理

# |  |  |  |
| 319 | A company is using Amazon Elastic Kubernetes Service (Amazon EKS) to run its applications. The EKS cluster is successfully running multiple
pods. The company stores the pod images in Amazon Elastic Container Registry (Amazon ECR).
The company needs to congure Pod Identity access for the EKS cluster. The company has already updated the node IAM role by using the
permissions for Pod Identity access. | A. Create an IAM OpenID Connect (OIDC) provider for the EKS cluster.
B. Ensure that the nodes can reach the EKS Auth API. Add and congure the EKS Pod Identity Agent add-on for the EKS cluster.
C. Create an EKS access entry that uses the API_AND-CONFIG_MAP cluster authentication mode.
D. Congure the AWS Security Token Service (AWS STS) endpoint for the Kubernetes service account that the pods in the EKS cluster use. |  |  |  |  |  |
| 320 | A company has multiple AWS accounts in an organization in AWS Organizations that has all features enabled. The company’s DevOps
administrator needs to improve security across all the company's AWS accounts. The administrator needs to identify the top users and roles in
use across all accounts. | A. Create a new organization trail in AWS CloudTrail. Congure the trail to send log events to Amazon CloudWatch Logs. Create a
CloudWatch Contributor Insights rule for the userIdentity.arn log eld. View the results in CloudWatch Contributor Insights.
B. Create an unused access analysis for the organization by using AWS Identity and Access Management Access Analyzer. Review the
analyzer results and determine if each nding has the intended level of permissions required for the workload.
C. Create a new organization trail in AWS CloudTrail. Create a table in Amazon Athena that uses partition projection. Load the Athena
table with CloudTrail data. Query the Athena table to nd the top users and roles.
D. Generate a Service access report for each account by using Organizations. From the results, pull the last accessed date and last
accessed by account elds to nd the top users and roles. |  |  |  |  |  |
| 321 | A company has an organization in AWS Organizations with many Oils that contain many AWS accounts. The organization has a dedicated
delegated administrator AWS account.
The company needs the accounts in one OU to have server-side encryption enforced for all Amazon Elastic Block Store (Amazon EBS) volumes
and Amazon Simple Queue Service (Amazon SQS) queues that are created or updated on an AWS CloudFormation stack. | A. Activate trusted access to CloudFormation StackSets. Create a CloudFormation Hook that enforces server-side encryption on EBS
volumes and SQS queues. Deploy the Hook across the accounts in the OU by using StackSets.
B. Set up AWS Cong in all the accounts in the OU. Use AWS Systems Manager to deploy AWS Cong rules that enforce server-side
encryption for EBS volumes and SQS queues across the accounts in the OU.
C. Write an SCP to deny the creation of EBS volumes and SQS queues unless the EBS volumes and SQS queues have server-side
encryption. Attach the SCP to the OU.
D. Create an AWS Lambda function in the delegated administrator account that checks whether server-side encryption is enforced for EBS
volumes and SQS queues. Create an IAM role to provide the Lambda function access to the accounts in the OU. | 一家公司在AWS Organizations中有一个组织，包含许多OU（组织单元），这些OU包含许多AWS账户。该组织有一个专门的委托管理员AWS账户。

公司需要在一个OU中的账户对所有在AWS CloudFormation堆栈中创建或更新的Amazon Elastic Block Store (Amazon EBS) 卷和Amazon Simple Queue Service (Amazon SQS) 队列强制执行服务器端加密。

 | **选项A：** 激活CloudFormation StackSets的可信访问。创建一个CloudFormation Hook来强制EBS卷和SQS队列的服务器端加密。使用StackSets在OU中的账户部署Hook。
- **分析：** CloudFormation Hooks主要用于部署过程中的生命周期管理，不是专门用于强制执行安全策略的工具。虽然StackSets可以跨账户部署，但Hook不是最佳的策略执行机制。

**选项B：** 在OU中的所有账户设置AWS Config。使用AWS Systems Manager部署AWS Config规则，在OU中的账户强制执行EBS卷和SQS队列的服务器端加密。
- **分析：** AWS Config主要用于合规性监控和检测，而不是预防性控制。它可以检测到违规行为，但不能阻止不合规资源的创建。

**选项C：** 编写SCP（服务控制策略）来拒绝创建EBS卷和SQS队列，除非这些资源启用了服务器端加密。将SCP附加到OU。
- **分析：** 这是最佳选择。SCP是AWS Organizations的预防性控制机制，可以在资源创建时强制执行策略。通过将SCP附加到OU，可以确保该OU下所有账户都必须遵守加密要求。

**选项D：** 在委托管理员账户中创建AWS Lambda函数，检查EBS卷和SQS队列是否强制执行服务器端加密。创建IAM角色为Lambda函数提供访问OU中账户的权限。
- **分析：** Lambda函数是反应性的解决方案，只能在资源创建后进行检查，无法阻止不合规资源的创建。这不符合"强制执行"的要求。

 |  |  |  |
| 322 | A company is running an internal application in an Amazon Elastic Container Service (Amazon ECS) cluster on Amazon EC2. The ECS cluster
instances can connect to the public internet. The ECS tasks that run on the cluster instances are congured to use images from both private
Amazon Elastic Container Registry (Amazon ECR) repositories and a public ECR registry repository.
A new security policy requires the company to remove the ECS cluster's direct access to the internet. The company must remove any NAT
gateways and internet gateways from the VPC that hosts the cluster. A DevOps engineer needs to ensure the ECS cluster can still download
images from both the public ECR registry and the private ECR repositories. Images from the public ECR registry must remain up-to-date. New
versions of the images must be available to the ECS cluster within 24 hours of publication. | A. Create an AWS CodeBuild project and a new private ECR repository for each image that is downloaded from the public ECR registry.
Congure each project to pull the image from the public ECR repository and push the image to the new private ECR repository. Create an
Amazon EventBridge rule that invokes the CodeBuild project once every 24 hours. Update each task denition in the ECS cluster to refer
to the new private ECR repository.
B. Create a new Amazon ECR pull through cache rule for each image that is downloaded from the public ECR registry. Create an AWS
Lambda function that invokes each pull through cache rule. Create an Amazon EventBridge rule that invokes the Lambda function once
every 24 hours. Update each task denition in the ECS cluster to refer to the image from the pull through cache.
C. 
D. Create an Amazon ECR interface VPC endpoint for the public ECR repositories that are in the VP
E. Create an Amazon ECR interface VPC endpoint for the private ECR repositories that are in the VP | 一家公司在Amazon EC2上的Amazon Elastic Container Service (Amazon ECS)集群中运行内部应用程序。ECS集群实例可以连接到公共互联网。在集群实例上运行的ECS任务被配置为使用来自私有Amazon Elastic Container Registry (Amazon ECR)存储库和公共ECR注册表存储库的镜像。

新的安全策略要求公司移除ECS集群对互联网的直接访问。公司必须从托管集群的VPC中移除所有NAT网关和互联网网关。DevOps工程师需要确保ECS集群仍然可以从公共ECR注册表和私有ECR存储库下载镜像。来自公共ECR注册表的镜像必须保持最新。新版本的镜像必须在发布后24小时内对ECS集群可用。

 | **选项A：** 创建AWS CodeBuild项目和新的私有ECR存储库来处理每个从公共ECR注册表下载的镜像。配置每个项目从公共ECR存储库拉取镜像并推送到新的私有ECR存储库。创建Amazon EventBridge规则每24小时调用一次CodeBuild项目。更新ECS集群中的每个任务定义以引用新的私有ECR存储库。
- 这个方案可以工作，但过于复杂，需要为每个镜像创建单独的CodeBuild项目和私有ECR存储库
- 维护成本高，管理复杂

**选项B：** 为每个从公共ECR注册表下载的镜像创建新的Amazon ECR拉取缓存规则。创建AWS Lambda函数调用每个拉取缓存规则。创建Amazon EventBridge规则每24小时调用一次Lambda函数。更新ECS集群中的每个任务定义以引用来自拉取缓存的镜像。
- ECR拉取缓存是专门为此类场景设计的功能
- 简化了从公共注册表获取镜像到私有环境的过程
- 自动处理镜像同步和缓存
- 符合24小时更新要求

**选项C：** (题目中显示不完整)

**选项D：** 为VPC中的公共ECR存储库创建Amazon ECR接口VPC端点。为VPC中的私有ECR存储库创建Amazon ECR接口VPC端点。
- VPC端点只能解决访问AWS服务的连接问题
- 但无法解决访问公共ECR注册表的问题，因为公共ECR注册表不在客户的VPC中
- 不能满足从公共ECR获取镜像的需求

 |  |  |  |
| 323 | A company has a continuous integration pipeline where the company creates container images by using AWS CodeBuild. The created images
are stored in Amazon Elastic Container Registry (Amazon ECR).
Checking for and xing the vulnerabilities in the images takes the company too much time. The company wants to identify the image
vulnerabilities quickly and notify the security team of the vulnerabilities. | A. Activate Amazon Inspector enhanced scanning for Amazon ECR. Congure the enhanced scanning to use continuous scanning. Set up a
topic in Amazon Simple Notication Service (Amazon SNS).
B. Create an Amazon EventBridge rule for Amazon Inspector ndings. Set an Amazon Simple Notication Service (Amazon SNS) topic as
the rule target.
C. Activate AWS Lambda enhanced scanning for Amazon ECR. Congure the enhanced scanning to use continuous scanning. Set up a
topic in Amazon Simple Email Service (Amazon SES).
D. Create a new AWS Lambda function. Invoke the new Lambda function when scan ndings are detected.
E. Activate default basic scanning for Amazon ECR for all container images. Congure the default basic scanning to use continuous
scanning. Set up a topic in Amazon Simple Notication Service (Amazon SNS). | 一家公司有一个持续集成管道，该公司使用AWS CodeBuild创建容器镜像。创建的镜像存储在Amazon Elastic Container Registry (Amazon ECR)中。

检查和修复镜像中的漏洞耗费了公司太多时间。公司希望快速识别镜像漏洞并通知安全团队相关漏洞。

 | **选项A：** 为Amazon ECR激活Amazon Inspector增强扫描。配置增强扫描使用持续扫描。在Amazon Simple Notification Service (Amazon SNS)中设置主题。
- ✅ **正确**：Amazon Inspector确实提供ECR的增强扫描功能
- ✅ **正确**：支持持续扫描模式，可以在新镜像推送时自动扫描
- ✅ **正确**：SNS是合适的通知服务
- ⚠️ **不完整**：缺少EventBridge规则来连接Inspector发现和SNS通知

**选项B：** 为Amazon Inspector发现创建Amazon EventBridge规则。将Amazon Simple Notification Service (Amazon SNS)主题设置为规则目标。
- ✅ **正确**：EventBridge可以监听Inspector的扫描发现事件
- ✅ **正确**：SNS作为目标可以发送通知给安全团队
- ⚠️ **不完整**：没有提及激活Inspector扫描功能

**选项C：** 为Amazon ECR激活AWS Lambda增强扫描。配置增强扫描使用持续扫描。在Amazon Simple Email Service (Amazon SES)中设置主题。
- ❌ **错误**：AWS Lambda不提供ECR扫描功能，这是Amazon Inspector的功能
- ❌ **错误**：SES不使用"主题"概念，这是SNS的术语

**选项D：** 创建新的AWS Lambda函数。当检测到扫描发现时调用新的Lambda函数。
- ✅ **部分正确**：Lambda可以用于处理扫描结果
- ❌ **不完整**：没有说明如何激活扫描功能
- ❌ **不完整**：没有说明如何通知安全团队

**选项E：** 为所有容器镜像激活Amazon ECR的默认基础扫描。配置默认基础扫描使用持续扫描。在Amazon Simple Notification Service (Amazon SNS)中设置主题。
- ❌ **错误**：基础扫描功能有限，不如增强扫描全面
- ❌ **错误**：基础扫描不支持持续扫描模式
- ❌ **不完整**：缺少通知机制的配置

 |  |  |  |
| 324 | A DevOps administrator is conguring a repository to store a company's container images. The administrator needs to congure a lifecycle
rule that automatically deletes container images that have a specic tag and that are older than 15 days. | A. Create a repository in Amazon Elastic Container Registry (Amazon ECR). Add a lifecycle policy to the repository to expire images that
have the matching tag after 15 days.
B. Create a repository in AWS CodeArtifact. Add a repository policy to the CodeArtifact repository to expire old assets that have the
matching tag after 15 days.
C. Create a bucket in Amazon S3. Add a bucket lifecycle policy to expire old objects that have the matching tag after 15 days
D. Create an EC2 Image Builder container recipe. Add a build component to expire the container that has the matching tag after 15 days. | 一名DevOps管理员正在配置一个存储库来存储公司的容器镜像。管理员需要配置一个生命周期规则，自动删除具有特定标签且超过15天的容器镜像。

 | **选项A：在Amazon Elastic Container Registry (Amazon ECR)中创建存储库。向存储库添加生命周期策略，使具有匹配标签的镜像在15天后过期。**
- ✅ **正确**：ECR是AWS专门用于存储Docker容器镜像的托管服务
- ✅ ECR原生支持生命周期策略功能
- ✅ 可以基于镜像标签和时间设置自动删除规则
- ✅ 完全符合题目要求的场景

**选项B：在AWS CodeArtifact中创建存储库。向CodeArtifact存储库添加存储库策略，使具有匹配标签的旧资产在15天后过期。**
- ❌ **错误**：CodeArtifact主要用于存储软件包（如npm、Maven、PyPI包等）
- ❌ 虽然技术上可以存储容器镜像，但不是其主要用途
- ❌ 不是存储容器镜像的最佳实践

**选项C：在Amazon S3中创建存储桶。添加存储桶生命周期策略，使具有匹配标签的旧对象在15天后过期。**
- ❌ **错误**：虽然S3可以存储容器镜像文件，但缺乏容器镜像管理的专业功能
- ❌ 无法提供容器镜像的版本管理、安全扫描等功能
- ❌ 不符合容器镜像存储的最佳实践

**选项D：创建EC2 Image Builder容器配方。添加构建组件，使具有匹配标签的容器在15天后过期。**
- ❌ **错误**：EC2 Image Builder主要用于构建和管理AMI和容器镜像
- ❌ 不是用于存储和管理容器镜像生命周期的服务
- ❌ 构建组件不具备生命周期管理功能

 |  |  |  |
| 325 | A company uses Amazon Redshift as its data warehouse solution. The company wants to create a dashboard to view changes to the Redshift
users and the queries the users perform. | A. Create an Amazon CloudWatch log group. Create an AWS CloudTrail trail that writes to the CloudWatch log group.
B. Create a new Amazon S3 bucket. Congure default audit logging on the Redshift cluster. Congure the S3 bucket as the target.
C. Congure the Redshift cluster database audit logging to include user activity logs. Congure Amazon CloudWatch as the target.
D. Create an Amazon CloudWatch dashboard that has a log widget. Congure the widget to display user details from the Redshift logs.
E. Create an AWS Lambda function that uses Amazon Athena to query the Redshift logs. Create an Amazon CloudWatch dashboard that
has a custom widget type that uses the Lambda function. |  |  |  |  |  |
| 326 | A company uses an organization in AWS Organizations to manage its 500 AWS accounts. The organization has all features enabled. The AWS
accounts are in a single OU. The developers need to use the CostCenter tag key for all resources in the organization's member accounts.
Some teams do not use the CostCenter tag key to tag their Amazon EC2 instances.
The cloud team wrote a script that scans all EC2 instances in the organization's member accounts. If the EC2 instances do not have a
CostCenter tag key, the script will notify AWS account administrators. To avoid this notication, some developers use the CostCenter tag key
with an arbitrary string in the tag value.
The cloud team needs to ensure that all EC2 instances in the organization use a CostCenter tag key with the appropriate cost center value. | A. Create an SCP that prevents the creation of EC2 instances without the CostCenter tag key. Create a tag policy that requires the
CostCenter tag to be values from a known list of cost centers for all EC2 instances. Attach the policy to the OU. Update the script to scan
the tag keys and tag values. Modify the script to update noncompliant resources with a default approved tag value for the CostCenter tag
key.
B. Create an SCP that prevents the creation of EC2 instances without the CostCenter tag key. Attach the policy to the OU. Update the
script to scan the tag keys and tag values and notify the administrators when the tag values are not valid.
C. Create an SCP that prevents the creation of EC2 instances without the CostCenter tag key. Attach the policy to the OU. Create an IAM
permission boundary in the organization's member accounts that restricts the CostCenter tag values to a list of valid cost centers.
D. Create a tag policy that requires the CostCenter tag to be values from a known list of cost centers for all EC2 instances. Attach the
policy to the OU. Congure an AWS Lambda function that adds an empty CostCenter tag key to an EC2 instance. Create an Amazon
EventBridge rule that matches events to the RunInstances API action with the Lambda function as the target. | 一家公司使用AWS Organizations中的组织来管理其500个AWS账户。该组织已启用所有功能。这些AWS账户都在一个单独的OU中。开发人员需要为组织成员账户中的所有资源使用CostCenter标签键。
一些团队没有使用CostCenter标签键来标记他们的Amazon EC2实例。
云团队编写了一个脚本，扫描组织成员账户中的所有EC2实例。如果EC2实例没有CostCenter标签键，脚本会通知AWS账户管理员。为了避免这种通知，一些开发人员使用CostCenter标签键，但在标签值中使用任意字符串。
云团队需要确保组织中的所有EC2实例都使用带有适当成本中心值的CostCenter标签键。

 | **选项A：** 创建一个SCP阻止创建没有CostCenter标签键的EC2实例。创建一个标签策略，要求所有EC2实例的CostCenter标签必须来自已知成本中心列表的值。将策略附加到OU。更新脚本以扫描标签键和标签值。修改脚本以使用默认批准的CostCenter标签值更新不合规资源。
- **优点：** 结合了SCP和标签策略，既阻止创建不合规资源，又验证标签值的有效性
- **缺点：** 脚本自动修改资源标签可能不是最佳实践，应该让资源所有者负责

**选项B：** 创建一个SCP阻止创建没有CostCenter标签键的EC2实例。将策略附加到OU。更新脚本以扫描标签键和标签值，当标签值无效时通知管理员。
- **优点：** 使用SCP阻止创建不合规资源
- **缺点：** 只有通知机制，没有强制验证标签值的有效性，开发人员仍可使用任意值

**选项C：** 创建一个SCP阻止创建没有CostCenter标签键的EC2实例。将策略附加到OU。在组织成员账户中创建IAM权限边界，将CostCenter标签值限制为有效成本中心列表。
- **优点：** 使用SCP和IAM权限边界
- **缺点：** IAM权限边界主要用于限制用户权限，不是标签值验证的最佳工具；需要在每个成员账户中配置

**选项D：** 创建一个标签策略，要求所有EC2实例的CostCenter标签必须来自已知成本中心列表的值。将策略附加到OU。配置AWS Lambda函数为EC2实例添加空的CostCenter标签键。创建Amazon EventBridge规则匹配RunInstances API操作事件，以Lambda函数为目标。
- **优点：** 使用标签策略验证值的有效性
- **缺点：** 只添加空标签键没有解决问题；没有阻止创建不合规资源的机制

 | A |  |  |
| 327 | A DevOps engineer uses a pipeline in AWS CodePipeline. The pipeline has a build action and a deploy action for a single-page web application
that is delivered to an Amazon S3 bucket. Amazon CloudFront serves the web application. The build action creates an artifact for the web
application.
The DevOps engineer has created an AWS CloudFormation template that denes the S3 bucket and congures the S3 bucket to host the
application. The DevOps engineer has congured a CloudFormation deploy action before the S3 action. The CloudFormation deploy action
creates the S3 bucket. The DevOps engineer needs to congure the S3 deploy action to use the S3 bucket from the CloudFormation template. | A. Add an output named BucketName to the CloudFormation template. Set the output's value to refer to the S3 bucket from the
CloudFormation template. Congure the output value to export to an AWS::SSM::Parameter resource named Stackvariables.
B. Add an output named BucketName to the CloudFormation template. Set the output's value to refer to the S3 bucket from the
CloudFormation template. Set the CloudFormation action's namespace to StackVariables in the pipeline.
C. Congure the output artifacts of the CloudFormation action in the pipeline to be an AWS Systems Manager Parameter Store parameter
named StackVariables. Name the artifact BucketName.
D. Congure the build artifact from the build action as the input to the CodePipeline S3 deploy action. Congure the deploy action to
deploy to the S3 bucket by using the StackVariables.BucketName variable.
E. Congure the build artifact from the build action and the AWS Systems Manager parameter as the inputs to the deploy action. Congure
the deploy action to deploy to the S3 bucket by using the StackVariables.BucketName variable. | 一个DevOps工程师在AWS CodePipeline中使用管道。该管道包含一个构建操作和一个部署操作，用于将单页Web应用程序交付到Amazon S3存储桶。Amazon CloudFront为Web应用程序提供服务。构建操作为Web应用程序创建构件。

DevOps工程师已创建了一个AWS CloudFormation模板，该模板定义了S3存储桶并配置S3存储桶来托管应用程序。DevOps工程师在S3操作之前配置了CloudFormation部署操作。CloudFormation部署操作创建S3存储桶。DevOps工程师需要配置S3部署操作以使用CloudFormation模板中的S3存储桶。

 | **选项A：** 在CloudFormation模板中添加名为BucketName的输出。将输出值设置为引用CloudFormation模板中的S3存储桶。配置输出值导出到名为Stackvariables的AWS::SSM::Parameter资源。
- 这种方法过于复杂，需要额外创建SSM参数资源，不是最直接的解决方案。

**选项B：** 在CloudFormation模板中添加名为BucketName的输出。将输出值设置为引用CloudFormation模板中的S3存储桶。在管道中将CloudFormation操作的命名空间设置为StackVariables。
- 这是正确的方法。通过设置CloudFormation操作的命名空间，可以在后续操作中使用输出变量。

**选项C：** 在管道中将CloudFormation操作的输出构件配置为名为StackVariables的AWS Systems Manager Parameter Store参数。将构件命名为BucketName。
- 这种描述不准确，CloudFormation操作的输出不是通过构件形式传递的。

**选项D：** 将构建操作的构建构件配置为CodePipeline S3部署操作的输入。配置部署操作使用StackVariables.BucketName变量部署到S3存储桶。
- 缺少CloudFormation输出的配置步骤，无法获取存储桶名称。

**选项E：** 将构建操作的构建构件和AWS Systems Manager参数配置为部署操作的输入。配置部署操作使用StackVariables.BucketName变量部署到S3存储桶。
- 同样缺少CloudFormation输出的正确配置。

 |  |  |  |
| 328 | A company used a lift and shift strategy to migrate a workload to AWS. The company has an Auto Scaling group of Amazon EC2 instances.
Each EC2 instance runs a web application, a database, and a Redis cache.
Users are experiencing large variations in the web application's response times. Requests to the web application go to a single EC2 instance
that is under signicant load. The company wants to separate the application components to improve availability and performance. | A. Create a Network Load Balancer and an Auto Scaling group for the web application. Migrate the database to an Amazon Aurora
Serverless database. Create an Application Load Balancer and an Auto Scaling group for the Redis cache.
B. Create an Application Load Balancer and an Auto Scaling group for the web application. Migrate the database to an Amazon Aurora
database that has a Multi-AZ deployment. Create a Network Load Balancer and an Auto Scaling group in a single Availability Zone for the
Redis cache.
C. Create a Network Load Balancer and an Auto Scaling group for the web application. Migrate the database to an Amazon Aurora
Serverless database. Create an Amazon ElastiCache (Redis OSS) cluster for the cache. Create a target group that has a DNS target type
that contains the ElastiCache (Redis OSS) cluster hostname.
D. Create an Application Load Balancer and an Auto Scaling group for the web application. Migrate the database to an Amazon Aurora
database that has a Multi-AZ deployment. Create an Amazon ElastiCache (Redis OSS) cluster for the cache. |  |  |  |  |  |
| 329 | A company is using AWS Organizations and wants to implement a governance strategy with the following requirements:
• AWS resource access is restricted to the same two Regions for all accounts.
• AWS services are limited to a specic group of authorized services for all accounts.
• Authentication is provided by Active Directory.
• Access permissions are organized by job function and are identical in each account. | A. Establish an organizational unit (OU) with group policies in the management account to restrict Regions and authorized services. Use
AWS CloudFormation StackSets to provision roles with permissions for each job function, including an IAM trust policy for IAM identity
provider authentication in each account.
B. Establish a permission boundary in the management account to restrict Regions and authorized services. Use AWS CloudFormation
StackSets to provision roles with permissions for each job function, including an IAM trust policy for IAM identity provider authentication
in each account.
C. Establish a service control policy in the management account to restrict Regions and authorized services. Use AWS Resource Access
Manager (AWS RAM) to share management account roles with permissions for each job function, including AWS IAM Identity Center for
authentication in each account.
D. Establish a service control policy in the management account to restrict Regions and authorized services. Use AWS CloudFormation
StackSets to provision roles with permissions for each job function, including an IAM trust policy for IAM identity provider authentication
in each account. |  |  |  |  |  |
| 330 | A company detects unusual login attempts in many of its AWS accounts. A DevOps engineer must implement a solution that sends a
notication to the company's security team when multiple failed login attempts occur. The DevOps engineer has already created an Amazon
Simple Notication Service (Amazon SNS) topic and has subscribed the security team to the SNS topic. | A. Congure AWS CloudTrail to send management events to an Amazon CloudWatch Logs log group. Create a CloudWatch Logs metric
lter to match failed ConsoleLogin events. Create a CloudWatch alarm that is based on the metric lter. Congure an alarm action to send
messages to the SNS topic.
B. Congure AWS CloudTrail to send management events to an Amazon S3 bucket. Create an Amazon Athena query that returns a failure
if the query nds failed logins in the logs in the S3 bucket. Create an Amazon EventBridge rule to periodically run the query. Create a
second EventBridge rule to detect when the query fails and to send a message to the SNS topic.
C. Congure AWS CloudTrail to send data events to an Amazon CloudWatch Logs log group. Create a CloudWatch logs metric lter to
match failed ConsoleLogin events. Create a CloudWatch alarm that is based on the metric lter. Congure an alarm action to send
messages to the SNS topic.
D. Congure AWS CloudTrail to send data events to an Amazon S3 bucket. Congure an Amazon S3 event notication for the
s3:ObjectCreated event type. Filter the event type by ConsoleLogin failed events. Congure the event notication to forward to the SNS
topic. | 一家公司在其多个AWS账户中检测到异常的登录尝试。DevOps工程师必须实施一个解决方案，当发生多次登录失败尝试时向公司安全团队发送通知。DevOps工程师已经创建了一个Amazon Simple Notification Service (Amazon SNS) 主题，并让安全团队订阅了该SNS主题。

 | **选项A：** 配置AWS CloudTrail将管理事件发送到Amazon CloudWatch Logs日志组。创建CloudWatch Logs指标过滤器来匹配失败的ConsoleLogin事件。基于该指标过滤器创建CloudWatch告警。配置告警操作向SNS主题发送消息。

- ✅ **正确**：登录事件属于管理事件，CloudTrail默认记录管理事件
- ✅ ConsoleLogin失败事件可以通过CloudWatch Logs指标过滤器准确捕获
- ✅ CloudWatch告警可以基于指标触发并发送SNS通知
- ✅ 这是一个实时、高效的解决方案

**选项B：** 配置AWS CloudTrail将管理事件发送到Amazon S3存储桶。创建Amazon Athena查询，如果在S3存储桶的日志中发现登录失败则返回失败。创建Amazon EventBridge规则定期运行查询。创建第二个EventBridge规则检测查询失败并向SNS主题发送消息。

- ❌ 过于复杂，需要多个组件协调工作
- ❌ 不是实时解决方案，依赖定期查询
- ❌ Athena查询失败不等同于检测到登录失败事件
- ❌ 架构设计不合理

**选项C：** 配置AWS CloudTrail将数据事件发送到Amazon CloudWatch Logs日志组。创建CloudWatch Logs指标过滤器来匹配失败的ConsoleLogin事件。基于该指标过滤器创建CloudWatch告警。配置告警操作向SNS主题发送消息。

- ❌ **关键错误**：ConsoleLogin事件是管理事件，不是数据事件
- ❌ 数据事件主要记录S3对象级操作和Lambda函数调用
- ❌ 配置数据事件无法捕获登录失败事件

**选项D：** 配置AWS CloudTrail将数据事件发送到Amazon S3存储桶。为s3:ObjectCreated事件类型配置Amazon S3事件通知。通过ConsoleLogin失败事件过滤事件类型。配置事件通知转发到SNS主题。

- ❌ ConsoleLogin事件是管理事件，不是数据事件
- ❌ S3事件通知用于S3对象操作，与登录事件无关
- ❌ 无法通过S3事件通知过滤ConsoleLogin事件
- ❌ 架构概念混淆

 |  |  |  |
| 331 | A company has deployed a new REST API by using Amazon API Gateway. The company uses the API to access condential data. The API must
be accessed from only specic VPCs in the company. | A. Create and attach a resource policy to the API Gateway API. Congure the resource policy to allow only the specic VPC IDs.
B. Add a security group to the API Gateway API. Congure the inbound rules to allow only the specic VPC IP address ranges.
C. Create and attach an IAM role to the API Gateway API. Congure the IAM role to allow only the specic VPC IDs.
D. Add an ACL to the API Gateway API. Congure the outbound rules to allow only the specic VPC IP address ranges. | 一家公司使用Amazon API Gateway部署了一个新的REST API。该公司使用这个API来访问机密数据。该API必须只能从公司内的特定VPC进行访问。

选项：
A. 创建资源策略并将其附加到API Gateway API。配置资源策略以仅允许特定的VPC ID。
B. 向API Gateway API添加安全组。配置入站规则以仅允许特定的VPC IP地址范围。
C. 创建IAM角色并将其附加到API Gateway API。配置IAM角色以仅允许特定的VPC ID。
D. 向API Gateway API添加ACL。配置出站规则以仅允许特定的VPC IP地址范围。

 | **选项A：创建资源策略并将其附加到API Gateway API**
- ✅ **正确**：API Gateway资源策略是控制API访问的正确方法
- 资源策略可以基于多种条件进行访问控制，包括VPC、VPC端点、IP地址等
- 可以使用条件键如`aws:sourceVpc`或`aws:sourceVpce`来限制特定VPC的访问
- 这是AWS推荐的最佳实践方法

**选项B：向API Gateway添加安全组**
- ❌ **错误**：API Gateway是托管服务，不支持直接附加安全组
- 安全组是用于EC2实例、RDS等资源的网络访问控制
- API Gateway使用资源策略而不是安全组进行访问控制

**选项C：创建IAM角色并附加到API Gateway API**
- ❌ **错误**：IAM角色主要用于身份验证和授权，而不是基于网络位置的访问控制
- IAM角色无法直接限制特定VPC的访问
- 虽然IAM可以与资源策略结合使用，但单独的IAM角色无法满足VPC限制需求

**选项D：向API Gateway添加ACL**
- ❌ **错误**：API Gateway不使用传统的网络ACL
- 网络ACL是VPC级别的网络控制，不适用于API Gateway
- 出站规则的配置方向也不正确，应该关注的是入站访问控制

 |  |  |  |
| 332 | A company runs a website by using an Amazon Elastic Container Service (Amazon ECS) service that is connected to an Application Load
Balancer (ALB). The service was in a steady state with tasks responding to requests successfully.
A DevOps engineer updated the task denition with a new container image and deployed the new task denition to the service. The DevOps
engineer noticed that the service is frequently stopping and starting new tasks because the ALB healtth checks are failing. | A. Ensure that a security group associated with the service allows trac from the AL
B. Increase the ALB health check grace period for the service.
C. Increase the service minimum healthy percent setting.
D. Decrease the ALB health check interval. | 一家公司使用连接到应用负载均衡器(ALB)的Amazon弹性容器服务(Amazon ECS)来运行网站。该服务之前处于稳定状态，任务能够成功响应请求。

一名DevOps工程师使用新的容器镜像更新了任务定义，并将新的任务定义部署到服务中。DevOps工程师注意到服务频繁地停止和启动新任务，因为ALB健康检查失败。

 | **A. 确保与服务关联的安全组允许来自ALB的流量**
- 如果安全组配置有问题，ALB无法访问ECS任务，会导致健康检查失败
- 但题目提到服务之前处于稳定状态，说明安全组配置应该是正确的
- 除非新镜像改变了端口配置，否则这不太可能是根本原因

**B. 增加服务的ALB健康检查宽限期**
- 健康检查宽限期是指新启动的任务在开始接受健康检查之前的等待时间
- 新容器镜像可能需要更长时间来启动和初始化应用程序
- 如果宽限期太短，ALB会在应用程序完全准备好之前就开始健康检查，导致检查失败
- 这是处理新镜像启动时间变化的常见解决方案

**C. 增加服务最小健康百分比设置**
- 这个设置控制在部署期间必须保持运行的任务百分比
- 增加这个值会让部署更保守，但不会解决健康检查失败的根本问题
- 如果健康检查仍然失败，增加这个百分比只会让问题更严重

**D. 减少ALB健康检查间隔**
- 减少检查间隔意味着更频繁地进行健康检查
- 这实际上会使问题变得更糟，因为会更快地检测到"失败"状态
- 不会给应用程序更多时间来启动

 | B |  |  |
| 333 | A company that uses electronic patient health records runs a eet of Amazon EC2 instances with an Amazon Linux operating system. The
company must continuously ensure that the EC2 instances are running operating system patches and application patches that are in
compliance with current privacy regulations. The company uses a custom repository to store application patches.
A DevOps engineer needs to automate the deployment of operating system patches and application patches. The DevOps engineer wants to
use both the default operating system patch repository and the custom patch repository. | A. Use AWS Systems Manager to create a new custom patch baseline that includes the default operating system repository and the
custom repository. Run the AWS-RunPatchBaseline document by using the Run command to verify and install patches. Use the
BaselineOverride API to congure the new custom patch baseline.
B. Use AWS Direct Connect to integrate the custom repository with the EC2 instances. Use Amazon EventBridge events to deploy the
patches.
C. Use the yum-cong-manager command to add the custom repository to the /etc/yum.repos.d conguration. Run the yum-cong-
manager-enable command to activate the new repository.
D. Use AWS Systems Manager to create a patch baseline for the default operating system repository and a second patch baseline for the
custom repository. Run the AWS-RunPatchBaseline document by using the Run command to verify and install patches. Use the
BaselineOverride API to congure the default patch baseline and the custom patch baseline. | 一家使用电子患者健康记录的公司运行着一组使用Amazon Linux操作系统的Amazon EC2实例。该公司必须持续确保EC2实例运行的操作系统补丁和应用程序补丁符合当前隐私法规的合规要求。该公司使用自定义存储库来存储应用程序补丁。

DevOps工程师需要自动化部署操作系统补丁和应用程序补丁。DevOps工程师希望同时使用默认的操作系统补丁存储库和自定义补丁存储库。

 | **选项A：** 使用AWS Systems Manager创建一个新的自定义补丁基线，包含默认操作系统存储库和自定义存储库。使用Run命令运行AWS-RunPatchBaseline文档来验证和安装补丁。使用BaselineOverride API配置新的自定义补丁基线。
- **正确性：高** - 这是AWS推荐的方法，可以在单个补丁基线中整合多个存储库
- Systems Manager Patch Manager支持自定义补丁基线
- BaselineOverride API允许灵活配置补丁基线
- 可以同时管理OS和应用程序补丁

**选项B：** 使用AWS Direct Connect将自定义存储库与EC2实例集成。使用Amazon EventBridge事件部署补丁。
- **正确性：低** - Direct Connect主要用于网络连接，不是补丁管理的合适工具
- EventBridge虽然可以触发事件，但不是补丁部署的最佳选择
- 缺乏补丁管理的自动化和合规性跟踪功能

**选项C：** 使用yum-config-manager命令将自定义存储库添加到/etc/yum.repos.d配置。运行yum-config-manager-enable命令激活新存储库。
- **正确性：中等** - 这是手动配置方法，可以工作但不够自动化
- 需要在每个实例上手动执行
- 缺乏集中管理和合规性报告功能
- 不符合"自动化部署"的要求

**选项D：** 使用AWS Systems Manager为默认操作系统存储库创建一个补丁基线，为自定义存储库创建第二个补丁基线。使用Run命令运行AWS-RunPatchBaseline文档来验证和安装补丁。使用BaselineOverride API配置默认补丁基线和自定义补丁基线。
- **正确性：中等** - 技术上可行，但不是最优方案
- 需要管理两个独立的补丁基线，增加复杂性
- 可能导致补丁冲突或重复执行

 |  |  |  |
| 334 | A company use an organization in AWS Organizations to manage multiple AWS accounts. The company has enabled all features enabled for
the organization. The company congured the organization as a hierarchy of OUs under the root OU. The company recently registered all its
OUs and enrolled all its AWS accounts in AWS Control Tower.
The company needs to customize the AWS Control Tower managed AWS Cong conguration recorder in each of the company's AWS accounts.
The company needs to apply the customizations to both the existing AWS accounts and to any new AWS accounts that the company enrolls in
AWS Control Tower in the future. | A. Create a new AWS account. Create an AWS Lambda function in the new account to apply the customizations to the AWS Cong
conguration recorder in each AWS account in the organization.
B. Create a new AWS account as an AWS Cong delegated administrator. Create an AWS Lambda function in the delegated administrator
account to apply the customizations to the AWS Cong conguration recorder in the delegated administrator account.
C. Congure an Amazon EventBridge rule in the AWS Control Tower management account to invoke an AWS Lambda function when the
Organizations OU is registered or reregistered. Re-register the root Organizations OU.
D. Congure the AWSControlTowerExecution IAM role in each AWS account in the organization to be assumable by an AWS Lambda
function. Congure the Lambda function to assume the AWSControlTowerExecution IAM role.
E. Create an IAM role in the AWS Control Tower management account that an AWS Lambda function can assume. Grant the IAM role
permission to assume the AWSControlTowerExecution IAM role in any account in the organization. Congure the Lambda function to use
the new IAM role.
F. Congure an Amazon EventBridge rule in the AWS Control Tower management account to invoke an AWS Lambda function when an AWS
account is updated or enrolled in AWS Control Tower or when the landing zone is updated. Re-register each Organizations OU in the
organization. |  |  |  |  |  |
| 335 | A company runs an application in an Auto Scaling group of Amazon EC2 instances behind an Application Load Balancer (ALB). The EC2
instances run Docker containers that make requests to a MySQL database that runs on separate EC2 instances.
A DevOps engineer needs to update the application to use a serverless architecture. | A. Replace the containers that run on EC2 instances and the ALB with AWS Lambda functions. Replace the MySQL database with an
Amazon Aurora Serverless v2 database that is compatible with MySQL.
B. Replace the containers that run on EC2 instances with AWS Fargate. Replace the MySQL database with an Amazon Aurora Serverless
v2 database that is compatible with MySQL.
C. Replace the containers that run on EC2 instances and the ALB with AWS Lambda functions. Replace the MySQL database with Amazon
DynamoDB tables.
D. Replace the containers that run on EC2 instances with AWS Fargate. Replace the MySQL database with Amazon DynamoDB tables. | 一家公司在应用负载均衡器(ALB)后面的Amazon EC2实例自动扩展组中运行应用程序。EC2实例运行Docker容器，这些容器向运行在独立EC2实例上的MySQL数据库发出请求。

DevOps工程师需要将应用程序更新为使用无服务器架构。

 | **选项A：用AWS Lambda函数替换运行在EC2实例上的容器和ALB。用与MySQL兼容的Amazon Aurora Serverless v2数据库替换MySQL数据库。**
- ✅ Lambda是真正的无服务器计算服务
- ✅ Aurora Serverless v2是无服务器数据库解决方案
- ✅ 保持MySQL兼容性，迁移成本较低
- ✅ 完全符合无服务器架构要求

**选项B：用AWS Fargate替换运行在EC2实例上的容器。用与MySQL兼容的Amazon Aurora Serverless v2数据库替换MySQL数据库。**
- ❌ Fargate虽然是托管容器服务，但不是完全无服务器的
- ✅ Aurora Serverless v2是无服务器数据库
- ❌ 不完全符合无服务器架构要求

**选项C：用AWS Lambda函数替换运行在EC2实例上的容器和ALB。用Amazon DynamoDB表替换MySQL数据库。**
- ✅ Lambda是无服务器计算服务
- ✅ DynamoDB是无服务器NoSQL数据库
- ❌ 从MySQL迁移到DynamoDB需要重大的应用程序重构
- ❌ 数据模型完全不同，迁移复杂度高

**选项D：用AWS Fargate替换运行在EC2实例上的容器。用Amazon DynamoDB表替换MySQL数据库。**
- ❌ Fargate不是完全无服务器的
- ✅ DynamoDB是无服务器数据库
- ❌ 数据库迁移复杂度高

 |  |  |  |
| 336 | A company uses an organization in AWS Organizations to manage 10 AWS accounts. All features are enabled, and trusted access for AWS
CloudFormation is enabled.
A DevOps engineer needs to use CloudFormation to deploy an IAM role to the Organizations management account and all member accounts
in the organization. | A. Create a CloudFormation StackSet that has service-managed permissions. Set the root OU as a deployment target.
B. Create a CloudFormation StackSet that has service-managed permissions. Set the root OU as a deployment target. Deploy a separate
CloudFormation stack in the Organizations management account.
C. Create a CloudFormation StackSet that has self-managed permissions. Set the root OU as a deployment target.
D. Create a CloudFormation StackSet that has self-managed permissions. Set the root OU as a deployment target. Deploy a separate
CloudFormation stack in the Organizations management account. | 一家公司使用AWS Organizations中的组织来管理10个AWS账户。所有功能都已启用，并且已为AWS CloudFormation启用了可信访问。

一名DevOps工程师需要使用CloudFormation将IAM角色部署到Organizations管理账户和组织中的所有成员账户。

 | **选项A：创建具有服务管理权限的CloudFormation StackSet。将根OU设置为部署目标。**
- 服务管理权限允许StackSet自动管理跨账户部署所需的IAM角色
- 将根OU作为目标可以覆盖所有成员账户
- 但是，服务管理的StackSet默认情况下不会部署到管理账户本身

**选项B：创建具有服务管理权限的CloudFormation StackSet。将根OU设置为部署目标。在Organizations管理账户中部署单独的CloudFormation堆栈。**
- 使用服务管理权限的StackSet部署到所有成员账户
- 通过单独的CloudFormation堆栈处理管理账户的部署
- 这种方法可以确保管理账户和所有成员账户都得到覆盖

**选项C：创建具有自管理权限的CloudFormation StackSet。将根OU设置为部署目标。**
- 自管理权限需要手动在每个目标账户中预先配置IAM角色
- 对于10个账户来说，这会增加管理复杂性
- 同样不会自动部署到管理账户

**选项D：创建具有自管理权限的CloudFormation StackSet。将根OU设置为部署目标。在Organizations管理账户中部署单独的CloudFormation堆栈。**
- 结合了自管理权限的复杂性和单独堆栈的方法
- 虽然能达到目标，但不是最优解决方案

 |  |  |  |
| 337 | A company runs an application that stores artifacts in an Amazon S3 bucket. The application has a large user base. The application writes a
high volume of objects to the S3 bucket. The company has enabled event notications for the S3 bucket.
When the application writes an object to the S3 bucket, several processing tasks need to be performed simultaneously. The company's DevOps
team needs to create an AWS Step Functions workow to orchestrate the processing tasks. | A. Create a Standard workow that contains a parallel state that denes the processing tasks. Create an Asynchronous Express workow
that contains a parallel state that denes the processing tasks.
B. Create a Synchronous Express workow that contains a map state that denes the processing tasks.
C. Create an Amazon EventBridge rule to match when a new S3 object is created. Congure the EventBridge rule to invoke an AWS
Lambda function. Congure the Lambda function to start the processing workow.
D. Create an Amazon EventBridge rule to match when a new S3 object is created. Congure the EventBridge rule to start the processing
workow. | 一家公司运行一个应用程序，该应用程序将工件存储在Amazon S3存储桶中。该应用程序拥有大量用户基础。应用程序向S3存储桶写入大量对象。公司已为S3存储桶启用了事件通知。

当应用程序向S3存储桶写入对象时，需要同时执行多个处理任务。公司的DevOps团队需要创建一个AWS Step Functions工作流来编排这些处理任务。

 | **选项A：** 创建一个包含并行状态定义处理任务的标准工作流。创建一个包含并行状态定义处理任务的异步Express工作流。
- 这个选项描述不清晰，似乎在说创建两种不同的工作流
- 没有说明如何触发工作流
- 缺少与S3事件通知的集成机制

**选项B：** 创建一个包含映射状态定义处理任务的同步Express工作流。
- 同步Express工作流适用于需要立即响应的短时间运行任务
- Map状态主要用于处理数组或集合中的每个项目，而不是并行执行不同的处理任务
- 同样没有说明如何与S3事件集成

**选项C：** 创建Amazon EventBridge规则来匹配新S3对象创建事件。配置EventBridge规则调用AWS Lambda函数。配置Lambda函数启动处理工作流。
- 提供了完整的事件驱动架构：S3事件 → EventBridge → Lambda → Step Functions
- Lambda函数作为中间层可以进行额外的处理或验证
- 这是一个可行的解决方案，但增加了额外的Lambda层

**选项D：** 创建Amazon EventBridge规则来匹配新S3对象创建事件。配置EventBridge规则直接启动处理工作流。
- 提供了最直接的事件驱动架构：S3事件 → EventBridge → Step Functions
- EventBridge可以直接启动Step Functions工作流，无需中间层
- 更简洁、成本更低、延迟更少的解决方案

 |  |  |  |
| 338 | A DevOps team supports an application that runs in an Amazon Elastic Container Service (Amazon ECS) cluster behind an Application Load
Balancer (ALB). Currently, the DevOps team uses AWS CodeDeploy to deploy the application by using a blue/green all-at-once strategy.
Recently, the DevOps team had to roll back a deployment when a new version of the application dramatically increased response times for
requests.
The DevOps team needs use to a deployment strategy that will allow the team to monitor a new version of the application before the team
shifts all trac to the new version. If a new version of the application increases response times, the deployment should be rolled back as
quickly as possible. | A. Modify the CodeDeploy deployment to use the CodeDeployDefault.ECSCanary10Percent5Minutes conguration.
B. Set the alarm to activate if the
metric is higher than the desired value. Associate the alarm with the CodeDeploy deployment group. Modify the deployment group to roll
back when alarm thresholds are met.
C. Create an Amazon CloudWatch alarm to monitor the UnHealthyHostCount metric for the AL
D. Create an Amazon CloudWatch alarm to monitor the TargetResponseTime metric for the AL
E. Create an Amazon CloudWatch alarm to monitor the TargetConnectionErrorCount metric for the AL | 一个DevOps团队支持运行在Amazon Elastic Container Service (Amazon ECS)集群中的应用程序，该集群位于Application Load Balancer (ALB)后面。目前，DevOps团队使用AWS CodeDeploy通过蓝/绿一次性部署策略来部署应用程序。

最近，当应用程序的新版本显著增加了请求的响应时间时，DevOps团队不得不回滚部署。

DevOps团队需要使用一种部署策略，允许团队在将所有流量切换到新版本之前监控应用程序的新版本。如果应用程序的新版本增加了响应时间，部署应该尽快回滚。

 | **选项A：** 修改CodeDeploy部署以使用CodeDeployDefault.ECSCanary10Percent5Minutes配置。
- 这是正确的部署策略选择
- Canary部署策略允许将10%的流量先路由到新版本，持续5分钟
- 这样可以在全量切换前监控新版本的性能表现
- 符合题目要求的渐进式部署需求

**选项B：** 设置告警在指标高于期望值时激活。将告警与CodeDeploy部署组关联。修改部署组在告警阈值达到时回滚。
- 这个选项描述不完整，没有指定具体的监控指标
- 虽然自动回滚机制是正确的概念，但缺少关键的指标定义

**选项C：** 创建Amazon CloudWatch告警监控ALB的UnHealthyHostCount指标。
- UnHealthyHostCount指标监控不健康的目标数量
- 这个指标主要反映目标健康状况，不是直接监控响应时间的最佳指标
- 不能很好地解决题目中提到的响应时间问题

**选项D：** 创建Amazon CloudWatch告警监控ALB的TargetResponseTime指标。
- TargetResponseTime是监控响应时间的正确指标
- 直接对应题目中提到的响应时间问题
- 可以设置阈值来检测响应时间的异常增加
- 这是监控响应时间性能的最佳选择

**选项E：** 创建Amazon CloudWatch告警监控ALB的TargetConnectionErrorCount指标。
- 这个指标监控连接错误数量
- 主要关注连接层面的问题，而不是响应时间性能问题
- 不符合题目中关于响应时间监控的具体需求

 |  |  |  |
| 339 | A security team must record the conguration of AWS resources, detect issues, and send notications for ndings. The main workload in the
AWS account consists of an Amazon EC2 Auto Scaling group that scales in and out several times during the day.
The team wants to be notied within 2 days if any Amazon EC2 security group allows trac on port 22 for 0.0.0.0/0. The team also needs a
snapshot of the conguration of the AWS resources to be taken routinely.
The security team has already created and subscribed to an Amazon Simple Notication Service (Amazon SNS) topic. | A. Congure AWS Cong to use periodic recording for the AWS account. Deploy the vpc-sg-port-restriction-check AWS Cong managed rule.
Congure AWS Cong to use the SNS topic as the target for notications.
B. Congure AWS Cong to use conguration change recording for the AWS account. Deploy the vpc-sg-open-only-to-authorized-ports AWS
Cong managed rule. Congure AWS Cong to use the SNS topic as the target for notications.
C. Congure AWS Cong to use conguration change recording for the AWS account. Deploy the ssh-restricted AWS Cong managed rule.
Congure AWS Cong to use the SNS topic as the target for notications.
D. Create an AWS Lambda function to evaluate security groups and publish a message to the SNS topic. Use an Amazon EventBridge rule
to schedule the Lambda function to run once a day. |  |  |  |  |  |
| 340 | A company has proprietary data available by using an Amazon CloudFront distribution. The company needs to ensure that the distribution is
accessible by only users from the corporate oce that have a known set of IP address ranges. An AWS WAF web ACL is associated with the
distribution and has a default action set to Count. | A. Create a new regex pattern set. Add the regex pattern set to a new rule group. Create a new web ACL that has a default action set to
Block. Associate the web ACL with the CloudFront distribution. Add a rule that allows trac based on the new rule group.
B. Create an AWS WAF IP address set that matches the corporate oce IP address range. Create a new web ACL that has a default action
set to Allow. Associate the web ACL with the CloudFront distribution. Add a rule that allows trac from the IP address set.
C. Create a new regex pattern set. Add the regex pattern set to a new rule group. Set the default action on the existing web ACL to Allow.
Add a rule that has priority 0 that allows trac based on the regex pattern set.
D. Create a WAF IP address set that matches the corporate oce IP address range. Set the default action on the existing web ACL to
Block. Add a rule that has priority 0 that allows trac from the IP address set. | 一家公司通过Amazon CloudFront分发拥有专有数据。该公司需要确保该分发只能被来自已知IP地址范围的企业办公室用户访问。AWS WAF web ACL已与该分发关联，并且默认操作设置为Count（计数）。

 | **选项A：** 创建新的正则表达式模式集，将其添加到新规则组中。创建默认操作设置为Block的新web ACL，将web ACL与CloudFront分发关联，添加基于新规则组允许流量的规则。
- **问题：** 使用正则表达式模式集来处理IP地址限制是不合适的。正则表达式模式集主要用于匹配字符串模式，而不是IP地址范围。IP地址应该使用专门的IP集合来处理。

**选项B：** 创建匹配企业办公室IP地址范围的AWS WAF IP地址集。创建默认操作设置为Allow的新web ACL，将web ACL与CloudFront分发关联，添加允许来自IP地址集流量的规则。
- **问题：** 默认操作设置为Allow是错误的安全配置。这意味着所有不匹配规则的流量都会被允许，这与题目要求的"只允许特定IP范围访问"相矛盾。

**选项C：** 创建新的正则表达式模式集，将其添加到新规则组中。将现有web ACL的默认操作设置为Allow，添加优先级为0的规则，基于正则表达式模式集允许流量。
- **问题：** 同样使用了不合适的正则表达式模式集来处理IP地址，且默认操作为Allow存在安全风险。

**选项D：** 创建匹配企业办公室IP地址范围的WAF IP地址集。将现有web ACL的默认操作设置为Block，添加优先级为0的规则，允许来自IP地址集的流量。
- **正确：** 使用了正确的IP地址集来匹配IP范围，默认操作设置为Block确保只有明确允许的流量才能通过，优先级0确保允许规则优先执行。

 |  |  |  |
| 341 | A company runs several applications in the same AWS account. The applications send logs to Amazon CloudWatch.
A data analytics team needs to collect performance metrics and custom metrics from the applications. The analytics team needs to transform
the metrics data before storing the data in an Amazon S3 bucket. The analytics team must automatically collect any new metrics that are
added to the CloudWatch namespace. | A. Congure a CloudWatch metric stream to include metrics from the application and the CloudWatch namespace. Congure the metric
stream to deliver the metrics to an Amazon Data Firehose delivery stream. Congure the Firehose delivery stream to invoke an AWS
Lambda function to transform the data. Congure the delivery stream to send the transformed data to the S3 bucket.
B. Congure a CloudWatch metrics stream to include all the metrics and to deliver the metrics to an Amazon Data Firehose delivery
stream. Congure the Firehose delivery stream to invoke an AWS Lambda function to transform the data. Congure the delivery stream to
send the transformed data to the S3 bucket.
C. Congure metric lters for the CloudWatch logs to create custom metrics. Congure a CloudWatch metric stream to deliver the
application metrics to the S3 bucket.
D. Congure subscription lters on the application log groups to target an Amazon Data Firehose delivery stream. Congure the Firehose
delivery stream to invoke an AWS Lambda function to transform the data. Congure the delivery stream to send the transformed data to
the S3 bucket. |  |  |  |  |  |
| 342 | A company uses an HPC platform to run analysis jobs for data. The company uses AWS CodeBuild to create container images and store the
images on Amazon Elastic Container Registry (Amazon ECR). The images are then deployed on Amazon Elastic Kubernetes Service (Amazon
EKS).
To maintain compliance, the company needs to ensure that the images are signed before the images are deployed on Amazon EKS. The
signing keys must be rotated periodically and must be managed automatically. The company needs to track who generates the signatures. | A. Use CodeBuild to retrieve the image that was previously pushed to Amazon ECR. Use AWS Signer to sign the image. Use AWS CloudTrail
to track who generates the signatures.
B. Use AWS Lambda to retrieve the image that was previously pushed to Amazon ECR. Use a Lambda function to sign the image. Use
Amazon CloudWatch to track who generates the signatures.
C. Use AWS Lambda to retrieve the image that was previously pushed to Amazon ECR. Use AWS Signer to sign the image. Use Amazon
CloudWatch to track who generates the signatures.
D. Use CodeBuild to build the image. Sign the image by using AWS Signer before pushing the image to Amazon ECR. Use AWS CloudTrail
to track who generates the signatures. | 一家公司使用HPC平台来运行数据分析作业。该公司使用AWS CodeBuild创建容器镜像并将镜像存储在Amazon Elastic Container Registry (Amazon ECR)上。然后将这些镜像部署在Amazon Elastic Kubernetes Service (Amazon EKS)上。

为了保持合规性，公司需要确保镜像在部署到Amazon EKS之前进行签名。签名密钥必须定期轮换并且必须自动管理。公司需要跟踪谁生成了签名。

 | **选项A：使用CodeBuild检索之前推送到Amazon ECR的镜像。使用AWS Signer对镜像进行签名。使用AWS CloudTrail跟踪谁生成签名。**
- ✅ AWS Signer是专门用于代码签名的托管服务，支持自动密钥轮换
- ✅ CloudTrail可以准确跟踪API调用和签名操作的用户身份
- ❌ 在镜像已经推送到ECR后再签名的流程不够优化

**选项B：使用AWS Lambda检索之前推送到Amazon ECR的镜像。使用Lambda函数对镜像进行签名。使用Amazon CloudWatch跟踪谁生成签名。**
- ❌ 使用Lambda自定义签名功能需要手动管理密钥，不符合自动管理要求
- ❌ CloudWatch主要用于监控指标，不是跟踪用户身份的最佳选择
- ❌ 增加了不必要的复杂性

**选项C：使用AWS Lambda检索之前推送到Amazon ECR的镜像。使用AWS Signer对镜像进行签名。使用Amazon CloudWatch跟踪谁生成签名。**
- ✅ AWS Signer提供自动密钥管理和轮换
- ❌ CloudWatch不是跟踪用户操作的合适工具
- ❌ 使用Lambda增加了不必要的复杂性

**选项D：使用CodeBuild构建镜像。在将镜像推送到Amazon ECR之前使用AWS Signer对镜像进行签名。使用AWS CloudTrail跟踪谁生成签名。**
- ✅ AWS Signer提供完整的签名解决方案和自动密钥管理
- ✅ CloudTrail是跟踪API调用和用户操作的标准服务
- ✅ 在推送到ECR之前签名是最佳实践，确保只有签名的镜像进入仓库
- ✅ 与现有的CodeBuild流程无缝集成

 |  |  |  |
| 343 | A company uses an AWS CodeArtifact repository to store Python packages that the company developed internally. A DevOps engineer needs
to use AWS CodeDeploy to deploy an application to an Amazon EC2 instance. The application uses a Python package that is stored in the
CodeArtifact repository. A BeforeInstall lifecycle event hook will install the package.
The DevOps engineer needs to grant the EC2 instance access to the CodeArtifact repository. | A. Create a service-linked role for CodeArtifact. Associate the role with the EC2 instance. Use the aws codeartifact get-authorization-token
CLI command on the instance.
B. Congure a resource-based policy for the CodeArtifact repository that allows the ReadFromRepository action for the EC2 instance
principal.
C. Congure ACLs on the CodeArtifact repository to allow the EC2 instance to access the Python package.
D. Create an instance prole that contains an IAM role that has access to CodeArtifact. Associate the instance prole with the EC2
instance. Use the aws codeartifact login CLI command on the instance. |  |  |  |  |  |
| 344 | A company has a le-reading application that saves les to a database that runs on Amazon EC2 instances. Regulations require the company
to delete les from EC2 instances every day at a specic time. The company must delete database records that are older than 60 days.
The database record deletion must occur after the le deletions. The company has created scripts to delete les and database records. The
company needs to receive an email notication for any failure of the deletion scripts. | A. Use AWS Systems Manager State Manager to automatically invoke a Systems Manager Automation document at the specied time
each day. Congure the Automation document to use a run command to run the deletion scripts in sequential order. Create an Amazon
EventBridge rule to use Amazon Simple Notication Service (Amazon SNS) to send failure notications to the company.
B. Use AWS Systems Manager State Manager to automatically invoke a Systems Manager Automation document at the specied time
each day. Congure the Automation document to use a run command to run the deletion scripts in sequential order. Create a conditional
statement inside the Automation document as the last step to check for errors. Use Amazon Simple Email Service (Amazon SES) to send
failure notications as email messages to the company.
C. Create an Amazon EventBridge rule that invokes an AWS Lambda function at the specied time. Add the necessary permissions for the
invocation to the Lambda function's resource-based policy. Congure the Lambda function to run the deletion scripts in sequential order.
Congure the Lambda function to use Amazon Simple Notication Service (Amazon SNS) to send failure notications to the company.
D. Create an Amazon EventBridge rule that invokes an AWS Lambda function at the specied time. Add the necessary permissions for the
invocation to the Lambda function's resource-based policy. Congure the Lambda function to run the deletion scripts in sequential order.
Congure the Lambda function to use Amazon Simple Email Service (Amazon SES) to send failure notications as email messages to the
company. | 一家公司有一个文件读取应用程序，该应用程序将文件保存到运行在Amazon EC2实例上的数据库中。法规要求公司每天在特定时间从EC2实例删除文件。公司必须删除超过60天的数据库记录。数据库记录删除必须在文件删除之后进行。公司已经创建了删除文件和数据库记录的脚本。公司需要在删除脚本失败时收到电子邮件通知。

 | **选项A：** 使用AWS Systems Manager State Manager在每天指定时间自动调用Systems Manager自动化文档。配置自动化文档使用运行命令按顺序运行删除脚本。创建Amazon EventBridge规则使用Amazon SNS向公司发送失败通知。
- 优点：State Manager适合定期任务，SNS是标准的通知服务
- 缺点：需要额外配置EventBridge规则来监控失败，架构相对复杂

**选项B：** 使用AWS Systems Manager State Manager在每天指定时间自动调用Systems Manager自动化文档。配置自动化文档使用运行命令按顺序运行删除脚本。在自动化文档中创建条件语句作为最后一步检查错误。使用Amazon SES发送失败通知邮件。
- 优点：State Manager适合定期任务，在自动化文档内部处理错误检查和通知
- 缺点：SES需要额外的配置和验证步骤

**选项C：** 创建Amazon EventBridge规则在指定时间调用AWS Lambda函数。为Lambda函数的基于资源的策略添加必要的调用权限。配置Lambda函数按顺序运行删除脚本。配置Lambda函数使用Amazon SNS向公司发送失败通知。
- 优点：EventBridge适合定时任务，Lambda灵活性高，SNS易于配置
- 缺点：Lambda可能不是运行EC2实例脚本的最佳选择

**选项D：** 创建Amazon EventBridge规则在指定时间调用AWS Lambda函数。为Lambda函数的基于资源的策略添加必要的调用权限。配置Lambda函数按顺序运行删除脚本。配置Lambda函数使用Amazon SES发送失败通知邮件。
- 优点：EventBridge适合定时任务，Lambda灵活性高
- 缺点：Lambda运行EC2脚本复杂，SES配置相对复杂

 | A |  |  |
| 345 | A company uses an organization in AWS Organizations that has all features enabled to manage its AWS accounts. Amazon EQ instances run in
the AWS accounts.
The company requires that all current EC2 instances must use Instance Metadata Service Version 2 (IMDSv2). The company needs to block
AWS API calls that originate from EC2 instances that do not use IMDSv2. | A. Create a new SCP statement that denies the ec2:RunInstances action when the ec2:MetadataHttpTokens condition key is not equal to
the value of required. Attach the SCP to the root of the organization.
B. Create a new SCP statement that denies the ec2:RunInstances action when the ec2:MetadataHttpPutResponseHopLimit condition key
value is greater than two. Attach the SCP to the root of the organization.
C. Create a new SCP statement that denies "*" when the ec2:RoleDelivery condition key value is less than two. Attach the SCP to the root
of the organization.
D. Create a new SCP statement that denies when the ec2:MetadataHttpTokens condition key value is not equal to required. Attach the
SCP to the root of the organization. |  |  |  |  |  |
| 346 | A DevOps team supports an application that runs on a large number of Amazon EC2 instances in an Auto Scaling group. The DevOps team
uses AWS CloudFormation to deploy the EC2 instances. The application recently experienced an issue. A single instance returned errors to a
large percentage of requests. The EC2 instance responded as healthy to both Amazon EC2 and Elastic Load Balancing health checks.
The DevOps team collects application logs in Amazon CloudWatch by using the embedded metric format. The DevOps team needs to receive
an alert if any EC2 instance is responsible for more than half of all errors. | A. Create a CloudWatch Contributor Insights rule that groups logs from the CloudWatch application logs based on instance ID and errors.
B. Create a resource group in AWS Resource Groups. Use the CloudFormation stack to group the resources for the application. Add the
application to CloudWatch Application Insights. Use the resource group to identify the application.
C. Create a metric lter for the application logs to count the occurrence of the term "Error.'' Create a CloudWatch alarm that uses the
METRIC_COUNT function to determine whether errors have occurred. Congure the CloudWatch alarm to send a notication to an Amazon
Simple Notication Service (Amazon SNS) topic to notify the DevOps team.
D. Create a CloudWatch alarm that uses the INSIGHT_RULE_METRIC function to determine whether a specic instance is responsible for
more than half of all errors reported by EC2 instances. Congure the CloudWatch alarm to send a notication to an Amazon Simple
Notication Service (Amazon SNS) topic to notify the DevOps team.
E. Create a CloudWatch subscription lter for the application logs that lters for errors and invokes an AWS Lambda function. Congure
the Lambda function to send the instance ID and error and in a notication to an Amazon Simple Notication Service (Amazon SNS) topic
to notify the DevOps team. |  |  |  |  |  |
| 347 | A company is using AWS CloudFormation to perform deployments of its application environment. A deployment failed during a recent update
to the existing CloudFormation stack. A DevOps engineer discovered that some resources in the stack were manually modied.
The DevOps engineer needs a solution that detects manual modication of resources and sends an alert to the DevOps lead. | A. Create an Amazon Simple Notication Service (Amazon SNS) topic. Subscribe the DevOps lead to the topic by using an email address.
Create an AWS Cong managed rule that has the CLOUDFORMATION_STACK_DRIFT_DETECTION_CHECK identier. Create an Amazon
EventBridge rule that is invoked on the NON_COMPLIANT resources status. Set the SNS topic as the rule target.
B. Tag all CloudFormation resources with a specic tag. Create an AWS Cong custom rule by using the AWS Cong Rules Development Kit
Library (RDKlib) that checks all resource changes that have the specic tag. Congure the custom rule to mark all the tagged resource
changes as NON_COMPLIANT when the change is not performed by CloudFormation. Create an Amazon EventBridge rule that is invoked
on the NON_COMPUANT resources status. Create an AWS Lambda function that sends an email message to the DevOps lead. Set the
Lambda function as the rule target.
C. Create an Amazon Simple Notication Service (Amazon SNS) topic. Subscribe the DevOps lead to the topic by using an email address.
Create an AWS Cong managed rule that has the CLOUDFORMATION_STACK_DRIFT_DETECTION_CHECK identier. Create an Amazon
EventBridge rule that is invoked on the COMPLIANT resources status. Set the SNS topic as the rule target.
D. Create an AWS Cong managed rule that has the CLOUDFORMATION_STACK_DRIFT_DETECTION_CHECK identier. Create an Amazon
EventBridge rule that is invoked on the NON_COMPLIANT resources status. Create an AWS Lambda function that sends an email message
to the DevOps lead. Set the Lambda function as the rule target. | 一家公司正在使用AWS CloudFormation来执行其应用程序环境的部署。在最近对现有CloudFormation堆栈进行更新时，部署失败了。DevOps工程师发现堆栈中的一些资源被手动修改了。

DevOps工程师需要一个解决方案来检测资源的手动修改，并向DevOps负责人发送警报。

 | **选项A：**
- 创建SNS主题并订阅DevOps负责人的邮箱
- 使用AWS Config托管规则`CLOUDFORMATION_STACK_DRIFT_DETECTION_CHECK`
- 创建EventBridge规则监听NON_COMPLIANT状态
- 将SNS主题设为规则目标
- **分析：** 这个方案完整且直接，使用托管规则检测堆栈漂移，通过EventBridge监听不合规状态，直接通过SNS发送邮件通知。

**选项B：**
- 为所有CloudFormation资源添加特定标签
- 使用AWS Config RDKlib创建自定义规则
- 检查带有特定标签的资源变更
- 当变更不是由CloudFormation执行时标记为NON_COMPLIANT
- 通过EventBridge和Lambda发送邮件
- **分析：** 这个方案过于复杂，需要手动标记所有资源并开发自定义规则，而AWS已经提供了专门的托管规则来检测CloudFormation堆栈漂移。

**选项C：**
- 与选项A类似，但EventBridge规则监听的是COMPLIANT状态
- **分析：** 这个配置是错误的，因为我们需要在检测到手动修改（NON_COMPLIANT）时发送警报，而不是在资源合规时发送警报。

**选项D：**
- 使用AWS Config托管规则`CLOUDFORMATION_STACK_DRIFT_DETECTION_CHECK`
- 创建EventBridge规则监听NON_COMPLIANT状态
- 通过Lambda函数发送邮件
- **分析：** 这个方案在技术上是可行的，但比选项A更复杂，需要额外的Lambda函数来发送邮件，而SNS可以直接处理邮件通知。

 |  |  |  |
| 348 | A DevOps engineer deployed multiple AWS accounts by using AWS Control Tower to support different business, technical, and administrative
units in a company. A security team needs the DevOps engineer to automate AWS Control Tower guardrails for the company. The guardrails
must be applied to all accounts in an OU of the company's organization in AWS Organizations.
The security team needs a solution that has version control and can be reviewed and rolled back if necessary. The security team will maintain
the management of the solution in its OU. The security team wants to limit the type of guardrails that are allowed and allow only new
guardrails that are approved by the security team. | A. Create individual AWS CloudFormation templates that align to a guardrail. Store the templates in an AWS CodeCommit repository.
Create an AWS::ControlTower::EnableControl logical resource in the template for each OU in the organization. Congure an AWS Code
Build project that an Amazon EventBridge rule will invoke for the security team's AWS CodeCommit changes.
B. Create individual AWS CloudFormation templates that align to a guardrail. Store the templates in an AWS CodeCommit repository.
Create an AWS::ControlTower::EnableControl logical resource in the template for each account in the organization. Congure an AWS
CodePipeline pipeline in the security team's account. Advise the security team to invoke the pipeline and provide these parameters when
starting the pipeline.
C. Create individual AWS CloudFormation templates that align to a guardrail. Store the templates in an AWS CodeCommit repository.
Create an AWS::ControlTower::EnableControl logical resource in the template for each OU in the organization. Congure an AWS
CodePipeline pipeline in the security team's account that an Amazon EventBridge rule will invoke for the security team's CodeCommit
changes.
D. Congure an AWS CodePipeline pipeline in the security team's account that an Amazon EventBridge rule will invoke for PutObject
events to an Amazon S3 bucket. Create individual AWS CloudFormation templates that align to a guardrail. Store the templates in the S3
bucket. Create an AWS::ControlTower::EnableControl logical resource in the template for each OU in the organization. |  |  |  |  |  |
| 349 | A company runs a web application on Amazon Elastic Kubernetes Service (Amazon EKS). The company uses Amazon CloudFront to distribute
the application. The company recently enabled AWS WAF. The company set up Amazon CloudWatch Logs to send logs to an aws-waf-logs log
group.
The company wants a DevOps engineer to receive alerts if there are sudden changes in blocked trac. The company does not want to receive
alerts for other changes in AWS WAF log behavior. The company will tune AWS WAF rules over time.
The DevOps engineer is currently subscribed to an Amazon Simple Notication Service (Amazon SNS) topic in the environment. | A. Create a CloudWatch Logs metrics lter for blocked requests on the AWS WAF log group to create a custom metric. Create a
CloudWatch alarm by using CloudWatch anomaly detection and the published custom metric. Congure the alarm to notify the SNS topic
to alert the DevOps engineer.
B. Create a CloudWatch anomaly detector for the log group. Create a CloudWatch alarm by using metrics that the CloudWatch anomaly
detector publishes. Use the high setting for the LogAnomalyPriority metric. Congure the alarm to go into alarm state if a static threshold
of one anomaly is detected. Congure the alarm to notify the SNS topic to alert the DevOps engineer.
C. Create a CloudWatch metrics lter for counted requests on the AWS WAF log group to create a custom metric. Create a CloudWatch
alarm that activates when the sum of blocked requests in the custom metric during a period of 1 hour is greater than a static estimate for
the acceptable number of blocked requests in 1 hour. Congure the alarm to notify the SNS topic to alert the DevOps engineer.
D. Create a CloudWatch anomaly detector for the log group. Create a CloudWatch alarm by using metrics that the CloudWatch anomaly
detector publishes. Use the medium setting for the LogAnomalyPriority metric. Congure the alarm to go into alarm state if a sum of
anomalies over 1 hour is greater than an expected value. Congure the alarm to notify the SNS topic to alert the DevOps engineer. | 一家公司在Amazon Elastic Kubernetes Service (Amazon EKS)上运行Web应用程序。该公司使用Amazon CloudFront来分发应用程序。该公司最近启用了AWS WAF。该公司设置了Amazon CloudWatch Logs将日志发送到aws-waf-logs日志组。

该公司希望DevOps工程师在被阻止流量突然变化时收到警报。该公司不希望因AWS WAF日志行为的其他变化而收到警报。该公司将随时间调整AWS WAF规则。

DevOps工程师目前已订阅环境中的Amazon Simple Notification Service (Amazon SNS)主题。

 | **选项A：** 
- 为AWS WAF日志组上的被阻止请求创建CloudWatch Logs指标过滤器以创建自定义指标
- 使用CloudWatch异常检测和发布的自定义指标创建CloudWatch警报
- 配置警报通知SNS主题以警告DevOps工程师
- **分析：** 这个方案正确地针对被阻止的请求创建了特定的指标过滤器，然后使用异常检测来识别突然变化，符合需求

**选项B：**
- 为日志组创建CloudWatch异常检测器
- 使用CloudWatch异常检测器发布的指标创建CloudWatch警报
- 对LogAnomalyPriority指标使用高设置
- 配置警报在检测到一个异常的静态阈值时进入警报状态
- **分析：** 这个方案监控整个日志组的异常，而不是专门针对被阻止的流量，可能会触发不需要的警报

**选项C：**
- 为AWS WAF日志组上的计数请求创建CloudWatch指标过滤器以创建自定义指标
- 创建CloudWatch警报，当1小时内自定义指标中被阻止请求的总和大于1小时内可接受被阻止请求数量的静态估计时激活
- **分析：** 使用静态阈值而不是异常检测，无法适应随时间变化的WAF规则调整，不够灵活

**选项D：**
- 为日志组创建CloudWatch异常检测器
- 使用CloudWatch异常检测器发布的指标创建CloudWatch警报
- 对LogAnomalyPriority指标使用中等设置
- 配置警报在1小时内异常总和大于预期值时进入警报状态
- **分析：** 同样监控整个日志组而不是特定的被阻止流量，可能产生不相关的警报

 |  |  |  |
| 350 | A video platform company is migrating its video catalog to AWS. The company will host MP4 videos les in an Amazon S3 bucket. The
company will use Amazon CloudFront and Amazon EC2 instances to serve the video les.
Users rst connect to a frontend application that redirects to a video URL. The video URL contains an authorization token in CloudFront. The
cache is activated on the CloudFront distribution. Authorization token check activity needs to be logged in Amazon CloudWatch.
The company wants to prevent direct access to video les on CloudFront and Amazon S3 and wants to implement checks of the authorization
token that the frontend application provides. The company also wants to perform regular rolling updates of the code that checks the
authorization token signature. | A. Implement an authorization token check in Lambda@Edge as a trigger on the CloudFront distribution. Enable CloudWatch logging for
the Lambda@Edge function. Attach the Lambda@Edge function to the CloudFront distribution. Implement CloudFront continuous
deployment to perform updates.
B. Implement an authorization token check in CloudFront Functions. Enable CloudWatch logging for the CloudFront function. Attach the
CloudFront function to the CloudFront distribution. Implement CloudFront continuous deployment to perform updates.
C. Implement an authorization token check in the application code that is installed on the EC2 instances. Install the CloudWatch agent on
the EC2 instances. Congure the application to log to the CloudWatch agent. Implement a second CloudFront distribution. Migrate the
trac from the rst CloudFront distribution by using Amazon Route 53 weighted routing.
D. Implement an authorization token check in CloudFront Functions. Enable CloudWatch logging for the CloudFront function. Attach the
CloudFront function to the CloudFront distribution. Implement a second CloudFront distribution. Migrate the trac from the rst
CloudFront distribution by using Amazon Route 53 weighted routing. | 一家视频平台公司正在将其视频目录迁移到AWS。该公司将在Amazon S3存储桶中托管MP4视频文件。公司将使用Amazon CloudFront和Amazon EC2实例来提供视频文件服务。

用户首先连接到前端应用程序，该应用程序重定向到视频URL。视频URL在CloudFront中包含授权令牌。CloudFront分发上启用了缓存。授权令牌检查活动需要记录在Amazon CloudWatch中。

公司希望防止直接访问CloudFront和Amazon S3上的视频文件，并希望实现对前端应用程序提供的授权令牌的检查。公司还希望对检查授权令牌签名的代码执行定期滚动更新。

 | **选项A：使用Lambda@Edge实现授权令牌检查**
- ✅ Lambda@Edge可以在CloudFront边缘位置执行授权检查
- ✅ 支持CloudWatch日志记录
- ✅ CloudFront持续部署支持滚动更新
- ✅ 能够防止直接访问，实现授权控制
- ⚠️ Lambda@Edge相对复杂，成本较高

**选项B：使用CloudFront Functions实现授权令牌检查**
- ✅ CloudFront Functions轻量级，适合简单的授权检查
- ✅ 支持CloudWatch日志记录
- ✅ CloudFront持续部署支持滚动更新
- ✅ 成本更低，延迟更小
- ✅ 能够防止直接访问，实现授权控制

**选项C：在EC2实例上实现授权令牌检查**
- ❌ 无法防止直接访问CloudFront和S3
- ❌ 使用Route 53加权路由进行更新复杂且不是最佳实践
- ❌ 不能在CloudFront层面进行授权控制
- ❌ 架构复杂度高

**选项D：使用CloudFront Functions但通过Route 53进行更新**
- ✅ CloudFront Functions适合授权检查
- ✅ 支持CloudWatch日志记录
- ❌ 使用Route 53加权路由而非CloudFront持续部署不是最佳实践
- ❌ 维护两个CloudFront分发增加复杂性

 |  |  |  |
| 351 | A company uses an organization in AWS Organizations to manage multiple AWS accounts in a hierarchical structure. An SCP that is associated
with the organization root allows IAM users to be created.
A DevOps team must be able to create IAM users with any level of permissions. Developers must also be able to create IAM users. However,
developers must not be able to grant new IAM users excessive permissions. The developers have the CreateAndManageUsers role in each
account. The DevOps team must be able to prevent other users from creating IAM users. | A. Create an SCP in the organization to deny users the ability to create and modify IAM users. Attach the SCP to the root of the
organization. Attach the CreateAndManageUsers role to developers.
B. Create an SCP in the organization to grant users that have the DeveloperBoundary policy attached the ability to create new IAM users
and to modify IAM users. Congure the SCP to require users to attach the PermissionBoundaries policy to any new IAM user. Attach the
SCP to the root of the organization.
C. Create an IAM permissions policy named PermissionBoundaries within each account. Congure the PermissionBoundaries policy to
specify the maximum permissions that a developer can grant to a new IAM user.
D. Create an IAM permissions policy named PermissionBoundaries within each account. Congure PermissionsBoundaries to allow users
who have the PermissionBoundaries policy to create new IAM users.
E. Create an IAM permissions policy named DeveloperBoundary within each account. Congure the DeveloperBoundary policy to allow
developers to create IAM users and to assign policies to IAM users of only if the developer includes the PermissionBoundaries policy as
the permissions boundary. Attach the DeveloperBoundary policy to the CreateAndManageUsers role within each account. | 一家公司使用AWS Organizations中的组织来管理分层结构中的多个AWS账户。与组织根关联的SCP允许创建IAM用户。

DevOps团队必须能够创建具有任何级别权限的IAM用户。开发人员也必须能够创建IAM用户。但是，开发人员不得向新IAM用户授予过度权限。开发人员在每个账户中都有CreateAndManageUsers角色。DevOps团队必须能够阻止其他用户创建IAM用户。

 | **选项A：** 在组织中创建SCP以拒绝用户创建和修改IAM用户的能力。将SCP附加到组织根。将CreateAndManageUsers角色附加给开发人员。
- **问题：** 这个方案会完全阻止所有用户（包括开发人员）创建IAM用户，不符合需求。而且角色不能"附加"给用户，这是概念错误。

**选项B：** 在组织中创建SCP，授予具有DeveloperBoundary策略的用户创建和修改IAM用户的能力。配置SCP要求用户为任何新IAM用户附加PermissionBoundaries策略。将SCP附加到组织根。
- **问题：** SCP主要用于限制权限，而不是授予权限。SCP不能强制要求附加权限边界，这需要通过IAM策略实现。

**选项C：** 在每个账户中创建名为PermissionBoundaries的IAM权限策略。配置PermissionBoundaries策略以指定开发人员可以授予新IAM用户的最大权限。
- **问题：** 仅创建权限边界策略是不够的，还需要强制开发人员在创建用户时使用这个边界。

**选项D：** 在每个账户中创建名为PermissionBoundaries的IAM权限策略。配置PermissionsBoundaries以允许具有PermissionBoundaries策略的用户创建新IAM用户。
- **问题：** 这个选项逻辑混乱，权限边界策略的作用是限制最大权限，而不是授予创建用户的权限。

**选项E：** 在每个账户中创建名为DeveloperBoundary的IAM权限策略。配置DeveloperBoundary策略以允许开发人员创建IAM用户，并且只有在开发人员将PermissionBoundaries策略作为权限边界包含时才能为IAM用户分配策略。将DeveloperBoundary策略附加到每个账户中的CreateAndManageUsers角色。
- **正确：** 这个方案通过条件策略强制开发人员在创建用户时必须设置权限边界，有效限制了开发人员能够授予的最大权限。

 |  |  |  |
| 352 | A company has deployed a landing zone that has a well-dened AWS Organizations structure and an SCP. The company's development team
can create their AWS resources only by using AWS CloudFormation and the AWS Cloud Development Kit (AWS CDK).
A DevOps engineer notices that Amazon Simple Queue Service (Amazon SQS) queues that are deployed in different CloudFormation stacks
have different congurations. The DevOps engineer also notices that the application cost allocation tag is not always set.
The DevOps engineer needs a solution that will enforce tagging and promote the reuse of code. The DevOps engineer needs to avoid different
congurations for the deployed SQS queues. | A. Create an Organizations tag policy to enforce the cost allocation tag in CloudFormation stacks. Instruct the development team to use
CloudFormation to dene SQS queues. Instruct the development team to deploy the SQS queues by using CloudFormation StackSets.
B. Update the SCP to enforce the cost allocation tag in CloudFormation stacks. Instruct the development team to use CloudFormation
modules to dene SQS queues. Instruct the development team to deploy the SQS queues by using CloudFormation stacks.
C. Use AWS CDK tagging to enforce the cost allocation tag in CloudFormation StackSets. Instruct the development team to use the AWS
CDK to dene SQS queues. Instruct the development team to deploy the SQS queues by using CDK stacks.
D. Use AWS CDK tagging to enforce the cost allocation tag in CloudFormation stacks. Instruct the development team to use the AWS CDK
to dene SQS queues. Instruct the development team to deploy the SQS queues by using CDK feature ags. | 一家公司已经部署了一个着陆区，该着陆区具有定义良好的AWS Organizations结构和SCP（服务控制策略）。公司的开发团队只能通过使用AWS CloudFormation和AWS云开发工具包（AWS CDK）来创建他们的AWS资源。

一位DevOps工程师注意到，在不同CloudFormation堆栈中部署的Amazon简单队列服务（Amazon SQS）队列具有不同的配置。该DevOps工程师还注意到应用程序成本分配标签并不总是被设置。

该DevOps工程师需要一个解决方案来强制执行标签并促进代码重用。DevOps工程师需要避免已部署的SQS队列出现不同的配置。

2. | **选项A：** 创建Organizations标签策略来在CloudFormation堆栈中强制执行成本分配标签。指导开发团队使用CloudFormation定义SQS队列。指导开发团队使用CloudFormation StackSets部署SQS队列。
- Organizations标签策略可以有效强制执行标签要求
- StackSets适用于跨多个账户和区域的部署，但对于代码重用和标准化配置帮助有限
- 不能很好地解决配置不一致的问题

**选项B：** 更新SCP来在CloudFormation堆栈中强制执行成本分配标签。指导开发团队使用CloudFormation模块定义SQS队列。指导开发团队使用CloudFormation堆栈部署SQS队列。
- SCP主要用于权限控制，不是强制执行标签的最佳工具
- CloudFormation模块可以促进代码重用和标准化配置
- 但SCP对标签强制执行的能力有限

**选项C：** 使用AWS CDK标签在CloudFormation StackSets中强制执行成本分配标签。指导开发团队使用AWS CDK定义SQS队列。指导开发团队使用CDK堆栈部署SQS队列。
- CDK标签功能强大，可以在应用级别统一应用标签
- CDK构造（constructs）天然支持代码重用和标准化
- StackSets在这个场景下不是必需的

**选项D：** 使用AWS CDK标签在CloudFormation堆栈中强制执行成本分配标签。指导开发团队使用AWS CDK定义SQS队列。指导开发团队使用CDK功能标志部署SQS队列。
- CDK标签可以有效强制执行标签
- CDK构造支持代码重用和配置标准化
- 功能标志（feature flags）主要用于功能开关，不是部署机制

3. | C |  |  |
| 353 | A DevOps team manages a company's AWS account. The company wants to ensure that specic AWS resource conguration changes are
automatically reverted. | A. Use AWS Cong rules to detect changes in resource congurations. Congure remediation action that uses AWS Systems Manager
Automation documents to revert the conguration changes.
B. Use Amazon CloudWatch alarms to monitor resource metrics. When an alarm is activated, use an Amazon Simple Notication Service
(Amazon SNS) topic to notify an administrator to manually reverts the conguration changes.
C. Use AWS CloudFormation to create a stack that deploys the necessary conguration changes. Update the stack when conguration
changes need to be reverted.
D. Use AWS Trusted Advisor to check for noncompliant congurations. Manually apply necessary changes based on Trusted Advisor
recommendations. | 一个DevOps团队管理着公司的AWS账户。公司希望确保特定的AWS资源配置更改能够自动回滚。

选项：
A. 使用AWS Config规则来检测资源配置的变更。配置修复操作，使用AWS Systems Manager自动化文档来回滚配置更改。
B. 使用Amazon CloudWatch告警来监控资源指标。当告警被触发时，使用Amazon Simple Notification Service (Amazon SNS)主题通知管理员手动回滚配置更改。
C. 使用AWS CloudFormation创建一个堆栈来部署必要的配置更改。当需要回滚配置更改时更新堆栈。
D. 使用AWS Trusted Advisor检查不合规的配置。根据Trusted Advisor建议手动应用必要的更改。

 | **选项A：** 
- ✅ AWS Config可以持续监控和记录AWS资源配置
- ✅ Config规则可以自动检测配置偏差
- ✅ 修复配置(Remediation Configuration)可以自动触发Systems Manager自动化文档
- ✅ 完全满足"自动回滚"的要求
- ✅ 这是AWS推荐的配置合规性和自动修复的最佳实践

**选项B：**
- ❌ CloudWatch告警主要监控性能指标，不是配置变更
- ❌ 需要管理员"手动"回滚，不符合"自动"要求
- ❌ SNS只是通知服务，无法实现自动修复

**选项C：**
- ❌ CloudFormation主要用于基础设施即代码部署
- ❌ 需要手动更新堆栈，不是自动化过程
- ❌ 不能实时检测和响应配置变更

**选项D：**
- ❌ Trusted Advisor主要提供成本优化、安全性等建议
- ❌ 需要"手动"应用更改，不符合自动化要求
- ❌ 不是实时配置监控工具

 |  |  |  |
