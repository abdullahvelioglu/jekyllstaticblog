---
layout: post
title: AĞ HİZMETLERİ
tags: [networking]
---




##<P class="p3 ft3">1. TAŞIMA KATMANI PROTOKOLLERİ</P>
#<P class="p4 ft4">1.1. <NOBR>İstemci-Sunucu</NOBR> İlişkisi</P>
<P class="p5 ft5">İnsanlar her gün başkalarıyla iletişim kurmak ve rutin görevlerini yerine getirmek için ağ ve internet üzerinden sağlanan hizmetleri kullanmaktadır. En yaygın kullanılan internet uygulamalarının çoğu, birçok farklı sunucu ve istemci arasındaki karmaşık etkileşimlere dayanır.</P>
<P class="p6 ft5">Sunucu, ağa bağlı diğer konak bilgisayarlara bilgi veya hizmet sağlayan bir yazılım uygulamasını çalıştıran konak bilgisayarı ifade eder.İstemci ise, sunucunun bilgi veya hizmetini talep eden bilgisayarları ifade eder. Bir web sayfası incelenirken kullanıcının bilgisayarı ve web tarayıcısı, istemci olarak adlandırılır. Web sayfasını, veritabanlarını ve uygulamaları üzerinde barındıran gelişmiş bilgisayarlar da sunucu olarak adlandırılır.Web tarayıcısı, web sunucusundan bir istekte bulunur ve sunucu istenen bilgileri toplar ve onu bir web sitesi şekline getirerek web tarayıcısına geri yollar. Kullanıcılar da ekranda web sitesini görmüş olur.Bu karmaşık etkileşimlerin gerçekleşmesini sağlayan en önemli faktör, tümünün üzerinde anlaşılmış standartları ve protokolleri kullanmasıdır. İstemci/sunucu sistemlerinin en önemli özelliği, istemcinin sunucuya bir istek göndermesi ve sunucunun istemciye bilgiyi geri göndermek gibi bir işlev yürüterek yanıt vermesidir. Web tarayıcısı ve web sunucusu bileşimi büyük olasılıkla en yaygın kullanılan istemci/sunucu sistemi örneğidir.</P>
<P class="p7 ft6">Ağ üzerinde sadece web sunucuları bulunmaz. Dosya aktarımı için FTP sunucular,IP adresi dağıtımı için DHCP sunucular, web sitelerinin IP adresini bulmak için DNS sunucular, <NOBR>e-posta</NOBR> alıp göndermek içinde <NOBR>e-posta</NOBR> sunucuları da ağ üzerinde yer alan sunucular arasındadır.</P>




#<P class="p8 ft4">1.2. Taşıma Katmanı Protokolleri</P>
<P class="p9 ft5">TCP/IP’de taşıma katmanı için TCP ve UDP olmak üzere iki protokol tanımlıdır. TCP bağlantı temelli bir protokoldür. Bu yüzden gönderici ve alıcı, veri iletişimi başlamadan önce iki taraf iletişim yapma konusunda istek ve onaylı mesajlarını birbirlerine gönderir. UDP ise bağlantısız basit bir protokoldür. Bu protokolde iletişim başlamadan önce gönderici ve alıcı arasında paket alışverişi yoktur.</P>
#<P class="p10 ft7">1.2.1. TCP</P>
<P class="p11 ft5">Gelişmiş bilgisayar ağlarında ve paket anahtarlamalı bilgisayar iletişiminde, kayıpsız veri gönderimi sağlayabilmek için TCP protokolü kullanılmaktadır. HTTP, HTTPS, POP3, SMTP ve FTP gibi protokollerin veri iletimi TCP aracılığıyla yapılır. TCP aşağıdaki işlemleri gerçekleştirir.</P>
<P class="p12 ft5"><SPAN class="ft7">Bağlantılı haberleşme:</SPAN>Bilgisayarlar iletişime geçmeden önce aralarında bir oturum açar. Oturumun açılması sırasında bilgisayarlar, kendi iletişim parametrelerini birbirlerine iletir ve bu parametreleri dikkate alarak iletişimde bulunur. Bu işleme el sıkışma (handshaking) adı verilir.</P>
<P class="p13 ft5"><SPAN class="ft7">Güvenli haberleşme:</SPAN>Bilginin karşı tarafa gittiğinden emin olma durumudur. Bu güvenilirlik, bilginin alındığına dair karşı taraftan gelen bir onay mesajı ile sağlanır. Eğer bilgi gönderildikten belli süre sonra bu mesaj gelmezse paket yeniden gönderilir.TCP’de tanımlı temel görevler aşağıdaki şekilde sıralanabilir:</P>
*<P class="p14 ft5">•Bir üst katmandan gelen verinin uygun uzunlukta parçalara bölünmesi.</P>
<P class="p15 ft5"><SPAN class="ft8">•</SPAN>Her bir parçaya, alıcı kısımda aynı biçimde sıraya koyulabilmesi amacıyla sıra numarası verilmesi.</P>
<P class="p16 ft5"><SPAN class="ft8">•</SPAN>Kaybolan veya bozuk gelen parçaların tekrarlanması.</P>
<P class="p17 ft5"><SPAN class="ft8">•</SPAN>Uygulamalar arasında yönlendirme yapılması.</P>
<P class="p18 ft5"><SPAN class="ft8">•</SPAN>Güvenilir paket dağıtımının sağlanması.</P>*

<DIV id="page_3">
<DIV id="p3dimg1">
<IMG src="http://www.abdullahvelioglu.com/blog/public/images/Resim1.1.png" id="p3img1">



#<P class="p8 ft4">1.2.1.1. TCP Protokolünün Yapısı</P>
<P class="p19 ft5">TCP, taşıma katmanında verileri parçalara bölerek her bir parçanın önüne başlık bilgisi ekler. Başlık bilgisiyle birlikte bu veriye, TCP Segmenti denir. TCP başlık bilgisi 20 byte’tır. TCP Segmenti aşağıdaki gibidir.</P>
<P class="p20 ft5"><SPAN class="ft7">Kaynak port:</SPAN>Veriyi gönderen bilgisayarın kullandığı TCP portudur.</P>
<P class="p3 ft5"><SPAN class="ft7">Hedef port:</SPAN>Hedef bilgisayarın TCP portudur.</P>
<P class="p21 ft5"><SPAN class="ft7">Sıra numarası:</SPAN>Gönderilen paketin sıra numarasını gösterir.Gönderilmeden önce daha küçük parçalara ayrılan verinin, alıcı kısımda yeniden aynı sırada elde edilmesinde kullanılır.</P>
<P class="p22 ft5"><SPAN class="ft7">Onay numarası:</SPAN>Gönderilen verinin en son hangi sekizlisinin alındığını göndericiye iletmek için kullanılır.</P>
<P class="p23 ft5"><SPAN class="ft7">Başlık uzunluğu:</SPAN>TCP segmentinin uzunluğunu gösterir.</P>
<P class="p3 ft5"><SPAN class="ft7">Rezerve:</SPAN>İleride kullanılmak üzere saklı tutulur.</P>

<DIV id="page_4">


<P class="p24 ft5"><SPAN class="ft7">Bayraklar:</SPAN>Segment ile ilgili kontrol bilgilerini taşır.6 tane bayrak biti bulunmaktadır.</P>
<P class="p23 ft7">Bunlar:</P>
*<P class="p25 ft5"><SPAN class="ft9">•</SPAN><SPAN class="ft7">Acil (urgent) bayrağı:</SPAN>Bu bayrak, acil işaretçisi alanının geçerli olup olmadığını belirtir.</P>
<P class="p26 ft5"><SPAN class="ft9">•</SPAN><SPAN class="ft7">Alındı (acknowledgement) bayrağı:</SPAN>Bu bayrak, acknowledgement alanının geçerli olup olmadığını belirtir.</P>
<P class="p27 ft5"><SPAN class="ft9">•</SPAN><SPAN class="ft7">Push bayrağı:</SPAN>Bu bayrak, modülün push fonksiyonunu işletip işletmeyeceğini belirtir.Push metodu, gönderilecek verinin hemen gönderilmesi için kullanılır.</P>
<P class="p28 ft11"><SPAN class="ft9">•</SPAN><SPAN class="ft10">Reset bayrağı:</SPAN>Bu bayrak, bağlantının resetlenmesi gerektiğini belirtir.Bağlantıyı, anormal durumlarda, başlangıç durumuna getirir.</P>
<P class="p29 ft5"><SPAN class="ft9">•</SPAN><SPAN class="ft7">Synchronize bayrağı:</SPAN>Bu bayrak, sıra numaralarının eş zamanlanmasının oluşturulmaya çalışıldığını bildirir. Bağlantı kurma segmentlerinde handshaking (el sıkışma) işlemlerinin oluştuğunu belirtmek için kullanılır.</P>
<P class="p30 ft5"><SPAN class="ft9">•</SPAN><SPAN class="ft7">Finish bayrağı:</SPAN>Bu bayrak, göndericinin gönderecek daha fazla verisinin olmadığını belirtir.</P>
<P class="p31 ft5"><SPAN class="ft7">•Pencere:</SPAN>Akış kontrolüiçin kullanılır.Art arda kaç veri paketi gönderileceğini belirler.</P>
<P class="p32 ft5"><SPAN class="ft7">•Hata kontrol bitleri:</SPAN>Segmentin hatalı ulaşıp ulaşmadığını kontrol etmek için kullanılır.</P>
<P class="p33 ft5"><SPAN class="ft7">•Acil işaretçisi:</SPAN>Bir verinin acil olarak iletilmek istendiği durumlarda kullanılır.</P>
<P class="p23 ft5"><SPAN class="ft7">•Seçenek:</SPAN>TCP segmentinin maksimum boyutunun bilgisini taşır.</P>
<P class="p34 ft5"><SPAN class="ft7">•Doldurma biti:</SPAN>Seçenek bitinin boyutunu,32 bit’e tamamlamak için kullanılır.</P>
<P class="p23 ft5"><SPAN class="ft7">•Veri:</SPAN>Verinin bulunduğu kısımdır.</P>*

<DIV id="page_5">
<DIV id="p5dimg1">
<IMG src="http://www.abdullahvelioglu.com/blog/public/images/Resim1.2.png" id="p5img1">



#<P class="p8 ft7">1.2.1.2. TCP ile İletişim</P>
<P class="p3 ft5">TCP veri iletiminin başlaması için aşağıdaki işlemler gerçekleşir:</P>
<P class="p35 ft5"><SPAN class="ft7">1.</SPAN>İstemci, sunucu ile bir TCP oturumunu başlatmak için sunucuya bir SYN paketi gönderir ve dinlemeye geçer.</P>
<P class="p36 ft5"><SPAN class="ft7">2.</SPAN>SYN başlatma paketini alan sunucu, ACK onay paketiyle birlikte SYN paketi gönderir ve dinlemeye geçer.</P>
<P class="p37 ft5"><SPAN class="ft7">3.</SPAN>İstemci, sunucunun gönderdiği SYN paketine karşılık ACK onay paketi gönderir. Sunucu, ACK onay paketini aldıktan sonra oturum başlatılır.</P>
<P class="p38 ft5">Bu işleme üç aşamalı el sıkışma <NOBR>(3way-handshake)</NOBR> adı verilir.</P>

<DIV id="page_6">
<DIV id="p6dimg1">
<IMG src="http://www.abdullahvelioglu.com/blog/public/images/Resim1.3.png" id="p6img1">



#<P class="p8 ft7">1.2.1.3. Servis Saldırıları</P>
<P class="p39 ft5">SYN saldırısı (SYN flood), hizmet engelleme saldırısının bir biçimidir. Bu saldırı biçiminde saldırgan, sistemi isteklere cevap veremeyecek duruma getirmek için sunucu kaynaklarını tüketme girişiminde buluna rak hedef alınan sisteme ardışık SYN istekleri (SYN requests) gönderir. Normal olarak bir istemci bir sunucuya TCP bağlantısı başlatma isteğinde bulunduğunda, sunucu ve istemci bir dizi mesaj takas eder ve bu durum şöyle işler:</P>
<P class="p40 ft5">1. İstemci sunucuya bir SYN (synchronize) mesajı göndererek bir bağlantı kurmak ister.</P>
<P class="p41 ft5">2. Sunucu bu mesajı, <NOBR>SYN-ACK</NOBR> mesajlarını istemciye dönerek kabul eder.</P>
<P class="p42 ft12">3. İstemci ACK ile yanıt verir ve bağlantı kurulmuş olur. Bu TCP üçlü</P>
<P class="p43 ft5">el sıkışma olarak adlandırılır ve bütün TCP protokolü kullanan kurulmuş bağlantılar için temeldir.</P>
<P class="p44 ft5">SYN saldırısı, sunucununbeklediği ACK kodunu göndermeyerek çalışan bir ataktır. Kötü niyetli istemci ya basit bir şekilde beklenen ACK'yı göndermez ya da sahte IP adresi kullanarak SYN'deki IP adres kaynağını zehirler. Çünkü sunucu,sahte IP adresine <NOBR>SYN-ACK</NOBR> göndermeye çalışır. Ancak ACK gönderemeyecektir. Çünkü o adresle bir SYN gönderilmediğini bilir.Sunucu bir süre ACK için bekleyecektir fakat saldırılarda bu istekler sürekli artan şekilde olduğundan sunucu yeni bağlantı oluşturamaz duruma gelir.</P>

<DIV id="page_7">
<DIV id="p7dimg1">
<IMG src="http://www.abdullahvelioglu.com/blog/public/images/Resim1.4.png" id="p7img1">



#<P class="p8 ft13">1.2.2. UDP</P>
<P class="p45 ft5">UDP, TCP / IP protokol grubunun iki taşıma katmanı protokolünden birisidir. Gelişmiş bilgisayar ağlarında paket anahtarlamalı bilgisayar iletişiminde bir datagrammodu oluşturabilmek için UDP protokolü oluşturulmuştur. Bu protokol minimum protokol mekanizmasıyla bir uygulama programından diğerine mesaj göndermek için bir yöntem içerir.</P>
<P class="p46 ft5">Bu protokol hareket yönlendirmelidir. Paketin teslim garantisini isteyen uygulamalar TCP protokolünü kullanır. Geniş alan ağlarında (WAN) ses ve görüntü aktarımı gibi gerçek zamanlı veri aktarımlarında UDP kullanılır. UDP bağlantı kurulum işlemlerini, akış kontrolü ve tekrar iletim işlemlerini yapmayarak veri iletim süresini en aza indirir. UDP ve TCP aynı iletişim yolunu kullandıklarında UDP ile yapılan gerçek zamanlı veri transferinin servis kalitesi TCP'nin oluşturduğu yüksek veri trafiği nedeniyle azalır. UDP güvenilir olmayan bir aktarım protokolüdür.</P>
<P class="p47 ft14">UDP protokolü ağ üzerinden paketi gönderir ve gidip gitmediğini takip etmez ve paketin yerine ulaşıp ulaşmayacağına onay
verme yetkisi yoktur. UDP protokolünü kullanan programlara örnek olarak 161 numaralı portu kullanan SNMP servisini verebiliriz.</P>
#<P class="p42 ft2">1.2.2.1. UDP Protokolünün Yapısı</P>
<P class="p49 ft5">UDP,datagramların belirli sıralara konmasının gerekli olmadığı uygulamalarda kullanılmak üzere tasarlanmıştır. TCP’de olduğu gibi UDP’de de bir başlık vardır. Ağ yazılımı bu UDP başlığını iletilecek bilginin başına koyar. Ardından UDP bu bilgiyi IP katmanına yollar. IP katmanı kendi başlık bilgisini ve protokol numarasını yerleştirir, bu kez numarası alanına UDP’ye ait değer yazılır. Fakat UDP, TCP’nin yaptıklarının hepsini yapmaz. Bilgi burada datagramlara bölünmez ve yollanan paketlerin kaydı tutulmaz. UDP’nintek sağladığı port numarasıdır. Böylece pek çok program UDP'yi kullanabilir. Daha az bilgi içerdiğinden UDP başlığı TCP başlığına göre daha kısadır.</P>
<P class="p50 ft5">UDP başlığı her biri 16 bit uzunluğunda olmak üzere 4 alandan oluşur. Başlık, kaynak ve hedef port numaraları, UDP uzunluğu ve hata kontrol bitlerini içerir.UDP başlık bilgisinin boyutu 8 Byte’tır.</P>

<DIV id="page_8">
<DIV id="p8dimg1">
<IMG src="http://www.abdullahvelioglu.com/blog/public/images/Resim1.5.png" id="p8img1">



#<P class="p8 ft15">1.3. Portlar</P>
<P class="p51 ft5">TCP ve UDP,üst protokollerle bağlantıda portları kullanır. 65535 adet port vardır ve IANA (Internet AssignedNumbersAuthority) ilk 1024 portu,iyi bilinen <NOBR>(Well-known)</NOBR> portlar olarak ilan etmiştir.</P>
<P class="p52 ft12">Bir bilgisayar, bir IP adresi ve bir port belirlediğinde buna soket (socket) ismi verilmektedir. Yani “X IP adresindeki bilgisayara, Y port’undan bilgi gönderildiğinde, bu bilgi şu işlem için ele alınacaktır.” şeklinde bir önerme ortaya çıkar.</P>
<P class="p53 ft5">Örneğin istemci bir web sitesine bağlanmak istediğinde TCP segmentindeki, Hedef Port bilgisi 80 olur. HTTP’nin varsayılan port numarası 80’dir. İsteği alan sunucu, hedef port bilgisine bakarak kendisine gelen isteği ilgili uygulama katmanındaki servise gönderir. Örnekte, ağ benzetim programı ile hazırlanmış basit bir ağ yapısı gözükmektedir. Web sayfasının olduğu sunucunun IP adresi 192.168.1.100, istemcinin ise 192.168.1.200’dür.</P>
<P class="p54 ft5">İstemci web sayfasını görüntülemek istediğinde sunucuya bir veri paketi gönderilir. Aşağıdaki resimde, TCP segmentinin içeriği şekilde gösterilmektedir.</P>

<DIV id="page_9">
<DIV id="p9dimg1">
<IMG src="http://www.abdullahvelioglu.com/blog/public/images/Resim1.6.png" id="p9img1">



<P class="p55 ft5">SRC PORT alanı (kaynak port), istemcinin portunu gösterir ve sunucudan istemciye gelecek olan bilgiler bu port numarası ile uygulama katmanına geçecektir. Kaynak port, iki aygıt arasındaki iletişimi tanımlamak için gönderen aygıt (istemci) tarafından rastgele oluşturulur.DEST PORT(hedef port) alanı ise sunucunun port numarasıdır. Bu port numarası sunucuya HTTP hizmeti istendiğini belirtir.</P>
<P class="p56 ft14">Birçok TCP/IP ve UDP/IP servisi,bu port numaraları ile tanınır. Port numaraları üç ayrı sınıfta toplanır. Bunlar:</P>
<P class="p57 ft5">0 ile 255 arasındaki port numaraları standart uygulama katmanlarına erişim için kullanılmıştır. Örneğin telnet için port 23, ftp için port 21 kullanılır. Windows İşletim Sisteminde, bilgisayarın hangi uygulama programı için hangi port numarasını kullandığı /etc/services dosyasından öğrenilebilir.</P>

<DIV id="page_10">


<P class="p58 ft6">255 ile 1023 arasında bulunan portlar,ticari şirketlerin geliştirdiği uygulamalar için kullanılır. 1024 ve üzerinde bulunan portlar, herhangi bir düzenlemeye tabi tutulmamıştır. Sunucuya istek yapıldığında kaynak port olarak bu portlardan atama işlemi yapılır.</P>
<P class="p59 ft5"><SPAN class="ft16">Netstat (network statistics): </SPAN>ağ bağlantıları (hem gelen hem giden), yönlendirme tabloları ve ağ arayüzü istatistiklerini görüntülemek için kullanılan bir komut satırı aracıdır.</P>
<P class="p60 ft5">Netstat komutu UNIX, Linux ve Windows NT tabanlı işletim sistemlerinde kullanılabilir.</P>
<P class="p61 ft11">Açık ve dinlenme durumunda olan portları görüntülemek için <SPAN class="ft17"><code>netstat </SPAN><NOBR><SPAN class="ft18">–</SPAN><SPAN class="ft17">an</SPAN></NOBR><SPAN class="ft17"> | find /i </SPAN><SPAN class="ft18">“</SPAN><SPAN class="ft17">listening”</SPAN></code> komutu kullanılır.</P>
<P class="p62 ft12">İletişimde olan portları görüntülemek için</P>
<P class="p38 ft19"><code>netstat <NOBR><SPAN class="ft18">–</SPAN>an</NOBR> | find /i “established<SPAN class="ft18">”</SPAN><SPAN class="ft5"></code> komutu kullanılır.</SPAN></P>
<P class="p63 ft20">1.3.1. Port Numaraları</P>
<P class="p64 ft5">En çok kullanılan port numaraları aşağıda listelenmiştir.</P>
*<P class="p8 ft21"><SPAN class="ft16">•</SPAN>FTP: <NOBR>20-21.</NOBR> port</P>
<P class="p8 ft22"><SPAN class="ft16">•</SPAN>HTTP: 80. port (Alternatif Port: 8080)</P>
<P class="p8 ft22"><SPAN class="ft16">•</SPAN>HTTPS: 443. port</P>
<P class="p8 ft22"><SPAN class="ft16">•</SPAN>SMTP: 25. port</P>
<P class="p8 ft22"><SPAN class="ft16">•</SPAN>TELNET: 23. port</P>
<P class="p8 ft22"><SPAN class="ft16">•</SPAN>SSH: 22. port</P>
<P class="p8 ft22"><SPAN class="ft16">•</SPAN>IMAP: 143. port</P>
<P class="p8 ft22"><SPAN class="ft16">•</SPAN>POP3: 110. port</P>
<P class="p8 ft22"><SPAN class="ft16">•</SPAN>SMPTS: 465. port</P>
<P class="p8 ft22"><SPAN class="ft16">•</SPAN>POP3S: 995.port</P>
<P class="p8 ft22"><SPAN class="ft16">•</SPAN>IMAPS: 993. port</P>
<P class="p8 ft22"><SPAN class="ft16">•</SPAN>DNS: 53. port</P>
<P class="p8 ft5"><SPAN class="ft16">•</SPAN>DHCP: <NOBR>67-68.</NOBR> port</P>*

<DIV id="page_11">


##<P class="p8 ft23">2. UYGULAMA KATMANI UYGULAMALARI</P>
#<P class="p65 ft2">2.1. TCP/IP Uygulama Katmanı</P>
<P class="p66 ft5">TCP/IP’nin uygulama katmanında, veriyi göndermek isteyen uygulama ve kullandığı dosya biçimi bulunarak gönderilen verinin türüne göre farklı protokoller çalıştırılır (HTTP,SMTP, FTP, Telnet, vs.). Programlarla taşıma protokollerinin haberleşmesi sağlanır. Uygulama katmanı,taşıma katmanıyla portlar aracılığıyla haberleşir. Portlar numaralandırılmış standart uygulamalardır.</P>
<P class="p67 ft6">(HTTP:80, FTP:21, vs.) ve taşıma katmanında gelen paket içeriğinin türünün anlaşılmasında rol oynar.Bu katman,TCP/IP uygulama protokollerini ve programların ağı kullanmak için taşıma katmanı hizmetleriyle nasıl bir arabirim oluşturacağını tanımlar.</P>
#<P class="p68 ft24">2.2. Uygulama Katmanı Protokolleri</P>
#<P class="p4 ft2">2.2.1. DNS</P>
<P class="p69 ft5">İnternet bağlı ve farklı alanlarda olan binlerce sunucu, her gün internette kullanılan hizmetleri sağlar. Bu sunucuların her birine, bağlı olduğu yerel ağda, sunucuyu tanımlayan benzersiz bir IP adresi atanır. İstemcilere hizmet veren bu sunuculara erişmek için sunucuların IP adreslerinin bilinmesi gerekir. Fakat tüm sunucuların IP adreslerinin akılda tutulması mümkün değildir. Bunun yerine, kullanıcı dostu internet adresleri (<A href="http://www.tegsoft.com/"><SPAN class="ft25">www.tegsoft.com</SPAN></A> gibi) kullanılmaktadır. DNS(Domain Name System, Etki Alanı Adlandırma Sistemi), <A href="http://www.tegsoft.com/"><SPAN class="ft25">www.tegsoft.com</SPAN></A> gibi internet adreslerinin, IP adreslerine çevrimini sağlar.</P>
#<P class="p70 ft16">2.2.1.1. DNS’nin Tarihçesi</P>
<P class="p71 ft6">İnternet yaygınlaşmamış ve internet üzerindeki bilgisayar sayısı azken internet <NOBR>adresi-IP</NOBR> adresi çözümlemesi, HOST adında metin dosyası ile yapılmaktaydı. İnternet adresi ve karşılığındaki IP adresi, bu dosyaya elle kayıt edilmekte ve internetteki bilgisayarların her birinde bu dosya nın bir kopyası bulunmaktaydı. Bir bilgisayar,bir başka bilgisayara ulaşmak istediğinde bu dosyayı inceliyor,eğer dosyada o bilgisayarın kaydı bulunuyorsa IP adresini alıyor ve iletişime geçiyordu.</P>
<P class="p72 ft5">Bu sistemin iyi işleyebilmesi için HOSTS dosyası içeriğinin hep güncel kalması gerekiyordu. Bunu sağlamak için de dosyanın aslının saklandığı ABD’deki Stanford Üniversitesi<SPAN class="ft8">’</SPAN>ne belli aralıklarla bağlanarak kopyalama yapılıyordu.</P>

<DIV id="page_12">


<P class="p73 ft26">Ama internetteki bilgisayarların sayısı arttıkça hem bu dosyanın büyüklüğü olağanüstü boyutlara ulaşmaya başladı hem de internetteki bilgisayarların dosyayı kopyalamak için yaptığı bağlantı Standford’daki bilgisayarları kilitlenmeye başladı.</P>
<P class="p46 ft5">Tek bir HOSTS dosyası kullanmanın başka bir kötülüğü de şuydu: Bütün bilgisayarlar aynı düzeyde yer aldığı için bir bilgisayar isminin bütün internette bir eşinin daha bulunmamasını sağlamak gerekiyordu.</P>
<P class="p74 ft27">Bu sorunlar yüzünden internet yetkili organları,1984 yılında DNS’yi ürettiler.DNS hem bilgisayar veri tabanını dağıtık bir yapıya
sokmakta hemde bilgisayarlar arasında hiyerarşik bir yapı kurulmasını sağlamaktadır.</P>
<P class="p76 ft5">DNS’de dağıtık veri tabanı şöyle sağlanır. Bilgisayarlar bulundukları yerlere,ait oldukları kurumlara göre sınıflandırılmaktadır. Örneğin, Türkiye<SPAN class="ft8">’</SPAN>deki bilgisayarların listesi</P>
<P class="p77 ft5">(.tr domaini),Türkiye’den sorumlu bir DNS sunucu makinede tutulmaktadır.Böylece internet ortamındaki bütün bilgisayarların bilgisinin tek bir yerde tutulması zorunluluğu kalmamıştır.</P>
<P class="p78 ft5">İnternet adresleri ülkelerden sonra alt bölümlere ayrılır. Bu bölümlere üst düzey domainler denir. Bu domainlerin ifade ettikleri bölümler şunlardır:</P>
<P class="p17 ft21"><SPAN class="ft16">•.</SPAN>com: Ticari kuruluşlar (COMmercial)</P>
<P class="p8 ft28"><SPAN class="ft16">•</SPAN>.edu: Yükseköğrenim kurumları (EDUcation)</P>
<P class="p8 ft22"><SPAN class="ft16">•</SPAN>.org: Sivil toplum kuruluşları(ORGanizations)</P>
<P class="p8 ft22"><SPAN class="ft16">•</SPAN>.gov: Hükümete ait kurumlar (GOVernment)</P>
<P class="p8 ft22"><SPAN class="ft16">•</SPAN>.mil: Askeri kurumlar (MILitary)</P>
<P class="p8 ft22"><SPAN class="ft16">•</SPAN>.net: Büyük ağ hizmetleri veren kuruluşlar (NETwork)</P>
<P class="p8 ft22"><SPAN class="ft16">•</SPAN>.int: Uluslararası organizasyonlar (INTernational)</P>
<P class="p8 ft22"><SPAN class="ft16">•</SPAN>.num: Telefon numaraları bulabileceğiniz yerler (NUMbers)</P>
<P class="p8 ft5"><SPAN class="ft16">•</SPAN>.arpa: Ters DNS sorgulaması yapılan yerler</P>

<DIV id="page_13">
<DIV id="p13dimg1">
<IMG src="http://www.abdullahvelioglu.com/blog/public/images/Resim1.7.png" id="p13img1">



#<P class="p8 ft29">2.2.1.2. DNS Çözümleme</P>
<P class="p79 ft26">DNS sunucusunda, sunucu adlarını karşılık gelen IP adresleriyle ilişkilendiren bir tablo yer alır. Bir istemcide, sunucunun adı (örneğin, bir web adresi) bulunuyor ancak IP adresinin istemci tarafından bulunması gerekiyorsa DNS sunucusuna hedef portu 53 olan</P>
<P class="p80 ft14">bir istek gönderir. İstemci, IP yapılandırmasındaki DNS ayarlarında yapılandırılmış, DNS sunucusunun IP adresini kullanır.</P>
<P class="p81 ft5">DNS sunucusu isteği aldığında, IP adresinin bir web sunucusuyla ilişkilendirilmiş olup olmadığını belirlemek için tablosunu kontrol eder. Yerel DNS sunucusunda, istenen ada ilişkin giriş yoksa sunucu etki alanı içindeki başka bir DNS sunucusunu sorgular. DNS sunucusu IP adresini öğrendiğinde, bu bilgi istemciye geri gönderilir. DNS sunucusu IP adresini belirleyemezse istek zaman aşımına uğrar ve istemci web sunucusuyla iletişim kuramaz.</P>

<DIV id="page_14">
<DIV id="p14dimg1">
<IMG src="http://www.abdullahvelioglu.com/blog/public/images/Resim2.1.png" id="p14img1">



#<P class="p8 ft30">2.2.1.3. NSLOOKUP Komutu</P>
<P class="p82 ft5">Nslookup, IP adresini girerek isim sorgusu ya da internet adresi girerek IP adresi sorgusu yapılmasına yarayan bir komuttur.Bu komutun çalışması,Windows ve Linux sistemlerin de ortaktır.Bir web sitesinin, IP adresini sorgulamak için nslookup yazıp bir boşluk bırakarak web sitesi adresini yazmanız yeterlidir. Komut çalıştığında, DNS’de çözümleme işlemi yapılacak ve size web sitesinin IP adresini görüntüleyecektir. Ayrıca “Server” alanı ile hangi DNS sunucusunu kullandığınızı ve “Address” alanı ile de DNS sunucusunun IP adresini görebilirsiniz.</P>
#<P class="p83 ft7">2.2.1.4. Host Dosyası</P>
<P class="p84 ft5">DNS oluşturulmadan önce IP çözümlemesi için her bilgisayar host dosyası kullanmaktaydı ve bu dosyanın sürekli güncellenmesi gerekmekteydi. DNS oluşturulduktan sonra bu işleme gerek kalmamıştır. Fakat işletim sistemlerinde bu host dosyaları hala bulunmakta ve kullanılmaktadır. Bu dosya,Linux işletim sistemlerinde <SPAN class="ft19">“etc\host”</SPAN> dizinindedir.</P>
<P class="p85 ft5">Tarayıcıya bir web sitesi adresi yazıldığında, önce host dosyasına bakılır, burada web <NOBR>adresi-IP</NOBR> adresi yoksa DNS sunucudan IP çözümlemesi yapılır. Bu dosyayı elle kendiniz güncelleyebilirsiniz.</P>

<DIV id="page_15">
<DIV id="p15dimg1">
<IMG src="http://www.abdullahvelioglu.com/blog/public/images/Resim2.2.png" id="p15img1">



#<P class="p8 ft13">2.2.2. FTP ve TFTP</P>
#<P class="p16 ft30">2.2.2.1. FTP (File Transfer Protocol)</P>
<P class="p17 ft21">File Transfer Protocol (FTP);veriyi,bir uç aygıttan diğerine iletim</P>
<P class="p86 ft12">için kullanılır. Bir dosyayı FTP kullanarak başka bir TCP/IP ağı üzerindeki kullanıcıya yollamak için o ağdaki bilgisayarda geçerli bir kullanıcı ismi ve şifresi gerekmektedir. Bir çok FTP sunucusu, kullanıcı ismi ve parola olmadan erişim için "anonim FTP" (anonymous FTP) desteği verir.</P>
<P class="p87 ft5">Bu kullanım için kullanıcı adı olarak <SPAN class="ft8">“</SPAN>anonymous<SPAN class="ft8">” </SPAN>parola olarak ise bir e <NOBR>-mail</NOBR> adresi girilmesi gerekmektedir.</P>
<P class="p88 ft6">FTP, TCP 20 ve 21 numaralı portlardan hizmet vermektedir. TCP port 20 üzerinden veri transferi gerçekleştirilirken TCP port 21 ise kontrol amaçlı kullanılmaktadır. FTP istemcileri iki farklı modda yapılandırılabilir.</P>
<P class="p89 ft16">•Aktif FTP</P>
<P class="p90 ft5">Bu FTP çeşidinde istemci aktif rol alır.Günümüz internet altyapısında çeşitli sorunlara yol açtığı için pasif FTP daha fazla tercih edilmektedir. Aktif FTP’de çıkan sorunlar pasif FTP’nin geliştirilmesini sağlamıştır. FTP istemcisi, TCP port 21 üzerinden sunucuya bir kontrol kanalı açar. Bu işlem sırasında FTP istemcisi rastgele bir port numarası kullanır. Örneğin istemci 1025 numaralı kanalı kullanmış olsun.</P>
<P class="p91 ft6">FTP sunucusu, gerekli karşılama mesajı ve kullanıcı adı sorgulamasını gönderir.İstemci gerekli erişim bilgilerini girer.Sunucu erişim bilgilerini kontrol eder, bilgiler doğru ise istemciye FTP komut satırını açar.</P>
<P class="p92 ft6">İstemci kendi tarafında 1024’ten büyük bir port numarası açar ve bunu PORT komutu ile FTP sunucuya bildirir. FTP sunucusu, istemcinin bildirdiği port numarasından bağlantı kurar ve gerekli aktarım işlemleri başlar. İstemci onay mesajı gönderir.</P>

<DIV id="page_16">
<DIV id="p16dimg1">
<IMG src="http://www.abdullahvelioglu.com/blog/public/images/Resim2.3.png" id="p16img1">



<P class="p8 ft16">•Pasif FTP</P>
<P class="p93 ft26">Pasif FTP, günümüz internet dünyasında kullanılan güvenlik duvarı, NAT cihazları gibi trafikte değişiklik yapan sistemlerden kaynaklanan FTP problemlerini sunucu tarafında halledebilmek için çıkarılmış FTP çeşididir. Pasif FTP’de istemci pasif roldedir, sunucu aktif roldedir. FTP istemcisi, TCP port 21 üzerinden sunucuya bir kontrol kanalı açar. Bu işlem sırasında FTP istemcisi rastgele bir port numarası kullanır. Örneğin istemci 1025 numaralı kanalı kullanmış olsun.</P>
<P class="p94 ft14">FTP sunucusu, gerekli karşılama mesajı ve kullanıcı adı sorgulamasını gönderir. İstemci gerekli erişim bilgilerini girer.</P>
<P class="p8 ft14">Sunucu erişim bilgilerini kontrol eder, doğru ise istemciye</P>
<P class="p81 ft5">FTP komut satırını açar. FTP istemcisi PASV komutu aracılığıyla sunucudan ek port açmasını bekler. Sunucu, yapılandırma dosyasında belirtilen port aralığından bir port açarak bunu istemciye belirtir. İstemci, sunucudan gelen bu porta bağlanarak veri alışverişini başlatır. İstemci onay mesajı gönderir.</P>

<DIV id="page_17">


#<P class="p8 ft30">2.2.2.2. TFTP (Trivial File Transfer Protocol)</P>
<P class="p17 ft21">TFTP (Trivial File Transfer Protocol)</P>
<P class="p95 ft31">FTP'nin temel fonksiyonel şekli olarak ifade edilen basit bir dosya transfer protokolüdür.Basit yapısından dolayı kullanılması</P>
<P class="p96 ft22">esnasında çok az bellek tüketilmektedir. Bu özelliğinden dolayı, yeterli yığın bellek cihazı (massstoragedevice) olmayan yönlendirici</P>
<P class="p8 ft27">lerin önyüklemesinde kullanılır.</P>
<P class="p97 ft32">Bu protokol UDP üzerinde 69. port kullanılarak uygulanmıştır.TFTP basit ve uygulanması kolay olacak şekilde tasarlanmıştır ve bu nedenle çoğu FTP özelliğinden yoksundur.TFTP sadece</P>
<P class="p8 ft27">dosya alma ve gönderme işlemlerini yapar.</P>
<P class="p98 ft5">Dizinleri listelemez ve şu anda kullanıcı kimlik doğrulaması için bir kural yoktur.</P>
#<P class="p99 ft30">2.2.3. HTTP ve HTTPS</P>
<P class="p100 ft5">HTTP (HyperText Transfer Protocol),web sayfalarını istemciye ulaştıran temel protokoldür.</P>
<P class="p101 ft26">Bir web adresine bakılmak istendiğinde, istenilen sayfa bilgisayara gelmeden önce arka planda bir dizi işlem gerçekleşir. İlk önce, internet tarayıcısı görüntülenmek istenen web sayfasının adresini ve port numarası olarak 80’i, sunucuya bildirir. Sunucu 80 numaralı</P>
<P class="p102 ft5">porttan bir istek aldığında bunun http isteği olduğunu anlar ve istemciye web sayfasını gönderir.Web sa</P>
<P class="p103 ft5">yfalarındaki bilgi HTML, XML veya XHTML dilleri kullanılarak kodlanır. İşlem gerçekleşmezse hata mesajı alınır. İşlemin gerçekleşmesi hâlinde son olarak http servisiyle yapılan bağlantı kesilir.</P>
<P class="p104 ft12">1990 yılından beri kullanımda olan http, internet adreslerinin önüne “http://” yazılarak kullanılır. Girilecek adresin önüne “http://” getirilmese bile internet tarayıcıları bu eksikliği tamamlayarak internette sorunsuzca gezinti yapılmasını sağlar.</P>
<P class="p105 ft5">HTTP protokolü güvenli bir protokol değildir; bilgi ağ üzerinden gönderilirken başka kullanıcılar tarafından kolayca müdahale edilebilir. Verilerin güvenliğini sağlamak amacıyla güvenlitaşıma protokolü olan HTTPSkullanılır.</P>
<P class="p106 ft5">HTTPS istekleri,443 numaralı portu kullanır. Bu istekler için tarayıcıdaki site adresinde “http://<SPAN class="ft8">” </SPAN>yerine <SPAN class="ft8">“</SPAN>https://<SPAN class="ft8">” </SPAN>kullanılması gerekir.</P>

<DIV id="page_18">


#<P class="p8 ft29">2.2.4. <NOBR>E-Posta</NOBR> Protokolleri</P>
#<P class="p107 ft30">2.2.4.1. SMTP</P>
<P class="p108 ft5">SMTP (Simple Mail Transfer Protocol), bir <NOBR>e-posta</NOBR> göndermek için sunucu ile istemci arasındaki iletişim şeklini belirleyen protokoldür. Sadece <NOBR>e-posta</NOBR> yollamak için kullanılan bu protokolde basitçe, istemci bilgisayar SMTP sunucusuna bağlanarak gerekli kimlik bilgilerini gönderir, sunucunun onay vermesi halinde gerekli <NOBR>e-postayı</NOBR> sunucuya iletir ve bağlantıyı sonlandırır.</P>
<P class="p8 ft31"><NOBR>E-posta</NOBR> almak için POP3 ya da IMAP protokolü kullanılır.</P>
<P class="p109 ft22">Outlook, Thunderbird, gibi <NOBR>e-posta</NOBR> istemcileri, <NOBR>e-postaları</NOBR> göndermek üzere sunucuya iletirken SMTP servisinden faydalanır.</P>
<P class="p8 ft5">25 numaralı port SMTP sunucusu için ayrılmıştır.</P>
#<P class="p3 ft16">2.2.4.2. POP3</P>
<P class="p110 ft26">POP3 (Port Office Protocol 3), istemciye gönderilmiş olan <NOBR>e-postaları</NOBR> istemcinin bilgisayarına indirmeye yarayan bir protokoldür. Bu protokol kimlik doğrulaması gerektirdiği içinkullanıcı adı ve parola, istemcinin kullandığı yazılımın ilgili alanlarına girilmesi gerekir.</P>
<P class="p111 ft5">POP istemcilerini destekleyen bir sunucu, kullanıcılarına adreslenen iletileri alır ve depolar. İstemci <NOBR>e-posta</NOBR> sunucusuna bağlandığında, iletiler istemciye indirilir. Varsayılan olarak iletiler istemci tarafından erişildikten sonra sunucuda tutulmaz. İstemciler, 110 numaralı port ile POP3 sunucularıyla iletişim kurar.</P>
#<P class="p23 ft30">2.2.4.3. IMAP4</P>
<P class="p112 ft26">IMAP (Internet Message Access Protocol), <NOBR>e-posta</NOBR> almak için kullanılan bir protokoldür. IMAP istemcilerini destekleyen bir sunucu, kullanıcılarına adreslenen iletileri alır ve depolar. Ancak bu sunucu, ilet ileri kullanıcı silmediği sürece sunucudaki posta kutularında tutar.</P>
<P class="p113 ft11">En güncel IMAP sürümü, 143 numaralı porttan istemci isteklerini dinleyen IMAP4'tür. POP3’e göre aşağıdaki avantajları bulunmaktadır.</P>
<P class="p114 ft26"><SPAN class="ft16">•</SPAN>İstemci, <NOBR>e-posta</NOBR> sunucusuna POP3 protokolü ile bağlandığında tüm yeni mesajlar istemciye çekilir ve bağlantı kapatılır.IMAP protokolü kullanıldığında ise oturum açıldıktan sonra bağlantı sadece istek olduğu durumlarda açık kalır (Bir mesajın açılması ve i</P>
<P class="p18 ft5">çeriğinin görüntülenmesi gibi).</P>

<DIV id="page_19">


<P class="p115 ft5"><SPAN class="ft16">•</SPAN>POP3 protokolü bir posta kutusunda aynı anda tek kullanıcıyı destekler. Tersi durumda işleyiş tarzı sorun yaratır. Bunun sebebi, tüm yeni mesajların istemciye çekilmesidir. IMAP ise çok kullanıcıyı destekler. Bir kullanıcının yaptığı değişiklik eş zamanlı olarak diğer oturum açmış kullanıcı tarafından görülebilir.</P>
<P class="p116 ft12"><SPAN class="ft16">•</SPAN>Nerdeyse bütün <NOBR>e-posta</NOBR> mesajları MIME (Multipurpose Internet Mail <NOBR>Extensions-Çok</NOBR> İşlevli Internet Posta Uzantıları) formatında gönderilir. Bir <NOBR>e-posta</NOBR> yazı bölümü, ekli dosya bölümü gibi bölümlere ayrılır. IMAP bu bölümleri birbirinden bağımsız olarak çekebilir. Örneğin, mesajı açmadan mesaj ekindeki bir dosya bilgisayara kopyalanabilir.</P>
#<P class="p117 ft30">2.2.5. DHCP</P>
<P class="p118 ft5">DHCP (Dynamic Host Configuration Protocol), sistemdeki bilgisayarlara IP adreslerini ve buna ek olarak değişik parametreleri (Alt Ağ Maskesi, Varsayılan Ağ Geçidi, DNS Sunucusu gibi) atamak için kullanılan servistir.DHCP’nin temel özelliği,sistemi kuran kişilerin tek tek tüm makineleri gezip aynı veya benzer parametreleri defalarca eliyle girmesini engellemek,böylece zaman kazanmak ve sistem yöneticisinin işini kolaylaştırmaktır.</P>
<P class="p119 ft5">DHCP aşağıdaki şekilde çalışır:</P>
<P class="p3 ft16">•DHCP Discover</P>
<P class="p120 ft5">İstemci bilgisayar ilk defa açıldığında öncelikle tüm ağa DHCP discover mesajını yollar. Bu mesajın içeriği,<SPAN class="ft8">“</SPAN>Sistemde herhangi bir DHCP sunucu bulunuyor mu?</P>
<P class="p38 ft5">Eğer var ise bir IP adresi istiyorum.<SPAN class="ft8">” </SPAN>olarak özetlenebilir.</P>
<P class="p121 ft5">Ağa gönderilen DHCP istek paketinde,istekte bulunulan IP adresi, MAC adresi ya da paketi gönderen bilgisayarın IP adresi bilinmediğinden, paketin içeriği aşağıdaki şekilde oluşacaktır:</P>
<P class="p42 ft5"><NOBR>1-Hedef</NOBR> IP adresi (Bilinmiyor): 255.255.255.255 (broadcast)</P>
<P class="p8 ft12"><NOBR>2-Hedef</NOBR> MAC adresi(Bilinmiyor): FF.FF.FF.FF.FF.FF.FF(broadcast)</P>
<P class="p8 ft27"><NOBR>3-Kaynak</NOBR> IP adresi(Bilinmiyor): 0.0.0.0</P>
<P class="p58 ft5"><NOBR>4-Kaynak</NOBR> MAC <NOBR>adresi:00-A0-CC-66-73-1F(Bu</NOBR> adres istemci bilgisayarın adresidir ve örnek olarak yazılmıştır.)</P>

<DIV id="page_20">


<P class="p8 ft16">•DHCP Offer</P>
<P class="p122 ft5">DHCP istemci tarafından sisteme atılan yayın paketi(broadcastpacket), DHCP sunucu tarafından alınır.IP veritabanı sorgulanır,istemciye verilecek IP adresi ve kira süresi belirlenir. Sunucudan çıkan isteğin onaylanması için istemciye bu belirlenen bilgiler geri yollanır. Sistemde birden fazla DHCP sunucu bulunabilir. Bu durumda,</P>
<P class="p28 ft5">istemci ağa bir istek gönderdiği zaman en hızlı DHCP offer mesajı yollayanın IP bilgilerini benimseyecek ve bu tanımlarla ağa bağlanacaktır.DHCP sunucusunun gönderdiği yanıt paketi aşağıdaki gibidir:</P>
<P class="p123 ft5"><NOBR>1-Hedef</NOBR> IP adresi (Henüz onaylanmadı): 0.0.0.0</P>
<P class="p3 ft5"><NOBR>2-Hedef</NOBR> MAC adresi(Biliniyor,istemci <NOBR>bilgisayar):00-A0-CC-66-73-1F</NOBR></P>
<P class="p3 ft5"><NOBR>3-Kaynak</NOBR> IP adresi(Biliniyor,DHCP sunucu): 10.0.0.1</P>
<P class="p3 ft5"><NOBR>4-Kaynak</NOBR> MAC adresi(Biliniyor, DHCP <NOBR>sunucu):00-A0-C0-B6-12-6F</NOBR></P>
<P class="p23 ft16">•DHCP Request</P>
<P class="p124 ft33">DHCP offer mesajını alan DHCP istemci, kendisine tahsis edilmiş IP adresini kiraladığına dair sunucuya bir yayın mesajı yollar.</P>
<P class="p125 ft31">Eğer DHCP istemci birden fazla DHCP offer mesajı almış ise ikinci bir broadcast mesajı daha yollar ve diğer DHCP sunuculara artık bir</P>
<P class="p126 ft5">IP adresine sahip olduğunu belirtir.</P>
<P class="p17 ft16">•DHCP Acknowledgement</P>
<P class="p127 ft5">DHCP request mesajını alan DHCP sunucu artık DHCP istemci için gerekli kayıtları gerçekleştirip ona gerekli olan IP,ağ maskesi,DNS adres veya adreslerini yollayacaktır.</P>

<DIV id="page_21">


#<P class="p8 ft13">2.2.6. TELNET</P>
<P class="p128 ft5"><SPAN class="ft16">Telnet, </SPAN>internet ağı üzerindeki çok kullanıcılı bir sunucuya, uzaktaki başka bir bilgisayardan bağlanmak için geliştirilen bir TCP/IP protokolü ve bu işi yapan programlara verilen genel isimdir. Bağlanılan bilgisayara girebilmek için bir kullanıcı isminizin ve bağlantının gerçekleşebilmesi için bir telnet erişim programınızın olması gereklidir.</P>
<P class="p129 ft5">Telnet 23 numaralı portu kullanmaktadır.Telnet güvensiz bir protokoldür. Tüm veriler,şifrelenmemiş olarak gönderilir. Bu yüzden telnet oturumundan, sniffer(koklayıcı) programları yardımıyla kolaylıkla önemli bilgilere ulaşılabilir.</P>
#<P class="p130 ft34">2.2.7. SSH</P>
<P class="p131 ft26">SSH, telnet gibi ağ üzerindeki bir sunucuya, uzakta bulunan bir başka bilgisayardan bağlantı sağlayan bir protokoldür. SSH açık haliyle “Secure Shell” yani güvenli kabuk anlamına gelir. Telnet’te, kullanıcı şifreleri dahil tüm iletişim açık yani şifrelenmeden</P>
<P class="p96 ft26">gerçekleştirilirken SSH güvensiz makineler arasındaki iletişimi, güçlü bir kripto yöntemiyle şifreler. SSH ile bağlantının gerçekleştirilebilmesi için Telnet ile bağlantıda olduğu gibi bağlanılmak istenen sunucu makinede bir kullanıcı hesabının ve kullanıcı şifresinin</P>
<P class="p80 ft5">bulunması gereklidir. Bunların dışında bir de SSH istemci programlarından birine ihtiyaç olacaktır. SSH ile bir bilgisayara bağlanabilmek için kullanıcı, öncelikle kimliğini ispatlayabilmelidir. SSH, 22 numaralı portu kullanır.</P>
#<P class="p132 ft13">2.2.8. SNMP</P>
<P class="p133 ft5">SNMP (Simple Network Management Protocol), ağ cihazlarının yönetimini ve izlenmesini kolaylaştıran bir uygulama katmanı protokolüdür. Bu protokol sayesinde ağdaki hemen her türlü cihaz izlenebilir hatta yapılandırmaları değiştirilebilir. SNMP, TCP/IP protokol kümesinin bir bileşenidir ve bir uygulama katmanı protokolü, veri tabanı şeması, veri nesneleri gibi standartlar barındırır.</P>
<P class="p126 ft5">SNMP’nin üç temel bileşeni vardır. Bunlar:</P>

<DIV id="page_22">


<P class="p134 ft5"><SPAN class="ft16">•NMS (Network Management System):</SPAN>Yönetici tarafında çalışan SNMP yazılımıdır.</P>
<P class="p23 ft5"><SPAN class="ft16">•Agent:</SPAN>Yönetilen cihaz tarafında çalışan yazılımdır.</P>
<P class="p135 ft5"><SPAN class="ft16">•MIB (Management Information Base):</SPAN>Her cihazın yerelinde bulunan, cihazdaki agent tarafından erişim sağlanan ve cihazla ilgili bilgileri bulunduran bir veri tabanıdır.</P>
<P class="p136 ft5">SNMP’nin çalışma mekanizması istek gönderme ve isteğe cevap alma şeklindedir ve bunun için taşıma katmanında kullandığı protokol UDP’dir. NMS istekleri herhangi bir portundan Agent’ın 161. portuna gönderir. İletişimi Agent’ın başlatması durumunda bildirimler NMS’in 162. portuna gönderilir. SNMP sayesinde bir cihazdan bilgi alınabileceği gibi cihazdaki bilgi değiştirilebilir ve cihazda yeni bir yapılandırma uygulanabilir. Örneğin cihaz baştan başlatılabilir, cihaza bir yapılandırma dosyası gönderilebilir ya da cihazdan alınabilir.</P>

<DIV id="page_23">


##<P class="p8 ft35">3. MODELLER VE PROTOKOLLER</P>
#<P class="p23 ft36">3.1. OSI Modeli ve Katmanları</P>
<P class="p137 ft5">Bilgisayar ağları kullanılmaya başlandığı ilk zamanlarda sadece aynı üreticinin ürettiği cihazlar birbirleriyle iletişim kurabiliyordu. Bu da şirketlerin,tüm cihazlarını sadece bir üreticiden almalarını zorunlu kılıyordu. 1970’lerin sonlarına doğru ISO (International Organization for <NOBR>Standardization<SPAN class="ft8">–</SPAN>Uluslararası</NOBR> Standartları Örgütü) tarafından, OSI (Open SystemInterconnection) modeli tanımlanarak bu kısıtlamanın önüne geçildi. Böylece farklı üreticilerden alınan cihazlar aynı ağ ortamında birbirleriyle haberleşebileceklerdi.OSI modeli, 7 k atmandan oluşmakta ve karmaşıklığı azaltmak, yeni standartlar geliştirmek amacıyla oluşturulmuştur.</P>
<P class="p138 ft5">OSI düzenlemelerinin en iyi fonksiyonlarından biri, tamamen farklı kullanıcı makineleri arasında veri transferine yardımcı olmasıdır. Yani, bir Unix host’u ve bir PC veya bir Mac arasında veri transferi yapılmasına izin verir.Buna rağmen, OSI fiziksel bir model değildir. Daha çok uygulama geliştiricilerin, bir ağda çalışan uygulamaları oluşturmak ve tamamlamak için kullanabildikleri bir kurallar bütünüdür. Ayrıca, ağ kurulumu standartları, cihazlar ve ağlar arası iletişim planları oluşturmak ve tamamlamak</P>
<P class="p8 ft21">için bir iskelet oluşturur.</P>
<P class="p8 ft14">OSI, temel olarak 2 gruba ayrılmış 7 katmana sahiptir.</P>
<P class="p134 ft5">Üstteki üç katman, uç istasyonlardaki uygulamaların birbirleri ve kullanıcılar ile nasıl iletişim kuracaklarını açıklar. Alttaki dört katman, verinin uçtan uca nasıl aktarılacağını açıklar.</P>

<DIV id="page_24">
<DIV id="p24dimg1">
<IMG src="http://www.abdullahvelioglu.com/blog/public/images/Resim2.4.png" id="p24img1">



<DIV class="dclr">
#<P class="p89 ft37">3.1.1.Uygulama Katmanı</P>
<P class="p140 ft5">Kullanıcıların bilgisayarlar ile iletişime geçtiği ve kullanıcıya en yakın olan katmandır. Uygulama katmanı bilgisayar ile ağ arasında monitör görevi görür. Diğer katmanlarda olduğu gibi bir üst katmanı olmadığı için o katmana servis sağlaması gibi bir durum da söz konusu değildir. Uygulamaların ağ üzerinde çalışması bu katmandan kontrol edilir. HTTP, TELNET, SSH, DNS, DHCP, SMTP, SNMP, FTP, TFTP gibi protokoller bu katmana aittir.</P>
#<P class="p141 ft7">3.1.2. Sunum Katmanı</P>
<P class="p142 ft6">Bu katmanda genel olarak yapılan iş,verinin diğer bilgisayarlar tarafından anlaşılabilir hâle gelmesini sağlamaktır. Verinin formatının belirlendiği katmandır. Ayrıca verinin sıkıştırılma, açılma ve şifrelenmesi gibi işlemlerin yapıldığı katmandır.</P>
#<P class="p89 ft7">3.1.3. Oturum Katmanı</P>
<P class="p143 ft5">İki bilgisayar arasında oturumun kurulması, kullanılması ve sonlanması bu katmanda yapılır. Bu katman, cihazlar veya düğümler arasında diyalog kontrolü de sağlar. Üç farklı mod (simplex, half</P>
<P class="p8 ft28">duplex ve fullduplex) önererek sistem ve hizmetler arası</P>
<P class="p8 ft5">ndaki iletişimi koordine eder ve düzenler. Birden fazla bilgisayarla</P>

<DIV id="page_25">


<P class="p52 ft11">iletişim halinde olunması durumunda doğru bilgisayarla haberleşmeyi sağlar. SMB, NFS, ISO8326, ISO 8327 protokolleri bu katmana aittir.</P>
#<P class="p144 ft38">3.1.4. Taşıma Katmanı</P>
<P class="p145 ft5">Taşıma katmanında üst katmandan gelen veri, segmentlere bölünür. Bu şekilde veri kaybı olması durumunda veriler daha küçük boyutlu olacağı için verilerin tekrardan gönderilmesi daha kolay olur. Bu katmanda verinin uçtan uca iletimi sağlanır. Veri iletimi sırasında verinin iletilip iletilmediği bu katmanda kontrol edilir ve gerekirse tekrardan gönderilme işlemi bu katmanda yapılır. Bu katmanda çalışan TCP ve UDP en bilinen protokollerdir.</P>
#<P class="p141 ft39">3.1.5. Ağ Katmanı</P>
<P class="p146 ft5">Ağ katmanı, verinin diğer ağlara gönderilmesi gerektiği durumda kullanılan IP adresinin eklendiği katmandır. Bu katmanda, verinin en iyi yoldan nasıl gönderileceği kararlaştırılır. Yönlendirme işlemi bu katmanda yapılan bir işlemdir. IP, ICMP ve ARP gibi protokoller bu katmanda görev yapar.</P>
#<P class="p147 ft39">3.1.6. Veri Bağlantısı Katmanı</P>
<P class="p148 ft33">Bu katmanda fiziksel katmana ulaşım için protokoller vardır. Yani verinin fiziksel ortama akışını kontrol eden katmandır.</P>
<P class="p149 ft5">Bu katmanda geçerli olan adres,MAC adresleridir. Yani ikinci katman cihazları MAC adresine göre anahtarlama yapar. Anahtar (Switch) ikinci katman cihazlarına örnektir. Bu katmanda akış kontrolü ile hatalı paketler kontrol edilip tekrar gönderilir. Ethernet, <NOBR>Token-Ring</NOBR> ve <NOBR>Wi-Fi</NOBR> bu katmanda çalışan protokollerdir.</P>
#<P class="p150 ft38">3.1.7. Fiziksel Katman</P>
<P class="p151 ft5">Fiziksel katman,adından da anlaşılabileceği gibi verinin fiziksel ortamlarda aktarımını sağlayan katmandır. Burada veri,bitler halinde gönderilir. Veri,farklı fiziksel ortamlarda gönderilebilir. Yani tüm başlıkları eklenmiş halde bulunan frameler elektrik, ışık veya dalga sinyalleri şeklinde gönderilebilir. Bu sinyallerin geçtiği fiziksel ortamlar da farklılık gösterir. Metal kablolar, fiberoptik kablolar veya havadan kablosuz bir şekilde iletilebilir. Tüm bu işlemlerin olmasını sağlayan protokoller sadece fiziksel katmanda tanımlıdır. Bu katmanda</P>
<P class="p152 ft11">çalışan cihaz olarak Dağıtıcı (Hub) örnek gösterilebilir. Dağıtıcı kendisine gelen sinyali tüm portlarına eşit bir şekilde iletir.</P>

<DIV id="page_26">
<DIV id="p26dimg1">
<IMG src="http://www.abdullahvelioglu.com/blog/public/images/Resim3.1.png" id="p26img1">



#<P class="p8 ft40">3.2. TCP/IP Modeli ve Katmanları</P>
<P class="p153 ft5">TCP/IP, DARPA (Defense Advanced ResearchProjectsAğency) ve Berkeley Software Distribution tarafından geliştirilen ve UNIX’de kullanılan bir protokoller grubudur. Günümüzde internetin temel protokolü olarak yerini almış TCP/IP’nin açılımı TransmissionControl Protocol / Internet Protocol’dür.TCP/IP modeli,OSI modelinden çok daha önce standartlaştığı için OSI içinde referans olmuş 4 katmanlı bir yapıdır.</P>
<P class="p154 ft7">•Uygulam a katmanı:</P>
<P class="p155 ft5">OSI</P>
<P class="p126 ft21">modelindeki Uygulama, Oturum ve Sunum</P>
<P class="p156 ft5">katmanlarına karşılık gelmekte ve o katmanların işlevlerini yerine getirmektedir. Bu katmanda TFTP, FTP, SMTP, SNMP gibi protokoller çalışmaktadır.</P>
<P class="p157 ft5"><SPAN class="ft7">•Taşıma katmanı: </SPAN>OSI modelindeki Taşıma katmanıyla birebir eşleştirilebilir. Bu katmanda iki farklı sınıfa ayrılabilecek iki protokol kullanılır. TCP ve UDP</P>
<P class="p158 ft5"><SPAN class="ft7">•Internet katmanı: </SPAN>OSI modelindeki Ağ katmanına denktir ve adresleme, en iyi yol seçimi gibi işlevleri yerine getirir.Bu katman da IP, ICMP,BOOTP, DHCP, ARP ve RARP gibi protokoller çalışmaktadır.</P>
<P class="p159 ft5"><SPAN class="ft7">•Ağarayüz katmanı:</SPAN>OSI modelindeki Veri Bağlantısı ve Fiziksel katmana denk gelmektedir.</P>

<DIV id="page_27">
<DIV id="p27dimg1">
<IMG src="http://www.abdullahvelioglu.com/blog/public/images/Resim3.2.png" id="p27img1">



<DIV class="dclr">
#<P class="p160 ft13">3.3. Veri Paketleme</P>
<P class="p137 ft5">Veri paketleri her katmandan geçtikçe hem başına hem de sonuna gerekli eklemeler yapılır ya da içeriği değiştirilebilir. Bu noktada katmanların her biri(ister OSI modeli içinde olsun isterse TCP/IP içinde), verileri her seferinde bir parça değiştirir ve içeriğini bozmadan verilerin nereye gideceği, ne iş için kullanılacağı ya da hangi katmanda değerlendirilmesi gerektiği gibi bilgiler eklenir. TCP/IP protokolünün katmanlarından çıkan bir veri paketinin başlık kısmında, temelde port numarası, ulaşacağı IP adresi yazılıdır. Veri paketleri, OSI katmanlarında hareket ettikçe, değişikliğe uğrar.Ethernet teknolojisiyle taşınacak IP paketleri artık Ethernet teknolojisi ile gönderilecek şekle dönüştürülür. Bu dönüştürme işlemi için IP paketleri Ethernet paketlerinin (Ethernet Frame’lerinin) içine eklenir. Bu işleme ise (kapsülleme manasına gelen) encapsulation adı verilmiştir.</P>
<P class="p63 ft5">ARP işlemi ve ARP protokolünün getirdiği veriler ise Ethernet</P>

<DIV id="page_28">
<DIV id="p28dimg1">
<IMG src="http://www.abdullahvelioglu.com/blog/public/images/Resim3.3.png" id="p28img1">



<P class="p161 ft5">Frame’lerine eklenmektedir. IP paketinin başlığında hedef ve kaynak IP adresleri yazar, Ethernet Frame’inin başlığında ise hedef ve kaynak MAC adresleri yazmaktadır.</P>
<P class="p162 ft33">Veri paketleme 5 adımdan oluşur:</P>
<P class="p163 ft22"><SPAN class="ft16">•</SPAN>Uygulama, Sunum ve Oturum Katmanları kullanıcının girdiği veriyi 4. katman yani Taşıma katmanına kadar getirir.</P>
<P class="p164 ft32"><SPAN class="ft16">•</SPAN>Taşıma katmanı kendisine gelen bilgiyi segment adı verilen bölümlere ayırır ve verinin hangi protokolle gönderileceği (TCP <NOBR>-UDP)</NOBR> bilgisini de ekleyerek ağ katmanına gönderir.Bu katmana gelen segment burada paketlere ayrılır ve IP başlığı denen, hedef ve kaynak IP’ler gibi bilgileri ,bulunduğu başlığı ekleyerek bir alt katman olan Veri Bağlantısı katmanına gönderir.</P>
<P class="p162 ft31"><SPAN class="ft16">•</SPAN>Burada veri artık framelere çevrilir ve MAC adresleri eklenir.</P>
<P class="p162 ft5"><SPAN class="ft16">•</SPAN>Frame yapısı katmanlara ayrılır ve iletilir.</P>
