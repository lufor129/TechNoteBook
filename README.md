# 技術筆記二
[toc]
# 畫圖
## Seaborn
與pandas合用很美麗

### 直方圖 barplot

```python=
%matplotlib inline
plt.figure(figsize=(10, 6))
barplot = sns.barplot(artists.name,artists.paintings) #(pandas X軸,Y軸)
for item in barplot.get_xticklabels():
    item.set_rotation(90)
```

![](https://i.imgur.com/VnxNEfw.png)


```python=
plt.title("Insurance Data Label Distribution")
g = sns.countplot(x="Response", data = df)
for p in g.patches:
    txt = (str((p.get_height()/len(df)).round(2)) + '%')[2:]
    txt_x = p.get_x()+0.3
    txt_y = p.get_height()+2000
    g.text(txt_x,txt_y,txt)
plt.show()
```
![](https://i.imgur.com/BXuNzyb.png)


## Matplotlib

### 刻度值 xticks
https://www.delftstack.com/zh-tw/howto/matplotlib/how-to-set-tick-labels-font-size-in-matplotlib/

```python=
# 第一項參數為間距，印出第0、300、600項
# 旋轉
plt.xticks(range(0,TSMC.shape[0],300),rotation=30)
```


# uWSGI 
作為配合Nginx做python多執行續響應
https://www.runoob.com/python3/python-uwsgi.html
## plt.plot value

# DevOps
## DevOps 工程師
DevOps是Development與Operation的交集。把開發的產品推向End User是終極目標。軟體流程如下:

![](https://i.imgur.com/fy475Ak.png)


因此需要設定伺服器，安裝相關工具、部屬、設定防火牆...等。此外還要維運，APP有沒有問題，User Experience有沒有可以改進的點、Higher load。此外還需要有多次的更新，版本控制...等。Major、Minor、Patch更新等。

你會發現流程如下:
![](https://i.imgur.com/vuXqycu.png)

DevOps就是為了將這段流程更快、更少bug而生。

### 挑戰
過去有很多流程被視為: slow down process、too much effort。DevOps就是為了改變下面的事情。

1. 開發與維運缺乏合作

過去develop與Operations是分開的。開發不考慮部屬、Operations知道App怎麼運作。 當Deployment文件寫的不足時，App無法部屬上去，雙方就不斷互相丟包，release take longer。

![](https://i.imgur.com/eGil2aR.png)

2. 開發維運的目標衝突

開發是為了有更快的產品產出，維運是為了有穩定的品質，因此維運的目的是slow down process與確保100%的安全。

![](https://i.imgur.com/IfSwIqw.png)

3. Security

Operations目標是防止系統不穩定，安全團隊是防止系統不安全，在檢測安全穩定性方面會耗日費時。

![](https://i.imgur.com/b6lrFxk.png)

為了能夠安全的部屬，因此有了DevSecOps。
![](https://i.imgur.com/YIMxygi.png)

4. Application Testing

![](https://i.imgur.com/G0ljcCF.png)
Testing、Operation、Security需要手工操作讓，slow、不透明...等問題。

DevOps試圖解決以上幾點，**加速部屬速度。使用自動化、streamline的方式部屬**，使得一天可以部屬無數版本。

### 概念
DevOps是文化、實作、工具的集合。
主要目的是:
1. 使得release更加快速與有品質
2. 使dev與ops能一起合作

不過其實每家公司流程都不一樣。但是遵循以下幾個流程:
![](https://i.imgur.com/BtiAIWn.png)

DevOps工程師的工作是使用工具來設定軟體部屬流程。

### DevOps需求
**Development端**
DevOps需要知道哪個App怎麼設定、怎麼自動測試。

![](https://i.imgur.com/eow3aLK.png)

**Operations端**
需要知道Linux用法、Linux file System、Key 管理
![](https://i.imgur.com/XU9y91t.png)

Firewall、Proxy、Laod Balance、Http

![](https://i.imgur.com/VU9bch1.png)

DevOps比起Operations來說知道Basic就行。
此外需要知道Visualization與Container。

**Cloud**
此外由於cloud崛起，你至少需要知道一個cloud。
![](https://i.imgur.com/RH7kAJU.png)

**Container Orchestation**
如果小專案，可以用docker-compose，但是一旦大規模的話你需要懂k8s。

**Monitoring**
此外你還要能錯誤追蹤、監控，如prometheus、Ngios。

![](https://i.imgur.com/KCYMtdV.png)

**Script Language**
此外為了能夠自動化，你還要能懂Scripting，如BASH、Powershell，或是python、go、ruby。Python是目前最簡單的。

**身為DevOps至少要將以下這些工具都學起來**
![](https://i.imgur.com/CbaDvYG.png)

### CI/CD
DevOps的核心重點就是要建立streamline流程，其中最重要的是Continuous Integration、Continuous Deployment。

當Development完成code後會編譯(maven、gradle)、接著會需要build docker image並push docker hub，接著部屬到server, 你需要把這段流程自動化會使用到Jenkins。

我們把以下的流程稱作為 Continuous Integrartion。

![](https://i.imgur.com/MULZ7pE.png)

當有新的code時會走完這段流程並部屬到Server，稱作Continuous Deployment。

![](https://i.imgur.com/Fik77GU.png)

**Infrastructure as Code**
Production、Testing、Development機器上各自會需要部屬相當多的時間。因此將intrastructure寫成code運行在不同環境上是更為輕鬆簡單的事情。

![](https://i.imgur.com/JaOGiCH.png)

例如如下

![](https://i.imgur.com/pKi4vyI.png)

接著把這些infrastructure as code用git 來版控。

### 與SRE的差異
DevOps更偏向概念，SRE更偏向實作。DevOps更偏向快速的部屬、SRE更偏向reliablity。

![](https://i.imgur.com/ZGzUFao.png)

## SRE 工程師
全名是Site Reliable Engineer。

實際上DevOps關注在快速部屬上，並不關心系統穩定性，因此需要SRE。

![](https://i.imgur.com/U4NKWTL.png)

1. SRE teams are made up of software engineer.
2. who build and implement software
3. to improve the reliability of their systems/services

SRE需要有開發經驗與Operations經驗，讓他可以快速定位錯誤，SRE必須知道software development。

### System reliability
System 就是那些環境與產品(DB、Network、App)，Reliablility可以看成產品錯誤率，YT、Google 這些產品很少發生unaccessable。

當你change System就會有unreliablity的問題。但你不可能不change。通常在dev開發完成後Ops會有一條長長的checklist來阻擋你發布，但是阻慢了發布速度。

SRE就是要自動化那條長長的checklist。

![](https://i.imgur.com/nZoMxQO.png)

**SLA**
該怎麼衡量reliability? 用稱作SLA，Service Level Agreement。用百分比來計算失敗率。

![](https://i.imgur.com/gcmqO7E.png)

要達到100% SLA是很困難的。因為木桶理論，總有一個環節無法達到100%

SLA會衡量Accessibility、reponse time、error rate。

Allow downtime，稱作Error budget，在市場發布會的時候會需要知道。要是SLA沒達標，公司就需要放更多人力去Operations Task，對公司來說不划算。

### SRE TASK
SRE 工程師的工作

**自動化流程**
讓長長的檢查自動化、SLA check
**monitoring、logging system**
衡量系統效能
**configure Monitoring、logging、alerting**
設定監控系統、alert給需要的資訊。
which service、in which clustering、what problem。
![](https://i.imgur.com/ek0ZuIV.png)
**on-call support**
**post-incident review**
災害維護，找出病徵，災害復原、文件記錄

**Goal**:
1. short duration of outage
2. few people affected
3. few services affected

當錯誤可見的時候，一定是是很多錯誤累積而來的

![](https://i.imgur.com/aqgIxEu.png)

# Virtual Machine

## 概念與好處

電腦分層如下，硬體上有OS，OS上有Application。
![](https://i.imgur.com/k7xT6Fu.png)

Virtual Machine就是在OS上額外一層Virtualization層並在之上安裝Linux OS。
![](https://i.imgur.com/wqQXsUn.png)

Virtaulization層有一個重要的技術稱作Hypervisor，VirtualBox有這樣的技術建立Virtual CPU、Virtual RAM、Storage。**所有的硬體是共享的，但是Virtual Machine之間是獨立的，給了A電腦2G RAM其他Virtaul Machine就不能取用了。**

![](https://i.imgur.com/3ZQQOTJ.png)

**好處**
1. 安全性較高，因為硬體層以上都虛擬化，因此安全性會相對較高。
2. 系統的選擇較多，在VM可以選擇各種不同的OS。
3. 應用程式不須要被拆分，因此不需要大幅更改應用程式的架構。簡單來說不需要降低應用程式內服務的耦合性，不需要將程式內的服務個別拆開來部屬。

**壞處**
1. VM的Image大小通常為GB以上，較Container大。
2. 啟動速度通常要花個幾分鐘，因此服務重啟的速度較慢。
3. 資源使用較多，因為不只給應用程式本身，還要將一部分資源分給VM的作業系統。

## Hypervisor 種類
![](https://i.imgur.com/HlNVT4E.png)

**Type 2**
在Main OS上建立Hypervisor，Guest OS從Host OS上借取hardware。通常用於個人電腦

**Type 1**
直接在硬體上建立Hypervisor。通常是企業應用場所(AWS、GCP)，同樣的硬體不同客戶有不同virtual machine。

![](https://i.imgur.com/AHE54ok.png)

Virtual Machine可以匯出如Image (VMI)，包含了OS、APP，因此更可攜帶與避免崩潰、備份。

## 與Container 差別
![](https://ithelp.ithome.com.tw/upload/images/20201008/20129609yCbxxeUh3r.png)

正常的OS包含兩層。HW、OS、APP。
![](https://i.imgur.com/oyiOzbx.png)

docker是在APP層做虛擬化，VM是在OS層做虛擬化。

![](https://i.imgur.com/sMBmfxd.png)

**好處**
* Image較小，通常幾MB。
* 啟動速度較快，通常幾秒就能生成一個Container。
* 因為免去了去在執行一個OS的資源。所以能將更多資源運用在跑服務上。
* 更新較為容易，只需要利用新的Image重新啟動就會更新了。

**壞處**
* 安全性較VM差，因為環境和硬體都是與本機共用。
* 在同一台機器中，每個Container的OS都是相同，例如無法一個為windows一個為Linux，還是依賴Host OS。
* Container通常切分成微服務(Microservices)的方式做部署，在各元件中的網路連結會比較複雜。


# OS
https://ithelp.ithome.com.tw/users/20112132/ironman/1884


# Linux file System

https://www.youtube.com/watch?v=HbgzrKJvDRw
![](https://i.imgur.com/7LOE3P4.png)
這是根據Filesystem Hierarchy Standard的規則所訂製的，幾乎所有的Unix base都是按照這個規則。

### /bin 、 /sbin、/lib
**bin:**
bin為binary的簡寫主要放置一些系統的必備執行檔例如:cat、cp、chmod df、dmesg、gzip、kill、ls、mkdir、more、mount、rm、su、tar等。
**/usr/bin:**
主要放置一些應用軟件工具的必備執行檔例如c++、g++、gcc、chdrv、diff、dig、du、eject、elm、free、gnome*、 zip、htpasswd、kfm、ktop、last、less、locale、m4、make、man、mcopy、ncftp、 newaliases、nslookup passwd、quota、smb*、wget等。
**/sbin:**
主要放置一些系統管理的必備程序例如:cfdisk、dhcpcd、dump、e2fsck、fdisk、halt、ifconfig、ifup、 ifdown、init、insmod、lilo、lsmod、mke2fs、modprobe、quotacheck、reboot、rmmod、 runlevel、shutdown等。
**/usr/sbin:**
放置一些網路管理的必備程序例如:dhcpd、httpd、imap、in.*d、inetd、lpd、named、netconfig、nmbd、samba、sendmail、squid、swap、tcpd、tcpdump等
* /  : this is root directory
* /bin : commands in this dir are all system installed user commands
* /sbin:  commands in this dir are all system installed super user commands
* /usr/bin: user commands for applications
* /usr/sbin: super user commands for applications
* /usr/local/bin : application user commands
* /usr/local/sbin: application super user commands
 
/bin: 是系統的一些指令.
/sbin: 一般是指超級用戶指令.
/usr/bin: 是你在後期安裝的一些軟件的運行腳本.

>如果是用戶和管理員必備的二進制文件，就會放在/bin；
如果是系統管理員必備，但是一般用戶根本不會用到的二進制文件，就會放在 /sbin。
如果不是用戶必備的二進制文件，多半會放在/usr/bin；
如果不是系統管理員必備的工具，如網絡管理命令，多半會放在/usr/sbin。

/lib 是/bin，/sbin會用到的library。

### boot、 dev
boot: Linux OS開機所需。
dev: 硬碟

Linux定義了每個東西都是file包含硬碟。你的硬碟會是/dev/sda，partition會是 /dev/sda1、/dev/sda2

### /etc
這是所有configuration的所在地(apt)，在這裡可以查看到apt安裝的軟體與設定檔。

### /mnt、/media
一些外接硬碟的驅動，USB、externel hard drive、network drive。所以這是 B、D drive mount的地方。

### /opt
一些重要軟體會放在這裡，如container、google、virtualbox、VPN。你可以把自己寫的程式放在上面。

### /proc
在 Linux 中 /proc 檔案系統可以用來做為 kernel module 傳送訊息給程式之用，也能夠記錄一些 kernel 的狀態，如 /proc/modules 用以記錄 module 的內容、/proc/meminfo 用以記錄記憶體的狀態。

### /root
root是root 使用者的home。

### /run
run 裡面保存的是RAM的暫存檔案，關機後就消失了。

### /srv
這是server的空間，但是通常是空的。只有你在運行Server如Web、FTP。放在srv會是一個安全的選擇。

### /sys
這是kernel暫存檔，同樣的關機後就會消失

### /tmp
這是application會暫存的空間，如修改文件時，系統會將文件暫存於此。系統不會主動刪除他。

### /usr
usr 指 Unix System Resource。
使用者安裝被視為不重要的app會在此。同樣的會包含/bin、/sbin、/lib。

/usr/bin下面的都是系統預裝的可執行程序，會隨著系統升級而改變。
/usr/local/bin目錄是給用戶放置自己的可執行程序的地方，推薦放在這裡，不會被系統升級而覆蓋同名文件。

如果兩個目錄下有相同的可執行程序，誰優先執行受到PATH環境變量的影響，比如我的一台服務器的PATH變量為。
echo $PATH
```
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```

這裡/usr/local/bin優先於/usr/bin, 一般都是如此

一些較大的APP會安裝在/usr/share。source code、headerfile會安裝在/usr/src 

### /var
var指variable，給那些長度會變化的檔案，如: log file、database、mail

### /home
進入/home可以看到每個人的home，保存個人資料，每個人只能進入他們的home(除非sudo)。你在裡面也可以找到影藏檔(.開頭)，這是屬於個人設定可以修改來客製化。

### /etc
On modern unix systems, almost all system-wide configuration files are under /etc, but not all files in /etc are configuration files. 

etc 通常都是放設定檔
