中文|[English](Readme.md)

# 开��上网<a name="ZH-CN_TOPIC_0228768064"></a>

开���以通过�务器主机侧网络�网，也�以通过网线连接�置DHCP方�上网，此时开��必须都以USB方�连接在�务器上。请�考以下两�方�选择其一�置开��的网络。

1.  开��通过�务器主机侧网络�网（无需�入网线）。
    1.  命令行执行以下命令，完��部分�置

        �置NAT转�， -s表示�对开�者�上的IP报文�转�。

        **echo "1" \> /proc/sys/net/ipv4/ip\_forward**

        **sudo iptables -t nat -A POSTROUTING -o **_enp2s0_** -s 192.168.1.0/24 -j MASQUERADE**

        �置转�。

        **sudo iptables -A FORWARD -i** _enp0s20f0u8_ **-o **_enp2s0_** -m state --state RELATED,ESTABLISHED -j ACCEPT**

        **sudo iptables -A FORWARD -i** _enp0s20f0u8_ **-o **_enp2s0_** -j ACCEPT**

        在开�者�上�置缺�路由。

        **sudo ip route change default via **_192.168.1.251_** dev usb0**

        >![](public_sys-resources/icon-note.gif) **说明：**   
        >-   enp0s20f0u8： Atlas 200 DK连接的Ubuntu�务器上usb虚拟网�，表示数�报的入�，需�根�自己的虚拟网��进行修改。  
        >-   enp2s0： 连接到外网的网�（wan\)，需�根�自己的网��进行修改。  
        >-   192.168.1.251：这个是虚拟网�的ip地�，需�根�自己的虚拟网�ip进行修改。  

    2.  在开�者�上添加DNS。
        1.  打开base文件

            **sudo vi /etc/resolvconf/resolv.conf.d/base**

        2.  在文件中添加如下行

            **nameserver 114.114.114.114**

        3.  输入:wq!�存文件退出�在命令行中执行如下命令

            **resolvconf -u**

        4.  使用cat命令检查文件确认是�添加�功。

            **cat /etc/resolv.conf**


2.  开��通过网线连接上网（需��入网线）
    1.  开��通过网线与�以上网的网�相连。
    2.  打开interfaces�置文件。

        **vim /etc/network/interfaces**

        �置dhcp：

        把eth0的�置修改为如下两行。

        **auto eth0**

        **iface eth0 inet dhcp**

        如[图 开��interface文件�置](#fig171560010152)所示，输入:wq!�存退出。

        **图 1**  开��interface文件�置<a name="fig171560010152"></a>  
        ![](figures/开��interface文件�置.png "开��interface文件�置")

    3.  执行以下命令��开��，使�置生效。

        **reboot**

    4.  等开��四个�常亮时则�明已�完���，����新ssh登录开��并切�到root用户下。此时�以ping外网验�网络是�通畅，如果ping通则已��置�功；如果ping失败，则执行以下命令。�功�如[图 开���网�置�功](#fig1515720081517)所示。

        **ifdown eth0**

        **ifup eth0**

        **图 2**  开���网�置�功<a name="fig1515720081517"></a>  
        ![](figures/开���网�置�功.png "开���网�置�功")



