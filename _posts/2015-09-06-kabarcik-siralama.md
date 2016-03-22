---
layout: post
title: KABARCIK SIRALAMA(BUBBLE SORT)
tags: [algorithm]
---




Ünlü sıralama algoritmalarından biri olan ve kabarcık sıralaması olarak da bilinen bubble sort aynı veri türleri arasında bulunan elemanların içinde , en büyük sayısal değerli elemanı komşu elemanlarıyla kıyaslayarak listenin sonuna atarak sıralama yapan bir sıralama algoritmasıdır.<br/<br/>
Selection Sort(seçerek sıralama) algoritmasının tersine en büyük elemanı hedefleyerek işleyişini surdurur.Tarama sırasında,şayet değer olarak komşu elemanından daha büyük ise o anda yerini değiştirir.Hatırlarsanız selection sort’te tarama işlemi sona kadar gider ve tarama işlemi bitiminde en küçük eleman ilk sıraya konurdu.Fakat bubble sort’te tarama sırasında yer değiştirme(Swap) operasyonu koşul sağlandığı anda gerçekleşir.Konumuzu örnekler ile pekiştirelim..<br/><br/>

Örneğin ;<br/><br/>

23  11   9   44   10   sayılarından oluşan bir kümemiz olsun.Kabarcık algoritması şu şekilde işleyecektir.İlk olarak 23 sayısı 11 ile karşılaştırılır. 23  > 11 olduğundan swap uygulanır ve yeni görünüm   11  23  9  44  10  olacaktır.<br/><br/>
Akabinde aynı işlemler devam eder. 23 > 9 olduğundan bir yer değiştirme işlemi daha olur. 11  9  23  44  10. Devamında,  23 < 44  olduğundan 23 sayısı olduğu yerde kalır ve elemanlarda yer değişikliği olmaz.<br/><br/>
 11  9  23  44  10. Daha sonra sıra 44 dedir. 44 > 10 olduğundan tekrar değişiklik olacaktır ve ilk tarama bakım sonrasında elemanlarımızın görünüm değerleri şu şekilde olur.<br/><br/>
11  9  23  10  44.
 Görüldüğü üzere en büyük eleman listemizde en sona ulaşmış oldu !<br/>
Selection Sort’te ise en küçük eleman ilk süzgeçten sonra en başta konumlanıyordu.Tekrar belirtmekte fayda var ki iki algoritmanın işleyişi tamamen farklıdır.Sadece akılda kalması babında algoritmalar arasındaki benzerliklere veya farklılıklara değinecektir.Elemanlarımıza dönecek olursak son görünümleri  11  9  23  10  44 oldu.<br/><br/>
Algoritmanın çalışması gereği işlem tekrardan ilk elemana döner.Yani 11 ile işlem tekrar başlatılır.Aynı mantıkla 11 > 9 olduğu için takas gerçekleşecektir. 9  11  23  10  44. Daha sonra 11 < 23 durumunda değişiklik olmayacaktır.Aynı şekilde sıra 23’e gelir ki 23 > 10 olduğu için tekrar transfer gerçekleşir.<br/><br/>
9  11  10  23  44.Bu süzgeçleme adımının son kısmında (23 < 44) durumundan dolayı Swap gerçekleşmez.İşlem tekrar 9 dan itibaren tekrar başlayacaktır.Yukarıda anlatılan aynı mantıkla işlemler gerçekleşecek ve algoritmanın son durumunda görünüm tahmin edebileceğiniz gibi,
9  10  11  23  44  olacaktır.
<br/><br/>
Simdi bir başka örnek ile sadece adımları inceleyelim ve konumuzu iyice hazmedelim.<br/>

<pre>
34  26  10  1  -4

1.	Adım --- 26  34  10  1  -4    
2.	Adım --- 26  10  34  1  -4
3.	Adım --- 26  10  1  34  -4
4.	Adım --- 26  10  1  -4   34 // Bu adımdan sonra en büyük eleman sona ulaşır.
5.	Adım --- 10  26  1  -4   34  //   Tekrar başa dönüldü ve 10-26 yer değişir.
6.	Adım --- 10  1  26  -4   34
7.	Adım --- 10  1  -4   26  34
8.	Adım --- 10  1  -4   26  34 // Değişme olmayacaktır çünkü 26 < 34
9.	Adım --- 1  10  -4   26  34  // Başa dönüldü ve  10-1 swap operasyonu
10.	Adım --- 1  -4   10  26  34
11.	Adım		Değişme Yok   ( 10 < 26)
12.	Adım 		Değişme Yok	  (26 < 34)
13.	Adım --- -4  1  10  26  34   // nihayetinde Sıralanmış olacaktır.
</pre>
Fakat makinemiz bunu fark etmeyecektir ve listenin sonuna kadar bakmaya devam edecektir.<br/>
14-15 ve 16.Adımlarda da değişmeler olmayacağından elemanlarımızı bubble sort algoritması ile başarılı bir şekilde sıralamış oluruz.<br/>
Bubble sort algoritmasıda selection sort algoritması gibi daha karmaşık elemanlı dizilerde veya başka veri yapılarında kullanışlı değildir.

<p>Algoritmanın C dilindeki karşığı aşağıda verilmiştir</p>
<pre>
<b>int</b> *BubbleSort(int dizi[]){
    register int i,j;
    int temp=0;
    for(i=0;i<boyut;i++) {
      for(j=0;j<boyut-1;j++){
        if(dizi[j] > dizi[j+1]){
          temp=dizi[j];
          dizi[j]=dizi[j+1];
          dizi[j+1]=temp;
        }
      }
    }
    return dizi;
  }
</pre>
<p>Algoritma ayrıca bağlı liste modeli ile aşağıdaki gibi tasarlanabilir</p>
<pre>
<b>node</b> *BubbleSort(node *kutu){
  if(kutu==NULL)
  retun NULL;
  else if(kutu->next==NULL)
  return kutu;
  else {
    int temp=0;
    node *iter=kutu;
    node *root=kutu;
    while(root->next!=NULL){
      while(iter->next!=NULL){
        if(iter->data > iter->next->data){
          temp=iter->data;
          iter->data=iter->next->data;
          iter->next->data=temp;
        }
        iter=iter->next;
      }
      iter=kutu;
      root=root->next;
    }
  }
  return kutu;
}
</pre>
