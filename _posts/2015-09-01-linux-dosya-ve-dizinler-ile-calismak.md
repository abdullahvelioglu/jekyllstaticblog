---
layout: post
title: LINUX DOSYA VE DIZINLER ILE CALISMAK
tags: [linux]
---

<p>
Linux işletim sisteminde dosya(file) ve dizin(directory) işlerinde temel olarak kullanılan 5 adet komut(command) bulunmaktadır. Bu komutlar, kopyalama işlemi yapan <b>cp</b>, dosya taşıma ve yeniden adlandırma işlemi yapan <b>mv</b>, dosya oluşturan <b>mkdir</b>, dosya ve dizin silen <b>rm</b> ve hard ve sembolik linkler oluşturmaya yarayan <b>ln</b> komutlarıdır. Bu yazıda Linux dosya işlemlerinin temelini oluşturan bu komutların her biri anlatılacaktır.
</p>
<h3>Dizin oluşturmak - mkdir komutu</h3>
<p>Bir dosya veya dizin oluşturmak için basitçe <b>mkdir</b>(make directory) komutu kullanılır. Genel formu ve örnekleri aşağıdaki gibidir.</p>
<pre>
mkdir directory...

mkdir directory1

mkdir directory1 directory2 directory3
</pre>
<h3>Dosya ve Dizin kopyalamak - cp komutu</h3>
<p>Bazen bir GUI programına nazaran, dosya/dizin kopyalama işlemlerini <b>cp</b> komutu ile yapmak çok daha kolaylık ve hız sağlar. Özellikle <a href="http://www.abdullahvelioglu.com/blog/2015/09/03/joker-karakterler/" target="_blank">Joker Karakterler(Wildcards)</a> kullanılarak koşturulan bazı komutlar ciddi zaman kazandırır. <i>cp(copy)</i> komutunun genel formu ve örnekleri aşağıdaki gibidir.</p>
<pre>
cp source destination

cp source1, source2 destination

cp sources... destination

Samples

cp tmp/a.txt root/a.txt -> tmp altında bulunan a.txt, root altında bulunan a.txt olarak kopyalanır.

cp -i tmp/a.txt root/a.txt -> eğer root altında a.txt var ise, kullanıcıdan onay istenir.

cp root/a.txt root/b.txt /var/etc -> a ve b dosyaları /var/etc/ altına kopyalanır.

cp root/* /var/etc -> root altındaki tüm dosyalar /var/etc altına kopyalanır.
</pre>
<br/>
<p>cp komutu bir takım option&#39; lar ile birlikte kullanıldığında, farklı işlevsellikler de sağlar. Aşağıda cp komutu ile birlikte kullanılan option&#39; lar açıklanmaktadır.</p>
<table style="border: 1px #ddd solid; padding-left:3em;">
<th>Option</th>
<th></th>
<th>Tanım</th>
<tr>
<td>-a</td> <td>--archive</td> <td>Dosya ve dizinleri sahiplik ve hakları dahil olmak üzere tüm özellikleri(attributes) ile kopyalar.</td>
</tr>

<tr>
<td>-i</td> <td>--interactive</td> <td>Dosyalar hedef dizin altına atılmadan önce, var olan bir dosyanın üstüne yazılıp yazılmaması konusunda(overwrite) kullanıcının onayına sunulur. Bu komut belirtilmez ise Linux dosyaları hedef dizin üzerine yazar.</td>
</tr>

<tr>
<td>-r</td> <td>--recursive</td> <td>Dizinleri kopyalarken içindeki dosya ve dizinleri ile birlikte kopyalar. Dizin kopyalama sırasında bu komutun veya -a komutunun yazılması gereklidir.</td>
</tr>

<tr>
<td>-u</td> <td>--update</td> <td>Bu komut ile hedef dizin altında kaynak dosyadan hiç yoksa, veya kaynak dosya hedef dizindeki dosyadan daha yeni bir sürüme sahipse çalışır.</td>
</tr>

<tr>
<td>-v</td> <td>--verbose</td> <td>Kopyalama işlemlerini bilgi mesajı olarak ekrana basar.</td>
</tr>
</table>
<h3>Dosya taşımak ve yeniden adlandırmak - mv komutu</h3>
<p>Dosyalara yeni isim vermek ve onları bir yerden başka bir yere taşımak(kes ve yapıştır, cut and paste) istediğiniz zaman <b>mv</b>(move) komutu yazmanız yeterlidir. <b>mv</b> komutunun genel formu ve örnekleri aşağıda verilmektedir. <b>mv</b> komutu --interactive, --update ve --verbose seçenekleri(option) ile birlikte kullanıldığında zengin işlevsellik sağlar.</p>
<pre>
mv source destination

mv item... directory

mv root/a.txt root/b.txt -> a dosyasının adını b olarak değiştirir.
mv -i root/a.txt root/b.txt -> a dosyasının adını b olarak değiştirmeden önce kullanıcıya sorar.
mv root/a.txt root/b.txt /var a ve b dosyalarını /var altında taşır.
mv dir1 dir2 -> dir1 dizinini dir2 ye taşır.
</pre>
<table style="border: 1px #ddd solid; padding-left:3em;">
<th>Option</th>
<th></th>
<th>Tanım</th>
<tr>
<td>-i</td> <td>--interactive</td> <td>Dosyalar hedef dizin altına taşınmadan önce, var olan bir dosyanın üstüne yazılıp yazılmaması konusunda(overwrite) kullanıcının onayına sunulur. Bu komut belirtilmez ise Linux dosyaları hedef dizin üzerine yazar.</td>
</tr>

<tr>
<td>-u</td> <td>--update</td> <td>Bu komut ile hedef dizin altında kaynak dosyadan hiç yoksa, veya kaynak dosya hedef dizindeki dosyadan daha yeni bir sürüme sahipse çalışır.</td>
</tr>

<tr>
<td>-v</td> <td>--verbose</td> <td>Taşıma işlemlerini bilgi mesajı olarak ekrana basar.</td>
</tr>
</table>
<h3>Dosya ve Dizinleri silmek - rm komutu</h3>
<p>Dosya ve dizinleri basitçe <b>rm</b>(remove) komutu ile silebilirsiniz. <b>rm</b> komutunun genel formu ve örnekleri aşağıda verilmektedir. <b>rm</b> komutu --interactive, --recursive, --force ve --verbose seçenekleri(option) ile birlikte kullanıldığında zengin işlevsellik sağlar.</p>
<pre>
rm item...

rm root/a.txt -> a dosyasını sessizce siler.
rm -i root/a.txt -> a dosyasını silmeden önce kullanıcıya sorar.
rm -r root/a.txt /tmp-> a dosyasını ve tmp dizinini siler.
rm -rf root/a.txt /tmp ->
</pre>
<table style="border: 1px #ddd solid; padding-left:3em;">
<th>Option</th>
<th></th>
<th>Tanım</th>
<tr>
<td>-i</td> <td>--interactive</td> <td>Dosyalar veya dizinler silinmeden önce kullanıcının onayına sunulur.</td>
</tr>

<tr>
<td>-r</td> <td>--recursive</td> <td>Dosya ve dizinler altındaki dosya ve dizinler ile birlikte silinir.</td>
</tr>

<tr>
<td>-f</td> <td>--force</td> <td>Dosyaları bulunmasa bile, kullanıcıya sormadan siler. --interactive seçeneğini devre dışı bırakır.</td>
</tr>

<tr>
<td>-v</td> <td>--verbose</td> <td>Silme işlemlerini bilgi mesajı olarak ekrana basar.</td>
</tr>
</table>
<h3>Link oluşturma - ln komutu</h3>
<p>Linux sisteminizde dosya ve dizinleri temsil eden bağlantı dosyaları oluşturabilirsiniz. Bunun için <a href="http://www.abdullahvelioglu.com/blog/2015/09/12/hard-links/" target="_blank">Hard Links</a> ve  <a href="http://www.abdullahvelioglu.com/blog/2015/09/13/symbolic-links/" target="_blank">Symbolic Links</a> kavramları bulunur. Linklerin genel formu aşağıda verilmektedir. </p>
<pre>
ln file link -> hard link oluşturur

ln -s item link -> symbolic link oluşturur.
</pre><br/>
