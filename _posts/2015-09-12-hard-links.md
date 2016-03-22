---
layout: post
title: HARD LINKS
tags: [linux]
---


<p>
Hard links, Unix ve Windows gibi sistemlerde bir dosyaya bir den fazla isim ataması yaparak, orjinal dosyalara kopya referans olan sabit bağlantılar olarak adlandırılır. Unix sistemlerde varsayılan olarak, her dosya kendi ismi ile en az 1 adet hard linke sahiptir. Bir hard link, orjinal dosyanın bir kopyasıdır ve içeriği değiştirildiği zaman, orjinal dosya da otomatik olarak değişir. Bunun anlamı, işletim sistemi üzerinde tek bir link üzerinden değişiklik yaparak, bağlantılı olan tüm komponentlerin kullandıkları veriler içinde bu değişikliği yansıtmaktır. Örneğin A dosyasına işaret eden bir hard linkin içeriğindeki değişiklik, orjinal A dosyasının içeriğine de yansır. Hard linkler silindiği zaman, orjinal dosya silinmez, yalnızca hard linkin kendisi silinir.
</p>
<p>Hard link&#39; lerin iki adet kısıtlaması bulunmaktadır. </p>
<p>
1. Bir hard link, kendi dosya sistemi dışında bulunan bir dosyaya bağlantı oluşturamaz.<br/>
2. Bir hard link, dizinlere(directory) bağlantı oluşturamaz.
</p>
<p>
Hard linkler genellikle yedek alma(backup) işlemlerinde kullanılmaktadır. Dosya kopyaları oluşturması ve eski bir metodoloji olduklarından kullanım alanları <a href="http://www.abdullahvelioglu.com/blog/2015/09/13/symbolic-links/" target="_blank">Sembolik Linkler(Symbolic Links)</a> kadar yaygın değildir.
</p>
<h3>ln Komutu</h3>
<p>
Unix işletim sisteminde <b>ln <i>file_name</i> <i>link_name</i></b> ifadesi bir hard link yaratır.
