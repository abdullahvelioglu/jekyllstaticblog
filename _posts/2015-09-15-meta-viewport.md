---
layout: post
title: META VIEWPORT
tags: [web]
---



<p>Responsive&nbsp;bir site yazacaksak işe direkt&nbsp;<strong><em>&lt;meta name="viewport" content="width=device-width, initial-scale=1" /&gt;</em>&nbsp;</strong>yazarak başlarız. İşe başlangıç gibi bir şey yani. Peki neden? Ne iş yapar bu viewport?</p>
<h2>Nedir bu pixel (piksel) dedikleri?</h2>
<p>Biraz kafa karıştırarak başlayalım. Aslında&nbsp;tek &ccedil;eşit pixel yoktur. Nasıl mı? CSS pixeli ve cihaz pixeli farklı değerlerdir. &Ccedil;ok da korkulacak bir konu değil. İkisini de tanıyoruz aslında... Biraz a&ccedil;alım:</p>
<h3>CSS'de pixel:</h3>
<p>CSS pixeli, deklerasyonumuzu yaparken (CSS dosyasında ya da style &ouml;zelliğinde) belirttiğimiz değerdir. Mesela, "width: 240px;" ya da "height: 180px;" gibi...</p>
<p>Bunlar soyut değerlerdir. &Ouml;rneğin kullanıcı zoom yaptığında bunların boyutları&nbsp;değişir.</p>
<h3>Cihaz'da pixel:</h3>
<p>Cihaz pixeli, kullanmakta olduğunuz cihazın ekranındaki pixel sayısıdır. Fiziksel bir değerdir. Cihazınızın ekranına bağlı olarak kesin ve değişmez bir miktardadır.</p>
<p>Farklı cihazlarda farklı pixel değerleri ile &ccedil;alışmak durumundayız.</p>
<h3>Peki ne yapacağız?</h3>
<p>Yeterince kafa karışıklığı yarattıysam sadede geleyim. Her zaman CSS pixel'i ile &ccedil;alışacağız.</p>
<h2>Viewport</h2>
<p>Viewport (g&ouml;r&uuml;nt&uuml;leme alanı) cihazımızdaki g&ouml;r&uuml;nt&uuml;leme alanı olarak tanımlanabilir. &lt;html&gt; elementinin genişliği viewporta g&ouml;re hesaplanır. Masa&uuml;st&uuml; bilgisayarlarda bu, tarayıcının genişliğine eşittir.</p>
<p><span style="line-height: 1.6;">Eğer zoom yaparsanız, CSS pixellerini genişletmiş olursunuz. Bu durum ekranınıza daha az pixelin sığması anlamına gelecektir. Başka bir deyişle, viewportunuz k&uuml;&ccedil;&uuml;l&uuml;r.</span></p>
<p>Mobil cihazlarda ise işler biraz daha karışık y&uuml;r&uuml;mek durumundadır.</p>
<p>Mobil tarayıcılar her siteyi, site mobil i&ccedil;in optimize edilmiş&nbsp;olmasa dahi doğru yorumlamalıdır. &Ouml;rneğin mobil cihaz dikey olduğunda (viewportunuz dar ise)&nbsp;bir&ccedil;ok site okunamaz derecede sıkıştırılır.</p>
<p>Bu nedenlerle mobil tarayıcı &uuml;reticileri, kuralları değiştirdiler.</p>
<p>Genellikle viewport (tarayıcıya bağlı olarak) 768 - 1024px genişliğindedir. En genel kullanım 980px'tir. Buna layout &nbsp;(bu terimin T&uuml;rk&ccedil;esini bir t&uuml;rl&uuml; bulamadım, belki "d&uuml;zenlenebilir - kullanılabilir" şeklinde &ccedil;evirebiliriz?) viewport denir.</p>
<p>Responsive (esnek) tasarım, layout viewportu cihazın genişliğine g&ouml;re d&uuml;zenlemekten ibarettir.</p>
<p>Ancak aşikardır ki bu değerler mobil cihazların ekranlarının g&ouml;r&uuml;nt&uuml;leme alanından b&uuml;y&uuml;kt&uuml;r. Bu nedenle g&ouml;r&uuml;nt&uuml;lenebilir alanı tanımlayabilecek ayrı bir viewporta da ihtiyacımız var. Bu viewporta <em>visual viewport</em> diyoruz.</p>
<p>Sonu&ccedil; olarak, masa&uuml;st&uuml; viewportunu mobil cihaza terc&uuml;me ettiğimizde iki par&ccedil;ada inceleyebiliyoruz:</p>
<ul>
<li>Layout viewport,</li>
<li>Visual viewport</li>
</ul>
<p>Ama aslında mobil cihazlarda, masa&uuml;st&uuml; bilgisayarlarda bir karşılığı olmayan bir viewport ile &ccedil;alışmalıyız:</p>
<ul>
<li>Ideal viewport</li>
</ul>
<h2>Ideal viewport</h2>
<p>Mobil cihazlarda&nbsp;sitemizi g&ouml;r&uuml;nt&uuml;lemek i&ccedil;in en uygun viewport genişliğini se&ccedil;mek isteriz. &Ouml;yle ki, ziyaret&ccedil;iler metinleri rahat&ccedil;a okuyabilsin, zoom yapmaya gerek kalmasın.</p>
<p>Ideal viewport boyutu cihazdan cihaza değişkenlik g&ouml;sterir.</p>
<h2>Meta Viewport</h2>
<p>Responsive bir tasarım oluşturabilmek i&ccedil;in layout viewportumuzun boyutlarını ideal viewporta eşitlemeliyiz. Bunun i&ccedil;in:</p>
<pre class="brush: xml">&lt;meta name="viewport" content="width=device-width" /&gt;</pre>
<p>Meta viewport etiketi layout viewportunuzun genişliğini istediğiniz boyuta ayarlayabilmenizi sağlar. Genişliği pixel cinsinden verebileceğiniz gibi (width=360px) "device-width" anahtar kelimesini kullanarak ideal viewport boyutunu da se&ccedil;ebilirsiniz.</p>
<p>ideal viewport boyutunu belirlemek i&ccedil;in&nbsp;ayrıca "initial-scale=1" değeri de kullanılabilir.</p>
<pre class="brush: xml">&lt;meta name="viewport" content="initial-scale=1" /&gt;</pre>
<p>Aslında "initial-scale" değeri başlangı&ccedil;taki zoom miktarını belirlemek i&ccedil;in kullanılır (1 = 100%).&nbsp;Elbette bu değer ideal viewporta g&ouml;re oranlama yaptığından&nbsp;<span style="line-height: 1.6;">"initial</span><span style="line-height: 1.6;">-</span><span style="line-height: 1.6;">scale=1" verildiğinde layout viewport boyutlarını da ideal viewport ile eşdeğer yapar.</span></p>
<p>Sonu&ccedil; olarak aynı işlevi g&ouml;rmek i&ccedil;in iki ayrı y&ouml;ntemimiz var. Garip. Bunların hepsi Apple'ın halt yemesi&nbsp;işte.</p>
<p><strong>İşleri biraz daha karıştıralım:</strong></p>
<pre class="brush: xml">&lt;meta name="viewport" content="width=360, initial-scale=1" /&gt;</pre>
<p>Tarayıcıya k&uuml;f&uuml;r etsek daha iyi aslında. Bir yandan viewport 360 pixel olsun diyoruz, bir yandan ideal genişlikte olsun diyoruz. B&ouml;yle durumlarda tarayıcı b&uuml;y&uuml;k olan&nbsp;değeri&nbsp;alır, diğerini ihmal eder.</p>
<p>Başka bir deyişle tarayıcıya "viewport boyutu 360px ve ideal genişlikten hangisi b&uuml;y&uuml;kse o olsun" demiş oluyoruz. Cihazın konumu (dikey - yatay) değişirse değerler yeniden hesaplanır.</p>
<p>Sonu&ccedil; olarak, aslında viewportun genişliği en az 360px olsun demiş olduk. Bir halta&nbsp;yaradı mı? Hayır...</p>
<h3>Safari'nin hatası</h3>
<p>Safari her sakallıyı dedesi zanneder. Başka bir deyişle,<strong>&nbsp;&lt;meta name="viewport" content="width=device-width" /&gt;</strong> kullanıldığında&nbsp;Safari, cihazın dikey genişliğini 320px (iphone)&nbsp;ya da&nbsp;768px (ipad) kabul eder. Bu her zaman doğru değerleri alamayacağınız anlamına gelir. Bu sebeple Safari tarayıcılarda&nbsp;<strong><span style="line-height: 1.6;">&lt;meta name="viewport" content="initial-scale=1" /&gt;&nbsp;</span></strong><span style="line-height: 1.6;">tercih etmeliyiz.</span></p>
<h3><span style="line-height: 1.6;">IE10 hatası</span></h3>
<p><span style="line-height: 1.6;">Safari'nin aksine IE10,&nbsp;</span><strong style="line-height: 1.6;"><span style="line-height: 1.6;">&lt;meta name="viewport" content="initial-scale=1" /&gt;&nbsp;</span></strong><span style="line-height: 1.6;">kullanıldığında hata yapabilmektedir. Bu nedenle IE10 tarayıcıda&nbsp;</span><strong style="line-height: 1.6;">&lt;meta name="viewport" content="width=device-width" /&gt;</strong> tercih etmeliyiz.</p>
<h3>Sonu&ccedil;:</h3>
<p>T&uuml;m tarayıcılarda doğru değerlere ulaşmak i&ccedil;in en doğru kullanım:</p>
<pre class="brush: xml">&lt;meta name="viewport" content="width=device-width, initial-scale=1" /&gt;</pre>
<p>&nbsp;</p>
<p>&nbsp;</p>
