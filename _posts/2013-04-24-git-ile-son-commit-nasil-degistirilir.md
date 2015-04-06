---
layout: post
title: Git ile son commit nasil degistirilir
---

Git surum kontrol sisteminin muhtesem ozellikleri vardir bunlardan biri de "amend" dir.

**Nedir & Ne ise yarar?**

Ornegin bir web projesi uzerinde calisiyorsunuz ve login ile alakali bir hatayi fark ettiniz ve aninda duzeltip. Commit ettiniz.

    git add login.php
    git commit -m 'login problemi duzeltildi'
    
Aa oda ne login problemi aslinda tam olarak duzelmemis birseyi unutmusuz. Him simdi ne olacak 2. bir commit ve mesajada "login problemi duzeltildi 2" gibi bir mesajmi yazacaktiniz. **amend** in farkinda olmasaydik muhtemelen aynen boyle olacakti. 

Neyseki amend var ve biz duzenlememizi yaptiktan sonra son commitimizi degistirecegiz.

    git add login.php
    git commit --amend -m 'login problemi duzeltildi'
    
Boylelikle loglarda yanlizca 1 commit yer alacak.

    git log --stat
    