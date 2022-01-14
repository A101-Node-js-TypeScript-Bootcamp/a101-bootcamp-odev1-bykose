# TypeScript ve JavaScript Arasındaki Farklar

Öncelikle bu karşılatırmaya başlamadan JavaScript(Sonraki kısımlarda js olarak kısaltılacaktır.)'in tarihi hakkında kısa bir bilgi vermek lazım. 1995 yılında ilk olarak Mocha adıyla piyasa çıktı ancak o dönemler Java'nın popülerliğinden esinlenerek ismi JavaScirpt olarak değiştirildi. Web sayfalarında etkileşimli dinamik içerikler oluşturmak amacıyla oluşturulan js, Node.js ile birlikte sunucu tarafında, çeşitli kütüphanelerle birlikte de hibrit mobil uygulama tarafında kullanılmaya başlandı. Tasarlanma amacı olarak bu tarz uygulamalar ve projeler düşünülmediği için nesne tabanlı dillerin tip kontrolü, sınıf gibi yapılar yok. Dinamik yapısı yüzünden derleme aşaması olmayan js'de hata kontrolü çok zor yapılmaktadır. Bu yüzden 2012 yılında, C#'ın tasarımcısı olan Anders Hejlsberg tarafından tasarlanmış TypeScript yayınlanmıştır. Resmi sitesinde(https://www.typescriptlang.org) TypeScript nedir sorusuna verilen cevap; "TypeScript, editörünüzde daha sıkı bir entegrasyonu desteklemek için JavaScript'e ek syntax'lar ekler. Hataları editörünüz üzerinde erkenden yakalayın"dır. TypeScript(Sonraki kısımlarda ts olarak kısaltılacaktır.) js'yi temel almaktadır. Yazılan ts kodları js kodlarına dönüştürülür. Bu yüzden js'nin çalıştığı her ortamda çalışabilmektedir. Ts js'nin bütün özelliklerini barındırdığı gibi ek özellikleri de bulunmaktadır. Bu sayede büyük ve karmaşık projelerde verimliliği arttırmaktadır. Ts üzerinde bütün js kütüphaneleri kullanılabilmektedir. Ts kodları js kodlarına dönüştürüldüğü için, js'nin çalışabildiği tüm ortamlarda çalışabilmektedir. Sanal bir makineye ya da özel bir çalışma ortamına ihtiyacı yoktur. Ts'nin çıkış amacını ve js ile olan benzerliklerininden bahsettiğimize göre ts'nin çıkma amacındaki farklılıklardan bahsedebiliriz.


## Farkları

-Js interpreted bir dildir. Yani derleme aşaması yoktur. Bu yüzden hatalarımızı kod çalışana kadar bilemeyiz. Ts ise derleme aşamasında hata denetimi sağlar.

-Js'de dinamik veri tiplemesi vardır. Yani veri tipleri kod çalıştığı zaman belirlenir. Ts'de ise statik veri tiplemesi vardır. Bu durum derleme esnasında tip kontrolüne izin vermektedir. 

-Js betik bir dildir. Ts ise nesne yönelimli bir dildir. Sınıflar, arayüzler, modüller, miras gibi nesne yönelimli dil özelliklerini destekler.

-Js parametreli fonksiyonları desteklemezken ts opsiyonel olarak bu durumu desteklemektedir.


# Node.js ile Sunucu Ayağa Kaldırmak

Önceki konuda olduğu gibi ilk önce Node.js'in tarihçesi hakkında kısa bir bilgi vererek giriş yapmak istiyorum. Node.js 2009 yılında Ryan Dahl'ın Google Chrome tarayıcısının js kodlarını çalıştırmak için kullanılan V8 js moturuna yaptığı eklemeler sonucunda ortaya çıkmıştır. Burada V8 motorundan da bahsetmek gerekmektedir. V8 motoru js kodlarını makine diline çevirmek için C/C++ ile geliştirilmiştir. V8 motoru sayesinden js kodları çok hızlı bir şekilde çalışabilmektedir. Node.js ile birlikte js artık sadece istemci(client) tarafında çalışan bir dil olmaktan çıkıp sunucu(server) tarafında da çalışabilen bir dil haline gelmiştir. Bu konunun asıl amacına gelecek olursak; Node.js ile bir sunucu ayağa kaldırmak çok kolay hale gelmiştir.


### Sunucu Oluşturma Örneği

Node.js ile yazılmış ve "Hello World" yanıtı veren bir sunucu örneği yazalım. Bu örneği Node.js'in resmi sitesi https://nodejs.org/en/ 'da da bulabilirsiniz. 
hello-world.js adında boş bir js dosyası oluşturduktan sonra HTTP isteklerine asenkron olarak cevap veren ve istek gönderen http modülünü eklememiz gerekiyor. Bunun için gereken kod satırı:
```
const http=require('http')
```
Daha sonra sunucumuzun çalışacağı hostname'i ve portu ayarlamamız gerekmektedir.
```
const hostname=127.0.0.1

const port=3000
```
Şimdi de sunucumuzun oluşturulacağı kısma geldik. http modülünün metodu olan createServer metodunu kullanacağız. Bu metot içine arrow function ile request ve response parametreleri göndericez.
```
const server=http.createServer((req,res)=>{
res.statusCode=200
res.setHeader('Content-Type', 'text/plain')
res.end('Hello, World!\n')
})
```
Son olarak sunucunun hangi porttan ve hostnameden gelen cevapları dinleyeceğini http modülünün listen metotu ile belirleyeceğiz.
```
server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```
Bu adımları bitirdikten sonra tarayıcımızda http://127.0.0.1:3000 adresini açtığımızda Hello World çıktısını alacağız.

Gördüğünüz gibi Node.js ile bir sunucu ayağa kaldırmak için yaklaşık 10 satır kod yazmak yetiyor. 
