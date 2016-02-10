---
layout: post
title:  "YAML incelemesi"
excerpt: ""
author: mustafa_altinkaynak
date:   2016-02-09
categories: articles
tags: [yaml]
comments: true
share: true
---

#### Başlarken

Merhabalar. Bu yazımızda YAML yapısı üzerinde duracağız. Neden YAML? sorusuna cevap bulup, kullanımı konusunda örnekler gerçekleştireceğiz.

Hemen hemen her uygulama yapılandırma ayarlarını saklamak ve düzenlemek için sağlam bir yola ihtiyaç duyar. Çeşitli ağaçlandırma teknikleriyle (json, xml, yaml) bu gerçekleştirilebilir. Fakat bunların içlerinde öyle birisi var ki içlerinden kolayca sıyrılıp bize çözüm üretiyor. YAML kolay okunabilir ve erişilebilir yapısıyla tercih sebebi olmasının yanı sıra key -> value, dizi ve istenilen derinlikte yazım biçimiyle tutulabilmektedir. Bu açıdan bakıldığında YAML diğer benzerlerine nazaran ön plana çıkmaktadır.

YAML dosyası içerisinde iki şekilde tanımlama gerçekleştirebilirsiniz. İlki sağladığı ek avantajlar nedeniyle symbol, diğer ise string tanımlamadır.


#### 1. Basit bakış açısı

##### 1.1 Örnek tanımlama

|Symbol|String|
|---|---|
|:isim: 'Mustafa'|isim: 'Mustafa'|

```ruby
default:
  :database: test # Symbol tanımlanmış.
  password: 123456 # String tanımlanmış
```
Burada unutulması gereken nokta; ifade ne şekilde tanımlandıysa o şekilde çağrılmasıdır. Symbol olarak tanımlandıyse **:isim** şeklinde, String olarak tanımlandıysa **'isim'** şeklinde çağrılmasıdır.

##### 1.2 Liste yapısı

```ruby
# ornek.yml
urunler:
    - urun_no:   001
      adi:   Su
      fiyat:  1

    - urun_no:   002
      adi:  Kola 
      fiyat: 3
```

##### 1.3 Key-value yapısı
```ruby
# ornek.yml
   urun_no: 001
   adi: Su
```

##### 1.4 Satır sonu koruması
```ruby
# ornek.yml
data: |
   Yaygın inancın tersine, Lorem Ipsum rastgele sözcüklerden oluşmaz.
   Yinelenen bir sayfa içeriğinin okuyucunun dikkatini dağıttığı bilinen bir gerçektir.
``` 

##### 1.5 Satır sonlarını dikkate alma
```ruby
# ornek.yml
data: >
   Yaygın inancın tersine, Lorem Ipsum rastgele sözcüklerden oluşmaz.
   Yinelenen bir sayfa içeriğinin okuyucunun dikkatini dağıttığı bilinen bir gerçektir.
``` 

##### 1.6 İlişkilendirilmiş diziler
```ruby
# ornek.yml
bay: [Ahmet, Ali]
bayan:
  - Ayşe
  - Fatma
``` 

Buraya kadar YAML yapısına tanımlamalar açısından giriş yapmış olduk. Şimdi ise biraz daha seviyemizi artırarak kullanım ve yazım kolaylığı sağlayacak çözümler üzerinde duralım.

#### 2. Gelişmiş bakış açısı 
##### 2.1 Yapı
YAML tekrarlanan ifadelerin çözümünde referans kullanımı gerçekleştirir. Yani YAML hiyenarşisi içerisinde girinti derecesi fark etmeksizin kendinizi tekrarlamayı önler.

##### 2.2 Tekrarlanan ifadeler
YAML içerisinde tanımlanan iki farklı isimdeki yapının içeriği aynı yada yapı içerisinde çok az farklılık olabilir. Bunu bir örnekle gösterelim.


Aşağıdaki örnekte göreceğiniz üzere farklı isimdeki iki yapının tüm değerleri aynıdır. İfadeler birbirini tekrarlayan niteliktedir. Yazım kolaylığının sağlanması ve kendini tekrarlamayı önlemek amacıyla çapa (**&**) ve referans belirterek (__*__) kullanılabilir. Bu kullanımların örneğini inceleyelim.

```ruby
# ornek.yml
default: 
  username: root
  password: 123456
  pool: 10
  socket: /var/run/mysqld/mysqld.sock
development:
  username: root
  password: 123456
  pool: 10
  socket: /var/run/mysqld/mysqld.sock
``` 

Aşağıdaki örnekte default ifadesine çapa ekleyerek istediğimiz yerde referans gösterebileceğimiz hale getirdik. Referans alacağımız yerde ise __*__ şeklinde kullanabiliriz. Böylece default ifadesinin birebir halini development altına da kullanabiliyor olduk. 

```ruby
# ornek.yml
default: &default # çapa ekledik
  username: root
  password: 123456
  pool: 5
  socket: /var/run/mysqld/mysqld.sock
development: *default
``` 

Aşağıdaki örnekte ise sadece **pool** ifadesinin değerini farklı kullanmak istememiz durumunda __<<: *default__ şeklinde kullandıktan sonra, yeni değer alan ifade yazılır.

```ruby
# ornek.yml
default: &default
  username: root
  password: 123456
  pool: 5
  socket: /var/run/mysqld/mysqld.sock
development:
  <<: *default
  pool: 10
``` 

Kaynak : https://en.wikipedia.org/wiki/YAML

Bir sonraki yazımızda görüşmek üzere. 
