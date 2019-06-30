# CTF

## 資源區

综合｛
1、CTF工具免费集：https://www.ctftools.com/down/
2、聊天机器人助手：https://github.com/CylanceSPEAR/CyBot

｝
密码学｛
1、培根密码在线解密：https://netair.xyz/tools/%E5%9F%B9%E6%A0%B9%E5%AF%86%E7%A0%81%E5%8A%A0%E5%AF%86%E8%A7%A3%E5%AF%86.html
2、md5解密：https://www.somd5.com/ | http://www.chamd5.org/
3、彩虹表：http://www.objectif-securite.ch/en/ophcrack.php
4、http://tomeko.net/online_tools/base32.php?lang=en 编码转换
5、http://imgbase64.duoshitong.com/ 图片和base64互转

｝
取证｛
1、pcap包修复：http://f00l.de/hacking/pcapfix.php
2、主机内常见机密文件的扫描：https://github.com/CERT-W/certitude
3、网络数据监控：https://github.com/opt-oss/NG-NetMS
4、网络流量隐含数据分析：https://github.com/sensepost/DET
5、JPHS隐写：http://linux01.gwdg.de/~alatham/stego.html

｝
社会工程：｛
1、钓鱼攻击防护：https://github.com/anilyuk/punydomaincheck
2、社会信息收集：https://github.com/DataSploit/datasploit
3、网络中数据的挖掘：https://github.com/SharadKumar97/OSINT-SPY

｝
无线网络：｛
1、wifi监控探测：https://github.com/lennartkoopmann/nzyme
2、wifi入侵检测：https://www.kismetwireless.net/

｝
AWD中防护：｛
1、攻击防护和漏洞检测：https://github.com/jzadeh/Aktaion
2、数据收集，威胁监控：https://github.com/Invoke-IR/ACE
3、AWS基础设施监控：https://github.com/SecurityFTW/cs-suite
4、渗透测试框架，团队协作：https://github.com/dradis/dradis-ce
5、本地扫描，安全度评估：https://github.com/OpenSCAP/openscap
6、日志分析管理：https://github.com/Graylog2/graylog2-server

｝
AWD中攻击：｛
1、网络注入攻击：https://github.com/xtr4nge/FruityC2

｝


## ROBOTS
robots.txt

![](https://i.imgur.com/ce2oE67.png)

## seelog

![](https://i.imgur.com/qSDlGAk.png)
打开acess.log文件，查找状态吗为200的日志记录，可以发现一个登录的路径 

![](https://i.imgur.com/vE6YzDa.png)
访问该路径即可得到flag 
![](https://i.imgur.com/598l40O.png)


## 天下武功唯快不破(找規律丟進去)

![](https://i.imgur.com/RjU2OXj.png)

```python=
import requests
import hashlib

for i in range(1,1000):
    m = hashlib.md5()
    data = m.update(str(i).encode('utf-8'))
    url = 'http://106.75.26.211:3333/u/'+ data +'.txt'
    res = requests.get(url)
    if(res.status_code == 200):
        print(res.text)
        break
```
![](https://i.imgur.com/HQwkNmH.png)


