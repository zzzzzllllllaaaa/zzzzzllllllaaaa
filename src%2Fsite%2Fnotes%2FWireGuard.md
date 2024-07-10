---
{"dg-publish":true,"permalink":"/WireGuard/","tags":["WireGuard","梯子"],"noteIcon":""}
---

[优选WARP的EndPoint IP，提高本地WARP节点访问性并修改各客户端的EndPoint IP | MisakaNo の 小破站](https://blog.misaka.rest/2023/03/12/cf-warp-yxip/)

1. [安装 - WireGuard](https://www.wireguard.com/install/)，安装。（有安卓版本）
2. [获取无限流量密钥的机器人](https://t.me/generatewarpplusbot)，获取密钥。
3. 通过[Cloudflare WARP提取WireGuard配置文件 - PEANUT996](https://peanut996.com/wireguard-from-warp/)，自己fork一个，然后运行获取配置文件，保存为.conf扩展，导入文件。
4. [下载ip优选工具](https://gitlab.com/Misaka-blog/warp-script/-/raw/main/files/warp-yxip/warp-yxip-win.7z?inline=false)，这个工具是电脑版的，解压点击“warp-yxip”文件，在导出的excel里面复制前面的一个ip，替换掉配置文件的对端。
5. 就这样开启就可以使用了，运行很稳定，刷tiktok不在话下。

[[优选ip\|优选ip]]

记得取消拦截未经隧道的流量。