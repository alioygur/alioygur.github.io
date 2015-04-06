---
layout: post
title: MySQL komut satiri ipuclari 
categories:
- mysql
- terminal
---

Bunun komut satiri ile bir alakasi yok ama bilmek isteyeceginizden eminim. [Michael Widenius](http://en.wikipedia.org/wiki/Michael_Widenius) MySQL e kizinin adini vermistir. Kizinin adi My dir. Hatta MySQL i oracle a sattiktan sonra MySQL i catallayip [MariaDB](https://mariadb.org/) adi altinda gelistirmeye devam etmektedir. Tahmin edersinizki Maria da 2. kizinin adidir. :)

___

Simdi Terminali acip mysql yazarak MySQL komut satirina duselim

    ali@ali-office:~/dev/ar-ge$ mysql
    Welcome to the MySQL monitor.  Commands end with ; or \g.
    Your MySQL connection id is 39
    Server version: 5.5.29-0ubuntu0.12.10.1 (Ubuntu)
    
    Copyright (c) 2000, 2012, Oracle and/or its affiliates. All rights reserved.
    
    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.
    
    Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
    
    mysql> 
    
Komut satirina \h (help) yazip cikan listeden isimize yariyacak olan bazi ozellikleri inceleyelim

    mysql> \h
    
    For information about MySQL products and services, visit:
       http://www.mysql.com/
    For developer information, including the MySQL Reference Manual, visit:
       http://dev.mysql.com/
    To buy MySQL Enterprise support, training, or other products, visit:
       https://shop.mysql.com/
    
    List of all MySQL commands:
    Note that all text commands must be first on line and end with ';'
    ?         (\?) Synonym for `help'.
    clear     (\c) Clear the current input statement.
    connect   (\r) Reconnect to the server. Optional arguments are db and host.
    delimiter (\d) Set statement delimiter.
    edit      (\e) Edit command with $EDITOR.
    ego       (\G) Send command to mysql server, display result vertically.
    exit      (\q) Exit mysql. Same as quit.
    go        (\g) Send command to mysql server.
    help      (\h) Display this help.
    nopager   (\n) Disable pager, print to stdout.
    notee     (\t) Don't write into outfile.
    pager     (\P) Set PAGER [to_pager]. Print the query results via PAGER.
    print     (\p) Print current command.
    prompt    (\R) Change your mysql prompt.
    quit      (\q) Quit mysql.
    rehash    (\#) Rebuild completion hash.
    source    (\.) Execute an SQL script file. Takes a file name as an argument.
    status    (\s) Get status information from the server.
    system    (\!) Execute a system shell command.
    tee       (\T) Set outfile [to_outfile]. Append everything into given outfile.
    use       (\u) Use another database. Takes database name as argument.
    charset   (\C) Switch to another charset. Might be needed for processing binlog with multi-byte charsets.
    warnings  (\W) Show warnings after every statement.
    nowarning (\w) Don't show warnings after every statement.
    
    For server side help, type 'help contents'
    
**edit      (\e) Edit command with $EDITOR.**  
Bu mysql konsolda uzun sql cumleleri yazarken isinize yarayabilir.  
**\e** yazip enterladiginizda terminalizinizin varsayilan editoru acilir vim veya nano gibi, siz burda sql cumlelerinizi yazip kaydet kapat dedikten sonra tekrar mysql konsola dusersiniz ve orada yazdiklariniz mysql tarafindan hafizaya alinir. Ardindan **\g** yazip enterladiktan sonra hafizadaki bu kod calistirilir. Sayet bundan vazgecerseniz **\c** ile mevcut hafizayi bosaltabilirsiniz.

**exit      (\q) Exit mysql. Same as quit.**  
Konsoldan cikar

**help      (\h) Display this help.**  
Mysql ile calisirken suphesiz en siki dostunuz bu olacaktir. Bence muhtesem. Hadi komut satirinda bir veritabani nasil olusturuluyormus ona bakalim

Komut satirina 'help create' yazalim. Mysql bize create ile alakali konu basliklarini listeleyecektir.

    mysql> help create
    Many help items for your request exist.
    To make a more specific request, please type 'help <item>',
    where <item> is one of the following
    topics:
       CREATE DATABASE
       CREATE EVENT
       CREATE FUNCTION
       CREATE FUNCTION UDF
       CREATE INDEX
       CREATE PROCEDURE
       CREATE SERVER
       CREATE TABLE
       CREATE TABLESPACE
       CREATE TRIGGER
       CREATE USER
       CREATE VIEW
       SHOW
       SHOW CREATE DATABASE
       SHOW CREATE EVENT
       SHOW CREATE FUNCTION
       SHOW CREATE PROCEDURE
       SHOW CREATE TABLE
       SPATIAL

Ihtiyacimiz olan basligi listede gorduk 'CREATE DATABASE', Simdide 'help CREATE DATABASE' yazarak bir tablo nasil olusturuluyormus onu gorelim.

    mysql> help CREATE DATABASE
    Name: 'CREATE DATABASE'
    Description:
    Syntax:
    CREATE {DATABASE | SCHEMA} [IF NOT EXISTS] db_name
        [create_specification] ...
    
    create_specification:
        [DEFAULT] CHARACTER SET [=] charset_name
      | [DEFAULT] COLLATE [=] collation_name
    
    CREATE DATABASE creates a database with the given name. To use this
    statement, you need the CREATE privilege for the database. CREATE
    SCHEMA is a synonym for CREATE DATABASE.
    
    URL: http://dev.mysql.com/doc/refman/5.5/en/create-database.html
    
Super! Demekki bir veritabani yukaridaki gibi olusturuluyormus.

*Ufak bir hatirlatma yapim genelde man sayfalarinda {} icerisindekilerin belirtilmesi zorunlu [] icerisindekilerde opsiyoneldir*

**status    (\s) Get status information from the server.**  
Bu komut bize mevcut durum hakkinda bilgi verir. DB, CHARSET vs.

**system    (\!) Execute a system shell command.**  
Bu komut mysql konsoldayken sistem tarafinda komut calistirmamizi saglar.  
Hadi bir ls cekelim.

    mysql> \! ls
    ali.php  composer.json    composer.lock  index.php  vendor
    
**use       (\u) Use another database. Takes database name as argument.**  
farkli bir veritabani secer. Ornegin A DB indesiniz B ye gecmek istediginizde kullanabilirsiniz.

**charset   (\C) Switch to another charset. Might be needed for processing binlog with multi-byte charsets.**  
Konsol karekter setini degistirir. Tablonuzdan kayit cekerken turkce karekterleri hatali gorebilirsiniz bu istemci ile db arasindaki karekter seti farkliligindan kaynaklaniyordur muhtemelen. Asagidaki kodu calistirin muhtemelen duzelecektir.

    mysql> charset utf8
    Charset changed