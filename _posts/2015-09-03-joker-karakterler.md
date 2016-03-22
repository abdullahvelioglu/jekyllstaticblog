---
layout: post
title: LINUX_WILDCARDS(JOKER_KARAKTERLER)
tags: [linux]
---

<p>
Linux işletim sistemi, yazdığınız komutları daha kısa ve işlevsel hale getiren joker karakterleri(wildcards) desteklemektedir.
<b>Wildcard</b>&#39; lar, size, nispeten daha kompleks işlemler yaparken, kolaylık sağlar. Örnek olarak bir dizin altında bulunan .cfg uzantılı dosyaları
başka bir dizine kopyalamak istediğimizi düşünelim. Bunun için normal şartlar altında, ya bir görsel arayüz programı kullanarak, ya da tüm dosyaları tek tek
kopyala komutu kullanarak, kaynak dosyaları başka bir dizine yerleştirebiliriz. Ancak wildcards&#39; lar sayesinde aşağıdaki gibi, çok daha kısa bir söz dizimi ile bu işlemi kolaylıkla gerçekleştirebiliriz.
</p>

<pre>
cp ~/workspace/*.cfg ~/workspace2
</pre><br/>

<p>
Linux, <i>globbing</i> olarak da anılan, bir çok joker karakter tanımlamıştır. Bunların her biri aşağıdaki tabloda açıklanmaktadır.
</p>
<h3>Joker Karakterler(Wildcards)</h3>
<table style="border: 1px #ddd solid; padding-left:3em;">
<th>Wildcard, Joker Karakter</th>
<th style="padding-left:2em;">Anlamı</th>
<tr>
<td>*</td><td style="padding-left:4em;">Bütün karakterler, çoğul seçim</td>
</tr>

<tr>
<td>?</td><td style="padding-left:4em;">Herhangi bir karakter, tekil seçim</td>
</tr>

<tr>
<td>[karakterler]</td><td style="padding-left:4em;">Karakter kümesi, veya operatörü ile çalışır.</td>
</tr>

<tr>
<td>[!karakterler]</td><td style="padding-left:4em;">Karakter kümesi haricinde demektir.</td>
</tr>

<tr>
<td>[[:sınıf:]]</td><td style="padding-left:4em;">Belirtilen bir karakter sınıfına ait olan eşleşme. Karakter sınıfları bir sonraki tabloda anlatılmaktadır.</td>
</tr>
</table><br/>

<h3>Karakter Sınıfları(Character Classes)</h3>
<table style="border: 1px #ddd solid; padding-left:3em;">
<th>Karakter sınıfı</th>
<th style="padding-left:2em;">Anlamı</th>
<tr>
<td>[:alnum:]</td><td style="padding-left:4em;">Herhangi bir alfanumerik karakter</td>
</tr>

<tr>
<td>[:alpha:]</td><td style="padding-left:4em;">Herhangi bir alfabetik karakter</td>
</tr>

<tr>
<td>[:digit:]</td><td style="padding-left:4em;">Herhangi bir rakam</td>
</tr>

<tr>
<td>[:lower:]</td><td style="padding-left:4em;">Herhangi bir küçük harfli karakter</td>
</tr>

<tr>
<td>[:upper:]</td><td style="padding-left:4em;">Herhangi bir büyük harfli karakter</td>
</tr>
</table>

<h3>Örnekler</h3>
<pre>
*.cfg -> Sonu .cfg ile biten dosyalar

A*.cfg -> A ile başlayan Sonu .cfg ile biten dosyalar

???.txt-> 3 harfli olup sonu .txt ile biten dosyalar

[abc]* -> a, b ya da c ile başlayan dosyalar

Version.[:digit:] [:digit:] -> Version.<i>rakam rakam</i> formatındaki dosyalar

*[[:upper:]] -> Sonu buyuk harfli biten dosyalar

*[[:lower:]012] -> Sonu küçük harfli biten veya 0, 1 ya da 2 ile biten dosyalar

[![:digit:]]* -> Başı rakamla başlamayan dosyalar
