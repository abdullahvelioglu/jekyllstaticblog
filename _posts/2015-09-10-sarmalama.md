---
layout: post
title: SARMALAMA(ENCAPSULATION)
tags: [programminglanguage]
---


Nesne yönelimli programlamanın felsefelerinden biri olan sarmalama(encapsulation),bulunduğu sınıf içerisinde kod ve veriyi bir bütün halinde kaplayarak(sarmalayarak) dış etkilerden koruyan bir soyut düşünce yapısıdır.Koruma ilgili programlama dilinin söz dizimine bağlı olarak gerçekleşsede genel olarak <b>public</b> ve <b>private</b> erişim belirteçleri ile sağlanmaktadır.Koruma güdüsü,tamamen iyi niyetli programcıların yanlışlıkla veriyi değiştirebileceği korkusu üzerine ön plana çıkmıştır.
<br/><br/>
Sık kullanılan C++,Java ve C# gibi nesne yönelimli programlama dillerinde,sarmalamanın temelinde <b>sınıf(class)</b> kavramı yatmaktadır.Bu dillerde bir sınıf oluşturulduğu zaman,içerisindeki üyeler kod ve verilerden oluşmaktadır.Veriler üye değişkenler(member instances) olarak adlandırılırken,kodlar ise üye metotlar(member methods) olarak adlandırılır.
<br/><br/>
Sarmalama örnek olarak çeşitli dillerde örnek olarak sınıflar ile verilebilir.
<h4 style="color:red;">C++</h4>
<pre>
<b>class</b> People
{
<b>private:</b>
<b>int</b> height;
<b>int</b> weight;
<b>char</b> *eyeColor;

<b>public:</b>
<b>int</b> getHeight() { <b>return</b> height; }
/*
.
.
.
.
.
*/
};
</pre>
<h4 style="color:red;">Java</h4>
<pre>
<b>public class</b> People
{
<b>private int</b> height;
<b>private int</b> weight;
<b>private String</b> eyeColor;

<b>public int</b> getHeight() { <b>return</b> height; }
/*
.
.
.
.
.
*/
}
</pre>
<h4 style="color:red;">C#</h4>
<pre>
<b>public class</b> People
{
<b>private int</b> height;
<b>private int</b> weight;
<b>private String</b> eyeColor;

<b>public int</b> getHeight() { <b>return</b> height; }
/*
.
.
.
.
.
*/
}
</pre>
Yukarıda da görüldüğü gibi bir insan sınıfı(People),boy,kilo ve göz rengi gibi bir takım veriler ile bu verileri işleyen metotları parselleyerek tek bir arabirim olarak tanımlamaktadır.Ayrıca bu mantıksal arabirimi <b>public</b> ve <b>private</b> erişim belirteçleri ile bu verileri programın dışındaki yan etkilerden de korumaktadır. </td> </tr>
                    </table>
