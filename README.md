# files contents
finlab_course包含了[hahow](https://hahow.in/courses/5a2170d5a6d4a5001ec3148d/main?curriculum=5b1308cb865ad2001ec28980)這門課的一些課程檔案以及modules.

# 開發流程
1. Pull from the origin master to local
2. "git checkout -b <new_branch_name_for_what_developing>" in local
3. "git add ." to add what is changed into a commit.
4. "git commit -m 'message about the commit.'" to formally commit changes to the *local* branch <new_branch_name_for_what_developing>.
3. "git push origin <new_branch_name_for_what_developing>" to *remote* after developing with brief messages in each commit during developement.
4. Create a pull request to remote with a detail message.
5. Let's code reviewing and decide whether to merge to the master branch.

# 友善連結
1. [關於目前要撈的資料的google sheet](https://docs.google.com/spreadsheets/d/13VaADmny6l8arsr5Wrymb-oMN_bLd7Oaeckz_BxylZ0/edit#gid=0)<br />
2. [關於投資策略方向的討論](https://docs.google.com/document/d/1Sim1e0Tl2re86skXnin1j372fLNWsAgD9XzFi9KAu0Q/edit?ts=5c4ef112)<br />
3. [程式交易討論區](http://www.coco-in.net/forum-17-1.html): 如果沒有什麼靈感，可以來這邊挖寶<br />
4. [爬蟲教程](https://piaosanlang.gitbooks.io/spiders/01day/README1.html)


# 要先做的事

~~請大家安裝[database browser](https://sqlitebrowser.org)以便直接透過軟體看sql database裡面的table。 <br />~~
- 目前我們使用[robo3T](https://robomongo.org/)來瀏覽存在server中的mongo database(mongoDB). 設定如下：
  - Connection/Address: localhost : 27017
  - Authentication
/Database: stock_data
/User Name: stockUser
/Password: stockUserPwd
  - SSH
  /SSH Address: 140.112.104.141
  SSH User Name: wenping
  SSH Auth Method: Password
  User Password: bobbyteeseanwp9
- 基本使用範例：
  - find:
    - `db.getCollection('dailyPrice').find({'timestamp': 'ISODate("2009-01-05T00:00:00.000Z")', 'stockId': '2330'})`
    - `db.getCollection('dailyPrice').find({“$or/and”:[ {'stockId':'2330'}, {'stockId':'0050'}]})`
  - distinct:
    - `db.getCollection('dailyPrice').distinct('timestamp')`: 列出所有unique的日期，意即此Documentation中的資料時間區間。
  - [ref.](https://ithelp.ithome.com.tw/articles/10206323)
- 如果想在自己的電腦上拿到日價量、月營收、季財報，[點這](https://drive.google.com/file/d/1l1cGiNruHTLDdGbHiDeWDBX47KwsIURT/view)。

# 常常要做的事
多上網吸收知識，例如[幣圖誌](http://www.bituzi.com/search/label/謀權奪利真英雄-牧清華)。<br />
上[hahow](https://hahow.in/courses/5a2170d5a6d4a5001ec3148d/main?curriculum=5b1308cb865ad2001ec28980)學怎麼用python做策略回測 。<br /> account: wplo
<br /> password: nafsoh-cegreD-3nivpi

# Server things
1. Log in <br />
  ssh wenping@140.112.104.141 <br />
  password: bobbyteeseanwp9 <br />
2. jupyter notebook <br />
  a. [Remote] jupyter notebook --no-browser --port=<specific_port> <br />
  b. [Local] ssh -N -f -L localhost:<specific_port>:localhost:<specific_port> wenping@140.112.104.141 <br />
  c. goto browser with the URL the remote provides. <br />

  <specific_port> for everyone:
  Bobby : 8886
  Lin   : 8887
  Tee   : 8889
  Sean  : 8890
  WP    : 8891
  (it's ok to use other ports, you can check by `lsof -ti:XXXX` to see the availability.)

  note: if you got something like: bind [127.0.0.1]:8889: Address already in use in the step b, please type <br />
  lsof -ti:8889 | xargs kill -9 <br />
  to kill all the processes related. <br />

  大家都有root權限，都可以灌東西。目前建議創立自己的資料夾，然後使用pipenv來避免衝突。

3. 若是mongodb掛掉了，用 <br /> sudo mongod -f /etc/mongod.conf <br />


# About Atom editor
簡介：Atom 是一款開源編輯器，包括Sublime直覺使用的優點，加上其開源性而多元的套件。缺點為易於過度包裝導致資源不足。以下介紹一些使開發更友善的有趣技巧。[連結](https://atom.io/)
## Use atom like jupyter notebook
**我們可以使得Python的開發與除錯在同一個編輯頁面下同時進行。**
- 需求套件:[Hydrogen](https://atom.io/packages/hydrogen)
- 安裝後若程式碼執行時無反應，請參考[點我](https://github.com/nteract/hydrogen/issues/1538)

**使其使用遠端的Kernel來做運算（使用遠端資源）**
- "Cmd+," 進入設定，找到Hydrogen，進入Hydrogen設定。
- 在Remote gateway欄位中打入，例如：

`[{"name": "wenping",`
`"options": {`
`"baseUrl": "http://localhost:8891",`
`"token":"4d9a28a99f779c0d09b6331525c96b9f2f96934b9a8c0855"}}]`
其為在遠端已建立的jupyter notebook port 和 token.
(記得ssh -N -f -L localhost:<specific_port>:localhost:<specific_port> wenping@140.112.104.141)
- 在欲使用遠端資源的程式碼頁面中按下Cmd+Shift+P，搜尋Connect Remote Kernel，選擇wenping，選擇new_session，就可以使用遠端資源做運算了。

**搭配[remote-ftp](https://atom.io/packages/remote-ftp)在本機端管理遠端專案。可以在資料夾目錄中直接瀏覽，編輯和同步（於本地端創立相對的資料夾階層）遠端項目，完整實現遠端編譯器即時編碼與除錯的功能。**
- remote-ftp 依隨Atom本質，以專案(Project)為單位。先於本地端建立Project folder。
  - Add project folder -> 新建資料夾(e.g. remoteWenping_home)
- Cmd+Shift+P, 搜尋Remote Ftp: Toggle, 並在Remote標籤下選擇Edit Configuration，例如：
`{
  "protocol": "sftp",
  "host": "140.112.104.141",
  "port": 22,
  "user": "wenping",
  "pass": "bobbyteeseanwp9",
  "remote": "/home/wenping/"
}`
- 編輯完成後選擇Connect即可瀏覽在ftpConfig中"remote"值中路徑的內容。此路徑即為同步某一檔案或資料夾時，在本地專案檔案夾中創造資料夾結構的根目錄。
- 任意編輯一py檔，依照上述方式選擇Remote Kernel。

至此應可於Atom中更改、除錯並儲存遠端的python程式碼，也能一覽無遺遠端專案中的資料和資料夾。

# About the GitHub
