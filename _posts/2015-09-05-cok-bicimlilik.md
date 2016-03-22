---
layout: post
title: COK BICIMCILIK(POLYMORPHISM)
tags: [programminglanguage]
---


Nesneye dayalı programlamanın felsefelerinden bir diğeri olan Çok biçimcilik,bir arabirimi referans alan bir den fazla metot felsefesini üstlenmektedir.Polymorphism Yunanca&#39;da &#39;<i>bir çok biçim </i>&#39; anlamına gelmektedir.Bu anlam da nesneye dayalı programlamanın temel prensiplerinden biri olmuştur.
<br/><br/>
Çok biçimcilik prensibi ile bir arabirim oluşturulur(interface).Daha sonra bir takım ilişkili mantıksal sınıflar kendi tasarladığı algoritmaya veya nesne tiplerine göre bu arabirimi uygular(implement eder).Buradaki amaç,aynı isim altındaki bir olayın,ilişkili bir çok sınıf tarafından farklı şekillerde uygulanma gereksiniminden ortaya çıkmaktadır.Bu gereksinimin sebebi pek tabi ki basitlik içindir.Nitekim Nesneye Dayalı Programlama sınıflar arasındaki karmaşıklığı mümkün olduğunca azaltmak için ortaya atılmıştı.<br/><br/>
Aşağıda bir sıralama arabirimini uygulayan 3 adet sıralama algoritma yapısı gösterilmektedir.
<center>
1)Kabarcık Sıralama<br>2)Ekleyerek Sıralama<br>3)Seçerek Sıralama
</center>
Yukarıya bakıldığında bir sıralama algoritmasının 3 farklı sıralama algoritmasına arabirim oluşturduğu görülmektedir.Genel bir arabirim ile tasarlanan bu sıralama arayüzü,mantıksal olarak hiyerarşiyi en iyi şekilde modelleyerek nesneye dayalı programlamayı en sade ve basit şekilde ortaya koyacaktır.<br/><br/>
Tasarlanan arabirimin UML diyagramı aşağıdaki gibi olabilir.
<center>
SIRALAMA ARABIRIMI UML DIYAGRAMI<br><div class="bundle row gutters fadeInDown animated">SIRALAMA<div class="bundle row gutters fadeInDown animated">+sort():void
</center>
UML diyagramına göre,genel arabirim içerisinde tanımlı bir sort() metodu bulunmaktadır.Tasarımda örnek olarak kullanılan;
<ul>
<li><a href="http://www.abdullahvelioglu.com/blog/2015/09/06/kabarcik-siralama/" style="color:blue;font-weight:normal;" target="_blank">Kabarcık Sıralama</a></li>
<li><a href="http://www.abdullahvelioglu.com/blog/2015/09/07/ekleyerek-siralama/" style="color:blue;font-weight:normal;" target="_blank">Ekleyerek Sıralama</a></li>
<li><a href="http://www.abdullahvelioglu.com/blog/2015/09/08/secerek-siralama/" style="color:blue;font-weight:normal;" target="_blank">Seçerek Sıralama</a></li>
</ul>
sınıfları bu sort metodunu uygulayarak kendi özel algoritmalarını uygulayacaktır.Bu sayede &#39;<span style="color:red;">bir arabirimden birden fazla metot</span>&#39; eldesi gerçekleşmiş olacaktır.<br/><br/>
