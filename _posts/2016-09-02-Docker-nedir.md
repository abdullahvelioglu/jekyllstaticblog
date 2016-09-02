---
layout: post
title: Docker Nedir?
tags: [linux]
---








<p class="p3"><strong><span class="s1">Motivasyon</span></strong></p>
<p class="p1"><span class="s1">Bu yazıyı okumaya başlamadan veya okumaya devam ederken aşağıdaki iki videoyu (özellikle de ilkini) izlemeniz kesinlikle tavsiye edilir. Linkler ve açıklamalar aşağıda.</span></p>
<ul class="ul1">
<li class="li1"><span class="s3"><a href="https://www.youtube.com/watch?v=wW9CAH9nSLs"><span class="s1">İlk video</span></a></span><span class="s1">‘da (5:21) Docker’ın fikir babası ve uygulayıcısı pek muhterem üstad Solomon Hykes’ın 21 Mart 2013’te Docker’ı ilk defa bir topluluk önünde demo etme görüntüleri var. Ecnebiler enteresan tabii, adam (Solomon) teknoloji dünyasını değiştirecek, 5 dakikası doldu diye adamın önce elini ayağına karıştırtıyorlar (hello world yerine hello wowlrd yazıyor). Prensip başka bir şey tabi. 🙂</span></li>
<li class="li1"><span class="s3"><a href="https://www.youtube.com/watch?v=3N3n9FzebAA"><span class="s1">İkinci video</span></a></span><span class="s1">‘da (20:47) yine Solomon Hykes, Docker’ı neden geliştirdiklerini çok sade ve vurucu bir biçimde anlatıyor.</span></li>

</ul>

<p class="p3"><strong><span class="s1">Doğuş Hikayesi</span></strong></p>
<p class="p4"><span class="s1">Tarihçe</span></p>
<p class="p1"><span class="s1">Klasik olarak bir tanımla başlamamız gerekirse Docker, dünyada en çok kullanılan yazılım konteynerleştirme platformudur. Konteynerleştirme konteyner içine koyma anlamına gelir. Docker, Linux Kernel’e 2008 yılında eklenen Linux Containers (LXC) üzerine kurulu bir teknolojidir. LXC, Linux’da aynı işletim sistemi içerisinde birbirinden izole olmuş bir biçimde çalışan Container’lar (Linux tabanlı sistemler) sağlamaktadır. Anlaşıldığı üzere LXC, işletim sistemi seviyesinde bir sanallaştırma (virtualization) altyapısı sunmaktadır. Container’lar içerisinde aynı işletim sistemi tarafından çalıştırılan process’lere, LXC tarafından işletim sisteminde sadece kendileri koşuyormuş gibi düşünmeleri için bir sanallaştırma ortamı sağlanmıştır. LXC, Container’lara işletim sistemi tarafından sunulan dosya sistemi, ortam değişkenleri (Environment Variable), vb fonksiyonları her bir Container’a özgü olarak sağlar. Aynı işletim sistemi içerisinde çalışmalarına rağmen Container’lar birbirlerinden izole edilmişlerdir ve birbirleri ile istenmediği müddetçe iletişime geçemezler. İletişim kısıtlamasının bir amacı da Container’larının güvenliğini aynı Host üzerindeki diğer Container’lara karşı da korumaktır. Bütün bu özelliklerin nasıl pek yararlı fonksiyonlara dönüştürüleceği noktasına birazdan geleceğiz. Biraz daha LXC, Docker ve klasik sanallaştırma üzerinden devam edelim.</span></p>
<p class="p1"><span class="s1">VMware, Xen, Hyper-V gibi Hypervisor’ler (sanallaştırma platformları), yönettikleri fiziksel veya sanal bilgisayarlar üzerine farklı işletim sistemleri kurulmasına olanak tanımaktadırlar. Günümüzde veri merkezleri (data center) çok büyük oranda sayılan Hypervisor’ler tarafından sanallaştırılmışlardır, Cloud (Bulut) olarak adlandırılan kavramın altyapı kısmını oluşturan geniş veri merkezleri tamamıyla Hypervisor’ler tarafından yönetilmektedir. Hypervisor platformları sayesinde fiziksel olarak işletilen güçlü sunucular, ihtiyaç ölçüsünde farklı işletim sistemleri (kimi zaman hem Windows hem de Linux aynı fiziksel sunucuda) kurularak kolaylıkla işletilebilmektedir. Sanallaştırılan farklı işletim sistemlerinin, Hypervisor tarafından fiziksel sunucu üzerinde kendisine sağlanan disk bölümlerine kurulması gerekmektedir. LXC’nin Hypervisor’e göre sağladığı avantajların en önemlilerinden birisi aynı işletim sistemi içerisinde sunabilmesidir. Hypervisor bazlı sanal sunucuların hepsinin kendine ait Guest işletim sistemi bulundurması gereklidir, LXC’de ise Container’lar Host’un işletim sistemini kullanırlar yani bir işletim sistemini ortak olarak kullanırlar. Bahsedilen çerçevede Virtual Machine (Sanal Sunucu) ve Docker Container’ların yapısı aşağıdaki gibidir.</span></p>
<div style="width: 454px" class="wp-caption alignnone"><img class="" src="http://www.abdullahvelioglu.com/blog/public/images/docker1.png" width="444" height="340" /><h5 align="center">Sanal Sunucu Mimarisi</h5></div>
<p>&nbsp;</p>
<div style="width: 454px" class="wp-caption alignnone"><img class="" src="http://www.abdullahvelioglu.com/blog/public/images/docker2.png" width="444" height="340" /><h5 align="center">Docker Container Mimarisi</h5></div>
<p class="p2"><span style="line-height: 1.5;">Container teknolojisi ile Hypervisor teknolojisine göre sanallaştırma için gerekli disk alanından önemli bir tasarruf sağlanmaktadır. Sanal olarak koşturulan işletim sistemlerinin her birinin 7GB disk alanı, 2GB RAM ve 1 Core gerektirdiğini düşünelim. Hypervisor’lerle 64 core’luk işlemciye sahip bir bilgisayara 20 adet sanal sunucu kurmak istediğimizde 20 x 7GB = 140GB bir disk alanı, 20 x 2GB = 40GB RAM ve 20 x 1 = 20 Core’a ihtiyacımız olacaktır ve bu kaynakların tamamı sadece işletim sistemi için kullanılacak olan kaynaklardır. 20 adet sanal sunucu kurmak yerine LXC ile sanallaştırma yaptığımızda ise sadece 7GB’lık bir disk alanı, 2GB RAM ve 1 Core bize yeterli olacaktır.</span></p>
<p class="p1"><span class="s1">Hyporvisor’lerle yapılan sanallaştırma her bir işletim sisteminin ayrı ayrı bakımının (güncellemelerin ve güvenlik yamalarının) yapılması gerekmektedir. Tek işletim sistemi içerisinde LXC kullanılarak yapılan sanallaştırmada ise bir işletim sisteminin bakımı yapılarak daha ekonomik bir yapı sunulur. LXC ile Hyporvisor’ler arasındaki farklar biraz daha uzatılabilir ancak bizi esas konumuzdan uzaklaştırır. Temel olarak LXC, Container açısından standart bir Linux kurulumundan hiçbir farklı olmayan fakat aynı çekirden (kernel) üzerinde koşan bir ortam sağlamaktadır. LXC 2008 yılında ortaya çıkmasına ve kendisine farklı alanlarda ciddi kullanım alanı bulmasına rağmen onu hakettiği geniş kitlelerle buluşturan 2013 yılında ortaya çıkan Docker’dır.</span></p>
<p class="p4"><strong><span class="s1">LXC’den Docker’a Geçiş</span></strong></p>
<p class="p1"><span class="s1">Açık konuşmak gerekirse Docker, LXC’nin zengin mirasının üzerine oturmuştur fakat LXC’de manuel olarak yapılan işlemleri ustaca paketleyerek standardize etmiştir. Docker, LXC’nin sunduğu kapsamlı fonksiyonları ve konfigürasyonları detaylarından arındırarak tabiri caizse halka indirmiştir. Docker’ın getirdiği en önemli özellik Container’ın yapısını metin bazlı Image formatı ile (detaylarına sonradan değineceğiz) tanımlamasıdır. Bu sayede aynı Image formatı kullanılarak aynı özellikteki Container’lar kolaylıkla yaratılabilir, başka kişilerle Docker Registery üzerinden paylaşılabilir ve kolaylıkla genişletilebilir. Image’lar katmanlar şeklinde organize edildiği için Image’da meydana gelecek değişikliklerde Image’ın güncellenmesi sadece belirli katmanları etkileyeceğinden Image’ların güncellenme maliyetleri minimum düzeydedir. Docker’ın LXC’ye göre getirdiği temel farklılıklardan bir başkası Docker’ın kullanıcılarını aynı Container’da sadece ve sadece tek process çalıştırmaya adeta zorlamasıdır. Birçoğumuz aşağıdaki caps’i görmüşüzdür. Kod silerek bug çözdüğünü iddia eden bir çocuk var. Aslında burada Docker’ın yaptığı da benzer bir şey bana göre. Docker, LXC’nin kullanıcıya sunduğu geniş ve kullanması zor fonksiyonları daraltarak aslında daha kullanılabilir ve daha çok işe yarar bir yapı elde etmiştir. Aynı Container’ın birden çok process yerine tek process çalıştırması Container’ların tekrar tekrar, kolaylıkla, genişletilebilir ve daha anlaşılabilir bir biçimde kullanılmasını sağlamaktadır. Bu kısmı ilerleyen bir sonraki yazıda detaylı bir şekilde defalarca örnekleyeceğiz, şimdilik küçük bir örnek olarak, oluşturacağımız sistemde bir web server, bir app server ve bir database server olduğunu düşünelim. Docker’ın önerdiği yapı bu üç bileşenin tek bir Container içine konması yerine ayrı ayrı Container’larda çalıştırılmasıdır.</span></p>
<p class="p1"><img class="alignnone" src="http://www.abdullahvelioglu.com/blog/public/images/docker3.jpg" width="400" height="400" /></p>
<p class="p1"><span class="s1">Ayrı ayrı Container’lar içinde çalıştırılan bileşenler (app server, web server, vb) gerektiği durumlarda teker teker genişletilebilir. Örneğin web server’ın istekleri karşılamada yetersiz olduğu görülürse web server Container’ından bir veya daha fazla ekstra Container yaratılarak gerekli işlem gücü diğer bileşenlerden (app server ve database server) bağımsız olarak sağlanmış olur. Eğer üç bileşeni aynı Container’a koysaydık ek web server isteğinde bu üç bileşeni birden içeren yeni bir Container’ı ayağa kaldırıp burada sadece web server’ın çalışması için gerekli konfigürasyon ve kod değişikliğinin yapılması gerekecekti. Bu yapı aslında gün geçtikçe daha da popüler hale gelen Microservices trendini de destekleyici bir özelliktir. Microservices’ler temellerini 1970’lerde Unix’ten “Do one thing and do it well” yani “Sadece bir şey yap ve iyi yap” olarak tercüme edilebilecek felsefeden almaktadır. Unix/Linux komut satırı fonksiyonlarını detaylı bir biçimde kullananlar ne demek istediğimi eminim daha iyi anlamışlardır. Docker Container’lar tam olarak bunu yapmaya zorlanmaktadır, sadece bir işi yapmak ve o işi iyi yapmak.</span></p>
<p class="p1"><span class="s1">Son olarak Docker geliştirmesinin en başlarında bence çok doğru bir kararla LXC bağımlılığını kaldırarak kendi bünyesinde LXC’yi yeniden kodlayarak </span><span class="s4">libcontainer</span><span class="s1"> adında kendisi ile birlikte dağıtmaya başlamıştır. Bu kararı almalarındaki en önemli iki neden Docker’ın hızlı geliştirilebilmesi için Linux Kernel’den ayrı ve kararları Linux Çekirdeği geliştiricileri yerine kendilerinin alabileceği bir proje yaratmak ve mümkün olduğunca Linux Distro bağımlılıklarını kaldırmak olarak sıralanabilir. Bu konuyu daha fazla uzatmadan burada bağlayarak devam edelim.</span></p>
<p class="p3"><strong><span class="s1">Kurulum ve Mimari</span></strong></p>
<p class="p1"><span class="s1">Başlık biraz yanıltıcı olabilir. Docker’ın kurulum detayları aşağıdaki linklerde çok detaylı ve ek izaha gerek bırakmayacak kadar güzel açıklanmıştır. Kullanıdığınız platforma göre aşağıdaki linklerden kurulum yapabilirsiniz. Burada biz biraz büyük resmi göstermeye çabalayacağız.</span></p>
<p class="p4"><span class="s1">Kurulum</span></p>
<ul class="ul1">
<li class="li2"><a href="https://docs.docker.com/engine/installation/windows"><span class="s1">Windows</span></a></li>
<li class="li2"><a href="https://docs.docker.com/engine/installation/mac/"><span class="s1">Mac OS X</span></a></li>
<li class="li2"><a href="https://docs.docker.com/engine/installation/"><span class="s1">Linux</span></a></li>
</ul>
<p class="p4"><span class="s1">Mimari</span></p>
<p class="p1"><span class="s1">Baştan beri Docker’ın Linux Kernel’inden destek alarak ortaya çıkan ve Linux İşletim Sistemi üzerinde çalışan bir sistem olduğunu yazdık. Peki nasıl oluyor da Docker Linux dışında hem Windows hem de Mac OS X’te kullanılabiliyor? Docker temel iki parçadan oluşmaktadır. Birincisi Linux Kernel’la direkt iletişim halinde olan Docker Daemon, ikincisi ise bu Daemon (Motor) ile iletişim kurmamıza olanak tanıyan Docker CLI (Command-Line Interface)’dır. Linux’ta hem Docker Daemon hem de Docker CLI doğal olarak direkt Linux üzerinde koşmaktadır. Windows ve Mac OS X’te ise Docker CLI Windows ve Mac OS X işletim sistemleri üzerinde koşmakta, Docker Daemon ise bu işletim sistemlerinde bir Hypervisor (duruma göre VMware, VirtualBox, Hyperkit, Hyper-V) yardımıyla çalıştırılan Linux üzerinde koşmaktadır.</span></p>
<p class="p1"><span class="s1">Windows ve Mac OS X’te (konfigüratif olarak aynı zamanda Linux’ta da) Docker CLI ve Docker Daemon TCP ile haberleşmektedirler. Docker CLI’dan verilen komutlar TCP ile Engine’e iletilmekte ve işlenip cevaplanmaktadır. Aralarında TCP haberleşmesi bulunduğundan aralarında TCP bağlantısı kurulabilen herhangi bir Docker CLI (Client) ile Docker Daemon’i konuşturmak mümkündür. İşte anlatılan bu yöntemle Windows ve Mac OS X’te Docker çalıştırmak mümkün hale gelmektedir. Bu kadar anlatmışken Linux’ta default olarak aynı makine üzerindeki CLI ile Engine’in Unix Socket’ler üzerinden konuştuğunu ve daha hızlı çalıştığını vurgulamakta fayda var.</span></p>
<p class="p1"><span class="s1">Windows ve Mac OS X’teki mimari aşağıdaki şekilde resmedilmiştir.</span></p>
<p class="p1"><img class="alignnone" src="http://www.abdullahvelioglu.com/blog/public/images/docker4.svg" width="336" height="427" /></p>
<p class="p3"><strong><span class="s1">Terminoloji</span></strong></p>
<p class="p1"><span class="s1">Docker yepyeni ve Linux bazlı bir teknoloji olduğu için hem kendi terimleri hem de bazı Linux terimleri birçoğumuza ilk bakışta biraz yabancı gelecek fakat çabucak ısınacaksınız.</span></p>
<p class="p4"><strong><span class="s1">Container</span></strong></p>
<p class="p1"><span class="s1">Docker Daemon tarafından Linux çekirdeği içerisinde birbirinden izole olarak çalıştırılan process’lerin her birine verilen isimdir. Virtual Machine (Sanal Makina) analojisinde Docker’ı Hypervisor’e benzetirsek fiziksel sunucu üzerinde halihazırda koşturulmakta olan her bir işletim sisteminin (sanal sunucunun) Docker’daki karşılığı Container’dır. Container’lar milisaniyeler içerisinde başlatılabilir, istenen herhangi bir anda duraklatılabilir (Pause), tamamen durdurulabilir (Stop) ve yeniden başlatılabilirler.</span></p>
<p class="p4"><strong><span class="s1">Image ve Dockerfile</span></strong></p>
<p class="p1"><span class="s1">Docker Daemon ile çalıştırılacak Container’ların baz alacağı işletim sistemi veya başka Image’ı, dosya sisteminin yapısı ve içerisindeki dosyaları, koşturacağı programı (veya bazen çok tercih edilmemekle birlikte programları) belirleyen ve içeriği metin bazlı bir Dockerfile (yazımı tam olarak böyle, ne dockerfile ne DockerFile ne de DOCKERFILE) ile belirlenen binary’ye verilen isimdir.</span></p>
<p class="p1"><span class="s1">Hatırlarsanız Docker’ın doğuşunu anlattığımız ilk bölümde, Docker’ın oyunu değiştiren bir hamle yaparak LXC’ye göre fonksiyon kıstığını ve böylece başarılı olduğunu söylemiştik. İşte Docker, koşturulacak Container’ların iskeletini oluşturan her bir Image’ın bir Dockerfile ile tanımlanmasını gerekli kılar. Bu Dockerfile içerisinde Image’ın hangi Image’ı baz aldığı (miras aldığı), hangi dosyaları içerdiği ve hangi uygulamayı hangi parametrelerle koşturacağı açık açık verilir. Dockerfile’ın içeriğini ve yeni bir Dockerfile dolayısıyla da yeni bir Image oluşturmayı <a href="#"><span class="s2">bir sonraki</span></a> yazımız’da ele alacağız.
<p class="p4"><strong><span class="s1">Docker Daemon (Docker Engine)</span></strong></p>
<p class="p1"><span class="s1">Docker ekosistemindeki Hypervisor’ün tam olarak karşılığıdır. Linux Kernel’inde bulunan LXC’nin yerini almıştır. İşlevi Container’ların birbirlerinden izole bir şekilde, Image’larda tanımlarının yapıldığı gibi çalışmaları için gerekli yardım ve yataklığı yani ortamı sağlamaktır. Container’ın bütün yaşam döngüsünü, dosya sistemini, verilen CPU ve RAM sınırlamaları ile çalışması vb bütün karmaşık (işletim sistemine yakın seviyelerdeki) işlerin halledildiği bölümdür.</span></p>
<p class="p4"><strong><span class="s1">Docker CLI (Command-Line Interface) &#8211; Docker İstemcisi</span></strong></p>
<p class="p1"><span class="s1">Kullanıcının Docker Daemon ile konuşabilmesi için gerekli komut setini sağlar. Registry’den yeni bir Image indirilmesi, Image’dan yeni bir Container ayağa kaldırılması, çalışan Container’ın durdurulması, yeniden başlatılması, Container’lara işlemci ve RAM sınırlarının atanması vb komutların kullanıcıdan alınarak Docker Daemon’e teslim edilmesinden sorumludur. Bu yazının ilerleyen bölümlerinde sık sık Docker CLI’ı kullanarak Docker’ı tanımaya devam edeceğiz.</span></p>
<p class="p4"><strong><span class="s1">Docker Registery</span></strong></p>
<p class="p1"><span class="s1">Zaten bir teknoloji harikası olan Docker’ı daha da kullanılabilir ve değerli kılan bir özellik bütün açık kaynak sistemler gibi paylaşımı özendirmesi, adeta işin merkezine koymasıdır. <a href="https://hub.docker.com/"><span class="s2">DockerHub</span></a>‘da topluluğun ürettiği Image’lar ücretsiz ve sınırsız indirilebilir, oluşturulan yeni Image’lar gerek topluluk ile gerekse kişisel veya şirket referansı için açık kaynaklı (ücretsiz) veya kapalı kaynaklı (ücretli) yüklenebilir ve sonradan indirilebilir. Cloud’da hizmet veren DockerHub’ın yanında Image’larını kendi Private Cloud’unda tutmak isteyenler için Docker’ın sunduğu Private Registery hizmeti de vardır.</span></p>
<p class="p1"><span class="s1">Sözün özü Container’lar Image’lardan oluşturulur. Image’larsa ortak bir eforun sonucu olarak meydana gelir ve Docker Registery’lerde tutulur. Örnek olarak, Ubuntu’nun üreticisi <a href="http://www.canonical.com/"><span class="s2">Canonical</span></a> DockerHub’da Official Repository’ler tutmakta ve Ubuntu versiyonlarını <a href="https://hub.docker.com/r/library/ubuntu/"><span class="s2">bu repository</span></a>‘lerde yayınlamaktadır. Ubuntu Image’ını kullanarak bir Container oluşturmak isteyen kişiler direkt olarak bu Image’ı kullanabilirler. İkinci bir kullanım senaryosu olarak, sağlanan bu Ubuntu Image’ını kullanarak başka bir işlev gerçekleştiren, örneğin Nginx ile statik web server hizmeti veren, bir Image yaratıp bunu DockerHub’da yayınlamak, yani hem kendi hem de başkalarının kullanımına sunmak verilebilir.</span></p>
<p class="p4"><span class="s1">Docker Repository</span></p>
<p class="p1"><span class="s1">Bir grup Image’ın oluşturduğu yapıdır. Bir repository’deki değişik Image’lar Tag’lanarak etiketlenir böylece değişik versiyonlar yönetilebilir. İlerleyen bölümlerde Image versiyonlama konusunda örnekler vereceğiz.</span></p>
<p class="p3"><strong><span class="s1">Docker CLI &#8211; Uzun Bir Tur</span></strong></p>
<p class="p1"><span class="s1">Bu bölümde Docker CLI’ı kullanarak yukarıda anlattığımız bileşenler ve terminolojileri örnekleyerek pekiştirmeye çalışacağız. Komutlar Mac OS X’te çalıştırıp çıktıları paylaşılacaktır ancak bütün komutlar Windows ve Linux sistemlerde de aynen çalışacaktır fakat üzerinde çalışılan sisteme göre farklı çıktılar üretecektir.</span></p>
<ol>
<li><span class="s1">Öncelikle Docker kurulumumuzun doğru çalışıp çalışmadığını kontrol edebilmek için </span><span class="s4">docker version</span><span class="s1"> komutunu verin.</span></li>
</ol>
<pre style="padding-left: 120px;"><span class="s1">
 </span><span class="s5"> abdullah-asusN550JV:~ abdullah$ docker version</span>

<span class="s1"> Client:</span>

<span class="s1"> Version:<span class="Apple-converted-space">      </span>1.12.0</span>

<span class="s1"> API version:<span class="Apple-converted-space">  </span>1.24</span>

<span class="s1"> Go version: <span class="Apple-converted-space">  </span>go1.6.3</span>

<span class="s1"> Git commit: <span class="Apple-converted-space">  </span>8eab29e</span>

<span class="s1"> Built:<span class="Apple-converted-space">        </span>Fri Sep 01 21:04:48 2016</span>

<span class="s1"> OS/Arch:<span class="Apple-converted-space">      </span>linux/amd64</span>

<span class="s1"> Experimental: true</span>

<span class="s1"> Server:</span>

<span class="s1"> Version:<span class="Apple-converted-space">      </span>1.12.0</span>

<span class="s1"> API version:<span class="Apple-converted-space">  </span>1.24</span>

<span class="s1"> Go version: <span class="Apple-converted-space">  </span>go1.6.3</span>

<span class="s1"> Git commit: <span class="Apple-converted-space">  </span>8eab29e</span>

<span class="s1"> Built:<span class="Apple-converted-space">        </span>Fri Sep 01 21:04:48 2016</span>

<span class="s1"> OS/Arch:<span class="Apple-converted-space">      </span>linux/amd64</span>

<span style="line-height: 1.5;">Experimental: true</span></pre>
<p><span class="s1"> Çıktıtan görebileceğiniz üzere </span><span class="s4">docker version</span><span class="s1"> komutu hem Client (Docker CLI) hem de Server (Docker Daemon) için ayrı ayrı versiyon bilgisi dönmektedir.
<p><span class="s1">2. İlk adımda Docker kurulumumuzun başarılı olduğu tespitini yaptıktan sonra <a href="http://hubs.docker.com/"><span class="s2">DockerHub</span></a>‘dan ilk Image’ımızı download edelim ve Image’ımızı listeleyelim.<br />
</span></p>
<p><span class="s4">hello-world</span><span class="s1"> isimli Image’ın DockerHub’dan bir kopyasını indirmek için </span><span class="s4">docker pull hello-world</span><span class="s1"> komutunu verin. Aşağıdaki gibi bir çıktı elde etmelisiniz.</span></p>
<p style="padding-left: 60px;"><span class="s1"><br />
</span><span class="s5"> abdullah-asusN550JV:~ abdullah$ docker pull hello-world</span></p>
<p style="padding-left: 60px;"><span class="s1"> Using default tag: latest</span></p>
<p style="padding-left: 60px;"><span class="s1"> latest: Pulling from library/hello-world</span></p>
<p style="padding-left: 60px;"><span class="s1"> c04b14da8d14: Pull complete</span></p>
<p style="padding-left: 60px;"><span class="s1"> Digest: sha256:0256e8a36e2070f7bf2d0b0763dbabdd67798512411de4cdcf9431a1feb60fd9</span></p>
<p style="padding-left: 60px;"><span class="s1"> Status: Downloaded newer image for hello-world:latest</span></p>
<p><span class="s5"><br />
</span><span class="s1"><br />
Dikkat ettiyseniz </span><span class="s4">hello-world</span><span class="s1"> Image’ı için herhangi bir versiyon belirtmedik. Bu sebeple Docker, ilk satırda, </span><span class="s4">latest</span><span class="s1"> Tag’li Image’ı seçip download ediyor. Sonra da Image’ın SHA256 Hash’ini (Digest) alarak onu ekranda gösteriyor.</span></p>
<p><span class="s1"><br />
</span><span class="s4">docker images</span><span class="s1"> komutunu verin, daha önceden başka bir Image indirmediyseniz aşağıdakine benzer bir çıktı elde etmeniz gerekir.</span></p>
<p style="padding-left: 60px;"><span class="s1"><br />
</span><span class="s5"> abdullah-asusN550JV:~ abdullah$ docker images</span></p>
<p style="padding-left: 60px;"><span class="s1"> REPOSITORY<span class="Apple-converted-space">                </span>TAG <span class="Apple-converted-space">                </span>IMAGE ID<span class="Apple-converted-space">            </span>CREATED <span class="Apple-converted-space">            </span>SIZE</span></p>
<p style="padding-left: 60px;"><span class="s1"> hello-world <span class="Apple-converted-space">              </span>latest<span class="Apple-converted-space">              </span>c54a2cc56cbb<span class="Apple-converted-space">        </span>5 weeks ago <span class="Apple-converted-space">        </span>1.848 kB</span></p>
<p>&nbsp;</p>
<p><span class="s1">3. Şimdi indirdiğimiz </span><span class="s4">hello-world</span><span class="s1"> Image’ını çalıştırarak bir Container yaratalım. </span><span class="s4">docker run hello-world</span><span class="s1"> komutunu verin. Önceki adımları eksiksiz tamamladıysanız aşağıdakine benzer bir çıktı elde etmeniz gerekir.</span></p>
<p style="padding-left: 60px;"><span class="s1"><br />
</span><span class="s5"> abdullah-asusN550JV:~ abdullah$ docker run hello-world</span></p>
<p style="padding-left: 60px;"><span class="s1"> Hello from Docker!</span></p>
<p style="padding-left: 60px;"><span class="s1"> This message shows that your installation appears to be working correctly.</span></p>
<p style="padding-left: 60px;"><span class="s1"> To generate this message, Docker took the following steps:</span></p>
<p style="padding-left: 60px;"><span class="s1"> 1. The Docker client contacted the Docker daemon.</span></p>
<p style="padding-left: 60px;"><span class="s1"> 2. The Docker daemon pulled the &#8220;hello-world&#8221; image from the Docker Hub.</span></p>
<p style="padding-left: 60px;"><span class="s1"> 3. The Docker daemon created a new Container from that image which runs the</span></p>
<p style="padding-left: 60px;"><span class="s1"> <span class="Apple-converted-space">    </span>executable that produces the output you are currently reading.</span></p>
<p style="padding-left: 60px;"><span class="s1"> 4. The Docker daemon streamed that output to the Docker client, which sent it</span></p>
<p style="padding-left: 60px;"><span class="s1"> <span class="Apple-converted-space">    </span>to your terminal.</span></p>
<p style="padding-left: 60px;"><span class="s1"> To try something more ambitious, you can run an Ubuntu Container with:</span></p>
<p style="padding-left: 60px;"><span class="s1"> $ docker run -it ubuntu bash</span></p>
<p style="padding-left: 60px;"><span class="s1"> Share images, automate workflows, and more with a free Docker Hub account:</span></p>
<p style="padding-left: 60px;"><span class="s1"> https://hub.docker.com</span></p>
<p style="padding-left: 60px;"><span class="s1"> For more examples and ideas, visit:</span></p>
<p style="padding-left: 60px;"><span class="s1"> https://docs.docker.com/engine/userguide/</span></p>
<p><span class="s5"><br />
</span><span class="s1"><br />
Aslında çıktıda ne olup bittiği özetleniyor fakat biz bu Image’ı hazırlayanların düşündüğünden farklı hareket ettiğimiz için çıktıda belirtilen 1 ve 2 numaralı işlemleri biz bir önceki adımda </span><span class="s4">docker pull hello-world</span><span class="s1"> adımı ile tamamlamıştık. Image’ı hazırlayanlar önce </span><span class="s4">docker pull hello-world</span><span class="s1"> yerine direkt </span><span class="s4">docker run hello-world</span><span class="s1"> komutunu çalıştıracağımızı öngörmüşler. </span><span class="s4">docker run</span><span class="s1"> Image eğer daha önceden Pull edilmediyse öncelikle Image’ı Pull etmekte ve sonra çalıştırmaktadır.<br />
</span><span class="s4">docker run hello-world</span><span class="s1"> komutunu verdiğimizde Daemon ilgili Image’dan yeni bir Container oluşturdu ve Container’ı çalıştırmaya başladı. Container da yukarıda okuduğumuz çıktıyı oluşturdu ve bu çıktı Daemon’dan Client’a gönderildi ve ekrana basıldı.</span></p>
<p><span class="s1"><br />
Burada yavaş yavaş Docker gerçekleri ile yüzleşmeye başlıyoruz. Farklı bir açıdan bakarak olayı tekrar yorumlarsak aslında </span><span class="s4">hello-world</span><span class="s1"> Image’ının tek işlevinin yukarıdaki </span><span class="s4">Hello from Docker!</span><span class="s1"> ile başlayan çıktıyı oluşturmak olduğunu söyleyebiliriz. Bu Image tam olarak Docker’ın esansını (essence) ortaya koymaktadır. Her bir Image tek bir iş yapmak üzere hazırlanır, çalıştırıldığında o işi bir kere (</span><span class="s4">hello-world</span><span class="s1"> Image’ının yaptığı gibi) ya da sürekli olarak (bir web sunucunun yapacağı gibi) yapar. İlerleyen bölümlerde bu konunun üzerinde çok çok detaylı duracağız çünkü burası bütün meselenin esansı, burayı anlarsak kalan kısımları anlamakta zorlanmayız.</span></p>
<p><span class="s1">4. Bu adımda çalıştırdığımız Container ile ilgili biraz bilgi edinmeye çalışalım. </span><span class="s4">docker ps</span><span class="s1"> komutunu vererek çalışan Container’ları listeleyebiliriz. Bu komutu vererek devam edelim.<br />
</span><span class="s5"> abdullah-asusN550JV:~ abdullah$ docker ps</span></p>
<p style="padding-left: 60px;"><span class="s1"> CONTAINER ID<span class="Apple-converted-space">        </span>IMAGE <span class="Apple-converted-space">              </span>COMMAND <span class="Apple-converted-space">            </span>CREATED <span class="Apple-converted-space">            </span>STATUS<span class="Apple-converted-space">              </span>PORTS <span class="Apple-converted-space">              </span>NAMES</span></p>
<p><span class="s5"><br />
</span><span class="s1"><br />
Eğer her şeyi doğru yaptıysanız siz de terminal ekranında sadece başlıkları görmelisiniz. Bu çıktıda bir hata yok çünkü </span><span class="s4">hello-world</span><span class="s1"> Container’ımız bir kereye mahsus çalıştı, kendisine verilen misyonu (ekrana metin yazdırma) tamamladı ve çıktı (exited).</span></p>
<p><span class="s1"><br />
Çalıştırılan koşan ve çıkış (exit) yapan Container’ları görmek için </span><span class="s4">docker ps -a</span><span class="s1"> komutunu kullanabiliriz, kullanalım ve çıktıya bakalım.</span></p>
<p style="padding-left: 90px;"><span class="s1"><br />
</span><span class="s5"> abdullah-asusN550JV:~ abdullah$ docker ps -a</span></p>
<p style="padding-left: 90px;"><span class="s1"> CONTAINER ID<span class="Apple-converted-space">        </span>IMAGE <span class="Apple-converted-space">              </span>COMMAND <span class="Apple-converted-space">            </span>CREATED <span class="Apple-converted-space">            </span>STATUS<span class="Apple-converted-space">                      </span>PORTS <span class="Apple-converted-space">              </span>NAMES</span></p>
<p style="padding-left: 90px;"><span class="s1"> e139e975009f<span class="Apple-converted-space">        </span>hello-world <span class="Apple-converted-space">        </span>&#8220;/hello&#8221;<span class="Apple-converted-space">            </span>2 minutes ago<span class="Apple-converted-space">      </span>Exited (0) 2 minutes ago <span class="Apple-converted-space">                      </span>angry_sammet</span></p>
<p><span class="s5"><br />
</span><span class="s1"><br />
Yukarıda görebileceğiniz gibi </span><span class="s4">e139e975009f</span><span class="s1"> ID ile </span><span class="s4">angry_sammet</span><span class="s1"> adında </span><span class="s4">/hello</span><span class="s1"> komutunu çalıştıran bir Container 2 dakika önce koşturulmuş ve 2 dakika önce çıkış yapmış.</span></p>
<p><span class="s1"><br />
Container ile ilgili daha detaylı bilgileri </span><span class="s4">docker inspect &lt;container_id&gt;</span><span class="s1"> yani örneğimizde </span><span class="s4">docker inspect e139e975009f</span><span class="s1"> komutu ile öğrenebiliriz ancak bu çaba bizi bu yazıdaki pragmatik yaklaşımımızdan uzaklaştırır.</span></p>
<p><span class="s1">5. Bir önceki adımda çıkış yapan Container’ı tekrar başlatabiliriz. </span><span class="s4">docker start -a e139e975009f</span><span class="s1"> komutu ile Container’ı tekrar çalıştırın ve çıktıyı gözlemleyin. </span><span class="s4">-a</span><span class="s1"> parametresi stop durumda olan Container’ın tekrar başlatılırken terminal’in (komut satırı input/output’unun) Container’a tekrar attach edilmesinin (bağlanmasının) istendiğini belirtmektedir.</span></p>
<p><span class="s1"><br />
</span><span class="s4">docker start -a e139e975009f</span><span class="s1"> komutunu </span><span class="s4">-a</span><span class="s1"> parametresi olmadan vermeyin deneyelim şimdi yani </span><span class="s4">docker start e139e975009f</span><span class="s1"> komutunu verin. Bu kez ekranda çıktı olmadığını sadece Container ID’nin yani </span><span class="s4">e139e975009f</span><span class="s1"> ekrana tekrar basıldığını göreceksiniz. Bunun anlamı Container’ın başlatıldığı fakat bu kez terminal’in attach edilmediğidir. Peki terminal attach etmediğimiz için Container çalışmadı mı? Hayır çalıştı ve yine aynı çıktıyı üretti. </span><span class="s4">Detached</span><span class="s1"> modda çalışan Container’ların çıktıları </span><span class="s4">docker logs &lt;container_id&gt;</span><span class="s1"> komutu ile görülebilir. </span><span class="s4">docker logs e139e975009f</span><span class="s1"> komutunu vererek çıktıyı gözlemleyin. Çıktıda </span><span class="s4">hello-world</span><span class="s1"> Image’ının çıktısı birden fazla kereler basıldı ise nedenini bakalım bulabilecek misiniz?</span></p>
<p><span class="s1">6. Bu adımda çalıştırdığımız ve birkaç kere tekrar başlattığımız </span><span class="s4">hello-world</span><span class="s1"> Container’ın silmeye çalışalım. </span><span class="s4">docker rm &lt;container_id&gt;</span><span class="s1"> komutu ile çıkış yapmış Container’lar silinebilir. </span><span class="s4">docker rm -f &lt;container_id&gt;</span><span class="s1"> komutu ile yani </span><span class="s4">-f</span><span class="s1"> Force parametresi ile bir Container çalışır durumda bile olsa onu silebiliriz. Force opsiyonunu kullanmak yerine önce </span><span class="s4">docker stop &lt;container_id&gt;</span><span class="s1"> ile Container’ı durdurmayı da seçebiliriz.<br />
</span><span class="s4">docker rm e139e975009f</span><span class="s1"> komutu ile Container’ı silin. Aşağıdakine benzer bir çıktı elde etmelisiniz ve </span><span class="s4">docker ps -a</span><span class="s1"> komutu artık çıktısında hiçbir Container’ı listelememeli.</span></p>
<p style="padding-left: 60px;"><span class="s1"><br />
</span><span class="s5"> abdullah-asusN550JV:~ abdullah$ docker rm e139e975009f</span></p>
<p style="padding-left: 60px;"><span class="s1"> e139e975009f</span></p>
<p><span class="s4">7. hello-world</span><span class="s1"> Image’ı 2MB’ın altında pek fazla faydalı bir şey yapmamıza imkan tanımayan fakat Container yaşam döngüsü ve Docker’ın çalışma prensibini güzel özetleyen bir Image’dı. Şimdi biraz daha göze hoş gelen işlemler yapmak için bir </span><span class="s4">Nginx</span><span class="s1"> Image’ı başlatalım fakat bu kez önce Pull etmek yerine direkt çalıştıralım. Önceki bölümde direkt çalıştırdığımızda Docker’ın önce lokal Image’lara baktığını, eğer istenen Image lokalde yoksa DockerHub’dan çektiğini söylemiştik. </span><span class="s4">Nginx</span><span class="s1"> Image’ını indirmek ve bu Image’dan Image içinde konfigüre edilmiş default web sitesini 8080 nolu portta sunmaya başlamak için </span><span class="s4">docker run -p 8080:80 nginx</span><span class="s1"> komutunu koşturun.<br />
</span><span class="s4">hello-world</span><span class="s1"> Image’ına benzer şekilde </span><span class="s4">Nginx</span><span class="s1"> Image’ının download edildiği sonrasında çalıştırıldığı ve istekler beklemeye başladığını göreceksiniz.<br />
Image’ın download edilmesi bittikten sonra tarayıcınızı açarak adres satırına </span><span class="s4">http://localhost:8080</span><span class="s1"> yazın. Aşağıdaki gibi bir ekran (</span><span class="s4">Nginx</span><span class="s1"> test sayfası) görmelisiniz.<br />
</span></p>
<p>&nbsp;</p>
<p><img class="alignnone" src="http://www.abdullahvelioglu.com/blog/public/images/docker5.png" width="1328" height="576" /></p>
<p><span class="s1"><br />
Şimdiye kadar büyük bir merakla verilen son komuttaki </span><span class="s4">-p 8080:80</span><span class="s1"> parametrelerinin ne anlama geldiğini sormanızı bekliyordum nihayet sordunuz 🙂 </span><span class="s4">-p</span><span class="s1"> parametresi kendisinden sonra verilen parametredeki portlar arasında port forwarding yani port yönlendirme yapar. İlk verilen port, örneğimizde 8080, host üzerindeki portu ikinci verilen port, örneğimizde 80, Container üzerindeki portu temsil eder. Yukarıdaki komutta Docker Daemon’e Host’un 8080 numaralı portuna gelen isteklerin Container’ın 80 numaralı portuna göndermesini ifade ettik. Burada Host tahmin ettiğiniz gibi Docker komutlarını koşturduğumuz bilgisayarımız Container ise yeni oluşturduğumuz </span><span class="s4">Nginx</span><span class="s1"> Container’ıdır.<br />
Burada yine kafamızı kaldıralım ve ne olup bittiğine bir göz atalım. Daha önce yaptığımız gibi yeni bir Image’dan bir Container ürettik, burada enteresan bir şey yok. Host’un 8080 numaralı portuna gelen istekleri Container’ın 80 numaralı port’una yönlendirdik ve Container tarafından sunulan Nginx test sayfasına erişmiş olduk. Peki bu ikinci kısım nasıl gerçekleşti? Yani Nginx Container’ına 80 numaralı port’u dinlemesi gerektiğini kim söyledi ve 80 numaralı port’a gelen request’lerde test sayfasını göndermesini kim salık verdi?<br />
İşte Docker mucizesi yine tam da burada karşımıza çıkmaktadır. Official </span><span class="s4">Nginx</span><span class="s1"> Image’ını hazırlayan arkadaşlar Nginx’i default olarak 80 numaralı portu dinlemeye ve bu porta gelen web isteklerini test web sitesine yönlendirmeye dolayısıyla da test ana sayfasını sunmak üzere ayarlamıştır. Dolayısıyla </span><span class="s4">Nginx</span><span class="s1"> Image’ından oluşturulan Container’ın yegane amacı budur. Bu Nginx Image’ı başka bir görevi, daha anlamlı olarak kendi web sitemizi, sunmak üzere ayarlanabilir. </span></p>
<p><span class="s1">8. Olayı biraz daha ilginçleştirelim ve bir önceki adımda çalıştırdığımız </span><span class="s4">Nginx</span><span class="s1"> Container’ının 80 numaralı portu dinlemeye ve default web site’ı sunmak üzere nasıl ayarlandığına göz atalım.<br />
Yeni bir terminal açarak (mevcut terminalimiz Nginx Container’ına attach durumda olduğu için onu kullanamıyoruz) önceki adımlarda yaptığımız gibi çalışan Container’ları </span><span class="s4">docker ps</span><span class="s1"> komutu ile sorgulayalım. Aşağıdakine benzer bir çıktı elde etmeniz gerekir.<br />
</span><span class="s5"> abdullah-asusN550JV:~ abdullah$ docker ps</span></p>
<p style="padding-left: 60px;"><span class="s1"> CONTAINER ID<span class="Apple-converted-space">        </span>IMAGE <span class="Apple-converted-space">              </span>COMMAND<span class="Apple-converted-space">                  </span>CREATED <span class="Apple-converted-space">            </span>STATUS<span class="Apple-converted-space">              </span>PORTS <span class="Apple-converted-space">                          </span>NAMES</span></p>
<p style="padding-left: 60px;"><span class="s1"> 54bad6cec3c4<span class="Apple-converted-space">        </span>nginx <span class="Apple-converted-space">              </span>&#8220;nginx -g &#8216;daemon off&#8221; <span class="Apple-converted-space">  </span>4 minutes ago <span class="Apple-converted-space">      </span>Up 4 minutes<span class="Apple-converted-space">        </span>443/tcp, 0.0.0.0:8080-&gt;80/tcp <span class="Apple-converted-space">  </span>angry_bell</span></p>
<p><span class="s5"><br />
</span><span class="s1"><br />
Yukarıdaki çıktıdan çalıştırılan Container’ın ID’sinin </span><span class="s4">54bad6cec3c4</span><span class="s1"> olduğu, komutunun </span><span class="s4">nginx -g &#8216;daemon off</span><span class="s1"> ile başladığı (komutun tamamını göremediğimize dikkat edin), 4 dakikadır çalıştığı ve host’un 8080 portundan Container’ın 80 portuna forwarding yapıldığı görülebilir.<br />
Açtığımız bu yeni terminalden Container’a attach olarak bazı komutlar çalıştırarak sistemi deşifre etmeye devam edelim. </span><span class="s4">docker exec -it &lt;container_id&gt; /bin/bash</span><span class="s1"> komutu ile Container’a bir Bash Shell açabiliriz. </span><span class="s4">-i</span><span class="s1"> interaktif terminali </span><span class="s4">-t</span><span class="s1"> ise terminalin attach olmasını istediğimizi belirtir. </span><span class="s4">docker exec -it 54b /bin/bash</span><span class="s1"> komutunu çalıştırın (Container ID’nin sadece baştan birkaç harfini vermemizin yettiğine -çakışma olmadığı müddetçe- dikkat edin). Aşağıdakine benzer bir görüntü elde edeceksiniz. Prompt’un nasıl değiştiğine ve Container ID’yi içerdiğine dikkat edin.<br />
</span><span class="s5"> abdullah-asusN550JV:~ abdullah$ docker exec -it 54b /bin/bash</span></p>
<p style="padding-left: 60px;"><span class="s1"> root@54bad6cec3c4:/# ###### Kullanıcı root oldu bilgisayar adı da Container ID oldu</span></p>
<p style="padding-left: 60px;"><span class="s5"><br />
</span><span class="s1"><br />
Container’ın Bash’inde iken </span><span class="s4">ps -ef</span><span class="s1"> komutunu verin ve Container içinde çalışan bütün process’leri listeleyin. Bende oluşan çıktı aşağıda.</span></p>
<p style="padding-left: 60px;"><span class="s1"><br />
</span><span class="s5"> root@54bad6cec3c4:/# ps -ef</span></p>
<p style="padding-left: 60px;"><span class="s1"> UID<span class="Apple-converted-space">        </span>PID<span class="Apple-converted-space">  </span>PPID<span class="Apple-converted-space">  </span>C STIME TTY<span class="Apple-converted-space">          </span>TIME CMD</span></p>
<p style="padding-left: 60px;"><span class="s1"> root <span class="Apple-converted-space">        </span>1 <span class="Apple-converted-space">    </span>0<span class="Apple-converted-space">  </span>0 00:06 ?<span class="Apple-converted-space">        </span>00:00:00 nginx: master process nginx -g daemon off;</span></p>
<p style="padding-left: 60px;"><span class="s1"> nginx<span class="Apple-converted-space">        </span>6 <span class="Apple-converted-space">    </span>1<span class="Apple-converted-space">  </span>0 00:06 ?<span class="Apple-converted-space">        </span>00:00:00 nginx: worker process</span></p>
<p style="padding-left: 60px;"><span class="s1"> root <span class="Apple-converted-space">        </span>7 <span class="Apple-converted-space">    </span>0<span class="Apple-converted-space">  </span>0 00:07 ?<span class="Apple-converted-space">        </span>00:00:00 /bin/bash</span></p>
<p style="padding-left: 60px;"><span class="s1"> root<span class="Apple-converted-space">        </span>14 <span class="Apple-converted-space">    </span>7<span class="Apple-converted-space">  </span>0 00:13 ?<span class="Apple-converted-space">        </span>00:00:00 ps -ef <span class="Apple-converted-space">   </span></span></p>
<p style="padding-left: 60px;"><span class="s5"><br />
</span><span class="s1"><br />
Gördüğünüz gibi Container tam olarak </span><span class="s4">nginx -g daemon off</span><span class="s1"> ile çalıştırılmış dolayısıyla bir konfigürasyon dosyası verilmemiş. </span><span class="s4">more /etc/nginx/nginx.conf</span><span class="s1"> komutunun çıktısından başka bir konfigürasyon dosyasının (</span><span class="s4">more /etc/nginx/conf.d/default.conf</span><span class="s1">) eklendiğini göreceksiniz. Bu konfigürasyon dosyasının içeriğine baktığınızda sunucunun localhost üzerinde 80 nolu portu dinlediği, root dizin olarak kendisine </span><span class="s4">/usr/share/nginx/html</span><span class="s1"> klasörünü aldığını ve index dosyası olarak index.html ve index.htm dosyalarını sunmak üzere ayarlandığını görebilirsiniz.</span></p>
<p style="padding-left: 60px;"><span class="s1"><br />
</span><span class="s5"> root@54bad6cec3c4:/# more /etc/nginx/conf.d/default.conf</span></p>
<p style="padding-left: 60px;"><span class="s1"> server {</span></p>
<p style="padding-left: 60px;"><span class="s1"> <span class="Apple-converted-space">    </span>listen <span class="Apple-converted-space">      </span>80;</span></p>
<p style="padding-left: 60px;"><span class="s1"> <span class="Apple-converted-space">    </span>server_name<span class="Apple-converted-space">  </span>localhost;</span></p>
<p style="padding-left: 60px;"><span class="s1"> <span class="Apple-converted-space">    </span>location / {</span></p>
<p style="padding-left: 60px;"><span class="s1"> <span class="Apple-converted-space">        </span>root <span class="Apple-converted-space">  </span>/usr/share/nginx/html;</span></p>
<p style="padding-left: 60px;"><span class="s1"> <span class="Apple-converted-space">        </span>index<span class="Apple-converted-space">  </span>index.html index.htm;</span></p>
<p style="padding-left: 60px;"><span class="s1"> <span class="Apple-converted-space">    </span>}</span></p>
<p style="padding-left: 60px;"><span class="s1"> <span class="Apple-converted-space">    </span># redirect server error pages to the static page /50x.html</span></p>
<p style="padding-left: 60px;"><span class="s1"> <span class="Apple-converted-space">    </span>#</span></p>
<p style="padding-left: 60px;"><span class="s1"> <span class="Apple-converted-space">    </span>error_page <span class="Apple-converted-space">  </span>500 502 503 504<span class="Apple-converted-space">  </span>/50x.html;</span></p>
<p style="padding-left: 60px;"><span class="s1"> <span class="Apple-converted-space">    </span>location = /50x.html {</span></p>
<p style="padding-left: 60px;"><span class="s1"> <span class="Apple-converted-space">        </span>root <span class="Apple-converted-space">  </span>/usr/share/nginx/html;</span></p>
<p style="padding-left: 60px;"><span class="s1"> <span class="Apple-converted-space">    </span>}</span></p>
<p style="padding-left: 60px;"><span class="s1"> }</span></p>
<p style="padding-left: 60px;"><span class="s5"><br />
</span><span class="s1"><br />
Son olarak isterseniz </span><span class="s4">more /usr/share/nginx/html/index.html</span><span class="s1"> komutu ile tarayıcıdan gördüğümüz sayfanın kaynak koduna erişebilirsiniz.</span></p>
<p><span class="s4">9. Nginx</span><span class="s1"> Container’ı terminal’e Attached bir şekilde ayağa kalktı. Bu çoğu zaman istenen durum değildir. </span><span class="s4">-d</span><span class="s1"> parametresi ile Container’ı Detached modda çalıştırabilir ve terminali bloklanmaktan kurtarabiliriz. Detached modda çalışan Container’ların ID’lerini </span><span class="s4">docker ps</span><span class="s1"> komutu ile elde edebilir, </span><span class="s4">docker kill &lt;container_id&gt;</span><span class="s1"> komutu ile de Container’ı acil çıkışa zorlayabiliriz.</span></p>
<p class="p1"><span class="s1">Şimdilik bu kısımda anlatacaklarımız bu kadar. Bir sonraki bölümde bulunan Cheat Sheet çok işimize yarayacak.</span></p>
<p class="p3"><strong><span class="s1">Docker’ın Kullanım Alanları ve Çözmeye Aday Olduğu Problemler</span></strong></p>
<p class="p1"><span class="s1">Bu bölüm kısa gelecekte muhtemelen eskiyecek ve yeniden yazıma ihtiyaç duyacaktır fakat gün itibariyle eldeki durumun bir fotoğrafının çekilmesi açısından burada yazılanları kavramak diğer bölümlere göre daha önemlidir. Yazının başında Motivasyon başlığında yer verilen videoların ilkinde Docker’ın fikir babası ve birinci adamı Solomon Hykes aslında projeyi neden ortaya koyduklarını DotCloud üzerinden anlatıyor. Temel olarak söylediği gittikçe artan cloud (bulut) gerensinimlerine cevap vermek üzere kurulan özellikle PaaS sağlayıcılardan biri olan ve Solomon’un da sahibi olduğu DotCloud, Linux Containers (LXC) kullanarak daha az maliyetli, daha performanslı ve daha az down-time’lı bir hizmet sunuyor. İnsanlar Solomon’a nasıl yaptıklarını sorunca Solomon, Linux Kernel’indeki Container desteğinin pek bilinmediği, bilinse bile etkili kullanılamadığı sonucunu çıkarıyor ve yaptıkları kurmaylar toplantısında LXC’yi halka indirmeye karar veriyorlar. Daha önce de yazdığımız gibi Kernel’in sunduğu Container desteğini bir Image formatı ile standardize edip Container’ın etrafında onun bütün yaşam döngüsünü basitleştiren ve yönetimini kolaylaştıran bir ekosistem inşa ediyorlar. Bu işleri o kadar hızlı ve doğru yapıyorlar ki rakipleri daha nefes alamadan neredeyse bitiş çizgisine ulaşıyorlar.</span></p>
<p class="p1"><span class="s1">Yukarıdaki paragrafta Docker projesinin başlatılma gerekçesini küçük yorumlar ekleyerek başlatan kişinin ağzından nakletmeye çalıştım. Tabii Docker belki Solomon’un da en başta hatta ortalarında hayal ettiği çizginin de ötesine geçti, çok farklı alanlarda kendine çok geniş kullanım alanları buldu buluyor. Şimdi biraz bunların üzerinden gidelim.</span></p>
<p class="p4"><strong><span class="s1">Benim Makinemde Çalışıyor (Works on my Machine) Problemine Çözüm Sağlaması</span></strong></p>
<p class="p1"><span class="s1">Yazılım geliştirme işi ile belirli bir süre uğraşan her yazılımcı, en az bir kere sahadan bildirilen problemi kendi geliştirme ortamında tekrarlayamama talihsizliğini yaşamıştır. Geliştirici ortamı ile uygulamanın deploy edildiği saha şartları arasında çoğu durumda gerek ölçek, gerek üzerinde koşulan platformun konfigürasyonu, gerekse de kullanıcı sayısı bakımından büyük farklılıklar bulunmaktadır. Docker’la birlikte uygulamalarımızı Docker altyapısı ile paketlediğimiz için aynı Image’ı hem geliştirici ortamında hem UAT (User Acceptance Test &#8211; Kullanıcı Kabul Test) ortamında ve PROD (Production &#8211; Canlı) ortamda kullanabiliriz. DEV (Development &#8211; Geliştirici) ve UAT ortamlarında sadece tek bir Container’ın çalıştırılması yeterli olacakken PROD ortamda gerektiği kadar Container ayağa kaldırılarak yük bir dengeleyici yardımıyla dağıtılabilir. Docker ile birlikte uygulamamızın koştuğu platformun DEV, UAT ve PROD ortamlarında aynı olmasını sağlamış ve platform farkından kaynaklı değişiklikleri de sıfırlamış oluruz. PROD ortamında Docker Container’da operasyon sırasında yapılmış bir değişiklik kolaylıkla geliştiricinin bilgisayarına yeni bir Image olarak getirebilir ve eğer oluşan problem ilgili değişiklerden kaynaklı ise geliştirici ortamında kolaylıkla tekrarlanabilir hale getirilir.</span></p>
<p class="p4"><strong><span class="s1">Geliştirme Ortamı Standardizasyonu Sağlaması</span></strong></p>
<p class="p1"><span class="s1">Geliştirme ortamları projeden projeye farklılık göstermektedir. Aynı projenin farklı müşterilerde olan kurulumları bile farklı bileşenler içermekte müşterilerin birinde çıkan problemin çözümü için aynı ortamın geliştirici ortamında kurulması bile çok ciddi bir zaman almaktadır. Bazı yazılım evleri, farklı müşterilerde farklı sürümlerde bulunan kurulumları geliştirici ortamlarında tekrarlayabilmek için geliştirici ortamlarını sanal sunucularda tutmaktadır. Bir sanal makinanın ortalama 20GB olduğunu düşünürsek tek bir projenin 5 müşteride kurulu olması halinde her bir geliştiricinin bilgisayarında 100GB’lık bir alan gerekli olacaktır.</span></p>
<p class="p1"><span class="s1">Sanal sunucu temin etmenin kaynak kullanımında yarattığı problemi görmezden geldiğimizde bile geliştirmesi aktif olarak devam eden projelerde her yapısal değişiklikte, web sunucu değişimi, database şema veya referans data değişikliği vb binary formatta olan master sanal makinanın bütün geliştiricilere dağıtılması ve varsa geliştiricilerin kendi özelleştirmelerini bu makinalara tekrar uygulamalarını gerektirmektedir.</span></p>
<p class="p1"><span class="s1">Bir başka geliştirme ortamı problemi de sanal sunucu kullanılmayan geliştirme ortamlarında ekibe yeni katılan kişilerin bilgisayarlarının gerekli araç gereçlerle kurulması işlemi için harcanan zamandır. Bu işlem genellikle ekibin deneyimli bir elemanı tarafından yapılır, bu durumda hem ekibin deneyimli bir elemanının hem de işe yeni başlayan elemanın efektif olarak kullanabilecekleri bir zaman dilimi kaybedilmiş olur.</span></p>
<p class="p1"><span class="s1">Docker’dan önce ortaya çıkan <a href="https://www.vagrantup.com/"><span class="s2">Vagrant</span></a> aslında yukarıda sıralanan bütün bu problemlere sanal sunucu bazlı bir çözüm sunmaktadır. Docker’ın ortaya çıkması ile birlikte Vagrant, sanal sunucu yerine Docker kullanılmasına da imkan sağlamaktadır. Docker-Compose geliştirici ortamının yapısını metin tabanlı olarak tutar ve tek bir komutla </span><span class="s4">docker-compose up</span><span class="s1"> geliştirici ortamını geliştiricinin çalışmasına hazır hale getirebilmektedir.</span></p>
<p class="p4"><strong><span class="s1">Test ve Entegrasyon Ortamı Kurulumu ve Yönetimini Kolaylaştırması</span></strong></p>
<p class="p1"><span class="s1">Popülerleşen DevOps kavramı ile birlikte, CI (Continuous Integration &#8211; Sürekli Entegrasyon) ortamları her geçen gün daha fazla şirket ve geliştirme ekibi tarafından kullanılmaktadır. Docker’ın sağladığı bağımlılığı azaltan fonksiyonlar sayesinde yeni bir Continuous Integration Pipeline oluşturulması ve var olan CI’ların bakımının yapılması kolaylaşmakta ve CI için kullanılan araçlara (Jenkins, Travis CI, vb) bağımlılığı azaltmakta ve farklı CI araçları arasında geçiş yapmayı kolaylaştırmaktadır.</span></p>
<p class="p1"></p>
<p class="p4"><span class="s1">Mikroservis Mimari için Kolay ve Hızlı Bir Şekilde Kullanıma Hazır Hale Getirilebilmesi</span></p>
<p class="p1"><span class="s1">Docker, işletim sistemi çekirdeği seviyesinde bir sanallaştırma sağladığı için Hypervisor’lerle sağlanan sanallaştırmaya göre çok daha maliyetsiz (lightweight) ve hızlı bir sistem sunmaktadır. Hypervisor’lerle kurulan bir sanallaştırma altyapısında yeni bir node’un (sanal makina) sisteme eklenmesi için öncelikle işletim sisteminin hypervisor üzerinde boot edilerek başlatılmasının beklenmesi gerekmektedir. İşletim sisteminin başlatılması için ise ön yükleyicinin (boot loader) işletim sistemini belleğe yüklemesi, sanallaştırılan donanım bileşenlerinin (sanal disk, sanal ekran kartı, vb) kullanıma hazır hale getirilmesi ile işletim sistemi modüllerinin kullanıma hazır hale getirilmesinin beklenmesi gereklidir. Bütün bu işlemler en iyi ihtimalle 20-25 saniye sürmektedir. Docker ile yeni bir node (Container) eklenmesi ise milisaniyeler mertebesinde (50 &#8211; 100 ms) gerçekleştirilebilmektedir.</span></p>
<p class="p1"><span class="s1">Mikroservis mimarilerde kullanım oranları artan servislerin kolaylıkla genişletilebilmesi yani yeni node’ların hızlı bir şekilde sisteme eklenebilmesi ve artık çok fazla kullanılmayan node’ların da hızlı bir şekilde kapatılarak kaynaklarının sisteme iade edilmesi gerekmektedir. Bu özellikler Docker’ın mikroservis mimariler için biçilmiş kaftan olmasını sağlamaktadır.</span></p>
<p class="p1"><span class="s1">Açılıp kapanma performansına ek olarak Docker’ın teşvik ettiği her bir Container içinde sadece bir uygulamanın çalıştırılması zaten mikroservis sistemlerin sahip olması gereken ideal özelliklerin başında gelmektedir. Bir Container içinde sadece bir uygulamanın yani servisin çalıştırılması, ilgili servisin genişletilmesi (yeni node’lar eklenmesi) gerektiğinde, diğer servislerden bağımsız olarak ilgili Image’dan yeni Container’lar oluşturulark maliyet-etkin ve çakışma yaşanmayacak bir biçimde genişleme sağlanmasına da olanak tanımaktadır.</span></p>
<p class="p4"><strong><span class="s1">Kaynakların Etkili ve Efektif Bir Biçimde Kullanılmasını Sağlaması</span></strong></p>
<p class="p1"><span class="s1">Hatırlarsanız tarihçe kısmında Docker’ın Hypervisor’lere göre donanım kaynaklarının nasıl daha etkin kullanılmasını sağlandığını örneklemiştik. Docker’ın uygulamaları birbirinden ayırmak için Hypervisor’ler gibi farklı işletim sistemlerine ihtiyaç duymaması, her bir uygulama için yeni bir işletim sistemi kurulması gereğini ortadan kaldırarak ciddi bir kaynak tasarrufu sağlamıştır.</span></p>
<p class="p1"><span class="s1">Tarihçe bölümünde detaylandırılan ve yukarıda özetlenen özelliğe ek olarak Docker’ın kaynakların daha etkili kullanılması için sağladığı başka fonksiyonlar da vardır. Bilindiği gibi Hypervisor’ler tarafından sağlanan sanal makinaların fiziksel makinalara göre en önemli avantajlarından birisi aynı fiziksel sunucuyu mantıksal parçalara bölerek farklı amaçlar için kullanabilmeleridir. Hypervisor’lerde bulunan bu mekanizma büyük bir avantaj sağlamasının yanında değişen ihtiyaçlara cevap verme noktasında Docker kadar esnek değildir. Aynı fiziksel sunucu üzerinde verilen A, B ve C servislerinden A’nın CPU ihtiyacının arttığını ve artık daha güçlü başka bir sunucuya taşınması gerektiğini düşünelim. Hypervisor teknolojisi ile A sanal sunucusu öncelikle halihazırda çalıştığı fiziksel sunucuda durdurulmalı, yeni sunucusuna kopyalanmalı ve tekrar çalıştırılmalıdır. Taşıma işlemi sırasında uygulama ve data’sının yanında işletim sistemi de taşındığı için bu işlem uzun sürmekte ve genellikle bakım periyodunda (maintenance period) yapılmakta ve değişik ihtiyaçların karşılanması için esnek bir yapı sunmamaktadır. Docker’ın sunduğu sanallaştırma ile Container durdurulur, yeni sunucusuna taşınır ve hızlı bir şekilde yeniden başlatılabilir. Gereken süre Hypervisor’e oranla daha kısa olduğu için değişikliğin yapılması için bakım periyodunun gelmesi beklenmeyebilir.</span></p>
<p class="p4"><strong><span class="s1">Multitenant Sistemlerde Tenancy Mantığını Uygulama Seviyesinden Çıkarmayı Sağlaması</span></strong></p>
<p class="p1"><span class="s1">Docker ile birlikte gelen az maliyetli ve esnek sanallaştırma ile birlikte artık uygulama kodlarının içerisine multitenancy (çok kiracılılık) mantığının konmasına gerek kalmamıştır. Multitenancy aynı uygulamanın birden çok müşteri için sanki farklı Instance’larda koşuyormuş izlenimi veren bir yazılım mimarisidir. Örnek olarak Konferans’lardaki oturum ve katılımcı bilgilerini yöneten bir uygulama, farklı müşterilerin farklı konferansları için tek bir instance’da hizmet verebilir. Her bir müşteri için ayrı birer web sunucu ve/veya uygulama sunucusu kurulması gerekmez böylelikle bakım maliyetleri düşürülür fakat uygulama seviyesinde Tenant’ları (kiracı) birbirinden ayıracak mantıklar (logic)’ler eklemek gerekmektedir ve bu da tahmin edebileceğiniz gibi hataya çok açık bir özelliktir. İşe yeni başlayan bir yazılımcı yeni tasarladığı bir ekranı Multitenancy özelliğini göz önünde bulundurmadan kodlarsa bütün tenant’lar diğer tenant’ların bilgilerini görebilir.</span></p>
<p class="p1"><span class="s1">Docker ile birlikte Tenancy mantığı uygulama kodundan kaldırılabilir. Uygulama sadece tek bir tenant varmış gibi çalışacak şekilde öncekine göre daha basit bir şekilde tasarlanır. Her bir Tenant için ilgili Image’dan yeni bir Container yaratılarak Tenant ile ilişkilendirilir böylece Tenant yönetimi daha karmaşık olan uygulama seviyesinden alınarak platform seviyesine çekilmiş olur ve daha yönetilebilir bir altyapı sağlar.</span></p>
<p class="p3"><strong><span class="s1">Docker CLI &#8211; Cheat Sheet (Kopya Kağıdı)</span></strong></p>
<table class="t1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="td1" valign="middle">
<p class="p1"><span class="s1">Komut</span></p>
</td>
<td class="td2" valign="middle">
<p class="p1"><span class="s1">Açıklaması</span></p>
</td>
</tr>
<tr>
<td class="td1" valign="middle">
<p class="p7"><span class="s1">docker images</span></p>
</td>
<td class="td2" valign="middle">
<p class="p1"><span class="s1">Lokal registery’de mevcut bulunan Image’ları listeler</span></p>
</td>
</tr>
<tr>
<td class="td3" valign="middle">
<p class="p7"><span class="s1">docker ps</span></p>
</td>
<td class="td4" valign="middle">
<p class="p1"><span class="s1">Halihazırda çalışmakta olan Container’ları listeler</span></p>
</td>
</tr>
<tr>
<td class="td1" valign="middle">
<p class="p7"><span class="s1">docker ps -a</span></p>
</td>
<td class="td2" valign="middle">
<p class="p1"><span class="s1">Docker Daemon üzerindeki bütün Container’ları listeler</span></p>
</td>
</tr>
<tr>
<td class="td3" valign="middle">
<p class="p7"><span class="s1">docker ps -aq</span></p>
</td>
<td class="td4" valign="middle">
<p class="p1"><span class="s1">Docker Daemon üzerindeki bütün Container’ların ID’lerini listeler</span></p>
</td>
</tr>
<tr>
<td class="td1" valign="middle">
<p class="p7"><span class="s1">docker pull &lt;repository_name&gt;/&lt;image_name&gt;:&lt;image_tag&gt;</span></p>
</td>
<td class="td2" valign="middle">
<p class="p1"><span class="s1">Belirtilen Image’ı lokal registry’ye indirir. Örnek: </span><span class="s4">docker pull abdullah/jmeter3.0:1.7</span></p>
</td>
</tr>
<tr>
<td class="td3" valign="middle">
<p class="p7"><span class="s1">docker top &lt;container_id&gt;</span></p>
</td>
<td class="td4" valign="middle">
<p class="p1"><span class="s1">İlgili Container’da </span><span class="s4">top</span><span class="s1"> komutunu çalıştırarak çıktısını gösterir</span></p>
</td>
</tr>
<tr>
<td class="td1" valign="middle">
<p class="p7"><span class="s1">docker run -it &lt;image_id|image_name&gt; CMD</span></p>
</td>
<td class="td2" valign="middle">
<p class="p1"><span class="s1">Verilen Image’dan terminal’i attach ederek bir Container oluşturur</span></p>
</td>
</tr>
<tr>
<td class="td3" valign="middle">
<p class="p7"><span class="s1">docker pause &lt;container_id&gt;</span></p>
</td>
<td class="td4" valign="middle">
<p class="p1"><span class="s1">İlgili Container’ı duraklatır</span></p>
</td>
</tr>
<tr>
<td class="td1" valign="middle">
<p class="p7"><span class="s1">docker stop &lt;container_id&gt;</span></p>
</td>
<td class="td2" valign="middle">
<p class="p1"><span class="s1">İlgili Container’ı durdurur</span></p>
</td>
</tr>
<tr>
<td class="td3" valign="middle">
<p class="p7"><span class="s1">docker start &lt;container_id&gt;</span></p>
</td>
<td class="td4" valign="middle">
<p class="p1"><span class="s1">İlgili Container’ı durdurulmuşsa tekrar başlatır</span></p>
</td>
</tr>
<tr>
<td class="td1" valign="middle">
<p class="p7"><span class="s1">docker rm &lt;container_id&gt;</span></p>
</td>
<td class="td2" valign="middle">
<p class="p1"><span class="s1">İlgili Container’ı kaldırır fakat ilişkili Volume’lara dokunmaz</span></p>
</td>
</tr>
<tr>
<td class="td3" valign="middle">
<p class="p7"><span class="s1">docker rm -v &lt;container_id&gt;</span></p>
</td>
<td class="td4" valign="middle">
<p class="p1"><span class="s1">İlgili Container’ı ilişkili Volume’lar ile birlikte kaldırır</span></p>
</td>
</tr>
<tr>
<td class="td1" valign="middle">
<p class="p7"><span class="s1">docker rm -f &lt;container_id&gt;</span></p>
</td>
<td class="td2" valign="middle">
<p class="p1"><span class="s1">İlgili Container’ı zorlayarak kaldırır. Çalışan bir Container ancak </span><span class="s4">-f</span><span class="s1"> ile kaldırılabilir</span></p>
</td>
</tr>
<tr>
<td class="td3" valign="middle">
<p class="p7"><span class="s1">docker rmi &lt;image_id|image_name&gt;</span></p>
</td>
<td class="td4" valign="middle">
<p class="p1"><span class="s1">İlgili Image’ı siler</span></p>
</td>
</tr>
<tr>
<td class="td1" valign="middle">
<p class="p7"><span class="s1">docker rmi -f &lt;image_id|image_name&gt;</span></p>
</td>
<td class="td2" valign="middle">
<p class="p1"><span class="s1">İlgili Image’ı zorlayarak kaldırır, başka isimlerle Tag’lenmiş Image’lar </span><span class="s4">-f</span><span class="s1"> ile kaldırılabilir</span></p>
</td>
</tr>
<tr>
<td class="td3" valign="middle">
<p class="p7"><span class="s1">docker info</span></p>
</td>
<td class="td4" valign="middle">
<p class="p1"><span class="s1">Docker Daemon’la ilgili özet bilgiler verir</span></p>
</td>
</tr>
<tr>
<td class="td1" valign="middle">
<p class="p7"><span class="s1">docker inspect &lt;container_id&gt;</span></p>
</td>
<td class="td2" valign="middle">
<p class="p1"><span class="s1">İlgili Container’la ilgili detaylı bilgiler verir</span></p>
</td>
</tr>
<tr>
<td class="td3" valign="middle">
<p class="p7"><span class="s1">docker inspect &lt;image_id|image_name&gt;</span></p>
</td>
<td class="td4" valign="middle">
<p class="p1"><span class="s1">İlgili Image’la ilgili detaylı bilgiler verir</span></p>
</td>
</tr>
<tr>
<td class="td1" valign="middle">
<p class="p7"><span class="s1">docker rm $(docker ps -aq)</span></p>
</td>
<td class="td2" valign="middle">
<p class="p1"><span class="s1">Bütün Container’ları kaldırır</span></p>
</td>
</tr>
<tr>
<td class="td3" valign="middle">
<p class="p7"><span class="s1">docker stop $(docker ps -aq)</span></p>
</td>
<td class="td4" valign="middle">
<p class="p1"><span class="s1">Çalışan bütün Container’ları kaldırır</span></p>
</td>
</tr>
<tr>
<td class="td1" valign="middle">
<p class="p7"><span class="s1">docker rmi $(docker images -aq)</span></p>
</td>
<td class="td2" valign="middle">
<p class="p1"><span class="s1">Bütün Image’ları kaldırır</span></p>
</td>
</tr>
<tr>
<td class="td3" valign="middle">
<p class="p7"><span class="s1">docker images -q -f dangling=true</span></p>
</td>
<td class="td4" valign="middle">
<p class="p1"><span class="s1">Dangling (taglenmemiş ve bir Container ile ilişkilendirilmemiş) Image’ları listeler</span></p>
</td>
</tr>
<tr>
<td class="td1" valign="middle">
<p class="p7"><span class="s1">docker rmi $(docker images -q -f dangling=true)</span></p>
</td>
<td class="td2" valign="middle">
<p class="p1"><span class="s1">Dangling Image’ları kaldırır</span></p>
</td>
</tr>
<tr>
<td class="td3" valign="middle">
<p class="p7"><span class="s1">docker volume ls -f dangling=true</span></p>
</td>
<td class="td4" valign="middle">
<p class="p1"><span class="s1">Dangling Volume’ları listeler</span></p>
</td>
</tr>
<tr>
<td class="td1" valign="middle">
<p class="p7"><span class="s1">docker volume rm $(docker volume ls -f dangling=true -q)</span></p>
</td>
<td class="td2" valign="middle">
<p class="p1"><span class="s1">Danling Volume’ları kaldırır</span></p>
</td>
</tr>
<tr>
<td class="td3" valign="middle">
<p class="p7"><span class="s1">docker logs &lt;container_id&gt;</span></p>
</td>
<td class="td4" valign="middle">
<p class="p1"><span class="s1">İlgili Container’ın terminalinde o ana kadar oluşan çıktıyı gösterir</span></p>
</td>
</tr>
<tr>
<td class="td1" valign="middle">
<p class="p7"><span class="s1">docker logs -f &lt;container_id&gt;</span></p>
</td>
<td class="td2" valign="middle">
<p class="p1"><span class="s1">İlgili Container’ın terminalinde o ana kadar oluşan çıktıyı gösterir ve </span><span class="s4">-f</span><span class="s1"> follow parametresi ile o andan sonra oluşan logları da göstermeye devam eder</span></p>
</td>
</tr>
<tr>
<td class="td3" valign="middle">
<p class="p7"><span class="s1">docker exec &lt;container_id&gt; &lt;command&gt;</span></p>
</td>
<td class="td4" valign="middle">
<p class="p1"><span class="s1">Çalışan bir Container içinde bir komut koşturmak için kullanılır</span></p>
</td>
</tr>
<tr>
<td class="td1" valign="middle">
<p class="p7"><span class="s1">docker exec -it &lt;container_id&gt; /bin/bash</span></p>
</td>
<td class="td2" valign="middle">
<p class="p1"><span class="s1">Çalışan bir Container içinde terminal açmak için kullanılır. İlgili Image’da /bin/bash bulunduğu varsayımı ile</span></p>
</td>
</tr>
<tr>
<td class="td3" valign="middle">
<p class="p7"><span class="s1">docker attach &lt;container_id&gt;</span></p>
</td>
<td class="td4" valign="middle">
<p class="p1"><span class="s1">Önceden detached modda </span><span class="s4">-d</span><span class="s1"> başlatılan bir Container’a attach olmak için kullanılır</span></p>
</td>
</tr>
</tbody>
</table>
