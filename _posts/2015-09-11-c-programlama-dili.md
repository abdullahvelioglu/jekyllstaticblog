---
layout: post
title:  C PROGRAMLAMA DILI
tags: [programminglanguage]
---



İlk olarak Dennis Ritchie tarafından 1969 yılında Bell laboratuvarında Unix üzerinde çalışan bir bilgisayar
üzerinde geliştirilen C,programcılık dünyasında bir devrim niteliğinde ortaya çıkmıştır.Bu devrimin temel
sebebi dilin bir programci dili olmasıdır.Ayrıca dilin genel kapsamda daha karmaşık programlar yazılmasına da
imkan vermesidir.
<br/><br/>
Fortran,Cobol ve Assembly gibi diller sadece belirli bir alanda program geliştirmeye izin verirken,C&#39;nin
en genel düzeyde bir programlama dili olmasıda bu dile olan öğrenme arzusunu da geliştirmiştir.Her ne kadar
Pascal dili mevcut olsa da,kod satırları uzayan bir program için C&#39;nin güçlü avantajı yadsınamaz düzeye
gelmiştir.
<br/><br/>
C programlama dili prosedürel(proses yönelimli) bir dildir.Yani program parçacıkları belirli bir ayrıştırma ile
bütün bir programın yapısal ve mantıksal temelini oluşturmaktadır.Bu yazıda her C programında kullanılan temel yapı
incelenecektir.
<pre>
1 <b>int</b> main()
2 {
3 <span style="color:green;">// TODO...</span>
4 <b>return</b> 0;
5 }
</pre>
Yukarıdaki 5 satırdan oluşan program her C programında bulunan bir yapıdır.Her C programı bir <b>main</b>
fonksiyonu ile başlar ve fonksiyonun bitiş bloğu ile sona erer.C programlama dilinde programcı tarafından
// ve /*...*/ olmak uzere 2 farklı yorum(comment) stili bulunmaktadır.Bunlar C derleyicisi tarafından dikkate
alınmayıp sadece programı yazan kişiye programda anlamını unuttuğu bir takım yerleri hatırlatma görevi üstlenen
yardımcılardır.
<br/><br/>
return 0 ifadesi ise işletim sistemine bu programin bulunduğu belleğe 0 degeri dönüldüğü belirtilir.Buradaki
0 değerinin bir anlamı yoktur.234124 gibi rastgele bir değer de derleyici tarafından kabul edilecektir.Ancak
geleneksel olarak 0(false) ve 1(true) değerleri bir programı sona erdirmek için kullanılmaktadır.
<pre>
1 <span style="color:green;">// Standart I/O kütüphanesi (printf icin)</span>
2<span style="color:green;">#include &#60;stdio.h></span>

4 <b>int</b> main()
5 {
6  /*
7  <span style="color:green;">Ekranda Hello world görüntülemek için</span>
8  */
9 printf(<span style="color:red;">"Hello world"</span>);
10 <b>return</b> 0;
11 }
</pre>
Yukarıdaki programda da,konsol ekranında &#39;Hello world&#39; ibaresi görüntülenmektedir.printf() fonksiyonu
stdio.h kütüphanesinde yer alan konsol ekranına aldığı parametreyi aktaran formatlama özelliğine sahip bir
fonksiyondur.
