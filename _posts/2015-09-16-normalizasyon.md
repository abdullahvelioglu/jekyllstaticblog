---
layout: post
title: VERI TABANLARINDA NORMALIZASYON
tags: [database]
---






<p>İster web uygulaması&nbsp;ister masa&uuml;st&uuml; yazılım olsun hemen her bilgisayar programının&nbsp;en temel ihtiyacı veri tabanıdır kuşkusuz. Ancak ne acıdır ki yazılımcıların, &ouml;zellikle de&nbsp;web geliştiricilerinin en donanımsız olduğu alanlardan biri de budur sanırım.</p>
<p>Eğer siz de&nbsp;projeniz i&ccedil;in bir veri tabanı oluştururken, ihtiya&ccedil; duyduğunuz t&uuml;m bilgileri tek bir tabloya, tesbih tanesi gibi dizenlerdenseniz bu konu sizi &ccedil;ok ilgilendiriyor &ccedil;&uuml;nk&uuml; bakkal defteri ile veri tabanı arasındaki en temel fark normalizasyondur.</p>
<p>&nbsp;</p>
<h3>G&uuml;&ccedil;l&uuml;, hızlı ve sağlıklı bir veri tabanı oluşturmanın olmazsa olmazı normalizasyon yapmaktır.</h3>
<p>Ge&ccedil;enlerde orta &ccedil;aplı bir proje i&ccedil;in yaklaşık 125.000 satır veri tutması gereken bir veri tabanı tasarlamam gerekti. Tasarımı tamamlayıp kayıtları veri tabanına aktardıktan sonra veri tabanının performansını g&ouml;rebilmek i&ccedil;in &uuml;zerinde bazıları basit, bazıları karmaşık sorgular &ccedil;alıştırdım. G&ouml;rd&uuml;m ki bazı&nbsp;karmaşık sorgularda cevap s&uuml;resi&nbsp;6 - 7 saniyeyi bulabiliyor.</p>
<p>Bu makaleyi yazmaya karar verince aynı veri tabanını bakkal defteri formunda, yukarıda bahsettiğim gibi tesbih tanesi normunda tekrar oluşturup aynı cevap k&uuml;mesini alan sorgular&nbsp;&ccedil;alıştırdım.</p>
<p>İlk veri tabanında cevap s&uuml;resi 6sn. olan sorgunun eşdeğeri bu veri tabanında 1&nbsp;dakikadan&nbsp;uzun s&uuml;rd&uuml;... 10 katından fazla.</p>
<p>Peki bu kadar b&uuml;y&uuml;k farkı doğuran neydi?</p>
<p>&nbsp;</p>
<h2>Normalizasyon Nedir?</h2>
<p>Normalizasyonun iki temel amacı vardır. Veri tabanında veri tekrarlarını ortadan kaldırmak&nbsp;ve&nbsp;veri tutarlılığını (doğruluğunu) artırmak.</p>
<p>Normalizasyon, veri tabanlarına seviyelerle (normal formlar)&nbsp;uygulanır. Bir veri tabanının bu normal formlardan herhangi birine uygun olduğunu s&ouml;yleyebilmek i&ccedil;in, s&ouml;z konusu normal formun t&uuml;m kriterlerini eksiksiz yerine getiriyor olması şarttır.</p>
<p>Başarılı bir şekilde uygulandığında normalizasyon işlemi veri tabanının s&uuml;ratini&nbsp;b&uuml;y&uuml;k oranda artırır. Veri tabanının sabit diskteki boyutunu azaltır. Ayrıca veri tutarlılığını artırarak veri tekrarlarını engeller. Bilmem, &ouml;zellikle g&uuml;ncelleme ve silme işlemlerinde ortaya &ccedil;ıkabilecek aksaklıkları minimize ettiğini&nbsp;s&ouml;ylemeye gerek var mı?</p>
<p>&nbsp;</p>
<h3>Normal Formlar</h3>
<p>Basit&ccedil;e tanımlamak gerekirse, normal formlar&nbsp;normalizasyon seviyeleridir. Bu seviyeler&nbsp;gereksiz veri tekrarlarını ne derecede engellediği ve tutarlılığı ne kadar sağladığına bağlı olarak derecelendirilir. Seviye y&uuml;kseldik&ccedil;e veri tutarlılığı artar, veri tekrarı d&uuml;şer.</p>
<p>Normalizasyon seviyeleri 1NF (Birinci Normal Form), 2NF, 3NF, BCNF(Boyce-Codd Normal Form, 3.5NF'de denir), 4NF şeklinde adlandırılır ve yukarı doğru devam eder. Ancak daha yukarı normalizasyon seviyeleri &ccedil;ok nadiren kullanılır &ccedil;&uuml;nk&uuml;&nbsp;&ccedil;oğu zaman uygulanması m&uuml;mk&uuml;n olmayabilir.</p>
<p>Konuyu detaylandırabilmek i&ccedil;in bir veri tabanı oluşturalım ve normalizasyonunu yapalım. Tabloda bir teknik destek firmasının &ccedil;alışanları, servis&nbsp;ara&ccedil;ları, servis sof&ouml;rleri ve servis verilen semtler bulunsun.&nbsp;Her bir şof&ouml;r&nbsp;tek ara&ccedil; ile semt bazında servis yapmaktadır. &Ouml;rneğin şof&ouml;r "Ahmet", teknik elemanları&nbsp;(&ccedil;alışanları)&nbsp;"Toyota" ara&ccedil;la, "Levent", "Etiler"&nbsp;ve "Ulus"&nbsp;semtlerindeki&nbsp;destek &ccedil;ağrılarına g&ouml;t&uuml;rmektedir.</p>
<table class="table table-striped table-bordered table-hover table-condensed">
<tbody>
<tr><th style="text-align: left;">Calisan</th><th style="text-align: left;">Soyad</th><th style="text-align: left;">Sofor</th><th style="text-align: left;">Arac</th><th style="text-align: left;">Semt</th></tr>
<tr>
<td>Or&ccedil;un</td>
<td>Yılmaz</td>
<td>Ahmet</td>
<td>Toyota</td>
<td>Levent, Etiler, Ulus</td>
</tr>
<tr>
<td>Metin</td>
<td>Seyyar</td>
<td>Mehmet</td>
<td>Honda</td>
<td>Bakırk&ouml;y, Atak&ouml;y, Yeşilk&ouml;y</td>
</tr>
<tr>
<td>Metin</td>
<td>Seyyar</td>
<td>Tolga</td>
<td>Ford</td>
<td>Kandilli, Beylerbeyi,&nbsp;Kuzguncuk</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p>&Ccedil;oğu programcı i&ccedil;in veri tabanı tasarımı burada biter. Cılkını&nbsp;&ccedil;ıkartmaya&nbsp;gerek yok, değil mi? Bu arkadaşlara tavsiyem: Wordpress'ten şaşmayın, sizi o paklar...</p>
<p>İşin doğrusu, veri tabanımızı oluşturmaya hen&uuml;z başladık.</p>
<p>&nbsp;</p>
<h3>1NF (1. Normal Form)</h3>
<p>Bir veri tabanının 1NF olabilmesi i&ccedil;in aşağıdaki &ouml;zellikleri karşılayabilmesi gerekir:</p>
<ul>
<li>Aynı tablo i&ccedil;inde&nbsp;tekrarlayan kolonlar bulunamaz,</li>
<li>Her kolonda yalnızca bir değer bulunabilir (bkz.&nbsp;"Semt" kolonu)</li>
<li>Her satır bir eşsiz anahtarla tanımlanmalıdır (Unique Key - Primary Key)</li>
</ul>
<p>Veri tabanımızda ikinci kurala a&ccedil;ık&ccedil;a uymayan bir kolon var: Semt. Bu durumu d&uuml;zeltmek i&ccedil;in tekrar d&uuml;zenleyelim:</p>
<p><strong>Ana Tablo</strong></p>
<table class="table table-striped table-bordered table-hover table-condensed">
<tbody>
<tr><th style="text-align: left;">Calisan</th><th style="text-align: left;">Soyad</th><th style="text-align: left;">Sofor</th><th style="text-align: left;">Arac</th><th style="text-align: left;">Semt 1</th><th style="text-align: left;">Semt 2</th><th style="text-align: left;">Semt 3</th></tr>
<tr>
<td>Or&ccedil;un</td>
<td>Yılmaz</td>
<td>Ahmet</td>
<td>Toyota</td>
<td>Levent</td>
<td>Etiler</td>
<td>Ulus</td>
</tr>
<tr>
<td>Metin</td>
<td>Seyyar</td>
<td>Mehmet</td>
<td>Honda</td>
<td>Bakırk&ouml;y</td>
<td>Atak&ouml;y</td>
<td>Yeşilk&ouml;y</td>
</tr>
<tr>
<td>Metin</td>
<td>Seyyar</td>
<td>Tolga</td>
<td>Ford</td>
<td>Kandilli</td>
<td>Beylerbeyi</td>
<td>Kuzguncuk</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p>Bir sorun var. Tablo bu şekliyle birinci kuralla &ccedil;elişti. Semt 1, Semt 2, Semt 3 tekrarlayan kolonlar. Bir daha deneyelim:</p>
<p><strong>Ana Tablo</strong></p>
<table class="table table-striped table-bordered table-hover table-condensed">
<tbody>
<tr><th style="text-align: left;">Calisan</th><th style="text-align: left;">Soyad</th><th style="text-align: left;">Sofor</th><th style="text-align: left;">Arac</th><th style="text-align: left;">Semt</th></tr>
<tr>
<td>Or&ccedil;un</td>
<td>Yılmaz</td>
<td>Ahmet</td>
<td>Toyota</td>
<td>Levent</td>
</tr>
<tr>
<td>Or&ccedil;un</td>
<td>Yılmaz</td>
<td>Ahmet</td>
<td>Toyota</td>
<td>Etiler</td>
</tr>
<tr>
<td>Or&ccedil;un</td>
<td>Yılmaz</td>
<td>Ahmet</td>
<td>Toyota</td>
<td>Ulus</td>
</tr>
<tr>
<td>Metin</td>
<td>Seyyar</td>
<td>Mehmet</td>
<td>Honda</td>
<td>Bakırk&ouml;y</td>
</tr>
<tr>
<td>Metin</td>
<td>Seyyar</td>
<td>Mehmet</td>
<td>Honda</td>
<td>Atak&ouml;y</td>
</tr>
<tr>
<td>Metin</td>
<td>Seyyar</td>
<td>Mehmet</td>
<td>Honda</td>
<td>Yeşilk&ouml;y</td>
</tr>
<tr>
<td>Metin</td>
<td>Seyyar</td>
<td>Tolga</td>
<td>Ford</td>
<td>Kandilli</td>
</tr>
<tr>
<td>Metin</td>
<td>Seyyar</td>
<td>Tolga</td>
<td>Ford</td>
<td>Beylerbeyi</td>
</tr>
<tr>
<td>Metin</td>
<td>Seyyar</td>
<td>Tolga</td>
<td>Ford</td>
<td>Kuzguncuk</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p>Evet, şimdi oldu. Tekrar eden kolonlar yok. Bir kolonda birden &ccedil;ok veri yok. S&uuml;per. Pardon? Eşsiz anahtar mı dediniz? Doğru... E, nasıl yaparız?</p>
<p>&Ouml;nce &nbsp;"aday anahtar" (candidate key) ve "eşsiz anahtar" (primary key) kavramlarına bir g&ouml;z atalım o zaman:</p>
<p><strong>Aday Anahtar (Candidate Key):</strong>&nbsp;Bir ya da daha fazla kolondan meydana gelir.&nbsp;Tablonun her bir veri satırını eşsiz olarak tanımlar, başka bir deyişle tabloda ka&ccedil; satır olursa olsun bu kombinasyonu bulunduran birden fazla satır asla olamaz. &Ouml;rneğin, "&Ccedil;alışan - Soyad" kombinasyonu&nbsp;bir&nbsp;aday anahtar değildir &ccedil;&uuml;nk&uuml; 1, 2 ve 3&uuml;nc&uuml; satırlar ve 4, 5, 6, 7, 8 ve 9uncu satırlarda değerler tekrar etmektedir.&nbsp;&Ouml;te yandan&nbsp;"&Ccedil;alışan - Semt" kombinasyonu hi&ccedil; bir şekilde tekrar etmiyor.&nbsp;&Ouml;yleyse&nbsp;<span style="line-height: 1.6;">"&Ccedil;alışan - Semt" kombinasyonu bir <strong>aday anahtar</strong>dır.</span></p>
<p><span style="line-height: 1.6;"><strong>Eşsiz Anahtar (Primary Key):</strong>&nbsp;Tablodaki aday anahtarlardan herhangi birini eşsiz anahtar olarak atayabiliriz. Bu anahtar tablodaki satırları tanımlamak i&ccedil;in kullanılır ve bir tabloda yalnızca 1 tane eşsiz anahtar bulunabilir.</span></p>
<p><span style="line-height: 1.6;">Tablomuza d&ouml;necek olursak,&nbsp;</span><span style="line-height: 1.6;">"&Ccedil;alışan - Semt" kombinasyonunu eşsiz anahtar olarak atayabiliriz.&nbsp;Elimizdeki &ouml;rnek son derece basit bir tablo olduğundan sorun yok ama daha karmaşık işlerde eşsiz anahtar i&ccedil;in kolon kombinasyonlarını pek tercih etmiyoruz.&nbsp;Eh, sonu&ccedil;ta veri tabanlarına <strong>Auto Increment (Otomatik Sayı - Otomatik Artış)&nbsp;</strong>fonksiyonlarını spor olsun diye koymuyorlar, değil mi?</span></p>
<p>&nbsp;</p>
<p><strong>Ana Tablo</strong>&nbsp;</p>
<table class="table table-striped table-bordered table-hover table-condensed">
<tbody>
<tr><th style="text-align: left;">Id</th><th style="text-align: left;">Calisan</th><th style="text-align: left;">Soyad</th><th style="text-align: left;">Sofor</th><th style="text-align: left;">Arac</th><th style="text-align: left;">Semt</th></tr>
<tr>
<td>1</td>
<td>Or&ccedil;un</td>
<td>Yılmaz</td>
<td>Ahmet</td>
<td>Toyota</td>
<td>Levent</td>
</tr>
<tr>
<td>2</td>
<td>Or&ccedil;un</td>
<td>Yılmaz</td>
<td>Ahmet</td>
<td>Toyota</td>
<td>Etiler</td>
</tr>
<tr>
<td>3</td>
<td>Or&ccedil;un</td>
<td>Yılmaz</td>
<td>Ahmet</td>
<td>Toyota</td>
<td>Ulus</td>
</tr>
<tr>
<td>4</td>
<td>Metin</td>
<td>Seyyar</td>
<td>Mehmet</td>
<td>Honda</td>
<td>Bakırk&ouml;y</td>
</tr>
<tr>
<td>5</td>
<td>Metin</td>
<td>Seyyar</td>
<td>Mehmet</td>
<td>Honda</td>
<td>Atak&ouml;y</td>
</tr>
<tr>
<td>6</td>
<td>Metin</td>
<td>Seyyar</td>
<td>Mehmet</td>
<td>Honda</td>
<td>Yeşilk&ouml;y</td>
</tr>
<tr>
<td>7</td>
<td>Metin</td>
<td>Seyyar</td>
<td>Tolga</td>
<td>Ford</td>
<td>Kandilli</td>
</tr>
<tr>
<td>8</td>
<td>Metin</td>
<td>Seyyar</td>
<td>Tolga</td>
<td>Ford</td>
<td>Beylerbeyi</td>
</tr>
<tr>
<td>9</td>
<td>Metin</td>
<td>Seyyar</td>
<td>Tolga</td>
<td>Ford</td>
<td>Kuzguncuk</td>
</tr>
</tbody>
</table>
<p>İşte şimdi oldu. "Id" s&uuml;tununu eşsiz anahtar olarak atadık. 1NF kurallarına harfiyen uyduk. S&uuml;periz...</p>
<p>&nbsp;</p>
<h3>2NF (2. Normal Form)</h3>
<p style="font-family: Roboto, sans-serif; font-size: 18px; font-weight: normal; line-height: 28.799999237060547px;">Bir veri tabanının 2NF olabilmesi i&ccedil;in aşağıdaki &ouml;zellikleri karşılayabilmesi gerekir:</p>
<ul>
<li><span style="line-height: 1.6;">Tablo 1NF olmalıdır,</span></li>
<li><span style="line-height: 1.6;">Anahtar olmayan değerler ile kompozit (bileşik) anahtarlar arasında kısmi (partial)&nbsp;bağımlılık durumu oluşmamalıdır. Kısmi bağımlılık durumu, anahtar olmayan herhangi bir değer kompozit bir anahtarın yalnızca bir kısmına bağıl ise oluşur. (Evet farkındayım &ccedil;ok karmaşık g&ouml;r&uuml;n&uuml;yor, &ouml;rnekte net bir şekilde anlayacaksınız. S&ouml;z...)</span></li>
<li>Herhangi bir veri alt k&uuml;mesi birden &ccedil;ok satırda tekrarlanmamalıdır. Bu t&uuml;r veri&nbsp;alt k&uuml;meleri&nbsp;i&ccedil;in yeni tablolar oluşturulmalıdır.</li>
<li>Ana tablo ile yeni tablolar arasında, dış anahtarlar (foreign key) kullanılarak ilişkiler tanımlanmalıdır.</li>
</ul>
<p>Aslında &uuml;&ccedil;&nbsp;ve d&ouml;rd&uuml;nc&uuml; maddeler ikinci maddenin sonu&ccedil;larıdır. Eğer anahtar olmayan bir kolonla herhangi bir komposit anahtar arasında kısmi bağımlılık varsa her zaman tekrarlayan veri alt k&uuml;meleri oluşur. Bu durumu d&uuml;zeltmek i&ccedil;in bahis konusu alt k&uuml;meleri farklı bir tablo haline getirmeli ve elde ettiğimiz tablolar ile ana tablomuz arasındaki ilişkiyi tanımlamalıyız.</p>
<p>Tablomuzu bir g&ouml;zden ge&ccedil;irelim: "&Ccedil;alışan - Soyad" kombinasyonuna bakın. &Ccedil;ok tekrarlanıyor &ccedil;&uuml;nk&uuml; eşsiz anahtara verimli bir şekilde bağlayamamışız. Bunu d&uuml;zeltmek i&ccedil;in&nbsp;tablomuzu aşağıdaki gibi ikiye b&ouml;lelim ve aralarında bir ilişki oluşturalım:</p>
<p><strong>Ana Tablo</strong></p>
<table class="table table-striped table-bordered table-hover table-condensed">
<tbody>
<tr><th style="text-align: left;">Id</th><th style="text-align: left;">Calisan</th><th style="text-align: left;">Soyad</th></tr>
<tr>
<td>1</td>
<td>Or&ccedil;un</td>
<td>Yılmaz</td>
</tr>
<tr>
<td>2</td>
<td>Metin</td>
<td>Seyyar</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p><strong>Servis Tablosu</strong>&nbsp;</p>
<table class="table table-striped table-bordered table-hover table-condensed">
<tbody>
<tr><th style="text-align: left;">Cid</th><th style="text-align: left;">Sofor</th><th style="text-align: left;">Arac</th><th style="text-align: left;">Semt</th></tr>
<tr>
<td>1</td>
<td>Ahmet</td>
<td>Toyota</td>
<td>Levent</td>
</tr>
<tr>
<td>1</td>
<td>Ahmet</td>
<td>Toyota</td>
<td>Etiler</td>
</tr>
<tr>
<td>1</td>
<td>Ahmet</td>
<td>Toyota</td>
<td>Ulus</td>
</tr>
<tr>
<td>2</td>
<td>Mehmet</td>
<td>Honda</td>
<td>Bakırk&ouml;y</td>
</tr>
<tr>
<td>2</td>
<td>Mehmet</td>
<td>Honda</td>
<td>Atak&ouml;y</td>
</tr>
<tr>
<td>2</td>
<td>Mehmet</td>
<td>Honda</td>
<td>Yeşilk&ouml;y</td>
</tr>
<tr>
<td>2</td>
<td>Tolga</td>
<td>Ford</td>
<td>Kandilli</td>
</tr>
<tr>
<td>2</td>
<td>Tolga</td>
<td>Ford</td>
<td>Beylerbeyi</td>
</tr>
<tr>
<td>2</td>
<td>Tolga</td>
<td>Ford</td>
<td>Kuzguncuk</td>
</tr>
</tbody>
</table>
<p>Yeni tablomuz ile ana tablomuzu ilişkilendirmek i&ccedil;in "Cid" (&Ccedil;alışan ID) isimli bir kolon&nbsp;yarattık. Dikkat ederseniz bu kolonun aldığı değer ana tablomuzdaki eşsiz anahtarı işaret ediyor. Bu ilişkilendirmeye <strong>Foreign Key</strong>&nbsp;diyoruz.</p>
<p>Ayrıca bilmem s&ouml;ylemeye gerek var mı, Şof&ouml;r - Ara&ccedil; - Semt kombinasyonu bu yeni tablomuzun eşsiz anahtarı olarak gayet iyi iş g&ouml;r&uuml;yor.</p>
<p>Evet, artık bu noktada 2NF işini hallettik diyebiliriz.</p>
<p>&nbsp;</p>
<h3>3NF (3. Normal Form)</h3>
<p><span style="font-family: Roboto, sans-serif; font-size: 18px; line-height: 1.6;">Bir veri tabanının 3NF olabilmesi i&ccedil;in aşağıdaki &ouml;zellikleri karşılayabilmesi gerekir:</span></p>
<ul>
<li>Veri tabanı 2NF olmalıdır,</li>
<li>Anahtar olmayan hi&ccedil; bir kolon bir diğerine (anahtar olmayan başka bir kolona) bağıl olmamalı ya da ge&ccedil;işken fonksiyonel bir bağımlılığı (transitional functional dependency) olmamalıdır. Başka bir deyişle her kolon eşsiz anahtara tam bağımlı olmak zorundadır.</li>
</ul>
<p>Veri tabanımızı 3NF şartlarına uydurabilmek i&ccedil;in anahtar olmayan ve eşsiz anahtara tam bağımlı olmayan t&uuml;m kolonları kaldırmalıyız. Dikkat ederseniz bizim tablomuzda "Ara&ccedil;" kolonu eşsiz anahtarımıza değil "Şof&ouml;r" kolonuna bağımlı. Birbirine bağlı olan bu iki kolonu (Şof&ouml;r - Ara&ccedil;) ayrı bir tabloya ayırmamız ve tablomuzla aralarında bir ilişki yaratmamız gerekiyor.</p>
<p><strong>Ana Tablo</strong></p>
<table class="table table-striped table-bordered table-hover table-condensed">
<tbody>
<tr><th>Id</th><th>Calisan</th><th>Soyad</th></tr>
<tr>
<td>1</td>
<td>Or&ccedil;un</td>
<td>Yılmaz</td>
</tr>
<tr>
<td>2</td>
<td>Metin</td>
<td>Seyyar</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p><strong>Servis Tablosu&nbsp;</strong></p>
<table class="table table-striped table-bordered table-hover table-condensed">
<tbody>
<tr><th style="text-align: left;">Cid</th><th style="text-align: left;">Sid</th><th style="text-align: left;">Semt</th></tr>
<tr>
<td>1</td>
<td>1</td>
<td>Levent</td>
</tr>
<tr>
<td>1</td>
<td>1</td>
<td>Etiler</td>
</tr>
<tr>
<td>1</td>
<td>1</td>
<td>Ulus</td>
</tr>
<tr>
<td>2</td>
<td>2</td>
<td>Bakırk&ouml;y</td>
</tr>
<tr>
<td>2</td>
<td>2</td>
<td>Atak&ouml;y</td>
</tr>
<tr>
<td>2</td>
<td>2</td>
<td>Yeşilk&ouml;y</td>
</tr>
<tr>
<td>2</td>
<td>3</td>
<td>Kandilli</td>
</tr>
<tr>
<td>2</td>
<td>3</td>
<td>Beylerbeyi</td>
</tr>
<tr>
<td>2</td>
<td>3</td>
<td>Kuzguncuk</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p><strong>Şof&ouml;r Tablosu</strong></p>
<table class="table table-striped table-bordered table-hover table-condensed">
<tbody>
<tr><th style="text-align: left;">Sid</th><th style="text-align: left;">Sofor</th><th style="text-align: left;">Arac</th></tr>
<tr>
<td>1</td>
<td>Ahmet</td>
<td>Toyota</td>
</tr>
<tr>
<td>2</td>
<td>Mehmet</td>
<td>Honda</td>
</tr>
<tr>
<td>3</td>
<td>Tolga</td>
<td>Ford</td>
</tr>
</tbody>
</table>
<p>&Ouml;ncelikle şof&ouml;r tablosu adında yeni bir tablo oluşturduk. Bu tabloda Sid (Şof&ouml;r ID) adıyla bir eşsiz anahtar yarattık ve Servis tablomuzdaki Sid kolonundan bu eşsiz anahtara referans vererek foreign key oluşturduk.</p>
<p>3NF'i de g&ouml;rd&uuml;k ya... Artık karada &ouml;l&uuml;m yok.</p>
<p>&nbsp;</p>
<h3>BCNF / 3.5NF (Boyce-Codd Normal Form)</h3>
<p><span style="font-family: Roboto, sans-serif; font-size: 18px; line-height: 1.6;">Bir veri tabanının 3.5NF olabilmesi i&ccedil;in aşağıdaki &ouml;zellikleri karşılayabilmesi gerekir:</span></p>
<ul>
<li><span style="line-height: 1.6;">Veri Tabanı 3NF olmalıdır,</span></li>
<li><span style="line-height: 1.6;">Her determinant (belirleyici kolon) aynı zamanda bir aday anahtar olmalıdır.</span></li>
</ul>
<p><strong>Determinant:</strong>&nbsp;Aynı satırdaki diğer kolon değerlerini belirlemek i&ccedil;in kullanılan kolon k&uuml;mesi determinant olarak adlandırılır.</p>
<p>Servis tablomuza dikkatle baktığımızda iki tane determinant olduğunu g&ouml;rebiliriz. <strong>Semt</strong> kolonu, <strong>Cid&nbsp;- Sid</strong>&nbsp;kombinasyonunun;&nbsp;<strong>Sid</strong> ise&nbsp;<strong>Cid</strong> kolonunun determinantıdır.</p>
<p>Bu noktada Semt kolonunun hali hazırda bir aday anahtar olduğunu g&ouml;rebiliyoruz &ccedil;&uuml;nk&uuml; her bir değer&nbsp;tekrar oluşturmaksızın t&uuml;m kayıt satırını tanımlayabilmekte. &Ouml;te yandan Sid i&ccedil;in aynı&nbsp;şeyi s&ouml;ylemek m&uuml;mk&uuml;n değil &ccedil;&uuml;nk&uuml; tekrarlanıyor.</p>
<p>Elbette bu durumu d&uuml;zeltmek i&ccedil;in tabloyu ikiye ayıracak semt tablosunun değerini tabloları ilişkilendirmek i&ccedil;in foreign key olarak kullanacağız.</p>
<p><strong>Ana Tablo</strong></p>
<table class="table table-striped table-bordered table-hover table-condensed">
<tbody>
<tr><th style="text-align: left;">Id</th><th style="text-align: left;">Calisan</th><th style="text-align: left;">Soyad</th></tr>
<tr>
<td>1</td>
<td>Or&ccedil;un</td>
<td>Yılmaz</td>
</tr>
<tr>
<td>2</td>
<td>Metin</td>
<td>Seyyar</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p><strong>Servis Tablosu&nbsp;</strong></p>
<table class="table table-striped table-bordered table-hover table-condensed">
<tbody>
<tr><th style="text-align: left;">Cid</th><th style="text-align: left;">Semt</th></tr>
<tr>
<td>1</td>
<td>Levent</td>
</tr>
<tr>
<td>1</td>
<td>Etiler</td>
</tr>
<tr>
<td>1</td>
<td>Ulus</td>
</tr>
<tr>
<td>2</td>
<td>Bakırk&ouml;y</td>
</tr>
<tr>
<td>2</td>
<td>Atak&ouml;y</td>
</tr>
<tr>
<td>2</td>
<td>Yeşilk&ouml;y</td>
</tr>
<tr>
<td>2</td>
<td>Kandilli</td>
</tr>
<tr>
<td>2</td>
<td>Beylerbeyi</td>
</tr>
<tr>
<td>2</td>
<td>Kuzguncuk</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p><strong>Semt&nbsp;Tablosu&nbsp;</strong></p>
<table class="table table-striped table-bordered table-hover table-condensed">
<tbody>
<tr><th style="text-align: left;">Semt</th><th style="text-align: left;">Sid</th></tr>
<tr>
<td>Levent</td>
<td>1</td>
</tr>
<tr>
<td>Etiler</td>
<td>1</td>
</tr>
<tr>
<td>Ulus</td>
<td>1</td>
</tr>
<tr>
<td>Bakırk&ouml;y</td>
<td>2</td>
</tr>
<tr>
<td>Atak&ouml;y</td>
<td>2</td>
</tr>
<tr>
<td>Yeşilk&ouml;y</td>
<td>2</td>
</tr>
<tr>
<td>Kandilli</td>
<td>3</td>
</tr>
<tr>
<td>Beylerbeyi</td>
<td>3</td>
</tr>
<tr>
<td>Kuzguncuk</td>
<td>3</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p><strong>Şof&ouml;r Tablosu</strong></p>
<table class="table table-striped table-bordered table-hover table-condensed">
<tbody>
<tr><th style="text-align: left;">Sid</th><th style="text-align: left;">Sofor</th><th style="text-align: left;">Arac</th></tr>
<tr>
<td>1</td>
<td>Ahmet</td>
<td>Toyota</td>
</tr>
<tr>
<td>2</td>
<td>Mehmet</td>
<td>Honda</td>
</tr>
<tr>
<td>3</td>
<td>Tolga</td>
<td>Ford</td>
</tr>
</tbody>
</table>
<p>G&ouml;r&uuml;lebileceği gibi artık tablolarımızın hi&ccedil;birinde aday anahtar olmayan determinant yok. Bu nedenle veri tabanımız BCNF'tir diyebiliriz.</p>
<p><strong>Not:</strong> Hazır Boyce - Codd demişken:&nbsp;<a href="http://en.wikipedia.org/wiki/Raymond_F._Boyce" target="_blank">Raymond F. Boyce</a>,&nbsp;<a href="http://en.wikipedia.org/wiki/Edgar_F._Codd" target="_blank">Edgar F. Codd</a>.</p>
<p>&nbsp;</p>
<h3>4NF (4. Normal Form)</h3>
<p><span style="font-family: Roboto, sans-serif; font-size: 18px; line-height: 1.6;">Bir veri tabanının 4NF olabilmesi i&ccedil;in aşağıdaki &ouml;zellikleri karşılayabilmesi gerekir:</span></p>
<ul>
<li><span style="line-height: 1.6;">Veri Tabanı 3NF olmalıdır,</span></li>
<li><span style="line-height: 1.6;">&Ccedil;ok-değerli bağımlılıkları (Multli-Valued dependency) olmamalıdır.</span></li>
</ul>
<p><strong>Multi-Valued Dependency:</strong>&nbsp;Bu durum bir ya da daha &ccedil;ok veri satırının var olması, aynı tabloda başka bir (ya da daha &ccedil;ok) veri satırının bulunmasını gerektirdiğinde ortaya &ccedil;ıkar. &Ouml;rneğin, bir yazılım firması d&uuml;ş&uuml;nelim. Geliştirdikleri yazılımların masa&uuml;st&uuml; bilgisayarlar i&ccedil;in olanlarını tek-kullanıcılı ve &ccedil;ok-kullanıcılı olarak iki versiyonla piyasaya sunuyor&nbsp;olsunlar. Diyelim ki bu firmanın geliştirdiği&nbsp;t&uuml;m yazılımları barındıran bir veri tabanı oluşturuyoruz. Bu veri tabanında bir masa&uuml;st&uuml; yazılımın tek-kullanıcılı versiyonunu eklediysek mutlaka bir&nbsp;başka satırda aynı yazılımın &ccedil;ok-kullanıcılı versiyonu i&ccedil;in de bir kayıt a&ccedil;ılmış olmak durumundadır...</p>
<p>Hali hazır &ouml;rneğimizde b&ouml;yle bir durum oluşmadığından 4NF uyarlaması yapılmasına gerek (ve imkan) yoktur.</p>
<p>&nbsp;</p>
<h3>Sonu&ccedil;</h3>
<p>En azından ilk &uuml;&ccedil; seviye normalizasyonu her zaman ve mutlaka yapmak gerektiğine inanıyorum. Ancak bazı &ouml;zel durumlarda (&Ouml;rneğin nadiren kayıt girişi yapılan fakat&nbsp;s&uuml;rekli yeni yeni sorgular yazılan&nbsp;bir veri tabanı d&uuml;ş&uuml;n&uuml;n) sorgularınızı kodlamanın biraz daha kolaylaşması i&ccedil;in bazı kolonların birden &ccedil;ok tabloda&nbsp;tekrarlanmasını isteyebilirsiniz. Bu t&uuml;rden durumlarda&nbsp;normalizasyonu bir seviyeden sonra yapmamayı&nbsp;tercih edebilirsiniz. O seviyenin 3NF'den aşağı olmamasını şiddetle tavsiye ederim. Yine de hi&ccedil; &uuml;şenge&ccedil;lik etmesek daha iyi tabii...</p>
<p>&nbsp;</p>
<p>Ne, size veri tabanı oluşturmak kolay mı demişlerdi? Veri tabanıyla&nbsp;Exceli karıştırmış onlar...</p>
<p>&nbsp;</p>
