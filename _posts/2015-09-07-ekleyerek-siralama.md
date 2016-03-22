---
layout: post
title: EKLEYEREK SIRALAMA(INSERTION SORT)
tags: [algorithm]
---




Sıralama algoritmalarının içerisinde yer alan Insertion Sort yani ekleyerek sıralama algoritmasının iki farklı metodu bulunmaktadır.Anlatımımı algoritmanın iki ozelliği ile ayrı ayrı betimleyeceğim.Bir Array’a elemanlar atanırken önce büyüklük-küçüklük durumuna göre bakılır.Eklenecek sayı,dizide bulunan elemanlardan büyük bir sayı ise sorun yoktur ve dizinin boş indeksine eklenir.Fakat eklenecek sayı dizideki herhangi bir sayıdan küçük ise,ekleneceği konumdan itibaren listedeki sayılar 1’er sıra kaydırılacaktır ki ekleyeceğimiz sayıya yer açılmış olsun.Bir örnekle konumuzu anlatmaya devam edelim.Aynı veri türlerinden oluşacak ve içi boş olan bir kümemiz olsun.Şimdi bu kümemize elemanlar ekleyelim.<br/><br/>
Örneğin,ilk olarak 7 sayısını ekliyoruz.<br/><br/>

7 - - - -. -> 7 sayısı listemizde oluşturuldu.<br/><br/>

Daha sonra 5 sayısını eklemek istediğimizi varsayalım.Ekleme yapılmadan önce eklenecek sayı ile listedeki elemanlar karşılaştırılacaktır.Listemizde şuan sadece 7 sayısı bulunduğundan yalnızca 1 sefer tarama yapılacaktır.Ekleyeceğimiz 5 sayısı 7 sayısından küçük olduğu için listemizde bulunan 7 sayısı bir kayarak 5 sayısına yer açmış olur.Dolayısıyla 5 sayısı yeni yerine yerleşecektir.<br/><br/>

5 7 - - - <br/><br/>
Eklemeye yeni sayımız 8 ile devam ediyoruz.8 sayısı önce 5 ile test edecektir. 5<8 olduğu için,sıra 7’ye gelir.7<8 olduğu için ve başka test edecek sayı olmadığı için 8 sayısı listedeki ilk boş yere yerini alacaktır.Yeni durumda görünüm,<br/><br/>
5 7 8 - - olacaktır.<br/><br/>
Şimdi ise 6 sayısını eklemeye çalışalım.Dikkat edilirse 6 sayısı arada kalacak bir sayıdır ve 5’ten büyük fakat 7’den küçük bir sayıdır.O yüzden 5’ten sonraki tüm sayılar 1’er sıra kaydırılır. <br/><br/>
5 – 7 8 -  ancak 6 sayısına bu şekilde yer açılabilir,yeni durumda görünüm,<br/><br/>
5 6 7 8 -  olacaktır.<br/><br/>
Son olarak 2 sayısını ekleyeceğimizi düşünelim.2 sayısı,listedeki ilk eleman olan 5 sayısı ile test edilecektir.2<5 olduğu için 2 sayısının yeri belirlenmiş olup, artık diğer elemanlarla test edilmesine gerek kalmaz.Çünkü 2 sayısı diğer elemanlardan zaten küçük olacaktır ve bakmak gereksizdir. Dolayısıyla listedeki 5 sayısından itibaren tüm sayılar 1’er sıra kaydırılacaktır.
Nihayi dörünüm 2 5 6 7 8 şeklinde olacaktır.<br/><br/>
Ekleyerek sıralama algoritmasının ilk versiyonu yukarıda anlatılan mantıkla çalışır.<br/><br/>

<h2>2.Versiyon</h2>

Algoritmanın bir de 2.versiyonu bulunmaktadır.Bu versiyon derki,dizide bir sıralı bölüm olsun bir de düzensiz bölüm olsun.Yukarıdaki örneklerde bahsi geçen sayılar tek seferde diziye yerleştirilir.Yukarıdaki örneğimizdeki elemanların ekleme sırası ile dizimize elemanları yerleştirelim.
<pre>
7	5	8	6	2
</pre>
Dizimizin bölmelerine bakılacak olursa siyah bölmedeki elemanlarımız düzensiz kısmımızdır,yani bu bölmeler taramaya tabi tutulmamış,henüz el atılmamış kısımlarıdır. Algoritmamızı yukarıda örneğimiz ile anlamaya çalışalım.İlk olarak yerleşik 7 sayısı ile bir sonraki dizi elemanı olan 5 karşılaştırılır.7>5 olduğundan yer değişikliği gerçekleşecektir ve ilk adımda tarama sona erecektir.(1.Adım)
<pre>
5	7	8	6	2
</pre>
 Bir sonraki adıma geçelim.dizimizin 1.indeksli elemanı olan 7 sayısı 8 ile   kıyaslanacaktır.7<8 olduğundan değişiklik olmayacaktır.7 sayısı 5 sayısından büyük olduğu için değişiklik olmayacaktır.8 sayısı 7’den büyük olduğu için yer değiştirme işlemi sonlanacaktır.(2.Adım)
<pre>
5	7	8	6	2
</pre>
İşleme 3.adımız ile devam ediyoruz.8 sayısı 6 ile kıyaslanacak.8>6 olduğundan yer değiştirilir.
<pre>
5	7	6	8	2
</pre>
Fakat işlem bitmedi!Çünkü 6 sayısı 7 sayısından da küçüktür.bir değişiklik daha gerçekleşir ve yeni görünüm
<pre>
5	6	7	8	2
</pre>
Şeklinde olacaktır.6>5 olduğu için 3.adımızda sonlanacaktır.(3.Adım)<br/><br/>
Siyah bölmemizde kalan tek sayı 2. sırayla 8 sayısı 2 ile karşılaştırılacaktır.8>2 olduğu için yer değişikliği olacaktır.2 sayısı bakılmaya daha sonra 7,6 ve 5 ile bakılıp onlarla da sırasıyla değişikliğe gidecektir çünkü dizimizin en küçük elemanı görüldüğü üzere 2 dir.
<pre>
5	6	7	2	8

5	6	2	7	8

5	2	6	7	8

2	5	6	7	8
</pre>
Görüldüğü üzere Insertion Sort algoritmasının 2.sıralanış modeli ilede sayılarımız sıralanmış oldu.<br/><br/>
İki model arasında şu <i>fark</i>bulunur.ilk modelimizde hatırlanacağı gibi sayılarımız önce taratılıp sonra yerleştiriliyor idi.Fakat 2.modelimizde sayılar once rastgele yerleştirilerek,ilk sayıdan başlanır ve indeks numarasının 1 fazlası kadar sayı taraması yapılır. Yukarıdaki örnekte sayılarımızı tekrar ele alırsak,ilk sayımız dizimizin 0 numaralı indeksi 5 idi.5 sayısı 8 ile kıyaslandı ve ilk adım tamamlanmıştı.Yani 1 sefer tarama yapıldı.(Bilindiği üzere diziler 0 numaralı indis değerleri ile başlar).<br/><br/>
Insertion sort algoritmasının en kötü durumda çalışacağı yer tersten sayıları düzenlerkendir.Örneğin, 5  4  3  2  1 olarak verilen bir sayı dizisinde N elemanlı bir dizi 2N tarama yaparak sonuca ulaşacaktır.
<p>Analizi yapılan algoritmanın C dilindeki karşılığı verilmiştir.</p>
<pre>
<b>int</b> *InsertionSort(int dizi[]){
  int sayi=0,flag=0,i,j,k=0;
  dizi=(int *)malloc(boyut*sizeof(int));
  printf("Boyutu 5 olan bir dizinin elemanlarını giriniz.");
  scanf("%d",&sayi);
  dizi[0]=sayi;
  for(i=1;i<boyut;i++){
    scanf("%d",&sayi);
    for(j=0;j<i;j++){
      if(dizi[j]>sayi){
        for(k=i-1;k>=j;k--)
        dizi[k+1]=dizi[k];
        dizi[j]=sayi;
        flag=1;
        break;
      }
    }
    if(flag==0)
    dizi[i]=sayi;
    flag=0;
  }
  return dizi;
}

</pre><br/>
<p>Bağlı liste modeli kullanıldığında aynı algoritma aşağıdaki gibi verilebilir.</p>
<pre>
node *InsertionSort(node *kutu,int data){
  if(kutu==NULL){
    kutu=(node *)malloc(sizeof(node));
    kutu->data=data;
    kutu->next=NULL;
    return kutu;
  }
  if(data<kutu->data){
    node *temp=(node*)malloc(sizeof(node));
    temp->next=kutu;
    temp->data=data;
    return temp;
  }
  node *iter=kutu;
  node *root=kutu;
  while(iter->next!=NULL){
    if(iter->next->data > data){
      node *temp=(node *)malloc(sizeof(node));
      temp->data=data;
      temp->next=iter->next;
      iter->next=temp;
      return kutu;
    }
    iter=iter->next;
  }
  if(iter->NULL){
    node *temp=(node *)malloc(sizeof(node));
    temp->data=data;
    iter->next=temp;
    temp->next=NULL;
    return kutu;
  }
}</pre>
<br/>
<p>Son olarak algoritmanın 2.versiyonu yine aynı dilde verilirse,</p>
<pre>
int *InsertionSort(int dizi[]){
  int sayi=0,temp=0,i,j;
  dizi=(int *)malloc(boyut*sizeof(int));
  printf("Boyutu 5 olan bir dizinin elemanlarını giriniz.");
  for(i=0;i<boyut;i++){
    scanf("%d",&sayi);
    dizi[i]=sayi;
  }
  for(i=0;i<boyut-1;i++){
    for(j=i;j>=0;j--){
      if(dizi[j+1]<dizi[j]){
        temp=dizi[j];
        dizi[j]=dizi[j+1];
        dizi[j+1]=temp;
      }
      else
      break;
    }
  }
  return dizi;
}
</pre>
<br/>
<p>şeklinde bir kod dilimi gerçeklenmiş olacaktır.</p>
