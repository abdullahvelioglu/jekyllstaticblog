---
layout: post
title: JQUERY EKLENTISI YAZMAK
tags: [web]
---




<p>jQuery hayatımıza o kadar girdi ki, artık herhangi bir HTML dosyasını yazmaya başlarken jQuery'yi include etmeden başlamayı neredeyse hayal dahi edemiyoruz.</p>
<p>Kabul etmek gerekir ki jQuery b&uuml;y&uuml;k kolaylıklar getirdi. Hayatımızı kolaylaştırdı desek herhalde yanılmış olmayız. O zaman&nbsp;jQuery'nin en başarılı &ouml;zelliklerinden biri olan pluginleri de&nbsp;bilgi dağarcığımıza almakta fayda var.</p>
<p>&nbsp;</p>
<h2>jQuery Pluginleri (eklentileri)</h2>
<p>Eklentiler aslında HTML'in DOM elementlerine uygulayabileceğimiz birer metoddan ibarettir. Bu şekli ile herhangi bir jQuery metodu (&ouml;rneğin ".toggle()" metodu) gibidir. Tek farkla: bu metodları biz kendi ihtiya&ccedil;larımıza g&ouml;re yazıp d&uuml;zenleyebiliyoruz.</p>
<p>&nbsp;</p>
<h3>jQuery Eklentisi Nasıl Yazılır</h3>
<p>Bu işlemi anlayabilmek i&ccedil;in &ccedil;ok basit bir&nbsp;jQuery eklentisi yazalım. Bu eklenti, uygulandığı elementlerdeki metin ve arka plan rengini istediğimiz&nbsp;renklerle değiştirsin.</p>
<p>&Ouml;ncelikle sağlıklı bir kod yazacağımızdan emin olmak i&ccedil;in bir temel şablon oluşturalım:</p>
<pre class="brush: js">(function($) {
  "use strict";
  /* Kod Buraya */
})(jQuery);</pre>

<p><strong>A&ccedil;ıklama:</strong>&nbsp;Burada,&nbsp;muhtemelen pek alışkın olmadığınız iki farklı kullanım g&ouml;r&uuml;yorsunuz.</p>
<ul>
<li><strong>(function($) {})(jQuery);</strong><br />jQuery'nin ana fonksiyonunu $ aliası ile kullanmaya &ccedil;ok alışkınız. Ancak bu alias olduk&ccedil;a pop&uuml;lerdir ve bir&ccedil;ok JavaScript kitaplığı&nbsp;i&ccedil;in kullanılır. Bu durum eklentinizin başka JS&nbsp;kitaplıkları ile kullanımı durumunda &ccedil;akışmalara ve beklenmeyen hatalara sebebiyet verebilir. Bu nedenle kodumuzu yazacağımız alanı bir fonksiyon gibi tanımlayarak bu fonksiyona jQuery nesnesini bir değişken olarak g&ouml;nderiyoruz. Bu değişkeni fonksiyonun i&ccedil;eriğinde $ ile isimlendirerek dış d&uuml;nyadan soyutluyor ve diğer kitaplıklarda kullanılması muhtemel olan diğer değişkenlerle &ccedil;akışmasını engellemiş oluyoruz. <strong>Not:</strong>&nbsp;(function($) {}(jQuery)); şeklinde de kullanılabilir.</li>
<li><strong>"use strict"</strong><br />Strict kelimesi katı - m&uuml;samahasız anlamına geliyor. JavaScript'i strict modda yazıyorsanız kodunuzu şişirecek k&ouml;t&uuml; kullanımlardan ve g&uuml;venlik d&uuml;zeyi d&uuml;ş&uuml;k işlemlerden ka&ccedil;ınmış olursunuz. &Ccedil;&uuml;nk&uuml; bu t&uuml;r durumlarda kod hata verir :) &Ouml;rneğin &ouml;nce deklare&nbsp;etmeden değişken kullanamazsınız. Uzun lafın kısası, strict modda yazıyorsanız mecburen daha kaliteli kod yazarsınız.<br />Herhangi bir kodunuzu alın, en &uuml;st satırına "use strict" yazın. Eğer&nbsp;hata veriyorsa o kodun kalitesi d&uuml;ş&uuml;kt&uuml;r...&nbsp;Bu kullanımı t&uuml;m JS kodlarınız i&ccedil;in bir alışkanlık haline getirmenizi&nbsp;&ouml;neririm.</li>
</ul>
<p>&nbsp;</p>
<h2>Eklentiyi oluşturalım</h2>
<p>Kodumuzu yazacağımız ortamı oluşturduk. Şimdi i&ccedil;eriğini oluşturmaya başlayabiliriz. &Ouml;nce eklentimizi oluşturalım:</p>
<pre class="brush: js">(function($) {
  "use strict";

  $.fn.renklendir = function() {
    /* Eklenti kodu buraya */
  }
})(jQuery);</pre>

<p><strong>A&ccedil;ıklama:</strong>&nbsp;G&ouml;rd&uuml;ğ&uuml;n&uuml;z gibi aslında eklentimiz bir fonksiyondan ibaret. jQuery nesnesini, i&ccedil;ine bir fonksiyon ekleyerek genişletiyoruz. Bu fonksiyonun i&ccedil;eriğini istediğimiz gibi oluşturabiliriz. &Ouml;rneğin fonksiyonumuzun i&ccedil;eriğine "alert('Merhaba');" yazarsak her &ccedil;ağırdığımızda bize "Merhaba" diyen bir jQuery eklentisine&nbsp;sahip oluruz.</p>
<p>&nbsp;</p>
<p>Artık fonksiyonumuzun i&ccedil;eriğini oluşturmaya başlayabiliriz:&nbsp;</p>
<pre class="brush: js">(function($) {
  "use strict";

  $.fn.renklendir = function() {
    this.css({
      color: 'red',
      backgroundColor: 'yellow'
    });
  }
})(jQuery);</pre>

<p><strong>A&ccedil;ıklama:</strong>&nbsp;Burada eklentiyi uyguladığımız DOM element(ler)inin metin renklerini kırmızı, arkaplan renklerini ise sarı yaptık. Buradaki "this" nesnesi eklentiye g&ouml;nderdiğimiz DOM elementleri değil jQuery nesnesidir (instance).</p>
<p>&nbsp;</p>
<p>jQuery'nin en keyifli &ouml;zelliklerinden biri de&nbsp;chaining (zincirleme) olarak adlandırılır. Se&ccedil;icinize ardı ardına istediğiniz kadar metod uygulayabileceğiniz anlamına gelir. &Ouml;rneğin ş&ouml;yle bir kod dizgisi gayet m&uuml;mk&uuml;n ve makuld&uuml;r:&nbsp;"$(element).addClass('hoy').css('display', 'block');". jQuery bunu her metodundan (birka&ccedil; istisna hari&ccedil;) o anki&nbsp;jQuery&nbsp;nesnesini (instance) geri d&ouml;nd&uuml;rerek başarır. Bizim yazdığımız eklenti ise geriye herhangi bir şey d&ouml;nd&uuml;rm&uuml;yor. Bu sorunu &ccedil;&ouml;zelim:</p>
<pre class="brush: js">(function($) {
  "use strict";

  $.fn.renklendir = function() {
    this.css({
      color: 'red',
      backgroundColor: 'yellow'
    });
    return this;
  }
})(jQuery);</pre>

<p><strong>A&ccedil;ıklama:</strong>&nbsp;Evet bu kadar basit. Fonksiyonumuza gelen jQuery instance'ını geri d&ouml;nd&uuml;r&uuml;yoruz.&nbsp;Bunu biraz sadeleştirelim. Unutmayın ne kadar az satır, o kadar iyi kod...</p>
<pre class="brush: js">(function($) {
  "use strict";

  $.fn.renklendir = function() {
    return this.css({
      color: 'red',
      backgroundColor: 'yellow'
    });
  }
})(jQuery);</pre>
<p>&nbsp;</p>
<p>S&uuml;periz, herşeyi hallettik... mi?</p>
<p>Evet bir eklenti yazdık ama bu eklenti yalnızca&nbsp;sarı - kırmızı kombinasyonu uyguluyor. Fenerliler ne yapsın? Uygulayacağımız renkleri kullanıcı se&ccedil;emez mi?</p>
<p>Se&ccedil;er elbette ancak bunun i&ccedil;in dışarıdan parametre kabul etmemiz gerekli. Peki bunu nasıl yapacağız. Elbette&nbsp;parametrelerimizi bir nesne (object) i&ccedil;inde fonksiyonumuza g&ouml;ndererek:</p>
<pre class="brush: js">(function($) {
  "use strict";

  $.fn.renklendir = function(param) {
    return this.css({
      color: param.renk,
      backgroundColor: param.arkaplan
    });
  }
})(jQuery);</pre>
<p>Tabii bu parametreleri eklentimizi aktive ederken HTML i&ccedil;inden g&ouml;ndereceğiz:</p>
<pre class="brush: js ; html-script: true">&lt;script&gt;
  $(element).renklendir({
    renk: 'red',
    arkaplan: 'yellow'
  });
&lt;/script&gt;</pre>
<p>&nbsp;</p>
<p>Tamam, artık eklentimiz kullanıcının g&ouml;nderdiği renkler ile &ccedil;alışıyor. Herşey iyi de, kullanıcı parametrelerden herhangi birini ya da hi&ccedil; birini g&ouml;ndermezse ne olacak? Kod hata mı versin? Bu parametrelerin bir varsayılan değeri olmalı, değil mi?</p>
<p>Bu iş i&ccedil;in parametreleri tek tek kontrol edip gelmeyen değerler i&ccedil;in varsayılanları atamanıza gerek yok (ger&ccedil;i bunu yapmayı tercih etmek isteyebileceğiniz durumlar olabilir ama bu onlardan biri değil). Bu iş i&ccedil;in jQuery bize bir ara&ccedil; sunmuş: ".extend();"</p>
<pre class="brush: js">(function($) {
  "use strict";

  $.fn.renklendir = function(param) {
    var degerler = $.extend({
      renk: '#666',
      arkaplan: '#fff'
    }, param);

    return this.css({
      color: degerler.renk,
      backgroundColor: degerler.arkaplan
    });
  }
})(jQuery);</pre>
<p>&nbsp;</p>
<p>Evet, artık ger&ccedil;ekten tamamlandı. Başlangı&ccedil;ta tarif ettiğimiz işlemleri yapabilen bir jQuery eklentisi oluşturduk. Elbette bu &ccedil;ok basit bir &ouml;rnek. İleride&nbsp;daha detaylı (ve ger&ccedil;ekten işe yarayabilecek) eklentiler paylaşacağım.</p>
<p>&nbsp;</p>
