# 技術筆記一
[TOC]

**從medium遷移過來，medium真的不適合寫程式碼**
# HackMD Latex 方法
https://hackmd.io/vJlEs9wcTc-eE9rfjTPbzA?both
# Linux 基本操作
```shell=
1.   sudo adduser 某某   //新增帳號
2.   adduser 某某 admin  //新增有管理權限帳號
3.   cat /etc/group     // 查看group
4.   passwd             //修改密碼
5.   whereis python
6.   vim tab ==> :set tabstop=2
7.   ssh 140.127.X.X -l huang -p [port number]
8.   vim nu ==> :set nu
9.   usermod -aG sudo username //將某個帳號(username)加入root
10.   ls -a  // ls 隱藏文件
```

重開機
shutdown -r now

安裝 htop監控管理
watch -n 1 nvidia-smi 動態刷新GPU
vimrc http://wiki.csie.ncku.edu.tw/vim/vimrc

windows版:
```while (1) {cls;nvidia-smi;sleep 1}```

## chmod
chmod +x file

$+$ 為增加權限
x 為執行權

chmod 777 file

LINUX下不同的文件类型有不同的颜色，这里
![](https://i.imgur.com/w4kLNly.png)
```
蓝色表示目录;
绿色表示可执行文件，可执行的程序;
红色表示压缩文件或包文件;
浅蓝色表示链接文件;
灰色表示其它文件;
```

chmod +x 和 chmod u+x的区别?
就是设置谁拥有执行这个文件权限
chmod +x 和chmod a+x 是一样的，一般没有明确要求，可以就用chmod +x

![](https://i.imgur.com/InPW7Dn.png)

chmod -R +777 dict
整個資料夾底下文件都給權限

## Screen 
``` = shell
1. Ctrl + ?                //查詢操作
2. Ctrl + a  d             //detach 脫離畫面
3. screen -r               //回到之前畫面
4. Ctrl + a  c             //新增create畫面
5. Ctrl + a  n             //下一個畫面 p上一個
6. Ctrl + a  S             //分割畫面  Q 關閉
7. Ctrl + a  |
8. Ctrl + a  X             //合併
9. Ctrl + a  tab           //切換分割
10. Ctrl + a  k             //關閉screen (kill)
11. screen -ls              //列出screen
12.screen -rd              //恢復誤操attached
```

## 服務啟動
https://askubuntu.com/questions/19320/how-to-enable-or-disable-services
```
sudo -i service XXX start
sudo -i service XXX stop
sudo -i service XXX status

同
systemctl start XXX

# 查看所有服務
service --status-all

## [+] is running, [-] is stopped, [?] without status command
```

開機啟動
```
sudo systemctl enable docker

# 關閉開機啟動
sudo systemctl disable docker
```

你所有的服務會在 /etc/init.d中
![](https://i.imgur.com/HvfjYoF.png)

要修改service指定文件可以修改/etc/systemd/system 內 如logstash.service。
如果不存在.service檔，可以像是filebeat的官網，直接創建
https://www.elastic.co/guide/en/beats/filebeat/current/running-with-systemd.html

## sudo 自動帶入密碼
```echo 'yourrootpassword' | sudo -S mkdir newfolder```

## Apache config
在/usr/local/apache2/conf/httpd.conf

```

```

## tmux
https://blog.gtwang.org/linux/linux-tmux-terminal-multiplexer-tutorial/
https://ithelp.ithome.com.tw/articles/10267466

安裝:
```
sudo apt install tmux
```

執行:
```
tmux
```
執行後底下會出現一條綠線

當我們執行 tmux 指令時，就會建立一個新的 session，在一個 session 中可以建立多個 windows，而每個 window 又可以分割成多個 panes，在下方的狀態列中會顯示目前所處的 session 與 window 編號。

![](https://i.imgur.com/vj9uous.png)

**Panes（分割視窗）**
在 tmux 的環境中，若想要將 window 視窗分割成多個 pane，並管理建立的 panes，可以使用以下的操作組合鍵：

| 組合鍵 | 說明 |
| -------- | -------- |
| Ctrl+b 再輸入 %    |垂直分割視窗。   	
Ctrl+b 再輸入 " |	水平分割視窗。
Ctrl+b 再輸入 o |	以輪流方式輪流切換 pane。
Ctrl+b 再輸入 方向鍵 |	切換至指定方向的 pane。
Ctrl+b 再輸入 空白鍵 |	切換佈局。
Ctrl+b 再輸入 ! |	將目前的 pane 抽出來，獨立建立一個 window 視窗。
Ctrl+b 再輸入 x |	關閉目前的 pane。|

**Windows**

若要建立與管理多個 windows 視窗，可以使用以下的操作組合鍵：
## alias
換名稱
例如每次都要打minikube kubectl太長了，可以換名字。

```alias kubectl="minikube kubectl"```

## tree 
列出目錄結構
需要安裝 ```apt-get install tree```

```tree /path/dir/```
![](https://i.imgur.com/aMqYAjR.png)

## vimrc
調整顏色與設定 .vimrc
https://ithelp.ithome.com.tw/articles/10272556

## export PATH
linux安裝套件的時候，假如是tar檔。
解壓縮後丟到 /usr/local裡。(/usr/local/bin : application user commands)
如： /usr/local/go

接著再```$HOME/.profile```路徑中加入```export PATH=$PATH:/usr/local/go/bin```

接著再應用 ```source .profile```

## .bashrc VS .profile
1. bashrc是在系统启动后就会自动运行。
2. profile是在用户登录后才会运行。
3. 通常我们修改bashrc,有些linux的发行版本不一定有profile这个文件

**针对个别用户**

用户HOME（家）目录/.bashrc
```~/.bashrc: executed by bash(1) for non-login shells.```

用户HOME（家）目录/.profile
```~/.profile: executed by Bourne-compatible login shells.```

**针对全体用户**

/etc/bash.bashrc
```System-wide .bashrc file for interactive bash(1) shells.```

/etc/profile
```/etc/profile: system-wide .profile file for the Bourne shell (sh(1))```


# Windows
## windows安裝linux指令
用管理員模式打開windows powershell
輸入: Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

看這個:
https://noob.tw/wsl/

方法二
下載git bash有一個 add to windows bash profile 打勾。

## 遠端桌面
重新開機、遠端桌面就是你的帳號密碼
帳: Lufor129
密: 5208




# regular expression
練習: https://regex101.com/

匹配文本

```
^ : 整句開頭
$ : 整句結尾
給full match用的

因此 ^XXX$ 就是整段必須是XXX才可匹配

[] : 匹配中括號中其中一個字符

[abc] : 匹配a or b or c 其中之一
[a-zA-Z] : 匹配a~zA~Z
[^a-zA-Z] : 在中括號內的 ^ 代表取反

{} 設定匹配個數
[a-zA-Z]{3} : 匹配a~zA~Z 3個
{3,} : 3個含以上
{3,6} : 3~6個

. : 表示匹配任意字符 (除了enter)
\d : 任意數字 相當於 [0-9]
\D : 任意字符除了數字

因此[\d\D] 相當於 .

\w : [a-zA-Z0-9_] 任意aA數字
\W : [^a-zA-Z0-9_]

\s : 匹配特殊字符 [\r\n\t\f\v]
\S : 非特殊字符

? : 匹配0次~1次相當於{0,1}
* : 0次~無窮次 {0,}
+ : 1次~無窮次 {1,}

匹配郵件帳號
^[a-zA-Z0-9]\w*@gmail\.com$

^[a-zA-Z0-9] 是開頭不得為_
\w* 後面字串出現0~無窮次
\. 是跳脫符

group是抓出字串內符號
s59654655@mail.nuk.edu.tw
用 ()抓出
(^[a-zA-Z0-9]\w+)@mail\.nuk\.edu\.tw$
抓出 s59654655 group 1 ， group是full match

(?<fit>^[a-zA-Z0-9]\w+)@mail\.nuk\.edu\.tw$
在小括號開頭?<XX> 是命名組 

result = "s59654655@mail.nuk.edu.tw".match(/(?<fit>^[a-zA-Z0-9]\w+)@mail\.nuk\.edu\.tw$/)

result.group[1] = s59654655
result.groups.fit = s59654655

group 可以在當前regex引用
引用 \數字

ex: 1212
正常: ^\d\d\d\d
我們想要找到兩兩成雙成對，後面pair等於前面pair

^(\d\d)\1 : \1相當於group1，而group 1 為\d\d
\k<group> 為複用
^(?<fit>\d\d)\k<fit> :命名為fit後接下來要接一樣的東西，所以可以匹配1212

高級運用:
EX: foobar,fooboo
foo(?=bar) : 想要找到bar前面的foo ?= Positive Lookhead
foo(?!bar) : 想要找到foo後面不等於bar，所以會匹配到fooboo的foo Negative Lookhead

EX: barfoo,boofoo
(?<=bar)foo : 要找foo但要出現在bar後面 Positve Lookbehind
(?<!bar)foo : 要找foo但不出現在bar後面 Negative Lookbehind

EX : 滔滔不絕
想要找到類似AABC的字串
(?<a>.)\k<a>(?!\<a>)(?<b>.)(?!\k<b>|?!\k<a>).
(?<a>.)第一個字命名為a。
\k<a>(?!\<a>)第二個字需要與group a相同，後面不能再接group a。
(?<b>.)(?!\k<b>|?!\k<a>)第三個字命名為b後面不能再接group b和a了。
. 第四個字為任意除了a、b group
```

# 變數命名規則
## 文件命名
文件名要全部小寫, 可以包含底線 (_) 或連字符 (-). 按專案約定來. 如果並沒有專案約定，”_” 更好。
```c++=
可接受的文件命名:
* my_useful_class.cc
* my-useful-class.cc
* myusefulclass.cc
```

## 類型命名 Class
類型名稱的每個單詞首字母均大寫, 不包含底線: MyExcitingClass, MyExcitingEnum.

```c++=
class UrlTable { ...
class UrlTableTester { ...
struct UrlTableProperties { ...
```

## 變數命名
本地變數、即時變數和類別變數也用 lowerCamelCase。變數名不能以底線 (_) 或美元符號 ($) 打頭，這與其他編碼規則里採用底線追尾所有即時變數字首的規定不同。
變數名稱應該簡潔易懂，便於記憶。儘量避免使用單字母，除非一些臨時變數。臨時變數常用名，整數型一般用 i, j, k, m 或 n；而字元型則用 c, d 或 e。

```java=
int i;
char c;
float myWidth;
```



**private變數**
後面接著下底線
```c++=
class TableInfo {
  ...
 private:
  string table_name_;  // 可 - 尾後加底線。
  string tablename_;   // 可。
  static Pool<TableInfo>* pool_;  // 可。
};
```

**全域變數**
可以用 g_ 或其它標誌作為前綴

## 函數命名

應該用動詞，用 lowerCamelCase，或者用一個小寫動詞打頭的詞組，即首字母小寫，之後的每個詞首字母大寫。

如果你的某函式出錯時就要直接 crash, 那麼就在函式名加上 OrDie. 但這函式本身必須集成在產品程式碼裡，且平時也可能會出錯。

```c++=
addTableEntry()
deleteUrl()
openFileOrDie()
```

**取值與設值函數**
要求與變數名匹配
```c++=
int num_entries() const { return num_entries_; }

int num_entries_;
```

## 常數
全部大寫
```c++=
ENUM_NAME
```

## 資料庫table命名
具備統一前綴，對相關功能的表應當使用相同前綴，如acl_xxx，house_xxx,ppc_xxx；其中前綴通常為這個表的模塊或依賴主實體對象的名字，通常來講表名為：業務_動作_類型，或是業務_類型；

表名使用英文小寫單詞，如果有多個單詞則使用下劃線隔開；

## 資料庫欄位命名
使用小寫英文單詞，如果有多個單詞使用下劃線隔開；

是別的表的外鍵均使用xxx_id的方式來表明；

表的主鍵一般都約定成為id，自增類型；
所有表示時間的欄位，統一以 Date 來作為結尾（而不是有的使用Date,有的使用Time）

時間欄位，除特殊情況一律採用int來記錄unix_timestamp

所有儲存相同數據的列名和列類型必須一致
![](https://i.imgur.com/vZkU0l8.png)


# Conda 
## 安裝anaconda
https://ithelp.ithome.com.tw/articles/10212288?sc=rss.qu
https://medium.com/@maniac.tw/%E5%AE%89%E8%A3%9D-anaconda-tensorflow-2bbc6e220fa4

在.bashrc檔案最下方加入
```shell=
export PATH="$HOME/anaconda3/bin:$PATH"
# 不可用"~/anaconda3/bin:$PATH" 會在conda時抓不到當前python(base還會存在)
```
最後再 source  ~/.bashrc

使用者permission
```
sudo chown -R huang /home/huang/anaconda3
```

windows 版要建立linux指令需要安裝m2-base
```conda install m2-base```

## 建立環境
``` = shell
conda create -n tensorflow python=3.6
//建立名為tensorflow的環境
source activate tensorflow
conda list

conda install jupyter
```

```
# 開啟jupyter notebook
conda install ipykernel
python -m ipykernel install --user --name NLP_course --display-name "NLP python"
cd to where you want 
jupyter notebook 開啟jupyter
```
```
#確認python是哪個環境底下的
import sys
sys.executable
```

```
jupyter 環境相關指令
# 查詢
jupyter kernelspec list

# 註冊
python -m ipykernel install --user --name 目標環境 --display-name "取名"

# 移除
jupyter kernelspec remove 目標環境
```


conda 管理
https://medium.com/python4u/%E7%94%A8conda%E5%BB%BA%E7%AB%8B%E5%8F%8A%E7%AE%A1%E7%90%86python%E8%99%9B%E6%93%AC%E7%92%B0%E5%A2%83-b61fd2a76566

tensorflow 安裝
先看顯示卡 Driver Version nvidia-smi
https://zhuanlan.zhihu.com/p/64376059
然後安裝相應cudatoolkit
cuda table
https://stackoverflow.com/questions/50622525/which-tensorflow-and-cuda-version-combinations-are-compatible

> tensorflow-gpu版本配合 gpu，不要直接進系統改cuda 

看處理器 cat /proc/cpuinfo
看記憶體 free -m

強制安裝Anaconda外的套件 如 jieba
>conda install -c conda-forge jieba
conda-forge 是 conda底下更大的包集合

你也可以下載whl檔，在環境底下的pip install whl檔
> sudo ~/anaconda3/envs/Semester/bin/pip install line_bot

此外你可以寫shell來自動執行conda activate，但是注意!此時只能用source 來執行.sh檔
例如:
```shell=
#!/bin/bash
conda activate Semester
cd ~/ettoday/
python crawlHourly.py
cd ~/Semester/
python genTFIDF.py

exit 0
# as reCrawl.sh
```
```shell=
source reCrawl.sh 
```
上面這個在一般環境可以執行，但是在crontab環境會有問題，在contab中還是只能找到python位置並使用執行。

指定特定版本 conda install tensorflow=1.14
tensorflow開始安裝時有固定2.0版本的坑，先安裝2.0再更新版本即可。

**ubuntu 18**
https://medium.com/@maniac.tw/ubuntu-18-04-%E5%AE%89%E8%A3%9D-nvidia-driver-418-cuda-10-tensorflow-1-13-a4f1c71dd8e5

## Raspberry jupyter
http://blog.ittraining.com.tw/2018/10/jupyter-notebook-raspberry-pi-3.html

不知道為什麼只能在.jupyter 才能root


# 伺服器 


管理密碼: https://blog.gtwang.org/linux/linux-passwd-command-examples/

獨顯裝linux:https://blog.csdn.net/qq_31192383/article/details/78876905

## 靜態IP設定
### Ubuntu Linux 18.04
https://blog.gtwang.org/linux/ubuntu-linux-1804-configure-network-static-ip-address-tutorial/

## PostgreSQL
安裝 18.04
https://blog.gtwang.org/linux/how-to-install-and-use-postgresql-ubuntu-18-04/

## Flask
安裝
https://blog.techbridge.cc/2017/06/03/python-web-flask101-tutorial-introduction-and-environment-setup/

### 教學
http://docs.jinkan.org/docs/flask/quickstart.html#a-minimal-application
外網連接 則需要:
```
if __name__ == "__main__":
    app.run(host="0.0.0.0",port=5000,debug=True)

```

Flask 不能return list 用jsonify包住list
```python=
from flask import jsonify

@bookings.route( '/get_customer', methods=[ 'POST' ] )
def get_customer():
    name = {}
    for key, value in request.form.items():
        name[ key ] = value

    customer_obj = customer_class.Customer()
    results = customer_obj.search_customer( name )

    return jsonify(customers=results) 
```

### kill Socket
sudo lsof -i:5000 查詢pid

```kill <pid>```


## crontab
```
crontab -l :列出目前的crontab
crontab -e :編輯

```

crontab 參考: https://crontab.guru/
crontab log查詢 grep CRON /var/log/syslog

crontab use anaconda時加上path才能爬scrapy
```
PATH=/home/huang/anaconda3/envs/OpenData/bin
```

crontab是根據:
[分 時 日 月 星期] 來排列
例如
```21 17 14 7 7```也就是7月14日17點21分星期天執行

```
* 代表任意: 不論多少都會執行
, 代表並列 

ex:
20,40 * * * * 每小時20，40分都會執行

- 代表連續
20-40 * * * * 每小時20到40分都會執行(是左右包含20 40都會執行，共21次)

/ 代表整除
*/2 * * * * 每二的倍數分都會執行0,2,4

0/2 等價於 */2
1/2 : 1,3,5,...,59 (時間點減去1能否被2整除)
7/2 : 7,9,11 (時間點減去7能否被2整除)

想要不同程式相隔一秒執行:
* * * * * 程式1;
* * * * * sleep 1; 程式2;
* * * * * sleep 2; 程式3;
```
星期、月最好不要用數字，而是用英文代替例如MON、JUL

星期還可以用W來代表工作日
日月用L代表最後，一個月的最後或一年的最後

## git 
新增ignore
https://poychang.github.io/gitignore-and-delete-untracked-files/

git ignore 取消已添加folder
```git rm -r --cached .```
```git add .```
```git commit -m "Gitignore issue fixed"```

### git branch
 git clone -b <branch 名稱> --single-branch ssh://git@172.1.2.3/opt/share.git 
 
### clone 下來換名稱

git clone https://github.com/user/userApp.git name_you_want

## system Thread
各種system thread 的process控管
參考:
https://www.redmine.org/boards/1/topics/32763?r=43267


## route
輸入route可以看到伺服器網路狀況
![](https://i.imgur.com/KDftDkh.png)

![](https://i.imgur.com/qXt7q3e.png)

default就是不滿足則走default路線

## npm
安裝NodeJS 
```shell=
sudo apt-get install -y nodejs

#確認
node -v
```

安裝npm
```shell=
sudo apt-get install npm

npm -v
```

公司內網設定npm proxy
```shell=
npm config set proxy http://fetfw.fareastone.com.tw:8080
npm config set https-proxy http://fetfw.fareastone.com.tw:8080
```

## check port open
sudo netstat -tulpn | grep LISTEN

或是
sudo lsof -i -P -n | grep LISTEN

## yml檔寫法
Map syntax:
```
environment:
  RACK_ENV: development
  SHOW: "true"
  USER_INPUT:
```
Array Syntax:
```
environment:
  - RACK_ENV=development
  - SHOW=true
  - USER_INPUT
```

YML檔環境變數:
* basic : ```${VAR}```
* default : ```${VAR:default_value}```
* custom error text : ```${VAR:?error_text}```(當VAR不存在會噴錯)

例子:
```
#變數
ES_HOSTS="10.45.3.2:9220,10.45.3.1:9230"

#吃 (用單引號)
output.elasticsearch:
  hosts: '${ES_HOSTS}'
```

環境變數吃export VAR=XXX

# mongo
sudo mongod --dbpath /var/lib/mongodb/ --smallfiles
/usr/bin/python3.5 OpendataScrapy/run.py
sudo mongod

高級操作
  http://marklin-blog.logdown.com/posts/1394100-mongodb-polymerization-of-30-14-1-aggregate-framework-with-buckle
	
https://itsfoss.com/install-mongodb-ubuntu/#install-from-ubuntu-repository
mongodb 安裝

## mongo regex
https://docs.mongodb.com/manual/reference/operator/query/regex/

mongo的not並不是$not而是 $ne針對特定事務
```javascript=
MongoClient.connect("mongodb://localhost:27017",{ useUnifiedTopology: true },function(err,client){
    if(err) throw err;
    client.db("semester").collection("ettoday",function(err,collection){
      collection.find({"tag":{"$ne":"政治"}},{"_id":0}).sort({$natural:-1}).limit(30).toArray(function(err,items){
        responseData = {
          "data":items,
          "count":items.length
        }
        res.send(responseData);
      });
    });
  });
```

### regex and 操作
```
db.taipei.find({"title":{$regex:"臺北.*水.*區",$options:'i'}}).count()
```
## mongodb text search 
https://www.itread01.com/article/1493690665.html
https://www.tutorialspoint.com/mongodb/mongodb_text_search.htm

中文需要目標(db)中文也是空白分詞，不好用

### mongo distinct
db.ettoday.distinct("title").length 
長度

### add new field on exist coll
https://stackoverflow.com/questions/7714216/add-new-field-to-every-document-in-a-mongodb-collection

db.taipei.update({},{$set:{"updateTime":"Update_2020_1"}},{upsert:false,multi:true})

# jupyter remote

https://zhuanlan.zhihu.com/p/33358809
jupyter conda
在 base 安裝conda nb_conda
在其他環境安裝conda jupyter 

使用ssh 連上目標主機port 
EX : ssh -N -L 8889:localhost:8889 huang@140.127.220.104
前port為自己主機，後為對面port

https://medium.com/@chen.ishi/%E8%87%AA%E5%B7%B1%E6%9E%B6%E4%B8%80%E5%80%8B-jupyter-remote-machine-4de7122ba272
jupyter remote 原理

https://stackoverflow.com/questions/37433363/link-conda-environment-with-jupyter-notebook
	

# pandas 
```python=
loc 切割
loc[:,:] 逗號前面是row切割，逗號後面是column切割
loc使用row、column名稱切割，iloc是index loc 使用index切割
Masking
male_and_age_over_70 = (df.Sex == 'male') & (df.Age > 70)
(df[male_and_age_over_70]
    .style
    .applymap(lambda x: 'background-color: rgb(153, 255, 51)', 
              subset=pd.IndexSlice[:, 'Sex':'Age']))
# 跟 df[(df.Sex == 'male') & (df.Age > 70)] 結果相同
使用MASK遮罩做切割，query也有同樣效果
age = 70
df.query("Age > @age & Sex == 'male'")
```
https://leemeng.tw/practical-pandas-tutorial-for-aspiring-data-scientists.html

https://xiaogenban1993.github.io/20.01/python_pandas.html

pandas pivot 可以快速建立二維
pandas.pivot(index，columns，values)函數根據DataFrame的3列生成數據透視表。使用索引/列中的唯一值並填充值。
https://vimsky.com/zh-tw/examples/usage/python-pandas-pivot.html

```python=
df = pd.read_csv(filename,
                   sep='\t', names=['user','item','rate','time'], engine='python', encoding='latin-1')
matrix = df.pivot(index='user', columns='item', values='rate')
matrix.fillna(0, inplace=True)
users = matrix.index.tolist()
items = matrix.columns.tolist()
matrix_list = matrix.iloc[:,:].values
```

## concat 
合併資料用
http://violin-tao.blogspot.com/2017/06/pandas-2-concat-merge.html

## sort
```python=
genre_class.sort_values(ascending=False, by='paintings')
```

## groupby
```python=
genre_class = artists.groupby("genre").sum()
```

## where
```python=
artists[artists["genre"] == "Impressionism"]
```

## iterrows
```python=
date_dict = {}
for index,instance in stock_df.iterrows():
  date_dict[instance["Date"]] = instance["Label"]
```

# gensim

http://cloga.info/python/2014/01/28/gensim_Similarity_Queries

https://www.machinelearningplus.com/nlp/gensim-tutorial/

LSI的训练是唯一的，我们可以在任意时候继续“训练”，只需要提供更多的训练文档。这是通过为底层模型增加更新达到的，这个过程称为线上训练。因为这个，特征，数据的文档流可能几乎是无限的-只要在新文档到达时喂给LSI就行，同时，将计算完的转换模型作为只读来使用！

```
model.add_documents(another_tfidf_corpus) # 现在 LSI 已经在 tfidf_corpus + another_tfidf_corpus 上进行训练
lsi_vec = model[tfidf_vec] # 将新文档转化到LSI空间，而不影响模型
...
model.add_documents(more_documents) # tfidf_corpus + another_tfidf_corpus + more_documents
lsi_vec = model[tfidf_vec]
...
```

有空可以寫LDA的文章。

# Linebot
Linebot官方真他媽天才，自己API自己寫錯，幹!!!
把最後一行先刪掉才能通過verify
```python=
from flask import Flask, request, abort

from linebot import (
    LineBotApi, WebhookHandler
)
from linebot.exceptions import (
    InvalidSignatureError
)
from linebot.models import (
    MessageEvent, TextMessage, TextSendMessage,
)

app = Flask(__name__)

line_bot_api = LineBotApi('V2k38s3HtXrB/IEeF8gLc3D4f1PBWQNTG5J56o8o6k8nQtyinHgAeP/MeM+CV21Xci+bOK42y6qseg99STmf+bPBXdecFH7bgjyJz06PMeowGAyfzAtYheAnpoNGbzWqfMU4NnzLKm/Df9Jr88V2FwdB04t89/1O/w1cDnyilFU=')
handler = WebhookHandler('39a9319aa7d756a5f76e27fd22ecda7c')


@app.route("/callback", methods=['POST'])
def callback():
    # get X-Line-Signature header value
    signature = request.headers['X-Line-Signature']

    # get request body as text
    body = request.get_data(as_text=True)
    app.logger.info("Request body: " + body)

    # handle webhook body
    try:
        handler.handle(body, signature)
    except InvalidSignatureError:
        print("Invalid signature. Please check your channel access token/channel secret.")
        abort(400)

    return 'OK'

@app.route("/",methods=["POST"])
def hello():
    return "hello world"

if __name__ == "__main__":
    app.run()
```
他的userID 在 event.source.user_id

你必須先通過callback
![](https://i.imgur.com/f9jjIJO.png)

再來測試回復
```python=
@handler.add(MessageEvent, message=TextMessage)
def handle_message(event):
    line_bot_api.reply_message(
        event.reply_token,
        TextSendMessage(text=event.message.text))
```

# openCV
安裝：
看這個：https://blog.gtwang.org/programming/ubuntu-linux-install-opencv-cpp-python-hello-world-tutorial/

https://websiteforstudents.com/how-to-install-opencv-on-ubuntu-18-04-16-04/

如果再linux 發現無法使用鏡頭，試試安裝opencv-contrib-python

這個很厲害，旋轉切割
https://blog.gtwang.org/programming/python-opencv-auto-crop-and-rotate-scanned-image-tutorial/


重要blog
https://chtseng.wordpress.com/category/%e5%bf%83%e5%be%97-%e5%bd%b1%e5%83%8f%e5%88%86%e6%9e%90/
## 侵蝕與膨脹
https://blog.csdn.net/hjxu2016/article/details/77837765
https://www.itread01.com/content/1545169145.html
侵蝕: 这对于去除白噪声很有用，也可以用来断开两个连在一块的物体等。  
膨脹: 膨胀也可以用来连接两个分开的物体。
```
cv.erode(dilation_3j,kernel,iterations = 3)
cv.dilate(img_j,kernel,iterations = 3)
```


開運算、閉運算

先侵蝕在膨脹:先把雜點吃掉(原圖縮小)，再膨脹使原圖放大，達到本體不變雜點消失的效果。
```
cv.morphologyEx(img_opening, cv.MORPH_OPEN, kernel) #(開)去除黑紙中白點

cv.morphologyEx(img_closing, cv.MORPH_CLOSE, kernel)#(閉)去除白紙上黑點
```

## 直方圖均化
可以讓圖片變得更清晰(平均分配)
```histEqu = cv.equalizeHist(image_gray)```

## HSV 篩選
HSV表看:
https://www.itread01.com/content/1542732610.html

https://codepen.io/HunorMarton/details/eWvewo?fbclid=IwAR1gC1QktHoFa8Vr5Y6PTK-1ahYVaw-6hbN1CTp46NyHvki6IWIie07E7Nk
opencv HSV色碼需要除2(0~180)，然後s v是0~255

```
hsv_img = cv.cvtColor(img_key, cv.COLOR_BGR2HSV)
#定義藍色部份 HSV_mask 的上下限值
lower_blue = np.array([110,50,50])
upper_blue = np.array([130,255,255])

#套用HSV_mask
hsvMask = cv.inRange(hsv_img, lower_blue, upper_blue)

#套用 HSV_mask道員圖上進行過濾
hsvMask_output = cv.bitwise_and(img_key, img_key, None, mask =  hsvMask)
cv.imshow('HSV_mask_result',hsvMask_output)
```
![](https://i.imgur.com/S4smcGr.png)
![](https://i.imgur.com/Zg9CUQO.png)

## 銳化與平滑
平滑:會變模糊
```
kernel_size = 5
#定義kernel值
kernel = np.ones((kernel_size, kernel_size), dtype=np.float32) / kernel_size**2 
#套用kernel
dst = cv.filter2D(image, -1, kernel)
```

銳化
```
#定義kernel值
kernel = np.array([[0, -1, 0], [-1, 5, -1], [0, -1, 0]], np.float32) #銳化
#套用kernel
dst = cv.filter2D(image, -1, kernel=kernel)
```
修改卷機核可以改變圖片銳利方式

## 濾波器
```
MedianBlur_key = cv.medianBlur(img_saltNoiseKey,5) 中值濾波器
bilateral_key = cv.bilateralFilter(img_key,9,75,75) 雙邊濾波
res = cv2.blur(image, (ksize, ksize))  #平均
res = cv2.GaussianBlur(image, (size, size), sigmaX, sigmaY) #高斯模糊(取高斯分布)
```

## 邊緣偵測
### Sobel
sobel可以對橫的直的做過濾找出橫的直的變化。把橫的直的過濾結果相加後就能找出邊緣
```
# Sobel 分別針對 x 與 y 方向響應
dx_key = cv.Sobel(src=gray_key, ddepth=cv.CV_16S, dx=1, dy=0, ksize=3)

# Sobel 計算 x 與 y 方向響應介於-1020~1020(若使用 8-bits unsigned integer 無法表示)
dy_key = cv.Sobel(src=gray_key, ddepth=cv.CV_16S, dx=0, dy=1, ksize=3)

# 因此此處使用 16-bits signed integer
# Sobel 將響應計算結果(-1020~1020)取絕對值後轉成 uint-8
Xaxis_key = cv.convertScaleAbs(src=dx_key)
Yaxis_key = cv.convertScaleAbs(src=dy_key)


# Sobel 將 x 與 y 方向響應合併
sobel_key = cv.addWeighted(src1=Xaxis_key, alpha=0.5, src2=Yaxis_key,beta=0.5, gamma=0)
```
![](https://i.imgur.com/g5SPuXb.png)


### Laplacian
利用微分計算邊緣的差異，二次微分找出差異的差異，計算得出filter
```
# Laplace 響應大小(kernel size)為 3*3
# ddepth: -1 表示影像深度與原圖相同
laplaceKey = cv.Laplacian(src=gray_key, ddepth=-1, ksize=3)
```
![](https://i.imgur.com/hbdUbPX.png)

### Canny
建立在Sobel的基礎上，先高斯濾波後再做Sobel，並做最大值抑制、加強連續段
```
# Canny 下界門檻值為 50;上界門檻值為 150
# 響應大小(kernel size)參數為 apertureSize 預設(3,3)
cannyKey = cv.Canny(gray_key, 50, 150)
```
![](https://i.imgur.com/m9EmXxk.png)

## haar 特徵 (人臉辨識)
哈爾特徵由黑色區域及白色區域組成的矩形遮罩，其計算方式為：將哈爾特徵放於目標區域上，計算目標區域上黑色區域的總和減去白色區域的總和。舉下圖為例，其計算為2-1（黑色減去白色區域）。
![](https://i.imgur.com/5mNKNuq.png)


不同種類的哈爾特徵便是藉由黑色及白色區域位置的不同，可適用於不同種類的特徵。

OpenCV中使用的哈爾特徵分類如下：
- Edge features：用於檢測邊緣特徵，包含水平、垂直及旋轉類型。
- Line features：用於檢測直線特徵，包含水平、垂直及旋轉類型。
- Center-surround features：用於檢測中心特徵，包含平放及旋轉類型。  

![](https://i.imgur.com/BubkZWV.png)

```python=
# 讀取內建的臉部辨識模型
face_cascade = cv.CascadeClassifier('./assets/cascade_training/haarcascades/haarcascade_frontalface_default.xml')
eye_cascade = cv.CascadeClassifier('./assets/cascade_training/haarcascades/haarcascade_eye.xml')

#打開相機
cap = cv.VideoCapture(0)

while cap.isOpened():
    _, frame = cap.read()
    gray = cv.cvtColor(frame, cv.COLOR_BGR2GRAY)
    faces = face_cascade.detectMultiScale(gray, 1.3, 5)
    for (x,y,w,h) in faces:
        cv.rectangle(frame,(x,y),(x+w,y+h),(255,0,0),2)
        roi_gray = gray[y:y+h, x:x+w]
        roi_color = frame[y:y+h, x:x+w]
        eyes = eye_cascade.detectMultiScale(roi_gray)
        for (ex,ey,ew,eh) in eyes:
            cv.rectangle(roi_color,(ex,ey),(ex+ew,ey+eh),(0,255,0),2)
    cv.imshow('face',frame)
    keyIn = cv.waitKey(30)
    if keyIn == 27:
        cap.release()
cv.destroyAllWindows()
```

## LBP
可以很好的解決"光影"誤差。

![](https://i.imgur.com/Vmo7li9.png)

而中間點是: 把原始圖片與過濾圖片相乘加總
![](https://i.imgur.com/A617Qqb.png)

```python=
def lbp(img):
    assert(len(img.shape) == 2) # 只接受灰階影像
    ret = np.zeros_like(img)    # 建立一張與輸入圖片大小一樣，但全黑的圖片
    
    img = cv.copyMakeBorder(img, 1, 1, 1, 1, cv.BORDER_REPLICATE)  # 將原圖四周擴展1格
    
    for y in range(1, img.shape[0] - 1):
        for x in range(1, img.shape[1] - 1):
            center = img[y][x]
            pixel = 0
            pixel |= (img[y - 1][x - 1] >= center) << 0
            pixel |= (img[y - 1][x + 0] >= center) << 1
            pixel |= (img[y - 1][x + 1] >= center) << 2
            pixel |= (img[y + 0][x + 1] >= center) << 3
            pixel |= (img[y + 1][x + 1] >= center) << 4
            pixel |= (img[y + 1][x + 0] >= center) << 5
            pixel |= (img[y + 1][x - 1] >= center) << 6
            pixel |= (img[y + 0][x - 1] >= center) << 7
            
            ret[y-1][x-1] = pixel
    return ret
```

通常我們會過濾0、255這兩的數字因為這種極值沒有甚麼意義
我們可以透過統計值方圖來判斷這個目標值方圖與人臉一般的質方圖是不是類似。
LBP的缺點是必須對目標有準確目標



# python
1. os.getpid() 查詢此python的process，可以寫出去給shell or systemd kill
2. 輸出覆蓋: print('', end='\r')
```
A**B A的B次方
A//B B整除A
```

assert 是斷言（Assertion），指的是程式進行到某個時間點，斷定其必然是某種狀態。
其實類似於註解的效果
類似的，在一個if判斷中，如果x大於0，就執行if區塊，否則x必須是等於0，這時也可使用斷言測試：
```python=
if x > 0:
    # do some
    ...
else:
    assert x == 0, 'x 此時一定要是 0，不會是負數'
    # do other
```

**可變參數**
function在使用可變參數時，必須先含有一個必要參數
*args是可變的positional arguments列表，**kwargs是可變的keyword arguments列表
```python=
def fun(a, *args, **kwargs):
    print("a={}".format(a))
    for arg in args:
        print('Optional argument: {}'.format( arg ) )

    for k, v in kwargs.items():
        print('Optional kwargs argument key: {} value {}'.format(k, v))

fun(1,22,33, k1=44, k2=55)
-----------------結果------
a=1
Optional argument: 22
Optional argument: 33
Optional kwargs argument key: k1 value 44
Optional kwargs argument key: k2 value 55
```
## Encoding
```python=
response.content.decode("utf-8", "replace")
```
## 多執行續 threading
https://blog.gtwang.org/programming/python-threading-multithreaded-programming-tutorial/
## matplot
印多圖片 subplot
![](https://i.imgur.com/OWj0ObE.png)

改變圖片大小:
```
pyplot.rcParams['figure.figsize'] = [10, 10]
```

詳細教學
https://zhuanlan.zhihu.com/p/96616339


基本圖線
```python=
plt.figure(figsize=(16,5))
# 16寬5高
plt.title("title")
plt.xlabel("data")
plt.ylabel("count")
plt.plot(df.data.str.apply(str),df.confirm,'go')
# df.data.str.apply(str) 為x軸
# df.confirm 為y 軸
# g 為綠色 o 為點狀
plt.plot(df.data.str.apply(str),df.suspect,'r--')
# r 為紅色 -- 為虛線
plt.legend(['confirm','suspect'])
# 圖例
plt.show()
```


## sort dict
https://segmentfault.com/a/1190000004959880
key=lambda 元素: 元素[字段索引]代表你想要排序的索引片段(可以lambda x:x[-1])
### sort by value
```sorted(d.items(), key=lambda x: x[1])```
### sort by key 
```[(k,di[k]) for k in sorted(di.keys())]```
#### Unpick
python解壓tuple
```python=
k = (N,500)
j,g = *k
#j=N
#g=500
##通常用在function

#一個*是tuple
#兩個**是list
```
http://blog.maxkit.com.tw/2018/12/python-args-kwargs.html

### iteratable
```python=
for i,data in list.items():
    print(i)
```
## 環境requirement
可以寫requirement.txt 來直接安裝玩需求套件
```pip freeze > requirements.txt```可以印出所有套件名稱

```txt=
django<2.0
djangorestframework==3.8.1
```
之後再```pip install -r requirements.txt```

## time
http://dangerlover9403.pixnet.net/blog/post/207711846-%5Bpython%5D-day13---python-time-%E6%A8%A1%E7%B5%84

## argparse
環境參數套件 (不須安裝)
https://medium.com/@dboyliao/python-%E8%B6%85%E5%A5%BD%E7%94%A8%E6%A8%99%E6%BA%96%E5%87%BD%E5%BC%8F%E5%BA%AB-argparse-4eab2e9dcc69
``import argparse``

![](https://i.imgur.com/7Mu5WTS.png)

## csv 
writeRows 時自動出現空行的問題
在stackoverflow上找到了比较经典的解释，原来 python3里面对 str和bytes类型做了严格的区分，不像python2里面某些函数里可以混用。所以用python3来写wirterow时，打开文件不要用wb模式，只需要使用w模式，然后带上newline=‘’。
```
writefile = open('result.csv','w'，newline =‘’)
writer = csv.writer(writefile)
```

2. 在read檔案時有時會遇到utf8 can not decodes那麼可以使用
```python=
f=open('HDM_bd_02-01_01_120.amc',encoding='ISO-8859-15')
```

## radix Sort
```
def sort(number, d):
    length = len(number)
    k = 0
    n = 1
    temp = []
    for i in range(length):
        temp.append([0] * length)
    order = [0] * length
    while n <= d:
        for i in range(length):
            lsd = (number[i] // n) % 10
            temp[lsd][order[lsd]] = number[i]
            order[lsd] += 1
        for i in range(length):
            if order[i] != 0:
                for j in range(order[i]):
                    number[k] = temp[i][j]
                    k += 1
            order[i] = 0
        n *= 10
        k = 0
        
number = [73, 22, 93, 43, 55, 14, 28, 65, 39, 81, 33, 100]
sort(number, 100)
print(number)
```

## numpy

https://github.com/sunwu51/notebook/blob/master/20.01/numpy101.ipynb

### reshape
一般用法：numpy.arange(n).reshape(a, b); 依次生成n个自然数，并且以a行b列的数组形式显示。

特殊用法：mat (or array).reshape(c, -1);  必须是矩阵格式或者数组格式，才能使用 .reshape(c, -1) 函数， 表示将此矩阵或者数组重组，以 c行d列的形式表示（-1的作用就在此，自动计算d：d=数组或者矩阵里面所有的元素个数/c, d必须是整数，不然报错）（reshape(-1, e)即列数固定，行数需要计算）
```
arr=np.arange(16).reshape(2,8)
array([[ 0,  1,  2,  3,  4,  5,  6,  7],
       [ 8,  9, 10, 11, 12, 13, 14, 15]])

arr.reshape(4,-1) #将arr变成4列的格式，列数自动计算的(c=4, d=16/4=4)
array([[ 0,  1,  2,  3],
       [ 4,  5,  6,  7],
       [ 8,  9, 10, 11],
       [12, 13, 14, 15]])

arr.reshape(8,-1) #将arr变成8行的格式，列数自动计算的(c=8, d=16/8=2)
array([[ 0,  1],
       [ 2,  3],
       [ 4,  5],
       [ 6,  7],
       [ 8,  9],
       [10, 11],
       [12, 13],
       [14, 15]])
```

其他用法：numpy.arange(a,b,c)/ numpy.arange(a,b,c).reshape(m,n); 从 数字a起, 步长为c, 到b结束，生成array。

### nparray indexing 
重要!!! 十分好用
可以參考 http://violin-tao.blogspot.com/2017/06/numpy-2.html
例子:
```python=
# np.argmax(predictions, axis=1) = [1 1 1 1 1 1 0 1 1 0]  
# predictions = [[2.9304740e-01 7.0694768e-01 4.9991995e-06]
#  [4.2720035e-01 5.6982458e-01 2.9750725e-03]
#  [2.8658855e-01 7.1341115e-01 2.7253316e-07]
#  [2.4754529e-01 7.5245470e-01 1.6214444e-09]
#  [3.3878914e-01 6.6116464e-01 4.6268226e-05]
#  [2.9966766e-01 7.0032877e-01 3.6000888e-06]
#  [6.6807103e-01 3.0811578e-01 2.3813138e-02]
#  [3.3389658e-01 6.6607779e-01 2.5651412e-05]
#  [3.2705170e-01 6.7294693e-01 1.3545706e-06]
#  [5.5636162e-01 4.0166456e-01 4.1973814e-02]]

#下面的nparray要被上面的取得 y index，可以這樣寫

print(predictions[range(10),np.argmax(predictions, axis=1)])
# x軸是0~9 index, y軸是上面的index
```
https://leemeng.tw/images/pca/IndexingDataMatrixScene.mp4

### axis 軸
```python=
np.argmax(a,axis = 0)
axis 指的是依照哪一個維度方向唯一組軸方向，例如axis=0則依照row的方向(垂直的)，，axis=1依照column方向(水平)
當a = [
[100,2,3],
[56,22,78],
[576,2,3]]
axis = 0 是column看，回傳index[2,1,1]
axis = 1 是row 看，回傳index[0,2,0]
```
![](https://i.imgur.com/shvGzBC.png)

axis = 1 時
![](https://i.imgur.com/96lTSvc.png)

在pandas也很常用到axis

### indexing 中取特定的column
例如你有一個(2,3)的矩陣，你要取第一列與第三列
可以用```[1,3]```來indexing

```python=
data = np.zeros((2,3))

filtered = data[:,[1,3]]
```

### shuffle dataset
```python=
def _shuffle(X,Y):
    randomize = np.arange(len(X))
    np.random.shuffle(randomize)
    return (X[randomize], Y[randomize])
```

### np.clip 代表取上下限
numpy.clip(a, a_min, a_max, out=None)

比 a_min小則為a_min，反之max。

## SSH SCP
之後要學一下

## tqdm
用position=0 and leave=True可以防止tqdm的多行bug

![](https://i.imgur.com/0H29Dvj.png)


```python=
train_pbar = tqdm(train_loader, position=0, leave=True)

for x, y in train_pbar:
```

## python 一行
### swap value
交換數值
```
a, b = b, a

a, b, c, d = b, c, d, a
```

### list comprehension
替代loop

```
ls = [i for i in range(5)]

ls = [-1, 2, -3, 6, -5]
ls = [i for i in ls if i > 0] #ls = [2, 6], positive integers only
```

### map
map是將list內的element都應用上一個function。

```
ls = list(map(int, ["1", "2", "3"])) #ls = [1, 2, 3]
```
把裡面的數值全部轉乘int

### filter
檢查list的element，移除對funciton檢查是false的element。
```
ls1 = [1, 3, 5, 7, 9]
ls2 = [0, 1, 2, 3, 4]
common = list(filter(lambda x: x in ls1, ls2)) #common = [1, 3]
```

### Reduce
reduce就如其名，會將一個list內的數值依照function內容整合進一個值。
此外，reduce位於functools package內。

reduce() 函数会对参数序列中元素进行累积。

函数将一个数据集合（链表，元组等）中的所有数据进行下列操作：用传给 reduce 中的函数 function（有两个参数）先对集合中的第 1、2 个元素进行操作，得到的结果再与第三个数据用 function 函数运算，最后得到一个结果。
```
from functools import reduce
print(reduce(lambda x, y: x*y, [1, 2, 3])) #print 6
```

### Lambda
過去:
```
def fullName(first, last):
    return f"{first} {last}"
name = fullName("Tom", "Walker") #name = Tom Walker
```
lambda是一個小型匿名函數，來幫助簡化程式。

```
fullName = lambda first, last: f"{first} {last}"
name = fullName("Tom", "Walker") #name = Tom Walker
```

lambda的妙用是可以把function當作是一個參數傳入
```
highOrder = lambda x, func: x + func(x)
result1 = highOrder(5, lambda x: x*x) #result1 = 30
result2 = highOrder(3, lambda x : x*2) #result2 = 9

# highorder 是參數1+function of 參數1
# 透過傳入不同function來達到不同的效果
```
### slice 妙用
https://docs.python.org/2.3/whatsnew/section-slices.html
slice 其實有第三個參數 step、stride。
```
# step == 2
L = range(10)
L[::2]
# [0, 2, 4, 6, 8]

# 反轉
L[::-1]
[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]

# 插入list
a = range(3)  # [0, 1, 2]
a[1:3] = [4, 5, 6]
a #[0, 4, 5, 6]

# step + 插入list
a = range(4) #[0, 1, 2, 3]
a[::2]  # [0, 2]
a[::2] = [0, -1] #[0, 1, -1, 3]

a[::2] = [0,1,2] #超過負擔，報錯
```

### 反轉
```
ls = [1, 2, 3]
ls = ls[::-1] #ls = [3, 2, 1]
```

不過上面那個會消耗memory，你可以選擇reverse()
```
ls = [1, 2, 3]
ls.reverse() #ls = [3, 2, 1]
```

### 列印多個

```
for i in range(5):
    print("x", end = "") #print xxxxx
    
print("x"*5) #print xxxxx
```

### 範例
1. 找出n!

原始:
```python=
def fact(n):
    if n == 1:
        return 1
    else:
        return n*fact(n-1)
```

可以使用reduce

```python=
from functools import reduce

reduce(lambda x, y: x*y, range(1, n+1)) #n factorial
```

2. 找出Fibonacci number

Fibonacci sequence are 0, 1, 1, 2, 3, 5, 8, 13

過去:
```python=
def fib(n):
    if n == 0 or n == 1:
        return n
    else:
        return fib(n-1) + fib(n-2)
print(fib(n)) #prints the nth Fibonacci number
```

Alternatively, you can do this:
```python=
fib = lambda x: x if x<=1 else fib(x-1) + fib(x-2)
print(fib(n)) #prints the nth Fibonacci number
```

3. 確認字串有無回文

```python=
# 過去
def is_palindrome(string):
    if string == string[::-1]:
        return True
    else:
        return False

print(is_palindrome("abcba")) #prints True

# 一行
string = "abcba" #a palindrome
print(string == string[::-1]) #prints True
```

4. 把2D扁平化

2D -> 1D
```python=
# 過去
ls = [[1, 2], [3, 4], [5, 6]]
ls2 = []
for i in ls:
    for j in i:
        ls2.append(j)
print(ls2) #prints [1, 2, 3, 4, 5, 6]

# 現在
ls = [[1, 2], [3, 4], [5, 6]]
print([i for j in ls for i in j]) #prints [1, 2, 3, 4, 5, 6]
```



# Keras的坑
## 安裝
```
conda install tensorflow
conda install keras 

# 測試是否有gpu support 
import tensorflow as tf
tf.test.gpu_device_name()

If the output is '', it means you are using CPU only;
If the output is something like that /device:GPU:0, it means GPU works.
```
# TFlite
用於respberry pi 越新越好 (4)
https://hackmd.io/RjLadPHVT16zmTJjda2WGA

### 放上伺服器時element not in the grap
```python=
model = load_model("./model/LSTM_model3.h5")
model._make_predict_function()
```

https://www.tensorflow.org/install/gpu

TF DATASET
https://www.tensorflow.org/tutorials/load_data/images

```
dataset = tf.data.Dataset.from_tensor_slices(image_list)
dataset = dataset.map(lambda x: (image_PATH+x+".jpg",mask_PATH+x+".png"))
dataset = dataset.map(load_image,num_parallel_calls=tf.data.experimental.AUTOTUNE)


for img,mask in dataset.take(1):
    plt.imshow(img)
    plt.show()
    
    arr = np.asarray(mask).squeeze()
    plt.imshow(arr,cmap="gray")
    plt.show()
```

# Nodejs
## 安裝
```bash=
sudo apt-get install nodejs npm 
```

https://github.com/nodejs/help/wiki/Installation
要輸出path修改 .bashrc在最下面加入export PATH如:
```bash=
export PATH="~/anaconda3/bin:$PATH"
export PATH="/usr/local/lib/nodejs/node-v12.13.0-linux-x64/bin:$PATH"


. /etc/profile
```
https://www.cnblogs.com/amboyna/archive/2008/03/08/1096024.html

### express 安裝
https://expressjs.com/zh-tw/starter/generator.html 


## Mongo-Session
會存在sessions這個collections中，看自己的code
範例: https://github.com/lufor129/OpenData
al/blob/master/app.js
使用: https://www.npmjs.com/package/connect-mongo

# Web Socket
詳細可以看這一篇
https://medium.com/enjoy-life-enjoy-coding/javascript-websocket-%E8%AE%93%E5%89%8D%E5%BE%8C%E7%AB%AF%E6%B2%92%E6%9C%89%E8%B7%9D%E9%9B%A2-34536c333e1b

http請求與web socket請求不同，http是客戶端主動發起請求，服務端再給予相應處理。
socket 是TCP socket，客戶端與server端之間建立起一個長連接，雙方都可以主動傳遞請求。

![](https://i.imgur.com/Qvv3wT5.png)

```npm -i ws```
在html5後出現web socket技術，例如前後端都指定好路徑"/ws"並在localhost下，JS寫法如下:

```javascript=
## client端request到服務端

# 建立起連線class
var c = new WebSocket("ws://localhost:1880/ws")

# 傳送
c.send("HAHA")

# 建立返回函數
c.onmessage = function(e){console.log(e.data)}
```

如果服務端也想要主動聯繫客戶端，在node.js上安裝好websocket套件，按照blog上做的。

```javascript=
//後端
const WebSocket = require("ws");
const wss = new WebSocket.Server({port:3000});

wss.on("connect",ws=>{
  console.log("有人連近來")
  
  //主動傳遞訊息 message事件
  ws.on("message",data =>{
    ws.send(data)
  })
  
  ws.on("close",()=>{
    console.log("走了")
  })
})

// 前端
const ws = new WebSocket('ws://localhost:3000')
ws.addEventListener('open',()=>{
  console.log("連上伺服器")
  //傳送訊息
  ws.send("AAA")
})
//監聽message事件
ws.addEventListener('mesage',({data})=> {console.log(data)})
```
wss 監聽函數

# ML
Linux Cuda:
https://medium.com/@zihansyu/ubuntu-16-04-%E5%AE%89%E8%A3%9Dcuda-10-0-cudnn-7-3-8254cb642e70


## loss
categorical_crossentropy 類別softmax型

## train&evaluate
用fit or train_on_batch(自己切)
train完後，可以model.evaluate(xtest,ytest,batch_size=32)

## pred
model.predict
model.predict_classes(test,batch_size=64)
model.predict_proba(test,batch_size=64)


## trainsfer learning
### fine tune
前面model不能train。
是指訓練自己接在transfer下的layer，當transfer model內有batch norm時容易出事情，train acc下降但test acc沒下降(平平的)。

1x1 conv是為了將多個channel合併，因為1x1 conv是有厚度的



## recall & percision
recall : 在所有辨識為A的真的是為A。 (更推薦提升)
percision: 在所有A中被辨識成功的。

recall 在文字探勘時，規則越放鬆越容易提升
EX: 大小寫不受限制、state-of-art == state of art

stop word 會降低recall
例如: to be or not to be 查詢不到(全部都是 stop word)

stemming 可以提升recall 做詞維度壓縮，多->少
stemmer 可以抓出stem
1. n-gram : 字與字之間的相似度來找出相同字根
S = 2C/A+B

EX:

statustics => st ta at ti is st ti ic cs
unique  => ar cs ic is st ta ti (共7個)
statisical => st ta at ti is st ti ic ca al
unique => al at ca ic is st ta ti (共8個)

共同:6個
S = 2C/A+B = 2*6/7+8 = 0.8

可以得出n-gram matrix 並分群 clustering

推薦用名詞當作 index term(還原成名詞，名詞最能代表句子的意思)
2. successor variety
3. afflix removal stemmer 最普遍使用
就是寫好規則
EX: if word end with 'ies' but not 'eies' or 'aies'
then 'ies'->'y'

若符合多個規則則longest match stemmer
去google porter stemmer rule

### cross validation
https://www.kaggle.com/stefanie04736/simple-keras-model-with-k-fold-cross-validation
(內涵Image Data Augmentation)

### Data Augmentation
1. 圖片色彩、翻轉、光影
2. Random crops、scales
3. color jitter contrast
4. PCA降維做 whitening做color offset相減或相加
![](https://i.imgur.com/QewV1DU.jpg)

**注意**
1. Test/train split before augumentation 不可在Test上augument 上使用。
2. Cross validation要特別注意 validation同樣不能augument，要明確指出那些圖片是生成出來的 

## 已有Model
### VGGNet
* two 3x3 = 5x5 receptive 參數: 
* three 3x3 = 7x7 receptive 參數: $C*(C*7*7)=49C^2$ vs $3*C(C*3*3) = 27C*2$
> less parameters 
> more non-lineary(relu) (經過2次vs經過1次)

做1x1把channel參數降下來。
![](https://i.imgur.com/1jIsZCv.jpg)

已可以把NxN的拆成Nx1、1xN，fewer parameters、less compute、more nonlinearity。


### GoogleNet
移除所有FC層
![](https://i.imgur.com/MHksdpu.png)



### ResNet
152 layers!但是runtime比VGG還快
發展趨勢，後面大多以ResNet開始使用
![](https://i.imgur.com/M5fTs6H.png)
因為他們認為X也很重要，所以額外拉一條線來保留X

使用152層效果最好。

目前的趨勢是把Pool/FC給拿掉
**GAN裡面不要加上POOL**

## 硬件加速
就是cuDNN加速matrix multiplication。
例如在做conv時，將圖片先攤成($K^2*C$)xN與D個conv Dx($K^2$C)相乘。(讓Mem Hit)
成DxN result

注意!! 每一條之間會有重複，重複的東西load多次使效率下降。(K^2C)xN
改良!! 一次load進來後，與上中下各計算一次(KC)xN

FFT:用Fast Fourier Transform，can compute N dimensional in O(NlogN)
用在conv很大時。

Strassen Algorithm 在小矩陣運算會比較快速

### Floating Point
現在趨勢是把float32降成16 bit，減少model參數大小

### Visualization Deep Learning
看看神經網路到底學了什麼
1. DeConv approaches
2. Neuron Receptive 中間層某個點往回看，看看focus在image哪個區域
3. 把最後一層(不是softmax)，降維看看分布
4. Deep Q Network 
5. occlusion experiments 在圖片上挖空，看出來的狀況。


# WebSocket
寫法與一般的web Server不太一樣

## Express WebSocket
https://medium.com/enjoy-life-enjoy-coding/javascript-websocket-%E8%AE%93%E5%89%8D%E5%BE%8C%E7%AB%AF%E6%B2%92%E6%9C%89%E8%B7%9D%E9%9B%A2-34536c333e1b

# Selenium Server安裝
參考自
http://zhaoyabei.github.io/2016/08/29/Linux%E9%85%8D%E7%BD%AESelenium+Chrome+Python%E5%AE%9E%E7%8E%B0%E8%87%AA%E5%8A%A8%E5%8C%96%E6%B5%8B%E8%AF%95/
https://medium.com/@keigi1203/python-%E9%80%B2%E9%9A%8E%E7%88%AC%E8%9F%B2%E6%8A%80%E5%B7%A7-selenium-chrome-d4ae4979a874

```shell=
sudo apt-get install libxss1 libappindicator1 libindicator7
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome*.deb
```
然後 google-chrome --version 確認版本
接著到
http://chromedriver.storage.googleapis.com/index.html 下載相應文件
安裝selenium
```shell=
sudo pip install selenium
sudo pip install requests
```
相應的文件chromedriver放在 /usr/bin
```shell=
wget -N http://chromedriver.storage.googleapis.com/版本/chromedriver_linux64.zip
unzip chromedriver_linux64.zip
chmod +x chromedriver
sudo mv -f chromedriver /usr/local/share/chromedriver
sudo ln -s /usr/local/share/chromedriver /usr/local/bin/chromedriver
sudo ln -s /usr/local/share/chromedriver /usr/bin/chromedriver
```

測試
```python=
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
options = Options()
options.add_argument('--headless')
options.add_argument('--no-sandbox')
driver = webdriver.Chrome('/usr/bin/chromedriver', chrome_options=options)
driver.get("https://google.com")
```

## Windows版 安裝

確定自己chrome版本後
到
https://sites.google.com/a/chromium.org/chromedriver/home 下載
然後丟到env 的python目錄一起放

測試
```=python
from selenium import webdriver
browser = webdriver.Chrome()
```

# Ngnix
sudo certbot --domains lufor130.nctu.me
https://xuexb.com/post/nginx-url-rewrite.html

## 改port
查詢port ```sudo netstat -lpn |grep 80```
將 /etc/nginx/site-availables/default 的所有port改掉後reload即可。
![](https://i.imgur.com/CS3KNXD.png)

https://blog.techbridge.cc/2018/08/11/nginx-static-dynamic-page-server-intro/
注意nginx location redirect

location 匹配規則
https://github.com/sunwu51/notebook/blob/master/19.07/nginx_%E7%9F%A5%E8%AF%86%E7%82%B9%E6%95%B4%E7%90%86.md

當多個要rewrite 類似如下，寫在Virtual Host:
```shell=
root /var/www/html;

# Add index.php to the list if you are using PHP
index index.html index.htm index.nginx-debian.html;
server_name lufor129.nctu.me; # managed by Certbot

location /black {
	rewrite ^.+black/?(.*)$ /$1 break;
	proxy_pass http://127.0.0.1:5000;
	proxy_set_header Host $host;
}

location /images{
  rewrite ^.+images/?(.*)$ /$1 break;
  root /home/huang/ettoday/pic;
}

location / {
	# First attempt to serve request as file, then
	# as directory, then fall back to displaying a 404.
	try_files $uri $uri/ =404;
	#proxy_pass  http://127.0.0.1:5000/ ;
	#proxy_pass http://127.0.0.1:5000;
	#proxy_set_header Host $host;
}
```
透過 nginx log 可以很清楚看到是否輸入指令正確
```cat /var/log/nginx/access.log```
## 匹配規則
### 優先權
```bash=
server {
        listen 80;
        server_name localhost;
        default_type text/html;
        location / {
            # lowestest priority, add nothing front
            echo "hello nginx";
        }
        location  = /a {
             # highest priority, need complete match
             echo " = /a";
        }
        location ^~ /a {
             # ^~ is the second priority, for example /a/b;/ab can match,but /c cant   
             echo " second ";
        }
        location ^~ /a/b {
             # same as the second priority, but longer match first 
             echo " second but longer";
        }
        location ~ ^/\w {
             # third priority
             # regExp match, \w means any word,number...
             echo "regExp match \w ";
        }
        location ~ ^/[a-z] {
             # regExp, the same match priority,same match, who write upper can be match 
             # in this case, the upper ~ ^/\w can be match
             echo "[a-z]";
        }
    }
```

### 反向代理
```bash=
location ^~ /a {
		echo "test";
		proxy_pass http://172.17.0.3;
}
```
### 網頁圖片轉址
![](https://i.imgur.com/pjFDQOt.png)

### 負載均衡
![](https://i.imgur.com/BEp7DoU.png)
他會隨機跳轉至80 or 81 端口來平衡

也可以給予權重
![](https://i.imgur.com/Z8b3K8k.png)
代表80端口出現的機率比81高10倍

## Nginx的static圖片位置
```shell=
# 例如我將圖片放在 /home/huang/ettoday/pic/20180101/aaa.jpg
# 要取得圖片，需要將location root 改變，同時要rewrite

location /images {
	rewrite ^.+images/?(.*)$ /$1 break;
	root /home/huang/ettoday/pic;
}

# 要獲得圖片時，在網址上輸入
# https://lufor129.nctu.me/images/20190101/aaa.jpg
```

# Openresty
推薦使用Openresty，集成nginx與Lua的web平台
## 安裝
https://openresty.org/cn/linux-packages.html

## 設定
通過修改 /etc/openresy/nginx.conf

```nginx -s reload```
來重新啟動修改過的openresty

# Curl 參數

# Python 視覺化Charify
解決80%繪圖需求，剩下交給matplot
## 安裝
https://github.com/spotify/chartify#installation
```conda install -c conda-forge chartify```

## 其他可視化教學
https://github.com/datawhalechina/pms50

# 網頁安全
## XSS 攻擊

## SQL 注入

# CouchDB
https://couchdb.apache.org/
你也可以用docker安裝，默認為5984 port。
```docker run -d -p 5984:5984 couchdb```
https://docs.couchdb.org/en/2.2.0/api/server/common.html 一些API

```http://192.168.99.100:5984/_utils/```進入管理介面
![](https://i.imgur.com/uxSbwiu.png)

## 新增資料庫 PUT
PUT 192.168.99.100:5984/cart

## 插入資料 POST
![](https://i.imgur.com/oe71y1p.png)
![](https://i.imgur.com/WL9KuVo.png)

## 獲取資料 GET
根據Id獲取資料及可
![](https://i.imgur.com/0BhSecE.png)
![](https://i.imgur.com/2E1eg3s.png)


## 資料覆蓋 PUT
![](https://i.imgur.com/m6WOAtt.png)
需要在要覆蓋的Data中加入_rev確保資料一致性

## 刪除 DELETE
一樣需要_rev，但你可以把rev直接寫在http中
![](https://i.imgur.com/wfbt7Be.png)

# Postgres
https://github.com/sameersbn/docker-postgresql#enabling-extensions
**用docker建啦!!!**
```docker run --name mypostgres -d -v $HOME/docker/volumes/postgres:/var/lib/postgresql/data -e POSTGRES_PASSWORD=123456 -p 5432:5432 postgres```

EXE:
```docker run --name postgres_p -d -v //d/program/ADBS/hw2_demo:/app -e POSTGRES_PASSWORD=123456 -p 5433:5432 hw_postgres```

## 進入
```
docker exec -it -u root postgres mypostgres bash
```

## 登入postgres
su postrges
psql <DB>

畫面很亂時 CTRL+L

## 基本操作
>\dt 列出所有Table
>\d <tableName> 列出table attributed
>

# Scrapy
https://city.shaform.com/zh/2016/02/28/scrapy/
## 安裝
```conda install -c conda-forge scrapy```

## 開始專案
scrapy startproject ptt

# WEKA
https://www.itread01.com/content/1546543628.html

## Feature Selection
weka可以做Feature Selection。選entropyGain、Ranking 選擇feature排序。

## association
https://medium.com/@bt2011aa/%E4%BB%A5weka%E5%B0%8D%E8%B3%87%E6%96%99%E9%9B%86%E9%80%B2%E8%A1%8C%E9%97%9C%E8%81%AF%E5%BC%8F%E8%A6%8F%E5%89%87%E4%B9%8B%E5%AF%A6%E4%BD%9C-e7a87c2005a9

# CORS 跨域問題
## 發生原因
![](https://i.imgur.com/1XPH4Ip.png)
不同網域之間的請求，如百度請求淘寶的網站。
不同接口、不同伺服器之間的請求會導致跨域問題。
## 解決辦法
### 1. header
![](https://i.imgur.com/58t2rRF.png)
資料輸送方給予跨域許可即可允許資料跨域

### 2. jsonp
輸送端
![](https://i.imgur.com/cUv5jxj.png)

請求端
![](https://i.imgur.com/vBdHKE8.png)

### 3. 開啟不安全模式
cmd 輸入 
```
"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --disable-web-security --disable-gpu --user-data-dir=~/chromeTemp
```

流程為先運行function f(data)先註冊函數f將輸入參數alert。下面callback=f傳入app2.get解析出裡面的callback(此時funcname = f了)，接著送出"f('你好')"到前端，前端script執行f函數。

CROS 完全解法
https://blog.huli.tw/2021/02/19/cors-guide-2/

# JS
## MapChart
台灣地圖
http://nhn.github.io/tui.chart/latest/

## Material icon
https://materialdesignicons.com/

## 功能
### 閉包解析上傳檔案
參考: https://stackoverflow.com/questions/34495796/javascript-promises-with-filereader
```javascript=
readFile(file){
  return new Promise((resolve,reject)=>{
    const reader = new FileReader();
    reader.onload = function(e) {
      var data = new Uint8Array(e.target.result);
      var workbook = XLSX.read(data, {type: 'array'});
      let sheetName = workbook.SheetNames[0]
      let worksheet = workbook.Sheets[sheetName];
      console.log(XLSX.utils.sheet_to_json(worksheet));
      resolve(worksheet)
    };
    reader.onerror = reject
    reader.readAsArrayBuffer(file)
  })
},
```

### 建立空陣列
```javascript=
let output = Array(5).fill(null)
```

### 下載檔案
```javascript=
let blob = new Blob([data],{type:"text/plain"})
let link = document.createElement('a')
link.href = window.URL.createObjectURL(blob)
link.download = name
link.click()
```

# Jetson nano
環境安裝
https://medium.com/@jackycsie/jetson-nano-9d89cbf2fc18

# Superset
學一下，可以輕鬆的用來連結資料庫並拉出漂亮的報表
https://superset.apache.org/