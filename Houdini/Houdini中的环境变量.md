浏览环境变量
使用hconfig命令显示所有与Houdini相关的环境变量的当前值。
要使hconfig在Windows命令行上可用，需要将包含hconfig.exe的目录路径添加到Windows系统的Path环境变量中。

设置环境变量
1、Houdini可以获取**操作系统的环境变量**（这意味着可以把Houdini环境变量定义在系统环境变量中）；
2、用Shell启动Houdini时，Houdini也可以获取Shell的环境变量（这意味着可以通过参数来设置环境变量）；
3、每个用户的Houdini主目录（例如，Windows上的“文档”目录）都可以包含一个**houdini.env**文件（如果不存在，Houdini运行时会创建一个），您可以使用它来指定环境变量（这种方式在调试或记录个性化设置时很有用）；
4、您也可以使用**package机制**来设置环境变量（开发大规模Package的时候很有用）。

由于Houdini大量使用Python进行开发，Python相关的环境变量也可以通过上述方法访问，例如PYTHONPATH。
Python的行为很大程度上受其相关的系统环境变量影响。 其中一个重要的变量是PYTHONPATH。它用于设置用户自定义模块的路径，以便可以直接导入到Python程序中。它还负责处理Python模块的默认搜索路径。PYTHONPATH变量包含一个字符串，其中包含 Python 需要添加到 sys.path 目录列表中的各种目录的名称。此变量的主要用途是允许用户导入尚未安装的模块。

常用环境变量
\$HIP：包含当前HIP文件的目录的路径，如果当前场景还未被保存过，默认是 C:/Users/账号名/
\$JOB：当前工程目录，如果可以通过 File > Set Project... 设置，如果设置，默认是 C:/Users/账号名/

详见：https://www.sidefx.com/docs/houdini/basics/config_env.html

