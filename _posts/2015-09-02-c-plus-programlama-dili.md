---
layout: post
title: C++ PROGRAMLAMA DİLİ
tags: [programminglanguage]
---

1970&#39;li yılların güçlü dili olan C&#39;nin nesne kardeşi olarak da bilinen C++ programlama dili yine kardeşinin dünyaya geldiği Bell laboratuvarında 1979 yılında Bjarne Stroustrup önderliğinde geliştirilmiştir.
<br/><br/>
Günümüzde de prosedürel programlama yaklaşımları hala geçerliliğini sürdürse de bu yaklaşımla hazırlanan programların karmaşıklığı arttıkça onu yönetmekte zor hale gelmektedir.<a href="http://www.abdullahvelioglu.com/blog/2015/09/04/nesneye-dayali-programlama/" target="_blank">Nesneye Dayalı Programlama</a> ilk kez Sınıflı C(C with Classes) adı altında bu dille ortaya çıkmıştır.Dilin ilk adı bu iken 1983 yilinda C++ adını almıştır.C++ çıktığı ve kullanımı yaygınlaştığı zamandan kısa bir süre sonra çok popüler bir dil hale gelmişti.Bunun altında yatan en önemli sebep kuşkusuz,kardeşi C dilinin güçlü alt yapısını devralarak,ona yeni özellikler eklemesiyle ortaya çok amaçlı çıkan sağlam bir dil olmasındandır.Gercekten de C++,C&#39;in sözdizimi ve bileşenlerini kapsamıs ve ona OOP felsefesini de dahil etmiştir.Bu sebepten ötürüdür ki C++ günümüzde hala bazı sistemler için geliştirilmekte ve kullanılmaktadır.
<br/><br/>
Aşagıda her C++ programında bulunan ve C&#39;den gelen iskelet gösterilmektedir.
<pre>
<span style="color:green;">/* Bu Bir C++ programıdır. */</span>
<span style="color:green;">#include &#60;iostream></span>
<b>int</b> main()
{
cout << <span style="color:red;">"Hello world"</span>;
<b>return</b> 0;
}
</pre>
Yukarıdakı programda <b><iostream></b> kütüphanesi C++&#39;in input/output stream yani giriş/cıkış akış kütüphanesidir.<i>cout</i> akışı bu sayede kullanılarak konsol ekranına çıktı oluşturmakla yükümlüdür.Diğer fonksiyonlar <a href="http://www.abdullahvelioglu.com/blog/2015/09/11/c-programlama-dili/" target="_blank">C Programlama Dilinden</a> devralındığı için bu kısımlara ilgili yazıdan göz gezdirebilirsiniz.Yukarıdaki program aşağıdaki C şekliyle de yazılabilirdi.
<pre>
<span style="color:green;">/* Bu Bir C++ programıdır. */</span>
<span style="color:green;">#include &#60;stdio.h></span>
<b>int</b> main()
{
printf("Hello world");
<b>return</b> 0;
}
</pre>
Ancak bu yazım şekli geçerli olsa da,profesyonel C++ programcıları C++&#39;ı kendi yazım şekliyle kullanmayı tercih ederler.Her ne kadar her C programı aynı zamanda bir C++ programı da olsa,C++ programcıları bu yazım şeklini demode olarak görmektedirler.Gerçekten de bir C++ programı geliştirildiği şekliyle yazılması onu daha anlamlı kılacaktır.Ancak bu hiçbir C fonksiyonunun kullanılmayacağı anlamına gelmez.
<br/><br/>
Örneğin C dilinin güçlü sistem fonksiyonu SYSTEM(); hala populerliğini sürdürmektedir.
<br/><br/>
Bu program nesne yönelimli olarak da başka bir şekilde aşagıdaki gibi yazılabilir.
<pre>
<span style="color:green;">/* Bu sınıflı bir C++ programıdır. */</span>
<span style="color:green;">#include &#60;iostream></span>
<b>class</b> Helloworld
{
<b>public:</b>
Helloworld(<b>char</b> message[])
{
cout << message << <span style="color:red;">"\n"</span>;
}
};
<b>int</b> main()
{
<span style="color:blue;">Helloworld</span> yeniDunya=<b>new</b> <span style="color:blue;">Helloworld</span>(<span style="color:red;">"Hello world"</span>);
<b>return</b> 0;
}
</pre>
Bir C++ programında sınıf tanımlamak için <b>class</b> anahtar sözcüğü kullanılır.Akabinde ise sınıfın adı yazılarak açılır ve kapanır küme parantezleri eklenerek içerisine sınıf üyeleri(member class) eklenir.C++ kapsamlı belirteçlerin kullanılmasına izin verir.Bu nedenle bir kez <b>public:</b> ifadesi yazdıktan sonra her yazılacak bir üye public olacaktır.<br/><br/>Yukarıdaki programda Helloworld adında bir nesne yaratılmaktadır.Bu nesne yaratıldığı anda kurucu metodu(constructor) çağrılarak ekrana <span style="color:red;">"Hello world"</span> ifadesi yazılmaktadır. </td> </tr>
                    </table>
