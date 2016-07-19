---
layout: post
title: CentOS 6.x Netinstall
tags: [networking]
---



<p style="text-align: left;"><a href="https://www.syslogs.org/tag/centos/" class="st_tag internal_tag" rel="tag" title="Posts tagged with CentOS">CentOS</a>&#8217;un netinstall özelliği küçük bir iso imajı kullanarak network üzerinden kurulum yapmayı mümkün kılan pratik bir yöntem. Basit olarak sisteminizi daha önceden indirdiğiniz bir netinstall iso&#8217;su ile boot edip kurulumu başlatıyorsunuz ve gerekli olan tüm dosyalar internetten indirilerek kurulum tamamlanıyor.</p>
<p style="text-align: left;">Kurulum sırasında dosyalar http üzerinden herhangi bir web sunucusundan ya da nfs üzerinden bir network paylaşımından download edilecek şekilde yapılabildiği için her seferinde güncel <a href="https://www.syslogs.org/tag/centos/" class="st_tag internal_tag" rel="tag" title="Posts tagged with CentOS">CentOS</a> cd ya da dvd&#8217;si indirmenize gerek kalmıyor.</p>
<p style="text-align: left;">Yazının devamında http üzerinden <a href="https://www.syslogs.org/tag/centos/" class="st_tag internal_tag" rel="tag" title="Posts tagged with CentOS">centos</a>.org kullanılarak netinstall yönetmi ile <a href="https://www.syslogs.org/tag/centos/" class="st_tag internal_tag" rel="tag" title="Posts tagged with CentOS">CentOS</a> 6.x kurulumun nasıl yapılabileceğinden bahsedeceğim.</p>
<p><span id="more-9801"></span></p>
<p style="text-align: left;">Netinstall&#8217;un dvd ya da cd üzerinden yapılan klasik kurulumlardan tek farkı sistemi netinstall.iso imajı üzerinden boot etmek ve kurulum dosyalarının nereden download edileceğini belirtmektir. İşlemler sırası ile şu şekildedir:</p>
<span id="Download_netinstall.iso"><h3>Download netinstall.iso</h3></span>
<p style="text-align: left;">Şu anki güncel CentOS sürümü 6.4.  Bu sürüme ait netinstall iso&#8217;sunu işlemci mimarinize göre download edin.</p>
<p style="text-align: left;">32bit için: <a href="ftp://ftp.linux.org.tr/centos/6/isos/i386/CentOS-6.8-i386-netinstall.iso" target="_blank" rel="nofollow">http://ftp.linux.org.tr/centos/6.4/isos/i386/CentOS-6.4-i386-netinstall.iso</a><a href="ftp://ftp.linux.org.tr/centos/6/isos/i386/CentOS-6.8-i386-netinstall.iso" target="_blank" rel="nofollow"><br />
</a>64bit için: <a href="ftp://ftp.linux.org.tr/centos/6/isos/x86_64/CentOS-6.8-x86_64-netinstall.iso" target="_blank" rel="nofollow">http://ftp.linux.org.tr/centos/6.4/isos/x86_64/CentOS-6.4-x86_64-netinstall.iso</a></p>
<p style="text-align: left;">Download için herhangi başka bir centos.org mirror&#8217;ını kullanmak isterseniz de <a href="http://mirror.centos.org" target="_blank" rel="nofollow">http://mirror.centos.org</a> adresinden yararlanabilirsiniz.</p>
<span id="Netinstall.iso_zerinden_boot"><h3>Netinstall.iso üzerinden boot</h3></span>
<p style="text-align: left;">netinstall.iso&#8217;yu bir cd&#8217;ye yazdıktan sonra sistemi bu cd üzerinden boot ediyoruz. Boot işlemi klasik welcome ekranını getiriyor:<br />
<img class="aligncenter" alt="CentOS 6.2 Kurulumu - Welcome Screen" src="http://www.abdullahvelioglu.com/blog/public/images/centos1.png" width="600" border="0" /></p>
<p>&#8220;<strong>Install or upgrade an existing system</strong>&#8221; seçeneğinden kurulumu başlatıyoruz.</p>
<span id="Check_Disk"><h3>Check Disk</h3></span>
<p style="text-align: left;">Sistem boot edildiğinde ilk olarak aşağıda görülen netinstall diskini herhangi bozukluğa karşı kontrol etmek isteyen test ekranı geliyor. Kurulum cd&#8217;nizin düzgün olduğunundan eminseniz bu adıma <strong>&#8220;skip&#8221;</strong> diyebilirsiniz:<br />
<img class="aligncenter" alt="Check Disc" src="http://www.abdullahvelioglu.com/blog/public/images/centos2.png" width="600" border="0" /></p>
<span id="Dil_Seimi"><h3>Dil Seçimi</h3></span>
<p style="text-align: left;">Bir sonraki adım sistem dilinin ne olacağını seçtiğimiz ekrandır:<br />
<img class="aligncenter" alt="Dil" src="http://www.abdullahvelioglu.com/blog/public/images/centos3.png" width="600" border="0" /></p>
<p>Ben sistemin orjinal diline sadık kalarak burada <strong>&#8220;English&#8221;</strong>&#8216;i seçip devam ediyorum.</p>
<span id="Klavye_Tipi"><h3>Klavye Tipi</h3></span>
<p style="text-align: left;">Sonraki ekran keyboard tipini seçtiğimiz aşağıdaki ekrandır:<br />
<img class="aligncenter" alt="Klavye - trq" src="http://www.abdullahvelioglu.com/blog/public/images/centos4.png" width="600" border="0" /></p>
<p>Burada da türkçe q klavye için <strong>&#8220;trq&#8221;</strong> seçeneğini işaretliyorum.</p>
<span id="Kurulum_Metodu"><h3>Kurulum Metodu</h3></span>
<p style="text-align: left;">Şimdiki ekran, kurulum metodunun seçileceği bölümdür:<br />
<img class="aligncenter" alt="Kurulum Metodu" src="http://www.abdullahvelioglu.com/blog/public/images/centos5.png" width="600" border="0" /></p>
<p>Gördüğünüz gibi kurulumu 4 farklı mecra üzerinden yapabilmek mümkün. Biz netinstall metodu ile internet üzerinden kurulum yapmak istediğimizden dolayı bu aşamada <strong>&#8220;URL&#8221;</strong> seçeneğinden gidiyoruz.</p>
<span id="TCPIP_Yaplandrmas"><h3>TCP/IP Yapılandırması</h3></span>
<p style="text-align: left;">Dosyalar internetten download edileceği için kurulumun bu aşamasında IP ayarlarının yapılacağı ekran gelir:<br />
<img class="aligncenter" alt="TCP/IP Yapılandırması" src="http://www.abdullahvelioglu.com/blog/public/images/centos6.png" width="600" border="0" /></p>
<p>Ekranda da gördüğünüz gibi burada en azından IPv4 desteğini etkinleştirmek gerekiyor. Sonrasında ise networkünüzde bir DHCP sunucu var ise sisteme otomatik IP atanması için <strong>&#8220;Dynamic IP configuration (DHCP)&#8221;</strong> seçeneğini seçebilir ya da DHCP ortamınız yok ise benim gibi IP yapılandırmasını manual olarak yapmak için <strong>&#8220;Manual Configuration&#8221;</strong> seçeneğinden gidebilirsiniz.</p>
<span id="Manual_IP_Yaplandrmas"><h3>Manual IP Yapılandırması</h3></span>
<p style="text-align: left;">Bir önceki seçenekte DHCP üzerinden gittiyseniz bu aşamayı atlayabilirsiniz. Ancak eğer manual configuration seçeneğinden gittiyseniz, IP tanımlamalarının yapılacağı aşağıdaki ekran gelecektir:<br />
<img class="aligncenter" alt="Manual TCP/IP Yapılandırması" src="http://www.abdullahvelioglu.com/blog/public/images/centos7.png" width="600" border="0" /></p>
<p>Bu bölümde kendi networkünüze ait IP tanımlarını doğru bir şekilde yapıp ilerleyin.</p>
<span id="Download_URL"><h3>Download URL</h3></span>
<p style="text-align: left;">Şimdiki aşamada ise download işlemlerinin yapılacağı mecranın tam URL&#8217;sini yazacağımız ekran gelecektir:<br />
<img class="aligncenter" alt="URL Setup" src="http://www.abdullahvelioglu.com/blog/public/images/centos8.png" width="600" border="0" /></p>
<p>Bu aşamada yukarıda gördüğünüz gibi dosyaların CentOS sunucularından download edilmesi için mirror.centos.org url&#8217;sini girmeniz gerekiyor. Sistem mimarinize göre kullanabileceğiniz tam URL&#8217;ler aşağıdaki gibidir:</p>
<p><strong>32bit için :</strong> http://mirror.centos.org/centos/6/os/i386<br />
<strong>64bit için :</strong> http://mirror.centos.org/centos/6/os/x86_64</p>
<span id="Downloading8230"><h3>Downloading&#8230;</h3></span>
<p style="text-align: left;">Bundan sonraki aşamada da aşağıda görüldüğü gibi gerekli imaj dosyaları download edilecektir:<br />
<img class="aligncenter" alt="Downloading" src="http://www.abdullahvelioglu.com/blog/public/images/centos9.png" width="600" border="0" /></p>
<span id="Grafiksel_Kurulum_Balangc"><h3>Grafiksel Kurulum Başlangıcı</h3></span>
<p style="text-align: left;">Download işlemlerinden sonra asıl grafiksel kurulum ekranı gelir:<br />
<img class="aligncenter" alt="CentOS Kurulumu Part 2" src="http://www.abdullahvelioglu.com/blog/public/images/centos10.png" width="600" border="0" /></p>
<span id="Depolama_Biriminin_Seilmesi"><h3>Depolama Biriminin Seçilmesi</h3></span>
<p style="text-align: left;">Bu bölümde kurulumun ne tip bir depolama alanı üzerine yapılacağının belirlendiği aşağıdaki ekran gelecektir:<br />
<img class="aligncenter" alt="Depolama Biriminin Secilmesi" src="http://www.abdullahvelioglu.com/blog/public/images/centos11.png" width="600" border="0" /></p>
<p>Biz kurulumu tipik olarak sistemin kendi üzerindeki diske yapacağımız için bu aşamada <strong>&#8220;Basic Storage Devices&#8221;</strong> seçeneğini işaretleyip next diyoruz.</p>
<span id="Depolama_Birimi_Data_Uyars"><h3>Depolama Birimi Data Uyarısı</h3></span>
<p style="text-align: left;">Bir önceki ekrana next dediğiniz zaman kurulum sistemdeki diski algılayacak ve devam etmeniz durumunda disk üzerindeki datanın uçabileceğini söyleyen aşağıdaki uyarıyı çıkaracaktır:<br />
<img class="aligncenter" alt="Depolama Birimi Uyarisi" src="http://www.abdullahvelioglu.com/blog/public/images/centos12.png" width="600" border="0" /></p>
<table class="tip" width="100%" border="0">
<tbody>
<tr>
<td width="55"><img alt="" src="http://www.syslogs.org/images/tips.gif" /></td>
<td width="545"><strong>NOT:</strong> Bu uyarı disk üzerinde herhangi bir dosya sistemi ya da partisyon tablosu tespit edilemediği durumlarda görüntülenir. Ben kurulumu bir sanal disk üzerine yaptığımdan ve üzerinde daha önceden kurulmuş herhangi bir dosya sistemi bulunmadığından bu uyarı verilmektedir.</td>
</tr>
</tbody>
</table>
<p>Sonuç olarak bu uyarıya <strong>&#8220;Yes, discard any data&#8221;</strong> diyerek devam ediyoruz.</p>
<span id="Hostname"><h3>Hostname</h3></span>
<p style="text-align: left;">Şimdiki adım ise sistemin hostname&#8217;inin belirlendiği bölümdür:<br />
<img class="aligncenter" alt="Hostname" src="http://www.abdullahvelioglu.com/blog/public/images/centos13.png" width="600" border="0" /></p>
<p>Bir isim belirledikten sonra nex diyelim.</p>
<span id="Timezone"><h3>Timezone</h3></span>
<p style="text-align: left;">Bu bölümde de sistem tarih ve saatinin set edilmesi için timezone belirlenir:<br />
<img class="aligncenter" alt="Timezone" src="http://www.abdullahvelioglu.com/blog/public/images/centos14.png" width="600" border="0" /></p>
<p>Basitçe haritadan sistemin bulunduğu konumu seçip next ediyoruz.</p>
<span id="Root_Password"><h3>Root Password</h3></span>
<p style="text-align: left;">Şimdiki adımda root password&#8217;ünün belirlenmesi gerekiyor:<br />
<img class="aligncenter" alt="Root Password" src="http://www.abdullahvelioglu.com/blog/public/images/centos15.png" width="600" border="0" /></p>
<p>Şifrenizi belirleyip next ile devam edin.</p>
<span id="Kurulum_Tipi"><h3>Kurulum Tipi</h3></span>
<p style="text-align: left;">Sonraki adım kurulum tipinin belirlenmesidir:<br />
<img class="aligncenter" alt="Kurulum Tipinin Belirlenmesi" src="http://www.abdullahvelioglu.com/blog/public/images/centos16.png" width="600" border="0" /></p>
<p>Bu bölümde kurulumun diski ne şekilde kullanacağını belirtiyoruz. Bu aşamada default olarak gelen <strong>&#8220;Replace existing <a href="https://www.syslogs.org/tag/linux/" class="st_tag internal_tag" rel="tag" title="Posts tagged with linux">Linux</a> System(s)</strong> seçeneği üzerinden giderek, (varsa) sadece <a href="https://www.syslogs.org/tag/linux/" class="st_tag internal_tag" rel="tag" title="Posts tagged with linux">Linux</a> bölümlerinin kaldırılması ve otomatik olarak yeni bir disk bölümü oluşturulmasını sağlıyoruz. Böylece diskte herhangi başka dosya sistemine sahip bir disk bölümü varsa aynı şekilde korunuyor ve sadece eski <a href="https://www.syslogs.org/tag/linux/" class="st_tag internal_tag" rel="tag" title="Posts tagged with linux">Linux</a> kurulumu kaldırılıyor.</p>
<p>Kendinize özel bir disk bölümlemesi yapmak için <strong>&#8220;Create Custom Layout&#8221;</strong> seçeneğinden de gidebilirsiniz. Ayrıca default olarak oluşturulacak disk bölümlemesini görmek ve isterseniz değişiklik yapmak için de ekranın en altındaki <strong>&#8220;Review and modify partitioning layout&#8221;</strong> checkbox&#8217;ını işaretleyebilirsiniz. Ancak ben default kurulum üzerinden gittiğim için o bahsettiğim işlemlere ait bilgilere ve ekran görüntülerine değinmeyeceğim.</p>
<span id="Disk_Yaplandrmasnn_Tamamlanmas"><h3>Disk Yapılandırmasının Tamamlanması</h3></span>
<p style="text-align: left;">Bir önceki ekrandandan sonra, disk bölümleme işlemlerinin yapılarak diske yazılacağından bahseden aşağıdaki ekran gelir:<br />
<img class="aligncenter" alt="Write to disk" src="http://www.abdullahvelioglu.com/blog/public/images/centos17.png" width="600" border="0" /></p>
<p>Bu ekranda <strong>&#8220;Write changes to disk&#8221;</strong> diyerek disk bölümleme, boot loader vs. ile ilgili tüm işlemlerin otomatik olarak yapılmasını sağlıyoruz.</p>
<span id="Kurulacak_Paketlerin_Seilmesi"><h3>Kurulacak Paketlerin Seçilmesi</h3></span>
<p style="text-align: left;">Disk ile alakalı işlemlerden sonra sisteme hangi paketlerin kurulacağını belirlediğimiz aşağıdaki ekran gelir:<br />
<img class="aligncenter" alt="Minimal Kurulum" src="http://www.abdullahvelioglu.com/blog/public/images/centos18.png" width="600" border="0" /></p>
<p>Bu kısımda sistemin kullanım amacına uygun paketlerin yüklenmesi için &#8220;Desktop, Web Server, Database Server vs.&#8221; gibi seçenekleri kullanabilirsiniz. Ben her zaman için kurulumları mümkün olduğu kadar az paket yüklenmiş halde yapmak istedğimden hep <strong>&#8220;Minimal&#8221;</strong>&#8216;i seçer, kurulum sonrasında ihtiyacım olan paketleri ayrıca kurarım. Bu yüzden bu seçeneği işaretleyip next diyorum.</p>
<span id="Kurulumun_Balamas"><h3>Kurulumun Başlaması</h3></span>
<p style="text-align: left;">Yüklenecek paketlerin belirlenmesinden sonra kurulum başlatılır:<br />
<img class="aligncenter" alt="Kurulumun Baslamasi" src="http://www.abdullahvelioglu.com/blog/public/images/centos19.png" width="600" border="0" /></p>
<span id="Paketlerin_Yklenmesi"><h3>Paketlerin Yüklenmesi</h3></span>
<p style="text-align: left;">Kurulum sürecinin başlatılmasından sonra tüm paketlerin yükleneceği son kurulum aşamasına geçilir:<br />
<img class="aligncenter" alt="Paketlerin Yüklenmesi" src="http://www.abdullahvelioglu.com/blog/public/images/centos20.png" width="600" border="0" /></p>
<span id="Kurulumun_Sonlandrlmas"><h3>Kurulumun Sonlandırılması</h3></span>
<p style="text-align: left;">Paketlerin yüklenmesinden sonra, kurulumun tamamlandığını belirten aşağıdaki ekran gelir:<br />
<img class="aligncenter" alt="Kurulumun tamamlanması" src="http://www.abdullahvelioglu.com/blog/public/images/centos21.png" width="600" border="0" /></p>
<p>Netinstall cd&#8217;sini çıkarıp &#8220;Reboot&#8221; butonuna basarak kurulumu tamamlayabilirsiniz.</p>
<span id="lk_Login"><h3>İlk Login</h3></span>
<p style="text-align: left;">Reboot ettikten sonra sistem sorunsuz olarak açılacaktır:<br />
<img class="aligncenter" alt="First Login" src="http://www.abdullahvelioglu.com/blog/public/images/centos22.png" width="600" border="0" /></p>
<p>root sifreniz ile login olabilirsiniz.</p>
<p>Bu şekilde netinstall.iso imajını kullanarak internet üzerinden kurulum yapmış oluyoruz.</p>
