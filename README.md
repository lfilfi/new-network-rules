# 介绍
自己经常用的分流网站都没有添加bing、openAI的规则，为了方便自己使用bing和chatGPT，新增了上述2者的分流规则。
# 使用方法
1. 以我常用的“ACL4SSR在线订阅转换”为例
2. 点击“进阶模式”
3. 导入订阅链接（机场、自建的）
4. 远程配置把这个仓库里面的“.ini”结尾的文件地址填上去
5. 转换导入clash即可



现在找到一个新的方法，方便多个设备上自动更新自定义的分流规则。（其实很早就有，只不过自己现在才知道）

步骤：

准备好2种文件，一种是配置文件.ini，这个是配置分流规则和分流策略组的文件。另一种是分流规则.list，不同的list文件里面存放着不同的域名、ip地址，配合ini文件里面设定的策略组实现分流。
建议新建一个GitHub仓库，存放这两种文件。
新建多个list文件，用于存放你想要的自定义的分流规则。比如我添加了2个，一个是必应的，一个是openai的。
把新建的list文件地址放在ini文件里面，配置好策略组。注意ini文件的语法，避免报错。
打开任意一个在线订阅转换网站-进阶模式，订阅链接填上你的机场、自建节点的地址，客户端默认即可，远程配置地址换成你ini文件的地址，后端随意（或者自建）
然后把生成的订阅地址导入clash即可。
以后添加自定义规则，只要在GitHub仓库里面修改一个ini文件和添加list文件就可以实现多个设备的规则自动更新。
自用ini配置文件地址：https://raw.githubusercontent.com/Wzieee/custom-network-rules/main/custom%20rules.ini
;截取一段ini文件内容
[custom]
;这里是分流规则，通过网络引用list文件里面的规则
ruleset=🤖 openAI,https://raw.githubusercontent.com/Wzieee/custom-network-rules/main/openAI.list
ruleset=Ⓜ️ 必应,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Clash/Bing/Bing.list
ruleset=🎯 全球直连,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/LocalAreaNetwork.list
ruleset=🎯 全球直连,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/UnBan.list
ruleset=🎯 全球直连,[]GEOIP,CN
ruleset=🐟 漏网之鱼,[]FINAL

;这里是策略组
custom_proxy_group=🚀 默认选择`select`[]🇺🇸 甲骨文`[]♻️ 自动选择`[]🇭🇰 香港`[]🇨🇳 台湾`[]🇸🇬 狮城`[]🇯🇵 日本`[]🇺🇲 美国`[]🇰🇷 韩国`[]🚀 手动切换`[]DIRECT
custom_proxy_group=🚀 手动切换`select`.*
custom_proxy_group=♻️ 自动选择`url-test`.*`http://www.gstatic.com/generate_204`300,,50
custom_proxy_group=🎥 奈飞视频`select`[]🎥 奈飞`[]🚀 默认选择`[]♻️ 自动选择`[]🇸🇬 狮城`[]🇭🇰 香港`[]🇨🇳 台湾`[]🇯🇵 日本`[]🇺🇲 美国`[]🇰🇷 韩国`[]🚀 手动切换`[]DIRECT
custom_proxy_group=📺 哔哩哔哩`select`[]🎯 全球直连`[]🇨🇳 台湾`[]🇭🇰 香港


enable_rule_generator=true
overwrite_original_rules=true
ini配置规则
[custom] 
enable_rule_generator=true
overwrite_original_rules=true
0. 上面3行代码别忘了，参考上面，或者参考我的完整文件
1. ;是省略号
2.  ruleset定义规则，ruleset=规则名字,规则地址
3. custom_proxy_group定义分流策略组和节点策略组，custom_proxy_group=策略组名字`选择方式`[]其他策略组1`[]其他策略组2
4. 策略组可以引用其他策略组，使用`分割，[]表示引用其他策略组
5. 选择方式指手动select，延迟检测url-tes后面跟延迟检测网址
6. .*是正则语法，代表匹配全部节点
7. 定义节点策略组时候，可以使用正则：custom_proxy_group=🇰🇷 韩国`url-test`(KR|Korea|KOR|首尔|韩|韓)`http://www.gstatic.com/generate_204`300,,50
8. 上面url-test后面跟的就是正则匹配，匹配节点名字带其中任何一个关键字的节点。
9. 🚀🎥这种emoji符号可用可不用，只要ruleset和custom-proxy-group用的名字一直就行，如果导入clash提示proxy not found，大概率二者名字不一致。
10. 🇸🇬 🇨🇳 这种是国旗emoji，需要的话可以自己网上找

list规则
参考：https://docs.cfw.lbyczf.com/contents/ui/profiles/rules.html
