## Clash  

#### 资源地址
1,官方文档：
[https://docs.cfw.lbyczf.com/](https://docs.cfw.lbyczf.com/)  
2,github下载地址：
[https://github.com/Fndroid/clash_for_windows_pkg/releases/freenode](https://github.com/Fndroid/clash_for_windows_pkg/releases/freenode)  
3,freenode(有效性未知)：  
[https://raw.githubusercontent.com/ssrsub/ssr/master/Clash.yml](https://raw.githubusercontent.com/ssrsub/ssr/master/Clash.yml)  
[https://drive.google.com/uc?export=download&id=1u2kemeUVBQ1EEoovDvt-1MyVzBTtvVL0](https://drive.google.com/uc?export=download&id=1u2kemeUVBQ1EEoovDvt-1MyVzBTtvVL0)  
4,parser设置教程  
[https://github.com/Fndroid/clash_for_windows_pkg/issues/2729](https://github.com/Fndroid/clash_for_windows_pkg/issues/2729)  
5,规则转换器  
[https://acl4ssr-sub.github.io/](https://acl4ssr-sub.github.io/)  

6.acl4ssr规则集(Branch-master)  
[https://github.com/ACL4SSR/ACL4SSR](https://github.com/ACL4SSR/ACL4SSR)  

6,自建分流配置ini  
[https://github.com/DestinyZxw/custom-network-rules/blob/main/README.md](https://github.com/DestinyZxw/custom-network-rules/blob/main/README.md)  
使用自建ini之后，不再需要配置Clash的Parsers，但是源机场可能存在SDN为redir-host的情况，需要先设置一下  

#### 浏览器插件 
Proxy SwitchyOmega教程：  
1，[http://www.qishunwang.net/news_show_7430.aspx](http://www.qishunwang.net/news_show_7430.aspx)  
2，[https://shipengliang.com/software-exp/Chrome-%E4%BD%BF%E7%94%A8%E4%BB%A3%E7%90%86-switchysharp%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E8%AE%BE%E7%BD%AE.html](https://shipengliang.com/software-exp/Chrome-%E4%BD%BF%E7%94%A8%E4%BB%A3%E7%90%86-switchysharp%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E8%AE%BE%E7%BD%AE.html)  

#### 添加规则 - 配置文件预处理
Setting>Parsers  
```
parsers:
  - url: https://93a26a2a.ghelper.me/clash/4a6a3d821b78a5d97cb9f122989e30e5
 # 可以只使用https://yoursubscribe.link/ 匹配该网址下的所有订阅  
 # 亦可使用 - reg: ^.*$ 匹配所有订阅  
    yaml:  
      commands:
        - dns.enhanced-mode=fake-ip # redir-host 不再被支持      
      append-rules: # Clash由上而下遍历规则，推荐将自定义规则排到rule组内靠前位置
        - DOMAIN-SUFFIX,google.com,DIRECT
        # - DOMAIN,time.is,DIRECT        
        # 格式： - 规则类型,分流目标,应该被分到的节点/节点组
        # 规则类型可参考 https://docs.cfw.lbyczf.com/contents/ui/profiles/rules.html
```

#### 场景
>问：clash不开启systemProxy的情况下，想指定某个程序走代理  
答：目前没有解决方案，windows直接设置代理也是全局代理，反而是可以通过白名单的方式，指定某个程序不走代理。除非该程序自己提供了设置指定代理服务器的设置（例如chorm插件：Proxy SwitchyOmega）

>问：那为什么以前用Proxy SwitchyOmega，现在不用了？  
答：原因有两个方面， 一方面clash开启系统代理之后，我们可以修改ProxiesMode配置为Rule，根据rules中列出的域名来区分，并非所有网络请求都走代理连接，这样能够避免流量浪费，以及国内访问需要兜圈子。另一方面，ProxySwitchyOmega等于在本地不同端口程序上再次代理，繁琐且无用，另外还需要又一次设置网络访问白名单（gfwlist），更加繁琐  

>问：在开启systemProxy后，rules中并没有P站地址，为何也能正常访问？  
答：猜测，P站自己锁大陆ip地址，拒绝了大陆ip访问？？？我也不太清楚    

#### 经验
1，ini、list文件地址配置了github.com，实际上要使用raw(源码)  
2，生成后的ini文件，需要注意内部的custom_proxy_group(策略组proxy-groups)与proxies的节点之间不能重名，尤其是使用url-test正则匹配的情况下  
3，Clash配置中注意空格，可能在多个文件中拷贝的情况下，空格被替换成其它编码格式  
4，原Ghelper的yml有全球和香港两种分类，使用自建ini之后，这两个分类没有进行区分，待后续观察，条件允许的情况下，应该是沿用Ghelper的策略组，仅对rules做补充。  
 
#### 测试网站
[https://cn.pornhub.com/](https://cn.pornhub.com/)  

#### 参考地址
*https://www.mattkaydiary.com/2021/07/2021-07-16-free-v2ray-clash-nodes.html*  
*https://freebrid.com/index.php/2021/07/12/free/*  
