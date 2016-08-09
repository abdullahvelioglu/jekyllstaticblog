---
layout: post
title: 20 Dakikada Ruby  
tags: [programminglanguage]
---


<div id="content">
    <h2>Giriş</h2>

<p>Bu tamamlaması 20 dakikadan fazla vakit almayacak küçük bir Ruby
eğitmenidir. Halihazırda Ruby’nin sisteminizde kurulu olduğunu kabul
eder. (eğer Ruby bilgisayarınızda yüklü değilse başlamadan önce
<a href="https://www.ruby-lang.org/tr/downloads/">indirin</a> ve kurun.)</p>

<h2>İnteraktif Ruby</h2>

<p>Ruby kendisine girdiğiniz her Ruby satırının sonucunu gösteren bir
programla beraber gelir. Ruby ile etkileşimli bir oturumda oynamak bu
dili öğrenmek için dehşet verici bir yoldur.</p>

<p>IRB’i açın (Interactive Ruby anlamına gelir).</p>

<ul>
  <li>Eğer <strong>Mac OS X</strong> kullanıyorsanız <code>Terminal</code> açın ve yazın : <code>irb</code>,
sonra enter basın.</li>
  <li>Eğer <strong>Linux</strong> kullanıyorsanız konsol açın ve yazın : <code>irb</code>, sonra
enter basın.</li>
  <li>Eğer <strong>Windows</strong> kullanıyorsanız başlat menüsü Ruby bölümünden
<code>Interactive Ruby</code> çalıştırın.</li>
</ul>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):001:0&gt;</code></pre></figure>

<p>Tamam açıldı şimdi ne yapacağız?</p>

<p>Şunu yazın : <code>"Hello World"</code></p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):001:0&gt; "Hello World"
=&gt; "Hello World"</code></pre></figure>

<h2>Ruby Size İtaat Eder!</h2>

<p>Ne yaptık şimdi? Dünyanın en kısa “Hello World” programını mı yazdık?
Tam olarak değil. İkinci satır sadece IRB’in yaptığı işlemin sonucunu
bildirme tekniği. Eğer ekrana “Hello World” yazdırmak istiyorsak daha
fazla birşeyler yapmalıyız:</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):002:0&gt; puts "Hello World"
Hello World
=&gt; nil</code></pre></figure>

<p><code>puts</code> Ruby’de çıktı almak için en basit bir komut. Fakat bu <code>=&gt; nil</code> ne
oluyor ki? Bu işlevin sonucudur. <code>puts</code> her zaman Ruby’de hiçbir şeyi
ifade eden nil değerini döndürür.</p>

<h2>Bedava Hesap Makinası Burada</h2>

<p>IRB basit bir hesap makinası olarak kullanılabilir:</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):003:0&gt; 3+2
=&gt; 5</code></pre></figure>

<p>Üç artı iki. Çok kolay. Peki üç <em>kere</em> iki nedir? Bunu girebileceğiniz
gibi bir önce girdiğiniz satırı yukarı tuşuna basarak tekrar
çağırabilirsiniz. Yukarı tuşuna basıp bunu test edin <code>+</code> işaretinin
üstüne gidip silin ve <code>*</code> ile değiştirin.</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):004:0&gt; 3*2
=&gt; 6</code></pre></figure>

<p>Sonra üçün karesini bulalım:</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):005:0&gt; 3**2
=&gt; 9</code></pre></figure>

<p>Ruby’de <code>**</code> “üssü” demenin yoludur. Fakat bir sayının karekökü için ne
yapmalı?</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):006:0&gt; Math.sqrt(9)
=&gt; 3.0</code></pre></figure>

<p>Tamam, bu ne demek sizce? Tahmin ederseniz dokuzun karekökü alınmış.
Haklısınız fakat daha yakından inceleyelim, en başta bu <code>Math</code> ne ?</p>

<h2>Modüller, Kodları Başlıklar Altında Toplar</h2>

<p><code>Math</code> matematik için bir dahili modüldür. Modüller Ruby’de iki hizmet
sunarlar. Bir rolü şu: benzer görevler yapan metotları bir grup başlığı
altında toplamak. <code>Math</code> içinde ayrıca <code>sin()</code> ve <code>tan()</code> gibi işlevler
de vardır.</p>

<p>Sonraki bir nokta işareti, nokta ne yapıyor? Nokta size mesajın
alıcısını gösteriyor. Burada mesaj <code>sqrt(9)</code> metot çağrısı, parametresi
9 olan “karekök” alma komutu.</p>

<p>Bu metodun cevabı <code>3.0</code> dır. Dikkat ettiyseniz sadece <code>3</code> değil. Çünkü
birçok karekök işleminin sonucu tamsayı değildir. Bu yüzden işlev kayan
noktalı bir sayı geri döndürür.</p>

<p>Peki bazı matematik işlemlerimizin sonucunu hatırlamak istersek? Cevabı
bir değişkene atama yaparız.</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):007:0&gt; a = 3 ** 2
=&gt; 9
irb(main):008:0&gt; b = 4 ** 2
=&gt; 16
irb(main):009:0&gt; Math.sqrt(a+b)
=&gt; 5.0</code></pre></figure>

<p>Bir hesap makinası için oldukça yeterli. Klasik <code>Hello World</code> mesajından
uzaklaşmaya başladık, geri dönelim.</p>

<div id="content">
    <p>Eğer parmaklarımızı çok yormadan defalarca “Hello” demek istersek ? Bir
metot tanımlamamız gerekiyor!</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):010:0&gt; def h
irb(main):011:1&gt; puts "Hello World!"
irb(main):012:1&gt; end
=&gt; nil</code></pre></figure>

<p><code>def h</code> kodu ile metot tanımlaması başlar. Bu Ruby’ye adı <code>h</code> olan bir
metot tanıtımı (definition) başlattığımızı bildirir. Sonraki satır
metodun gövdesini oluşturur. Daha önce gördüğümüz gibi: <code>puts "Hello
World"</code>. Son satırdaki <code>end</code> Ruby’ye metot tanımlamasını bitirdiğimizi
belirtir. Ruby’nin <code>=&gt; nil</code> cevabı da metot tanımlamamızı algıladığını
belirtir.</p>

<h2>Kısaca Bir Metot Defalarca Yaşar</h2>

<p>Şimdi bu metodu birkaç defa çalıştıralım:</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):013:0&gt; h
Hello World!
=&gt; nil
irb(main):014:0&gt; h()
Hello World!
=&gt; nil</code></pre></figure>

<p>Pekala, bu kolaydı. Ruby’de metotları çağırmak için adlarını Ruby’ye
söylemek yeterli. Eğer metot bir parametre almıyorsa tüm yapmanız
gereken bundan ibaret. Eğer isterseniz boş parantezlerle parametresiz
bir metot çağırdığınızı belirtebilirsiniz, ama gereği yok.</p>

<p>Eğer dünyaya değil de bir kişiye merhaba demek istersek ne olacak? Hemen
<code>h</code> metodunu bu sefer parametre alacak şekilde tekrar tanımlayalım.</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):015:0&gt; def h(name)
irb(main):016:1&gt; puts "Hello #{name}!"
irb(main):017:1&gt; end
=&gt; nil
irb(main):018:0&gt; h("Matz")
Hello Matz!
=&gt; nil</code></pre></figure>

<p>Çalıştığını gördükten sonra neler olduğunu tekrar bir inceleyelim.</p>

<h2>String İçine Erişmek</h2>

<p><code>#{name}</code> kısmı nedir? Bu bir string içine birşeyler eklemenin Ruby
yoludur. Süslü parantez içindeki kısım stringe çevrilir ve ana string
içine bu noktada eklenir. Bunu verilen ismin ilk harfinin büyük
olduğundan emin olmak için kullanabilirsiniz:</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):019:0&gt; def h(name = "World")
irb(main):020:1&gt; puts "Hello #{name.capitalize}!"
irb(main):021:1&gt; end
=&gt; nil
irb(main):022:0&gt; h "chris"
Hello Chris!
=&gt; nil
irb(main):023:0&gt; h
Hello World!
=&gt; nil</code></pre></figure>

<p>Burda birkaç diğer şekil görünüyor. Biri metodu parantez kullanmadan
çağırıyoruz. Parantezler keyfe bağlı kullanılır, görsel olarak isterseniz
kullanırsınız. Diğer şekil varsayılan parametre değeri <code>World</code>. Bunun
anlamı eğer parametre verilmediyse <code>name</code> değeri varsayılan olarak
<code>"World"</code> alınacaktır.</p>

<h2>Bir Selamlayıcıya Dönüştürmek</h2>

<p>Eğer bir selamlayıcı yapmak istersek, adınızı hatırlayacak ve sizi
karşılayacak, sonra uğurlayacak. Bunu yapmak için bir nesne kullanmak
isteyebilirsiniz. Bir “Greeter” sınıfı oluşturalım.</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):024:0&gt; class Greeter
irb(main):025:1&gt;   def initialize(name = "World")
irb(main):026:2&gt;     @name = name
irb(main):027:2&gt;   end
irb(main):028:1&gt;   def say_hi
irb(main):029:2&gt;     puts "Hi #{@name}!"
irb(main):030:2&gt;   end
irb(main):031:1&gt;   def say_bye
irb(main):032:2&gt;     puts "Bye #{@name}, come back soon."
irb(main):033:2&gt;   end
irb(main):034:1&gt; end
=&gt; nil</code></pre></figure>

<p>Buradaki yeni kelime <code>class</code>. Bu Greeter adı verilen bir nesne ve içinde
birkaç metot tanımlar. Ayrıca dikkat ederseniz <code>@name</code> bu sınıfın bir
örnek değişkeni. Göreceğiniz gibi <code>say_hi</code> ve <code>say_bye</code> metotları
içinde kullanılıyor.</p>

<p>Peki bu Greeter sınıfını nasıl çalıştıracağız? Bir nesne
üretin.</p>


<div id="content">
    <p>Şimdi bir selamlayıcı nesnesi üretelim ve kullanalım:</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):035:0&gt; g = Greeter.new("Pat")
=&gt; #&lt;Greeter:0x16cac @name="Pat"&gt;
irb(main):036:0&gt; g.say_hi
Hi Pat!
=&gt; nil
irb(main):037:0&gt; g.say_bye
Bye Pat, come back soon.
=&gt; nil</code></pre></figure>

<p>Birkez <code>g</code> nesnesi üretildi mi, ismin Pat olduğunu hep hatırlayacaktır.
Hımm, peki ismi direk olarak almak istersek nolcak?</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):038:0&gt; g.@name
SyntaxError: compile error
(irb):52: syntax error
        from (irb):52</code></pre></figure>

<p>Yok, yapamadık.</p>

<h2>Nesnenin Derisinin Altında</h2>

<p>Örnek değişkenleri nesnenin içinde gizli kalırlar. Mutlak olarak gizli
değillerdir, onlara erişmenin başka yolları vardır, fakat Ruby
verileri dışardan erişime gizleyecek çeşitli nesne yönelimli teknikler
kullanır.</p>

<p>Pekala Greeter nesnesinin ne metotları mevcut?</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):039:0&gt; Greeter.instance_methods
=&gt; ["method", "send", "object_id", "singleton_methods",
    "__send__", "equal?", "taint", "frozen?",
    "instance_variable_get", "kind_of?", "to_a",
    "instance_eval", "type", "protected_methods", "extend",
    "eql?", "display", "instance_variable_set", "hash",
    "is_a?", "to_s", "class", "tainted?", "private_methods",
    "untaint", "say_hi", "id", "inspect", "==", "===",
    "clone", "public_methods", "respond_to?", "freeze",
    "say_bye", "__id__", "=~", "methods", "nil?", "dup",
    "instance_variables", "instance_of?"]</code></pre></figure>

<p>Vay, bir sürü metot varmış. Biz sadece iki metot tanımladık. Burada neler
oluyor? Pekala bunlar Greeter nesnesinin tüm metotları, kalıtımdan
gelenler dahil. Eğer kalıtımdan gelen atalarının metotlarını görmek
istemezsek az evvelki çağrıyı <code>false</code> prametresiyle yapmalıyız. Bunun
anlamı kalıtımsal metotları istemediğimizdir.</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):040:0&gt; Greeter.instance_methods(false)
=&gt; ["say_bye", "say_hi"]</code></pre></figure>

<p>Ah, şimdi daha iyi. Haydi şimdide selamlayıcı nesnemiz hangi metotlara
cevap veriyor, bulalım:</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):041:0&gt; g.respond_to?("name")
=&gt; false
irb(main):042:0&gt; g.respond_to?("say_hi")
=&gt; true
irb(main):043:0&gt; g.respond_to?("to_s")
=&gt; true</code></pre></figure>

<p>Gördüğünüz gibi <code>say_hi</code> ve <code>to_s</code> (bir şeyi stringe çevirme emridir)
kelimelerinin anlamını biliyor, fakat <code>name</code> anlamını bilmiyor.</p>

<h2>Sınıfları Değiştirmek—Asla Çok Geç Değildir</h2>

<p>Fakat eğer ismi görmek ve değiştirmek isterseniz ne olacak? Ruby
nesnenin değişkenlerine erişmek için kolay bir yol sunar.</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):044:0&gt; class Greeter
irb(main):045:1&gt;   attr_accessor :name
irb(main):046:1&gt; end
=&gt; nil</code></pre></figure>

<p>Ruby’de bir sınıfı tekrar açıp değiştirebilirsiniz. Yapılan değişiklikler
yeni üretilecek nesnelerde etkili olacağı gibi üretilmiş nesnelerde de
etkilidir. Öyleyse yeni bir nesne üretelim ve onun <code>@name</code> özelliği ile
biraz oynayalım.</p>

<figure class="highlight"><pre><code class="language-irb" data-lang="irb">irb(main):047:0&gt; g = Greeter.new("Andy")
=&gt; #&lt;Greeter:0x3c9b0 @name="Andy"&gt;
irb(main):048:0&gt; g.respond_to?("name")
=&gt; true
irb(main):049:0&gt; g.respond_to?("name=")
=&gt; true
irb(main):050:0&gt; g.say_hi
Hi Andy!
=&gt; nil
irb(main):051:0&gt; g.name="Betty"
=&gt; "Betty"
irb(main):052:0&gt; g
=&gt; #&lt;Greeter:0x3c9b0 @name="Betty"&gt;
irb(main):053:0&gt; g.name
=&gt; "Betty"
irb(main):054:0&gt; g.say_hi
Hi Betty!
=&gt; nil</code></pre></figure>

<p><code>attr_accessor</code> kullanarak iki yeni metot tanımlanmış olur, değeri
okumak için <code>name</code> ve değeri değiştirmek için <code>name=</code> metotları.</p>

<h2>Herşeyi ve Hiçbirşeyi Selamlamak, MegaGreeter Hiçbirini Atlamaz!</h2>

<p>Bu selamlayıcı yeterince ilginç değil. Sadece bir kişi ile ilgileniyor.
Eğer biz dünyayı, bir kişiyi yada kişiler listesinin hepsini
selamlayacak bir MegaGreeter istersek nasıl olacak?</p>

<p>Bu seferki kodumuzu direk IRB’de yazmak yerine bir dosyaya yazarak
saklayalım.</p>

<p>IRB’den çıkmak için “quit” veya “exit” yazın ya da sadece Control-D basın.</p>

<figure class="highlight"><pre><code class="language-ruby" data-lang="ruby"><span class="c1">#!/usr/bin/env ruby</span>

<span class="k">class</span> <span class="nc">MegaGreeter</span>
  <span class="kp">attr_accessor</span> <span class="ss">:names</span>

  <span class="c1"># Nesnenin üretilmesi</span>
  <span class="k">def</span> <span class="nf">initialize</span><span class="p">(</span><span class="n">names</span> <span class="o">=</span> <span class="s2">"World"</span><span class="p">)</span>
    <span class="vi">@names</span> <span class="o">=</span> <span class="n">names</span>
  <span class="k">end</span>

  <span class="c1"># Herkese merhaba de</span>
  <span class="k">def</span> <span class="nf">say_hi</span>
    <span class="k">if</span> <span class="vi">@names</span><span class="p">.</span><span class="nf">nil?</span>
      <span class="nb">puts</span> <span class="s2">"..."</span>
    <span class="k">elsif</span> <span class="vi">@names</span><span class="p">.</span><span class="nf">respond_to?</span><span class="p">(</span><span class="s2">"each"</span><span class="p">)</span>
      <span class="c1"># @names içinde bir çeşit liste var, içinde döndür!</span>
      <span class="vi">@names</span><span class="p">.</span><span class="nf">each</span> <span class="k">do</span> <span class="o">|</span><span class="nb">name</span><span class="o">|</span>
        <span class="nb">puts</span> <span class="s2">"Hello </span><span class="si">#{</span><span class="nb">name</span><span class="si">}</span><span class="s2">!"</span>
      <span class="k">end</span>
    <span class="k">else</span>
      <span class="nb">puts</span> <span class="s2">"Hello </span><span class="si">#{</span><span class="vi">@names</span><span class="si">}</span><span class="s2">!"</span>
    <span class="k">end</span>
  <span class="k">end</span>

  <span class="c1"># Herkese hoşçakal de</span>
  <span class="k">def</span> <span class="nf">say_bye</span>
    <span class="k">if</span> <span class="vi">@names</span><span class="p">.</span><span class="nf">nil?</span>
      <span class="nb">puts</span> <span class="s2">"..."</span>
    <span class="k">elsif</span> <span class="vi">@names</span><span class="p">.</span><span class="nf">respond_to?</span><span class="p">(</span><span class="s2">"join"</span><span class="p">)</span>
      <span class="c1"># Liste elemanlarını virgülle birleştir</span>
      <span class="nb">puts</span> <span class="s2">"Goodbye </span><span class="si">#{</span><span class="vi">@names</span><span class="p">.</span><span class="nf">join</span><span class="p">(</span><span class="s2">", "</span><span class="p">)</span><span class="si">}</span><span class="s2">.  Come back soon!"</span>
    <span class="k">else</span>
      <span class="nb">puts</span> <span class="s2">"Goodbye </span><span class="si">#{</span><span class="vi">@names</span><span class="si">}</span><span class="s2">.  Come back soon!"</span>
    <span class="k">end</span>
  <span class="k">end</span>

<span class="k">end</span>


<span class="k">if</span> <span class="kp">__FILE__</span> <span class="o">==</span> <span class="vg">$0</span>
  <span class="n">mg</span> <span class="o">=</span> <span class="no">MegaGreeter</span><span class="p">.</span><span class="nf">new</span>
  <span class="n">mg</span><span class="p">.</span><span class="nf">say_hi</span>
  <span class="n">mg</span><span class="p">.</span><span class="nf">say_bye</span>

  <span class="c1"># İsmi "Zeke" olarak değiştir</span>
  <span class="n">mg</span><span class="p">.</span><span class="nf">names</span> <span class="o">=</span> <span class="s2">"Zeke"</span>
  <span class="n">mg</span><span class="p">.</span><span class="nf">say_hi</span>
  <span class="n">mg</span><span class="p">.</span><span class="nf">say_bye</span>

  <span class="c1"># İsmi bir isimler dizisine çevir</span>
  <span class="n">mg</span><span class="p">.</span><span class="nf">names</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"Albert"</span><span class="p">,</span> <span class="s2">"Brenda"</span><span class="p">,</span> <span class="s2">"Charles"</span><span class="p">,</span>
    <span class="s2">"Dave"</span><span class="p">,</span> <span class="s2">"Engelbert"</span><span class="p">]</span>
  <span class="n">mg</span><span class="p">.</span><span class="nf">say_hi</span>
  <span class="n">mg</span><span class="p">.</span><span class="nf">say_bye</span>

  <span class="c1">#  nil yap</span>
  <span class="n">mg</span><span class="p">.</span><span class="nf">names</span> <span class="o">=</span> <span class="kp">nil</span>
  <span class="n">mg</span><span class="p">.</span><span class="nf">say_hi</span>
  <span class="n">mg</span><span class="p">.</span><span class="nf">say_bye</span>
<span class="k">end</span></code></pre></figure>

<p>Bu dosyayı “ri20min.rb” olarak kaydedin ve “ruby ri20min.rb” konsol
komutuyla çalıştırın. Çıktısı şöyle olmalı:</p>

<pre class="code"><code>Hello World!
Goodbye World.  Come back soon!
Hello Zeke!
Goodbye Zeke.  Come back soon!
Hello Albert!
Hello Brenda!
Hello Charles!
Hello Dave!
Hello Engelbert!
Goodbye Albert, Brenda, Charles, Dave, Engelbert.  Come
back soon!
...
...
</code></pre>

<p>Bu son örnekle birçok yeni şey ortaya çıktı, daha derinden
inceleyelim.</p>

  </div>
</div>



<div id="content">
    <p>Peki, yeni programımıza daha derin bir inceleme yapalım, (#) ile
başlayan ilk satıra dikkat edin. Ruby’de diyez işareti ile başlayan
satırlar bilgilendirme satırlarıdır ve komut işleyici tarafından dikkate
alınmaz. Dosyanın ilk satırının Unix benzeri işletim sistemlerinde özel
bir anlamı vardır. İşletim sistemine dosyanın nasıl çalıştırılacağını
anlatır. Diğer bütün yorum satırları sadece bilgilendirme amaçlıdır.</p>

<p>Bizim <code>say_hi</code> metodunda biraz kurnazlıklar mevcut:</p>

<figure class="highlight"><pre><code class="language-ruby" data-lang="ruby"><span class="c1"># Herkese merhaba de</span>
<span class="k">def</span> <span class="nf">say_hi</span>
  <span class="k">if</span> <span class="vi">@names</span><span class="p">.</span><span class="nf">nil?</span>
    <span class="nb">puts</span> <span class="s2">"..."</span>
  <span class="k">elsif</span> <span class="vi">@names</span><span class="p">.</span><span class="nf">respond_to?</span><span class="p">(</span><span class="s2">"each"</span><span class="p">)</span>
    <span class="c1"># @names içinde bir çeşit liste var, içinde döndür!</span>
    <span class="vi">@names</span><span class="p">.</span><span class="nf">each</span> <span class="k">do</span> <span class="o">|</span><span class="nb">name</span><span class="o">|</span>
      <span class="nb">puts</span> <span class="s2">"Hello </span><span class="si">#{</span><span class="nb">name</span><span class="si">}</span><span class="s2">!"</span>
    <span class="k">end</span>
  <span class="k">else</span>
    <span class="nb">puts</span> <span class="s2">"Hello </span><span class="si">#{</span><span class="vi">@names</span><span class="si">}</span><span class="s2">!"</span>
  <span class="k">end</span>
<span class="k">end</span></code></pre></figure>

<p>Bu betik nasıl cevap vereceğine karar vermek için <code>@names</code> değişkenine
bakıyor. Eğer değişken boşsa üç nokta koyuyor, selamlanacak kimse yoksa
ne yapacak ki?</p>

<h2>Çevirmek, Döngü veya Yineleme</h2>

<p>Eğer <code>@names</code> nesnesi <code>each</code> metoduna cevap verirse içinde yineleme
yapabileceğiniz bir listedir, öyleyse onun içinde bir yineleme ile
listedeki her kişiyi selamlayabilirsiniz. En son olarak da <code>@names</code>
bunların hiçbiri değilse otomatik olarak stringe dönüşür ve önceki
selamlama şeklini yapar.</p>

<p>Haydi bu yineleyiciyi daha yakından inceleyelim:</p>

<figure class="highlight"><pre><code class="language-ruby" data-lang="ruby"><span class="vi">@names</span><span class="p">.</span><span class="nf">each</span> <span class="k">do</span> <span class="o">|</span><span class="nb">name</span><span class="o">|</span>
  <span class="nb">puts</span> <span class="s2">"Hello </span><span class="si">#{</span><span class="nb">name</span><span class="si">}</span><span class="s2">!"</span>
<span class="k">end</span></code></pre></figure>

<p><code>each</code> metodu arkasından gelen kod bloğunu listenin her elemanı için
çalıştırır. <code>do</code> ve <code>end</code> arasında kod bloğu yer alır. Liste elemanları
tek tek bar karakterleri arasındaki değişkene konur ve kod işlenir.
Sonra bir sonraki liste elemanına geçilir.</p>

<p>Eğer isimleri bir liste içinde verirseniz ne olacak? <code>name</code> listenin
elemanlarına bağlanır ve <code>puts "Hello #{name}!"</code> satırı bu isimle
çalışır.</p>

<p>Birçok diğer programlama dilinde bir liste <code>for</code> döngüsü ile işlenir,
C’de şuna benzer bir kod olur:</p>

<figure class="highlight"><pre><code class="language-c" data-lang="c"><span class="k">for</span> <span class="p">(</span><span class="n">i</span><span class="o">=</span><span class="mi">0</span><span class="p">;</span> <span class="n">i</span><span class="o">&lt;</span><span class="n">number_of_elements</span><span class="p">;</span> <span class="n">i</span><span class="o">++</span><span class="p">)</span>
<span class="p">{</span>
  <span class="n">do_something_with</span><span class="p">(</span><span class="n">element</span><span class="p">[</span><span class="n">i</span><span class="p">]);</span>
<span class="p">}</span></code></pre></figure>

<p>Bu kod çalışıyor ama şık bir görüntüsü yok. <code>i</code> gibi bir değişken
üretmek zorundasınız, listenin uzunluğunu bulmak zorundasınız ve liste
elemanlarının nasıl işleneceğini anlatmak zorundasınız. Ruby yolu çok
daha zarif, tüm ayrıntılar bir <code>each</code> kelimesinin içinde saklı ve
sadece her elemanı ne yapacağınızı anlatmak zorundasınız. Ayrıca daha
okunaklı oluyor, Ruby yolu böyle olmalı. İçeride <code>each</code> metodu sırayla
<code>yield "Albert"</code> sonra <code>yield "Brenda"</code> sonra <code>yield "Charles"</code> şeklinde
çalışmaktadır.</p>

<h2>Bloklar, Ruby’nin En Işıldayan Özelliği</h2>

<p>Blokların bir şeyleri işlemekteki gücü listelerden daha karmaşıktır.
Metodun içerisindekileri toparlamanın ötesinde, ayrıca kullanıcı farkında
olmadan ayarlarlar, parçalama ve hatalarla ilgilenebilirsiniz.</p>

<figure class="highlight"><pre><code class="language-ruby" data-lang="ruby"><span class="c1"># Herkese hoşçakal de</span>
<span class="k">def</span> <span class="nf">say_bye</span>
  <span class="k">if</span> <span class="vi">@names</span><span class="p">.</span><span class="nf">nil?</span>
    <span class="nb">puts</span> <span class="s2">"..."</span>
  <span class="k">elsif</span> <span class="vi">@names</span><span class="p">.</span><span class="nf">respond_to?</span><span class="p">(</span><span class="s2">"join"</span><span class="p">)</span>
    <span class="c1"># Liste elemanlarını virgülle birleştir</span>
    <span class="nb">puts</span> <span class="s2">"Goodbye </span><span class="si">#{</span><span class="vi">@names</span><span class="p">.</span><span class="nf">join</span><span class="p">(</span><span class="s2">", "</span><span class="p">)</span><span class="si">}</span><span class="s2">.  Come back soon!"</span>
  <span class="k">else</span>
    <span class="nb">puts</span> <span class="s2">"Goodbye </span><span class="si">#{</span><span class="vi">@names</span><span class="si">}</span><span class="s2">.  Come back soon!"</span>
  <span class="k">end</span>
<span class="k">end</span></code></pre></figure>

<p><code>say_bye</code> metodu <code>each</code> kullanmaz onun yerine <code>@names</code> değişkeninin
<code>join</code> metoduna cevap vermesini sınar ve kullanır. Diğer durumda liste
değil de string olarak işlenir. Bu metot, değişkenin orjinal <em>tipi</em> ile
ilgilenmez <code>join</code> metoduna cevap veriyorsa <code>join</code> ile değişkeni işler,
liste değil başka bir tipte değişken de <code>join</code> metoduna cevap verse onu
da aynı şekilde işler. Buna “Duck Typing” denir, “eğer ördek gibi
yürüyorsa ve ördek gibi ötüyorsa …” gibi bir şey.</p>

<h2>Betiğe Giriş</h2>

<p>Peki, bu MegaGreeter sınıf tanımıydı, dosyanın geri kalanı ise bu
sınıfın kullanılmasından ibaret. Dikkatinizi çekecek son bir nokta
kaldı, o da şu:</p>

<figure class="highlight"><pre><code class="language-ruby" data-lang="ruby"><span class="k">if</span> <span class="kp">__FILE__</span> <span class="o">==</span> <span class="vg">$0</span></code></pre></figure>

<p><code>__FILE__</code> sihirli bir değişkendir ve bulunduğu dosyanın ismini içerir.
<code>$0</code> ise bu programı çağıran dosyanın ismini içerir. Buradaki koşul ile
“Eğer bu dosya direk çağrıldıysa .. ” deniyor. Başka bir program burada
tanımlanan sınıfı <code>require</code> satırı ile içerip kullanacaksa bu koşul
içindeki blok çalışmayacaktır. Ancak ve ancak bu dosya tek başına
çalıştırıldığında bu satırlar işlenecekir.</p>

<h2>Artık Kendinizi Tanışmış Kabul Edin</h2>

<p>Ruby’ye hızlı bakış bu kadar. Daha Ruby’nin sunduğu incelenebilecek
birçok değişik kontrol yapıları var; blokların ve <code>yield</code>in kullanımı,
modüller ve dahası. Umarız bu anlattıklarımız sizde Ruby hakkında daha
fazla şeyler öğrenmek için bir arzu yaratmıştır.</p>

<p>Eğer öyleyse lütfen <a href="https://www.ruby-lang.org/tr/documentation/">Belgeler</a> bölgesindeki ücretsiz
el kitapları ve öğreticileri inceleyin.</p>

<p>Ya da gerçekten kapsamlı bir kitap bakıyorsanız, <a href="http://www.ruby-doc.org/bookstore">kitap listesinde</a>
 yararlı kitaplar bulabilirsiniz.</p>

 <p> Bu yazı <a href="http://www.ruby-lang.org/tr">ruby-lang</a>'tan alınmıştır.</p> 


  </div>
</div>
