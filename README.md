# files contents
finlab_course包含了[hahow](https://hahow.in/courses/5a2170d5a6d4a5001ec3148d/main?curriculum=5b1308cb865ad2001ec28980)這門課的一些課程檔案以及modules. 

# 開發流程
1. Pull from the origin master to local
2. "git checkout -b <new_branch_name_for_what_developing>" in local
3. "git push origin <new_branch_name_for_what_developing>" to remote after developing with brief messages in each commit during developement.
4. Create a pull request to remote with a detail message.
5. Let's code reviewing and decide whether to merge to the master branch.

# 友善連結
1. [關於目前要撈的資料的google sheet](https://docs.google.com/spreadsheets/d/13VaADmny6l8arsr5Wrymb-oMN_bLd7Oaeckz_BxylZ0/edit#gid=0)<br />
2. [關於投資策略方向的討論](https://docs.google.com/document/d/1Sim1e0Tl2re86skXnin1j372fLNWsAgD9XzFi9KAu0Q/edit?ts=5c4ef112)<br />
3. [程式交易討論區](http://www.coco-in.net/forum-17-1.html): 如果沒有什麼靈感，可以來這邊挖寶<br />
4. [爬蟲教程](https://piaosanlang.gitbooks.io/spiders/01day/README1.html)


# 要先做的事
請大家安裝[database browser](https://sqlitebrowser.org)以便直接透過軟體看sql database裡面的table。 <br />
如果想在自己的電腦上拿到日價量、月營收、季財報，[點這](https://drive.google.com/file/d/1l1cGiNruHTLDdGbHiDeWDBX47KwsIURT/view)。

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

  note: if you got something like: bind [127.0.0.1]:8889: Address already in use in the step b, please type <br />
  lsof -ti:8889 | xargs kill -9 <br />
  to kill all the processes related. <br />
  
  大家都有root權限，都可以灌東西。目前建議創立自己的資料夾，然後使用pipenv來避免衝突。
  
3. 若是mongodb掛掉了，用 <br /> sudo mongod -f /etc/mongod.conf <br />
