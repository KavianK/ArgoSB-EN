## ArgoSB-EN one-click non-interactive small steel cannon script 💣 [Current version: V25.7.15]

<img width="636" height="238" alt="0cbc3f82134b4fc99afd6cee37e98be" src="https://github.com/user-attachments/assets/a76ca418-badb-4e9a-a771-6682ec713e06" />

#### 1. Automatic allocation based on Sing-box + Xray + Cloudflared-Argo three cores

#### 2. Support Docker Image deployment, public image library: ```ygkkk/argosb```

#### 3. The SSH script is extremely simple and lightweight, almost without dependencies, supports non-root, and is compatible with all mainstream VPS systems

#### 4. Support NIX container system, especially recommend IDX-Google, Clawcloud and other servers

#### 5. Specify the kernel optional Wireguard-WARP global outbound mode and change the landing IP to WARP IP

#### 6. All proxy agreements do not require a domain name, with high freedom of choice, supporting any combination of single or multiple proxy agreements
【Currently supported：AnyTLS、Vless-xhttp-reality、Vless-reality-vision、Vmess-ws、Hy2、Tuic、Argo Temporary/Fixed Tunnels】

#### 7. If you need a variety of functions, it is recommended to use the VPS-specific four-in-one script[Sing-box-yg](https://github.com/yonggekkk/sing-box-yg)

----------------------------------------------------------

### 1. Custom variable parameter description：

| Variable meaning | Variable name | Fill in variable value | Delete variable | Leave variable value blank | Variable requirements and instructions |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1、启用vless-reality-vision | vlpt | 端口指定 | 关闭vless-reality-vision | 端口随机 | 必选之一 【xray内核：TCP】 |
| 2、启用vless-xhttp-reality | xhpt | 端口指定 | 关闭vless-xhttp-reality | 端口随机 | 必选之一 【xray内核：TCP】 |
| 3、启用anytls | anpt | 端口指定 | 关闭anytls | 端口随机 | 必选之一 【singbox内核：TCP】 |
| 4、启用vmess-ws | vmpt | 端口指定 | 关闭vmess-ws | 端口随机 | 必选之一 【xray/singbox内核：TCP】 |
| 5、启用hy2 | hypt | 端口指定 | 关闭hy2 | 端口随机 | 必选之一 【singbox内核：UDP】 |
| 6、启用tuic | tupt | 端口指定 | 关闭tuic | 端口随机 | 必选之一 【singbox内核：UDP】 |
| 7、warp开关 | warp | 填写s或者x | 关闭warp | 所有内核协议启用warp | 可选，s表示singbox所有协议启用warp，x表示xray所有协议启用warp |
| 8、argo开关 | argo | 填写y | 关闭argo隧道 | 关闭argo隧道 | 可选，填写y时，vmess变量vmpt必须启用 |
| 9、argo固定隧道域名 | agn | 解析在CF上的域名 | 使用临时隧道 | 使用临时隧道 | 可选，argo填写y才可激活固定隧道|
| 10、argo固定隧道token | agk | CF获取的ey开头的token | 使用临时隧道 | 使用临时隧道 | 可选，argo填写y才可激活固定隧道 |
| 11、uuid密码 | uuid | 符合uuid规定格式 | 随机生成 | 随机生成 | 可选 |
| 12、reality域名 | reym | 符合reality域名规定 | yahoo | yahoo | 可选 |
| 13、切换ipv4或ipv6配置 | ip | 填写4或者6 | 自动识别IP配置 | 自动识别IP配置 | 可选，4表示IPV4配置输出，6表示IPV6配置输出 |
| 14、【仅容器类docker】监听端口，网页查询 | PORT | 端口指定 | 3000 | 3000 | 可选 |
| 15、【仅容器类docker】启用vless-ws-tls | DOMAIN | 服务器域名 | 关闭vless-ws-tls | 关闭vless-ws-tls | 可选，vless-ws-tls可独立存在，uuid变量必须启用 |


![f776f1b3b1e0ebe9a537baf8660a387](https://github.com/user-attachments/assets/b9b357de-85b8-4270-aa87-2f50d63d672e)


#### Notes when using the ```ygkkk/argosb``` image：

1. It is recommended to add uuid variables. UUID will remain unchanged after restart.

2. Click restart to automatically update the image, but the key related to the reality protocol will be reset and the reality node needs to be exported again.

3. After the argo temporary tunnel is restarted, the temporary domain name will change and the argo node needs to be re-exported. The fixed tunnel will remain unchanged.

4. Running xray/sing-box/argo kernels at the same time will trigger some docker container restrictions and cause errors. It is recommended to run at most two kernels at the same time

#### Note when using VPS:

1. After leaving uuid blank and generating it randomly, uuid will remain unchanged after restart

2. Update scripts can only be uninstalled and reinstalled. It is recommended to keep the script with variables for quick reinstallation

3. After the argo temporary tunnel is restarted, the temporary domain name will change and the argo node needs to be re-exported. The fixed tunnel will remain unchanged

4. If the warp script has been installed, it will conflict with the built-in warp of argosb. You must choose one of them

----------------------------------------------------------

### 2. SSH one-key variable script template:

Note: Fill in the variable value between "", leave one space between variables, and unused variables can be deleted

```
vlpt="" vmpt="" hypt="" tupt="" xhpt="" anpt="" warp="" uuid="" reym="" argo="" agn="" agk="" ip="" bash <(curl -Ls https://raw.githubusercontent.com/yonggekkk/argosb/main/argosb.sh)
```

----------------------------------------------------------

### 3. Three combinations of SSH one-key scripts are recommended:

1: All protocols coexist or single protocol + Argo temporary/fixed tunnel
```
vlpt="" vmpt="" hypt="" tupt="" xhpt="" anpt="" argo="y" agn="" agk="" bash <(curl -Ls https://raw.githubusercontent.com/yonggekkk/argosb/main/argosb.sh)
```

2: Only argo temporary tunnel, fixed tunnel must fill in port (vmpt), domain name (agn), token (agk)

Similar to IDX-Google-VPS containers without public network, it is recommended to use this script to quickly penetrate the intranet and obtain nodes with one click

```
vmpt="" argo="y" agn="" agk="" bash <(curl -Ls https://raw.githubusercontent.com/yonggekkk/argosb/main/argosb.sh)
```

3: Single protocol, mainstream UPD protocol or TCP protocol runs alone

Take hy2 as an example: the following script enables the hy2 variable hypt, and other protocol variables refer to the variable parameter description

```
hypt="" bash <(curl -Ls https://raw.githubusercontent.com/yonggekkk/argosb/main/argosb.sh)
```

---------------------------------------------------------

### 4. SSH shortcut (after the first successful installation, you need to reconnect to SSH for the agsb shortcut to take effect):

1. View Argo's fixed domain name, fixed tunnel token, temporary domain name, and currently installed node information:

```agsb list``` or ```bash <(curl -Ls https://raw.githubusercontent.com/yonggekkk/argosb/main/argosb.sh) list```

 2、Online switching of IPV4/IPV6 node configuration (exclusive for dual-stack VPS):

Display IPV4 node configuration:

```ip=4 agsb list```or```ip=4 bash <(curl -Ls https://raw.githubusercontent.com/yonggekkk/argosb/main/argosb.sh) list```

Display IPV6 node configuration:

```ip=6 agsb list```or```ip=6 bash <(curl -Ls https://raw.githubusercontent.com/yonggekkk/argosb/main/argosb.sh) list```

 3、Restart Script：

```agsb res``` or ```bash <(curl -Ls https://raw.githubusercontent.com/yonggekkk/argosb/main/argosb.sh) res```

 4、Uninstall Script：

```agsb del``` or ```bash <(curl -Ls https://raw.githubusercontent.com/yonggekkk/argosb/main/argosb.sh) del```

----------------------------------------------------------


#### For related tutorials, please refer to Yongge's blog. The video tutorial is as follows:

Latest recommendation: [Good news for Clawcloud and IDX Google VPS: Solve the problem of server IP access! Argosb script adds WARP outbound function, easily changing the landing IP to Cloudflare WARP IP](https://youtu.be/HO_XLBmIYJw)

[Final tutorial for Claw.cloud free VPS proxy setup (V): ArgoSB script docker image update supports AnyTLS and Xhttp-Reality](https://youtu.be/-mhZIhHRyno)

[Final tutorial for Claw.cloud free VPS proxy setup (IV): As low as 1 cent, 4 price + 7 protocol packages are available for you to choose; instructions for viewing nodes, restarting and upgrading, changing IP, and changing configuration](https://youtu.be/xOQV_E1-C84)

[Claw.cloud Free VPS Proxy Setup Final Tutorial (III): ArgoSB all-purpose docker image release, support for real-time web page node update; TCP/UDP direct connection protocol setting client "CDN" free domain name](https://youtu.be/JEXyj9UoMzU)

[Claw.cloud Free VPS Proxy Setup Final Tutorial (II): As low as 2 cents; support any combination of Argo | Reality | Vmess | Hysteria2 | Tuic proxy protocols](https://youtu.be/NnuMgnJqon8)

[Claw.cloud Free VPS Proxy Setup Final Tutorial (I): The simplest in the entire network | Two non-interactive carriage return scripts | CDN preferred IP | Workers reverse generation | ArgoSB tunnel setup](https://youtu.be/Esofirx8xrE)

[IDX Google Free VPS Proxy Setup Tutorial (II): ArgoSB One-Click Proxy Script Release | One-Click Enter to Get Everything Done | Lazy Newbie's Strongest Argo Proxy Node Script](https://youtu.be/OoXJ_jxoEyY)

[IDX Google Free VPS Proxy Setup Tutorial (III): NIX Container Latest Workspace Method to Build Argo Free Node | One-Click Enter to Get Everything Done | Argo Fixed Tunnel One-Click Resurrection](https://youtu.be/0I5eI1KKx08)

[IDX Google Free VPS Proxy Setup Tutorial (IV): Supports Automatically Starting Proxy Node Function After Reset | The Easiest Way to Keep Alive](https://youtu.be/EGrz6Wvevqc)

Updating...

----------------------------------------------------------

### Communication platform: [Yongge blog address](https://ygkkk.blogspot.com), [Yongge YouTube channel](https://www.youtube.com/@ygkkk), [Yongge TG Telegram Group](https://t.me/+jZHc6-A-1QQ5ZGVl), [Yongge TG Telegram Channel](https://t.me/+DkC9ZZUgEFQzMTZl)

----------------------------------------------------------
### Thank you for your support! WeChat reward Yongge Kankankanygkkk
![41440820a366deeb8109db5610313a1](https://github.com/user-attachments/assets/e5b1f2c0-bd2c-4b8f-8cda-034d3c8ef73f)

----------------------------------------------------------
### Thank you for the star in the upper right corner🌟
[![Stargazers over time](https://starchart.cc/yonggekkk/ArgoSB.svg)](https://starchart.cc/yonggekkk/ArgoSB)

----------------------------------------------------------
### Disclaimer: All codes come from the integration of Github community and ChatGPT

### Thanks to [VTEXS](https://console.vtexs.com/?affid=1558) for the sponsorship support
