# 试验数据版本与批准发布

catalog 保存数据集、契约、版本和派生血缘；artifacts 校验内容寻址文件并入库；contracts 管理字段规则；releases 执行批准、撤回与目录导出。

数据版本与发布批准分开管理，读取和导出应使用明确版本。文件摘要验证完整性，不构成第三方真实性担保。撤回发布后保留记录但限制继续交付。示例中的试件和压力读数都是本地合成数据。

## 运行

Python 3.11，使用标准库及内置 SQLite，无第三方依赖。无需安装第三方包。 在项目根目录执行，命令不访问公网。演示在临时目录内创建数据，结束后自行清理，不需要预置凭据或另启服务。

```sh
python3 -m trialvault demo
```

## 开发检查

测试覆盖当前产品的核心计算、边界输入、事务或版本恢复及异常路径。编译或语法检查可单独运行。

```sh
python3 -m unittest discover -s tests -v
python3 -m compileall -q trialvault
```

## 容器复现

先在有网络的准备阶段取得运行镜像。之后可在断网容器中复制项目到临时工作区运行，避免向源目录写入缓存。

```sh
docker build -t local/analysis-product .
docker run --rm --network none local/analysis-product
```

具体接口参数可通过主入口的帮助命令查看。数据库、归档和导出文件应存入调用者指定的工作目录，不提交到源码仓库。
