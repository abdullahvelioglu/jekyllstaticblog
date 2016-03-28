---
layout: post
title: AZER KOCULU, KIK, LEFT-PAD VE NPM
tags: [softwarenews]
---




<p>Birkaç gün önce "11 satır internet'i kırdı" benzeri başlıklarla çıkan haber mutlaka sizlere de ulaşmıştır.</p>

<p>Konu internette bolca konuşuldu. Olayın tarafları olan <a href="http://medium.com/@azerbike/i-ve-just-liberated-my-modules-9045c06be67c">Azer Koçulu</a>, <a href="https://medium.com/@mproberts/a-discussion-about-the-breaking-of-the-internet-3d4d2a83aa4d">Kik</a> ve <a href="http://blog.npmjs.org/post/141577284765/kik-left-pad-and-npm">NPM</a> sırasıyla olay hakkında bizleri bilgilendirdiler. Ben hızlıca bir tekrar edeceğim, bunu yaparken de başlıklar kullanacağım ki okuyucu olarak konunun bildiğiniz kısımlarını hızlıca geçebilirsiniz.</p>

<h2 id="npmnedir">NPM Nedir?</h2>

<p>NPM genellikle JavaScript'de oluşturulmuş projeler ve kütüphaneler için bir liman. İnsanlar/organizasyonlar kodlarını NPM'e bir isim altında gönderebiliyorlar. Ve NPM'in bünyesindeki projeler birbirlerine referans göstererek daha önce üretilmiş bir kodu tekrar yazmak yerine tekrar kullanarak zamandan tasarruf ediyorlar.</p>

<p>Bu kadar yüzeysel geçtiğime bakmayın, o ufak kodlar zaman geçtikçe, standartlar geliştikçe kendi ufak ölçeğinde sürekli güncellenerek diğer projeleri de mikro düzeyde sağlam tutmak gibi faydalar sağlıyor.</p>

<p>Bu zaman zaman ufak, zaman zaman kullanan projenin kendisinden büyük paketleri genellikle açık kaynak gönüllüsü insanlar NPM ve benzeri platformlarda paylaşıyorlar. Evet, birileri mesailerinden, sevdikleri ile geçirebileceği zamandan arttırıp insanlık için çalışıyor.</p>

<h2 id="olay"> Olay</h2>

<p>Azer Koçulu NPM'de <a href="https://gist.githubusercontent.com/azer/db27417ee84b5f34a6ea/raw/50ab7ef26dbde2d4ea52318a3590af78b2a21162/gistfile1.txt">274 adet</a> paketi bulunan bir geliştirici.</p>

<p>Bunlardan bir tanesi de <a href="https://github.com/starters/kik">kik</a>. Kik komut satırınca "kik" yazarak yeni proje oluşturmanızı sağlıyor. Ve bildiğim/anladığım kadarıyla "kick", "kickstart" gibi bir anlama sahip.</p>

<p>Benim NPM'de komut satırından çalışan 1 adet paketim bulunuyor. Onun da ismi "sey", o da üç harfli. Nasıl dosya listesi aldığınız komut "ls" veya "dir" ise komut satırı kullanırken kısa ve akılda kalabilecek bir isim koymaya özen gösteriyorsunuz.</p>

<p>Muhtemelen aynı motivasyonlarla ismini belirlemiş "kik" isimli bir mesajlaşma programı var. Azer Koçulu'dan kendi "kik" isimli projelerini başka bir yere taşımasını, "kik" ismini de kendilerine bırakmasını istiyorlar. Neden olarak da "kendi kullanıcılarının kafalarının karışabileceğini" öne sürüyorlar.</p>

<p>Azer Koçulu'nun "üzgünüm, ben açık kaynak bir proje yürütüyorum" diyerek tekliflerini reddetmesiyle birlikte mesajlaşma programı'nın sahibi firma patent avukatlarını Azer Koçulu'nun üzerine salacaklarını, kapısının çalınacağını, bu tarz hesaplarının ele geçirileceğini ve kaybedeceğini söyleyerek tehdit ediyor. Mesajın sonuna da "avukatları karıştırmadan bu işi halledelim, bir tazminat belirlesek de ismi değiştirsen?" anlamında bir şeyler ekliyor.</p>

<p>Azer Koçulu'nun yanıtı "bir daha beni rahatsız etmeyin" oluyor. Bu noktadan sonra işler daha da çirkinleşiyor fakat aradaki kısımları hızlıca geçersek firma "avukatlar gerçekten karışsın istemiyoruz" diyerek arabuluculuk yapılması için NPM'i devreye sokuyor.</p>

<p>NPM'in kararı "evet bizce kullanıcılar kik yazdıklarında mesajlaşma programını bulabilmeliler" olunca Azer Koçulu durumu protesto etmek için NPM üzerindeki tüm paketlerini geri çekiyor.</p>

<p>Geri çekerken söylediği bir söz bence oldukça etkili "Bu durum NPM'in kurumların bireylerden daha güçlü olduğu bir özel mülk olduğunu idrak etmemi sağladı" diyor Azer Koçulu.</p>

<p>Bunun üzerine bir kelebek etkisi ortaya çıkıyor ve React, Babel gibi bir çok popüler paket işlemez hale geliyor. Sorun 2.5 saatlik bir süre içerisinde çözülüyor.</p>

<p>Twitter üzerinde Azer Koçulu'yu fırsatçılıkla suçlayan bazı görüşlere de denk geldim. Ben mümkün olduğunca bu konuyla ilgili görüşlerimi olay aktarımına yansıtmamaya çalışsam da, şu noktayı eklemeden geçmek istemiyorum. İstatistik olarak düşünürseniz, dünyada başlatılan start-up sayısı ve projelere koyulan isim sayısının birbirine denk gelmesi oldukça olağan bir durum. Kik ismi halihazırda bir konfeksiyon üreticisi, Kamu İhale Kurumu gibi organizasyonlar tarafından da paylaşılıyor.</p>

<h2 id="sonras">Sonrası</h2>

<p>NPM bu olaydan dersler çıkartıyor. Artık paket geri çekmek o kadar da kolay olmayacak.</p>

<p>Projesi çalışmayanlar olaydan ders çıkartıyorlar. Artık mikro düzeyde bağımlılık/kütüphane kullanacakları zaman daha ince eleyip daha sık dokuyacaklar.</p>

<p>Azer Koçulu'nun görüşü ise "açık kaynak camiasının eninde sonunda tamamiyle özgür bir NPM alternatifi üreteceği" yönünde.</p>

<hr />

<p>Bu yazıyı olayı gerek İngilizce takip edemeyenler için gerekse örnek teşkil eden bir konunun kaybolmaması için buraya eklemek istedim.</p>
