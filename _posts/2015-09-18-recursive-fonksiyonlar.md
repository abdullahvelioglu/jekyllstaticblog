---
layout: post
title: YINELEYEN (RECURSIVE) FONKSIYONLAR
tags: [algorithm]
---







<p>Sık sık duyarız, <strong>recursive (yineleyen) fonksiyon</strong> terimini. "Şunu yazmam gerek, nasıl yazarım?" sorusuna sıklıkla "recursive fonksiyon kullan" yanıtını alırız... Nedir bu&nbsp;recursive fonksiyon? Her haltı bununla mı yazacağız?</p>
<p>&nbsp;</p>
<p>Hayır elbette... Aslında recursive fonksiyonları m&uuml;mk&uuml;n olduğunca az kullanmak belki de en iyisi ama bazı işlevleri başka&nbsp;t&uuml;rl&uuml; yazmak m&uuml;mk&uuml;n olmayabiliyor. İşte yalnızca b&ouml;yle durumlarda ve b&uuml;y&uuml;k dikkatle kullanmamız gerekir recursive fonksiyonları. Tehlikelidir, daha n'oluyoruz demeden bilgisayarı&nbsp;kilitleyiverirsiniz...</p>
<p>&nbsp;</p>
<h3>Recursion</h3>
<p>Recursive fonksiyon tanımı, k&ouml;kenini "<strong>recursion</strong>" kelimesinden alır. Recursion kelimesinin T&uuml;rk&ccedil;e anlamı "<strong>&ouml;zyineleme</strong>" dir.&nbsp;Google'da bir aratın:</p>
<p><img style="float: none; max-width: 100%; display: block; margin-left: auto; margin-right: auto;" src="http://www.abdullahvelioglu.com/blog/public/images/recursion.png" alt="Recursion" /></p>
<p>Sanırım bir fikir vermiştir. Evet, recursive fonksiyon demek kendine referans veren fonksiyon demektir.</p>
<p>&nbsp;</p>
<h2>Recursive Fonksiyon t&uuml;rleri</h2>
<p>Temelde iki &ccedil;eşit recursive fonksiyon vardır: Direkt ve endirekt recursive fonksiyonlar...</p>
<p>&nbsp;</p>
<h3>Direkt&nbsp;&Ouml;zyineleme</h3>
<p>Eğer bir fonksiyon, direkt olarak kendine referans veriyorsa buna "<strong>direkt recursive fonksiyon</strong>" diyoruz.</p>
<pre class="brush: js">function direkt() {
  document.body.innerHTML = (document.body.innerHTML + '&lt;br&gt;Direkt');
  direkt();
  return;
}
</pre>
<p>Hayırlı olsun, kullanıcının makinasını sonsuz d&ouml;ng&uuml;ye sokarak kilitledik... Aman, recursive fonksiyon yazarken kontrol parametreleri kullanarak sonsuz d&ouml;ng&uuml;y&uuml; engellemeye &ouml;zen g&ouml;sterelim. &Ccedil;ok k&uuml;f&uuml;r yeriz...</p>
<p>&nbsp;</p>
<h3>Endirekt&nbsp;&Ouml;zyineleme</h3>
<p>Eğer bir fonksiyonun referans verdiği fonksiyon ya da onun referans verdiği bir diğer fonksiyon (bu zincir uzar gider) ilk fonksiyona tekrar referans veriyorsa buna "<strong>endirekt recursive fonksiyon</strong>" diyoruz.</p>
<pre class="brush: js">function fonkA(gelen) {
  if(!gelen) gelen = 1;
  document.body.innerHTML = (document.body.innerHTML + '&lt;br&gt;' + gelen);
  fonkB(gelen);
  return;
}

function fonkB(gelen) {
  gelen++;
  if(gelen &lt;= 10) fonkA(gelen);
  return;
}
</pre>
<p>İstediğimiz sayıdan 10'a kadar alt alta yazan bir fonksiyon grubu yazdık. Hem bu defa kullanıcının bilgisayarını da kilitlemedik.</p>
<p>&nbsp;</p>
<h2>Hangi durumlarda recursion kullanmalıyız?</h2>
<p>Recursive fonksiyonlarla ilgili &ouml;rnekleme yapmak gerektiğinde herkesin aklına ilk olarak (nedense) faktoriyel hesabı geliyor. Yine bir JavaScript kodu ile inceleyelim:</p>
<pre class="brush: js">function faktoriyel(gelen, sonuc) {
  if(!gelen) gelen = 1;
  if(!sonuc) sonuc = 1;

  if(gelen &gt; 1) {
    sonuc *= gelen;
	gelen--;
	return faktoriyel(gelen, sonuc);
  }

  return sonuc;
}

document.body.innerHTML = (document.body.innerHTML + '&lt;br&gt;Sonuc: ' + faktoriyel(5));
</pre>
<p>İstediğimiz (&ouml;rneğimizde 5) sayının faktoriyelini&nbsp;hesaplayan bir recursive fonksiyon yazdık. Peki anlamlı bir iş mi yaptık?</p>
<p>&nbsp;</p>
<pre class="brush: js">function faktoriyel(gelen) {
  if(!gelen) gelen = 1;
  var sonuc = 1;

  for(var i = 1; i &lt;= gelen; i++) sonuc *= i;

  return sonuc;
}

document.body.innerHTML = (document.body.innerHTML + '&lt;br&gt;Sonuc: ' + faktoriyel(5));
</pre>
<p>&Ccedil;ok daha basit, değil mi?</p>
<p>&nbsp;</p>
<p>İşte bu nedenle, recursive fonksiyonlara faktoriyel hesaplama &ouml;rneğini "<strong>aman b&ouml;yle sa&ccedil;ma işler yapmayın, bir işi d&ouml;ng&uuml; kurarak yaptırabiliyorsanız recursive yazmayın</strong>" alt başlığı ile vermeyi tercih ederim. Peki ne zaman kullanacağız bu recursive fonksiyonları?</p>
<p>&nbsp;</p>
<p>Basit, işi d&ouml;ng&uuml;&nbsp;kurarak&nbsp;kıvıramıyorsak&nbsp;recursive yazacağız...</p>
<p>&nbsp;</p>
<p>Evet b&ouml;yle durumlar ortaya &ccedil;ıkabiliyor. PHP ile b&ouml;yle bir &ouml;rnek oluşturalım.</p>
<p>&nbsp;</p>
<h2>&Ouml;rnek</h2>
<p>Sık&ccedil;a karşılaşabileceğimiz bir&nbsp;senaryo d&uuml;ş&uuml;nelim: Bir veri tabanımız olsun. Bu veri tabanında kategorilerimizi tutuyor olalım. Tablomuz "<strong>id</strong>", "(&uuml;st)<strong> kategori id</strong>" ve "<strong>kategori adı</strong>" kolonlarını i&ccedil;ersin. Kullanıcıya bu kategori listesini tree-view sistemi ile sunmak istiyoruz. Ne yapacağız? Bunu basit bir d&ouml;ng&uuml; ile kurgulamak maalesef m&uuml;mk&uuml;n değil. Hangi kategorinin ka&ccedil; alt kategorisi var bilmiyoruz, alt kategorilerin ka&ccedil; tanesinin ka&ccedil;ar tane alt kategorisi var bilmiyoruz. İşte bu senaryo <strong>recursive fonksiyonu</strong> gerekli kılıyor...</p>
<p>&nbsp;</p>
<h3>Tablo&nbsp;yapısı</h3>
<p>Tablomuzun ismi kategoriler olsun. İşlevi ise web sitemizin &ccedil;ok seviyeli men&uuml;s&uuml;n&uuml; tutmak olsun... Veri tabanı &ouml;rneğini <a href="http://www.abdullahvelioglu.com/blog/public/recursive.rar">buradan</a>&nbsp;indirebilirsiniz.</p>
<p>&nbsp;</p>
<h3>Fonksiyon</h3>
<pre class="brush: php ; html-script: true">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;meta charset="utf-8" /&gt;
    &lt;title&gt;Yineleyen (recursive) fonksiyonlar&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;?php
      kategoriYaz();
    ?&gt;
  &lt;/body&gt;
&lt;/html&gt;
&lt;?php
  function kategoriYaz($kid) {
    /* $kid hangi kategorinin &ccedil;ocuk kategorilerini
    ** listeleyeceğimizi belirlemek i&ccedil;in gerekli.
    ** Eğer bir değer belirtilmemişse babası olmayan
    ** (en &uuml;st d&uuml;zey) kategorileri listeleyeceğiz. */

    $db = new mysqli('sunucu', 'kullanici', 'sifre', 'vt_adi');

    $rs = $db-&gt;query("
      SELECT *
      FROM kategori
      WHERE ".($kid ? "kid = ".$kid : "ISNULL(kid)")."
      ORDER BY id
    ");

    if($rs-&gt;num_rows) {
      echo '&lt;ul&gt;';
      while($row = $rs-&gt;fetch_assoc()) {
        echo '&lt;li&gt;'.$row['isim'];
        kategoriYaz($row['id']); // Burası sayesinde
                                 // fonksiyon recursive
        echo '&lt;/li&gt;';
      }
      echo '&lt;/ul&gt;';
    }
  }
?&gt;</pre>
<p><strong>Sonu&ccedil;:</strong></p>
<ul>
<li>Ana Sayfa</li>
<li>&Uuml;r&uuml;nler
<ul>
<li>Bilgisayar
<ul>
<li>Asus
<ul>
<li>Desktop</li>
<li>Laptop</li>
</ul>
</li>
<li>Casper</li>
<li>HP</li>
</ul>
</li>
<li>Tablet
<ul>
<li>Apple
<ul>
<li>7 Inch</li>
<li>10 Inch</li>
</ul>
</li>
<li>Samsung
<ul>
<li>7 Inch</li>
<li>10 Inch</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
<li>Hizmetler
<ul>
<li>Telefon Destek</li>
<li>Tamir, Bakım</li>
<li>Yazılım Geliştirme</li>
</ul>
</li>
<li>İletişim</li>
</ul>
<p>&nbsp;</p>
