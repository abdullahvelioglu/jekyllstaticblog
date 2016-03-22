---
layout: post
title: SYMBOLIC LINKS
tags: [linux]
---


<p>
Symbolic links, Unix ve Windows gibi sistemlerde orjinal dosyalara referans olan sembolik bağlantılar olarak adlandırılır. Bir symbolic link kopya dosya olmayıp yalnızca orjinal dosyaya işaret eden bir bağlantıdır. Sembolik bağlantıların içeriği değiştirildiği zaman, orjinal dosyalar da otomatik olarak değişir. Symbolic link&#39; ler yapı itibari ile Windows&#39; da ki kısayollara(shortcut) benzetilir. Aynı hard link&#39; ler de olduğu gibi işletim sistemi üzerinde tek bir link üzerinden değişiklik yaparak, bağlantılı olan tüm komponentlerin kullandıkları veriler içinde bu değişikliği yansıtmaktır.
</p>
<p>
Örnek olarak sistem üzerinde 7 versiyona sahip JRE olduğunu düşünelim. Bu JRE&#39; nin Linux üzerinde /usr/java/jre1.7.0/bin/java dosya yolu altında kayıtlı olduğunu varsayalım. Sistem de bu versiyonu kullanan java programları her defasında bu path&#39; e erişerek Javayı kullanır. Ancak güncelleme işlemi olarak, JRE 8 yüklediğimiz durumda, bu path&#39; e erişen her java programı çağrısı da update edilmek zorunda kalacaktır. Bu durumda bir symbolic link tanımlayarak mevcut java çağrıları tek bir yerden sağlanabilir. Ayrıca güncelleme oldukça mevcut linkleri yeni versiyonlar ile güncelleyebiliriz. Örnek yazının sonunda verilmiştir.
</p>
<p>
Sembolik bağlantılar(symbolic links), aşağıda açıklanan <a href="http://www.abdullahvelioglu.com/blog/2015/09/12/hard-links/" target="_blank">Sabit Bağlantıların(Hard Links)</a> kısıtlı iki özelliğini ortadan kaldırmak için tanımlanmıştır.
</p>
<p>Daha öncede açıklandığı gibi, hard link&#39; lerin iki adet kısıtlaması bulunmaktadır. </p>
<p>
1. Bir hard link, kendi dosya sistemi dışında bulunan bir dosyaya bağlantı oluşturamaz.<br/>
2. Bir hard link, dizinlere(directory) bağlantı oluşturamaz.
</p>
<p>
Bir sembolik link silindiği zaman, dosyanın kendisi silinmez, yalnızca işaretçisi kaldırılır. Eğer orjinal dosya silinirse, sembolik link işaretçisinin linki kırılır(broker) ve iş göremez duruma gelir. Bu kırık linkler <i>ls</i> komutlarında kırmızı olarak boyanır.
</p>
<h3>ln Komutu</h3>
<p>
Unix işletim sisteminde <b>ln -s <i>item</i> <i>link_name</i></b> ifadesi bir hard link yaratır.
<pre>
item: file or directory
</pre>
<pre>
/usr/java/jre1.7.0/bin/java
/usr/java/jre1.8.0/bin/java

ln -s /usr/java/jre1.8.0/bin/java java_symlink

java_symlink -> /usr/java/jre1.8.0/bin/java

> java_symlink program1
> java_symlink program2
