---
layout: post
title: SOLID PRENSIBI
tags: [programminglanguage]
---


<div class="container">
           <article>
   <div class="row">
       <div class="col-lg-8 col-lg-offset-2 col-md-10 col-md-offset-1">
           <div class="blog-post"><p>2000’lerin başında konuşulmaya başlanan, <a href="https://twitter.com/mfeathers" target="_blank">Michael Feathers</a> tarafından tanıtılan
ve &quot;İlk Beş Prensip&quot; diye <a href="http://en.wikipedia.org/wiki/Robert_Cecil_Martin" target="_blank">Robert C. Martin</a> adlandırılan Nesne Yönelimli
Programlama’nın temel prensibidir <strong>S.O.L.I.D</strong></p>

<p>Bu beş kural, aşağıdaki konulardan oluşur;</p>

<ul>
<li><strong>S</strong>ingle responsibility principle</li>
<li><strong>O</strong>pen/closed principle</li>
<li><strong>L</strong>iskov substitution principle</li>
<li><strong>I</strong>nterface segregation principle</li>
<li><strong>D</strong>ependency inversion principle</li>
</ul>

<p>Bu prensipler, daha iyi program yazmanın yanı sıra, sürdürülebilir uygulama
geliştirmeye yardımcı olur. <a href="https://twitter.com/sandimetz" target="_blank">Sandi Metz</a>’in 2009’da düzenlenen
<a href="http://confreaks.tv/events/goruco2009" target="_blank">GoRuCo</a> konferansında yaptığı <a href="http://confreaks.tv/videos/goruco2009-solid-object-oriented-design" target="_blank">sunumun</a> başında;</p>

<blockquote>
<p>Uygulamanızı görmedim, ne yaptığınızı bilmiyorum ama kesin olarak bildiğim
şey şu: uygulamanız değişecek!</p>
</blockquote>

<p>Evet, Sandi Metz, bu konuda çok haklıydı. Çünkü gerçekten de yazdığımız
uygulama, bir noktada mutlaka değişikliklere uğrayacaktı. İster hata düzeltme
ister yeni özellikler ekleme olsun, uygulamalar bir şekilde hiçbir zaman
ilk yazıldığı gün gibi kalmayacaktı.</p>

<p>Sağlam temelleri olan bir uygulama geliştirmek için ilk adımın Test Driven
Development olduğunu biliyoruz, ama bir noktada ne yazıkki bu yöntem de
<a href="http://www.sandimetz.com/blog/2009/03/21/solid-design-principles" target="_blank">yetersiz kalabiliyor</a>. </p>

<p>Uygulama geliştirirken başımızın fazla ağrımaması için, uzmanlar <strong>SOLID</strong>
prensipleri ortaya koydular. Şimdi tek tek bu prensiplere göz atalım.</p>

<h2>(S): Single responsibility</h2>

<p>Bir sınıf (<em>class</em>) sadece tek bir işten sorumlu olmalıdır. Örneğin, bir
web uygulaması içinde, veritabanı ile bağlantı yapacak olan sınıfın tek işi
bağlantıyı açması ve kapatması olmalıdır. Sorgu yapmak, tablo silmek
ya da oluşturmak işlerinden biri <strong>OLMAMALIDIR</strong>!</p>

<p><a href="https://docs.google.com/file/d/0ByOwmqah_nuGNHEtcU5OekdDMkk/edit" target="_blank">Kaynak</a>, <a href="http://en.wikipedia.org/wiki/Single_responsibility_principle" target="_blank">Kaynak</a></p>

<hr>

<h2>(O): Open/closed</h2>

<p>Bir sınıf, genişlemeye açık olmalı ama değişime kapalı olmalı. Yani kodu
değiştirmeden, değişebilmeli. Modüller <code>extend</code> edilebilmeli ama asla ilgili
işi yapabilmek adına, hali hazırda bulunan kod tekrardan yazılmamalı,
değiştirilmemeli.</p>

<p>Örneğin, Daire ve Kare çizen bir uygulama olsun. Çizdirme işini yaparken,
&quot;eğer tipi daire ise şöyle çiz, kare ise böyle çiz&quot; şeklinde bir akış
kullanırsak, ileride <strong>üçgen</strong> çizdirmemiz gerektiğinde bu prensibi bozmak
zorunda kalırız. Kodu değiştirip &quot;eğer tipi üçgen ise&quot; koşulunu eklememiz
gerekir.</p>

<p>Halbuki, <code>Şekil</code> adında bir sınıf olsa, <code>Daire</code> ve <code>Kare</code> bu sınıftan türese,
her iki şeklinde kendi <code>çizim</code> metodu olsa. En sonda da <code>ŞekliÇiz</code> diye
ayrı bir sınıf olsa, bu sınıfı oluştururken ilgili şekli parametre olarak
geçsek ve çizme işlemi için ilgili şeklin <code>çizim</code> metodunu çağırsak?</p>

<p>Aşağıdaki örnek bu prensibi ihlal eder. Yarın <code>json</code> çıktı almak yerine
<code>pdf</code> ya da <code>xml</code> çıktı gerekse kodu değiştirmek gerekecek...</p>
<div class="highlight"><pre><code class="language-ruby" data-lang="ruby"><span class="k">class</span> <span class="nc">Rapor</span>
 <span class="k">def</span> <span class="nf">dokuman</span>
   <span class="n">dokumani_uret</span>
 <span class="k">end</span>

 <span class="k">def</span> <span class="nf">yazdir</span>
   <span class="n">dokuman</span><span class="o">.</span><span class="n">to_json</span> <span class="c1"># json çıktı alır</span>
 <span class="k">end</span>
<span class="k">end</span>
</code></pre></div>
<p>Halbuki aşağıdaki durum bu kurala uyar;</p>
<div class="highlight"><pre><code class="language-ruby" data-lang="ruby"><span class="k">class</span> <span class="nc">Rapor</span>
 <span class="k">def</span> <span class="nf">dokuman</span>
   <span class="n">dokumani_uret</span>
 <span class="k">end</span>

 <span class="k">def</span> <span class="nf">yazdir</span><span class="p">(</span><span class="ss">cikti_formati</span><span class="p">:</span> <span class="no">JSONFormatter</span><span class="o">.</span><span class="n">new</span><span class="p">)</span>
   <span class="n">cikti_formati</span><span class="o">.</span><span class="n">format</span> <span class="n">dokuman</span>
 <span class="k">end</span>
<span class="k">end</span>

<span class="n">aylik_rapor</span> <span class="o">=</span> <span class="no">Rapor</span><span class="o">.</span><span class="n">new</span>
<span class="n">aylik_rapor</span><span class="o">.</span><span class="n">yazdir</span><span class="p">(</span><span class="ss">cikti_formati</span><span class="p">:</span> <span class="no">XMLFormatter</span><span class="o">.</span><span class="n">new</span><span class="p">)</span> <span class="c1"># xml olarak aldık...</span>
</code></pre></div>
<p><a href="https://drive.google.com/file/d/0BwhCYaYDn8EgN2M5MTkwM2EtNWFkZC00ZTI3LWFjZTUtNTFhZGZiYmUzODc1/view" target="_blank">Kaynak</a></p>

<hr>

<h2>(L): Liskov substitution</h2>

<p>Alt sınıf (<em>türeyen sınıf - sub class</em>), üst sınıfın (<em>base class</em>) yerini
alabilecek şekilde olmalıdır. Şimdi iki tane sınıfımız olsun. <strong>Dörtgen</strong> ve <strong>Kare</strong>.
Kare, Dörtgen’den türemiş olsun. Dörtgen sınıfının <code>genislik</code> ve <code>yukseklik</code>
adında iki tane <strong>accessor</strong>’ü (<em>getter-setter</em>) var, Ruby’den örnekliyoruz:</p>
<div class="highlight"><pre><code class="language-ruby" data-lang="ruby"><span class="k">class</span> <span class="nc">Dortgen</span>
 <span class="kp">attr_accessor</span> <span class="ss">:genislik</span><span class="p">,</span> <span class="ss">:yukseklik</span>
<span class="k">end</span>
</code></pre></div>
<p>ve <code>Dortgen</code>’den türemiş <code>Kare</code>:</p>
<div class="highlight"><pre><code class="language-ruby" data-lang="ruby"><span class="k">class</span> <span class="nc">Kare</span> <span class="o">&lt;</span> <span class="no">Dortgen</span>
 <span class="k">def</span> <span class="nf">yukseklik</span><span class="o">=</span><span class="p">(</span><span class="n">yukseklik</span><span class="p">)</span>
   <span class="vi">@degisken</span> <span class="o">=</span> <span class="n">yukseklik</span>
 <span class="k">end</span>
 <span class="k">def</span> <span class="nf">genislik</span><span class="o">=</span><span class="p">(</span><span class="n">genislik</span><span class="p">)</span>
   <span class="vi">@degisken</span> <span class="o">=</span> <span class="n">genislik</span>
 <span class="k">end</span>
 <span class="k">def</span> <span class="nf">genislik</span>
   <span class="vi">@degisken</span>
 <span class="k">end</span>
 <span class="k">def</span> <span class="nf">yukseklik</span>
   <span class="vi">@degisken</span>
 <span class="k">end</span>
<span class="k">end</span>
</code></pre></div>
<p>Ruby’de <code>=</code> ile biten metod <code>setter</code> anlamına geliyor. Yani <code>yukseklik=</code> <strong>setter</strong>,
<code>yukseklik</code> ise <strong>getter</strong>.</p>

<p>Şimdi her iki şeklinde alanını hesap edelim:</p>
<div class="highlight"><pre><code class="language-text" data-lang="text">alan = genislik * yukseklik
</code></pre></div><div class="highlight"><pre><code class="language-ruby" data-lang="ruby"><span class="n">dortgen</span> <span class="o">=</span> <span class="no">Dortgen</span><span class="o">.</span><span class="n">new</span>
<span class="n">kare</span> <span class="o">=</span> <span class="no">Kare</span><span class="o">.</span><span class="n">new</span>

<span class="n">dortgen</span><span class="o">.</span><span class="n">genislik</span> <span class="o">=</span> <span class="mi">4</span>
<span class="n">dortgen</span><span class="o">.</span><span class="n">yukseklik</span> <span class="o">=</span> <span class="mi">5</span>
<span class="n">dortgen</span><span class="o">.</span><span class="n">genislik</span> <span class="o">*</span> <span class="n">dortgen</span><span class="o">.</span><span class="n">yukseklik</span> <span class="c1"># =&gt; 20</span>

<span class="n">kare</span><span class="o">.</span><span class="n">genislik</span> <span class="o">=</span> <span class="mi">4</span>
<span class="n">kare</span><span class="o">.</span><span class="n">yukseklik</span> <span class="o">=</span> <span class="mi">5</span>
<span class="n">kare</span><span class="o">.</span><span class="n">genislik</span> <span class="o">*</span> <span class="n">kare</span><span class="o">.</span><span class="n">yukseklik</span>       <span class="c1"># =&gt; 25 ???</span>
</code></pre></div>
<p><code>Kare</code> sınıfı, Liskov değişimi kuralını ihlal edip, üst sınıftan gelen
özellikleri modifiye etmiştir.</p>

<p>Başka bir örnek;</p>
<div class="highlight"><pre><code class="language-ruby" data-lang="ruby"><span class="k">class</span> <span class="nc">Hayvan</span>
 <span class="k">def</span> <span class="nf">yuru</span>
    <span class="n">yurume_islemi</span>
 <span class="k">end</span>
<span class="k">end</span>

<span class="k">class</span> <span class="nc">Kedi</span> <span class="o">&lt;</span> <span class="no">Hayvan</span>
 <span class="k">def</span> <span class="nf">kos</span>
   <span class="n">kosma_islemi</span>
 <span class="k">end</span>
<span class="k">end</span>
</code></pre></div>
<p>Verdiğim örnek Ruby’den ve Ruby’de <strong>interface</strong> mantığı yok. Yukarıdaki
kod Liskov değişimi prensibini ihlal ediyor. Neden? <code>Kedi</code> sınıfı <code>Hayvan</code>dan
türedi ve <code>Hayvan</code> sınıfının <code>kos</code> diye bir metodu yok... Bu durumda,
<code>Hayvan</code> sınıfını bir <strong>interface</strong> gibi düşünmeli ve interface’de olan
metodları <strong>implement</strong> etmeliyiz. Bu bakımdan <code>Hayvan</code> sınıfı aşağıdaki
gibi olmalı:</p>
<div class="highlight"><pre><code class="language-ruby" data-lang="ruby"><span class="k">class</span> <span class="nc">Hayvan</span>
 <span class="k">def</span> <span class="nf">yuru</span>
   <span class="n">yurume_islemi</span>
 <span class="k">end</span>
 <span class="k">def</span> <span class="nf">kos</span>                          <span class="c1"># koşma özelliği olmasa bile</span>
   <span class="k">raise</span> <span class="no">NotImplementedError</span>      <span class="c1"># prensibe göre çapraz</span>
 <span class="k">end</span>                              <span class="c1"># eşitlik olmalı...</span>
<span class="k">end</span>
</code></pre></div>
<p><a href="http://en.wikipedia.org/wiki/Liskov_substitution_principle" target="_blank">Kaynak</a>, <a href="https://drive.google.com/file/d/0BwhCYaYDn8EgNzAzZjA5ZmItNjU3NS00MzQ5LTkwYjMtMDJhNDU5ZTM0MTlh/view" target="_blank">Kaynak</a></p>

<hr>

<h2>(I) Interface segregation</h2>

<p>Genel amaca hizmet eden tek bir arayüz yapmak yerine, istemciye uygun farklı
farklı arayüzler yapmak daha iyidir. Yani bir sınıf, bir interface’den
türerken sadece kendi işine yarayacak metodları almalıdır.</p>

<p>Bu sayede daha uyumlu kod yazma ve <strong>less coupling</strong> yani başka kütüphane/kod’a
bağlı kalmama özelliğini arttırmış/sağlamış oluruz.</p>

<p><a href="https://drive.google.com/file/d/0BwhCYaYDn8EgOTViYjJhYzMtMzYxMC00MzFjLWJjMzYtOGJiMDc5N2JkYmJi/view" target="_blank">Kaynak</a>, <a href="http://en.wikipedia.org/wiki/Interface_segregation_principle" target="_blank">Kaynak</a></p>

<hr>

<h2>(D) Dependency inversion</h2>

<p>Bağımlılığın tersine dönmesi. Tek parça monolit/devasa bir sınıf olmak yerine
kendi işlerini yapan küçük parçalardan oluşan sınıflar haline gelmek. Bağımlılıkları
minimale indirmek, hatta başka bir değişle <strong>Dependency Injection</strong> yapmak.</p>

<p>Özellikle <a href="http://en.wikipedia.org/wiki/Test-driven_development" target="_blank">TDD</a> yaparken sık kullandığımız <a href="http://en.wikipedia.org/wiki/Mock_object" target="_blank">Mock</a>, <a href="http://en.wikipedia.org/wiki/Method_stub" target="_blank">Stub</a>,
<a href="http://en.wikipedia.org/wiki/Test_double" target="_blank">Test Double</a> gibi kavramlar bu prensip üzerine kuruludur.</p>

<p>Bir sınıf oluşturuken parametre olarak <code>Hash</code> / <code>Dictionary</code> yani <strong>key-value</strong>
tutan nesne geçmek ya da ilgili başka bir sınıfı geçmek araya bağımlılık enjekte
etmek anlamına gelir. Buradaki bağımlılık aslında bize esneklik sağlar.</p>

<p>Fonksiyonu ya da metodu çağırken sabit parametre yerine kullanılan Hash, hem
bize parametre sırası zorunluluğundan kurtatır hem de ilgili fonksiyon içinde
bağımsız hareket edebilme özgürlüğünü sağlar.</p>
<div class="highlight"><pre><code class="language-ruby" data-lang="ruby"><span class="no">DEFAULTS</span> <span class="o">=</span> <span class="p">{</span>
 <span class="ss">a</span><span class="p">:</span> <span class="mi">1</span><span class="p">,</span>
 <span class="ss">b</span><span class="p">:</span> <span class="mi">2</span><span class="p">,</span>
 <span class="ss">c</span><span class="p">:</span> <span class="s2">&quot;c&quot;</span>
<span class="p">}</span>

<span class="k">def</span> <span class="nf">test_func</span><span class="p">(</span><span class="n">args</span><span class="o">=</span><span class="p">{})</span>
 <span class="n">args</span> <span class="o">=</span> <span class="no">DEFAULTS</span><span class="o">.</span><span class="n">merge</span><span class="p">(</span><span class="n">args</span><span class="p">)</span>
<span class="k">end</span>

<span class="n">test_func</span>
<span class="c1"># =&gt; {:a=&gt;1, :b=&gt;2, :c=&gt;&quot;c&quot;}</span>

<span class="n">test_func</span><span class="p">({</span><span class="ss">a</span><span class="p">:</span> <span class="s2">&quot;ali&quot;</span><span class="p">,</span> <span class="ss">b</span><span class="p">:</span> <span class="s2">&quot;veli&quot;</span><span class="p">,</span> <span class="ss">c</span><span class="p">:</span> <span class="kp">nil</span><span class="p">})</span>
<span class="c1"># =&gt; {:a=&gt;&quot;ali&quot;, :b=&gt;&quot;veli&quot;, :c=&gt;nil}</span>
</code></pre></div>
<p>Test yazarken, henüz nasıl çalışacağına karar vermediğimiz ama tahminen sonucunu
ne olması gerektiğini bildiğimiz durumlara, bu metodu varmış gibi taklit etmek,
gerçek kodda kullanmak da tam bir <strong>Dependency Injection</strong> örneğidir.</p>
<div class="highlight"><pre><code class="language-ruby" data-lang="ruby"><span class="c1"># Ruby, Rspec örnek...</span>
<span class="n">f</span> <span class="o">=</span> <span class="s2">&quot;./test_file.txt&quot;</span>

<span class="n">file_downloader</span> <span class="o">=</span> <span class="n">double</span><span class="p">(</span><span class="s2">&quot;Fetcher&quot;</span><span class="p">)</span>
<span class="c1"># Henüz Fetcher sınıfını yazmadık ama </span>

<span class="n">file_downloader</span><span class="o">.</span><span class="n">stud</span><span class="p">(</span><span class="ss">:download</span><span class="p">)</span><span class="o">.</span><span class="n">and_return</span><span class="p">(</span><span class="n">f</span><span class="p">)</span>
<span class="c1"># download metodu olacağını ve bir text dosyası döneceğini biliyoruz!</span>
</code></pre></div>
<hr>

<p>Tüm bu prensipler aslında daha kullanışlı, daha rahat yönetilebilen ve
sürdürülebilir yazılım geliştirmemizi sağlamak amacıyla uzmanların
ortaya koyduğu kurallardır.</p>

<p>Başta da belirttiğim gibi, usta <a href="https://twitter.com/sandimetz" target="_blank">Sandi Metz</a> bu konuyla ilgili çok
güzel bir sunum yapmıştı. Bu sunumu da <a href="https://speakerdeck.com/skmetz/solid-object-oriented-design" target="_blank">linkten</a> indirebilirsiniz.</p>
</div>
