# ansible-playbook-redis-cluster

执行这个ansible脚本之前需要先安装好ansible。这里修改了ansible.cfg文件中的inventory参数，使得执行脚本时不需要在/etc/ansible下去执行。可以直接在其他的

文件夹中去执行，但是这个文件夹得包含ansible.cfg这个文件。

hosts为远程控制机器的配置文件。
basis.yml为脚本的入口   执行脚本时  ansible-playbook  basis.yml   即可

group_vars里面的all文件  是配置全局变量的文件，脚本中所有的变量都可以在里面设置

roles里面才是关于redis部署的具体文件。

tasks是redis集群安装的主要任务文件，里面包含所有节点都需要的任务all_node.yml 和一台主节点需要做的master_node.yml

all_node主要是将redis安装包在各个节点进行安装解压配置的工作

master_node是将所有的节点加入到集群中的操作



template中主主要是配置文件的模板文件和脚本的模板文件 都是jinja2格式的文件 


Jinja2是基于python的模板语言，所以使用python的语法就可以编写



yes [字符串]...  用法参考/roles/redis/template/redis_join_cluster.sh.j2

Repeatedly output a line with all specified STRING(s), or 'y'.

脚本执行成功之后再任意的一台redis机器 进入安装目录下的src目录执行

./redis-cli -c -h {ip}  -p  {port}  cluster nodes即可查看集群状态

