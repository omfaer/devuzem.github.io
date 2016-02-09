---
layout: post
title:  "Action Cable Examples"
excerpt: ""
author: omfaer
date:   2015-12-28
categories: articles
comments: true
share: true
---

## Action Cable

Action Cable Rails5 ile gelecek yeni özelliklerden biridir.
Basit bir şekilde Websocket kullanmamıza olanak sağlar.
Action Cable Rails uygulaması içinde bir soket bağlantısı açar. Ve o soket (kanal da denilebilir) içerisindeki akışa
erişim sağlar.

Diğer bir açıdan Realtime push notification.

## Websocket

HTML5 ile birlikte gelen Websocket, herhangi bir yazılıma gerek duymadan Sunucu ile İstemci arasında bir bağlantı kurup
bu bağlantıyı sürekli olarak kullanmaya yarayan bir protokoldür.
Yani aradaki bu bağlantıyla istemci hızlı bir şekilde hem veri alıp hem de veri gönderebilir.

## Push Notification(Anlık Bildirimler)

Doğrudan teslim edilen anlık mesajlar gönderilmesi olayı.

## Action Cable Examples

Action Cable yeteneklerini sergileyen örneklerden oluşan bir koleksiyon.

### Bağımlılıklar (Dependencies)

Redis yüklü ve çalışır durumda olmalıdır. Default port:6379

```bash
$netstat -tulpn
```
 ile port kontrol edilebilir.

Redis Kurulumu

#### Linux Üzerine

```bash
$ wget http://download.redis.io/redis-stable.tar.gz
```
```bash
$ tar xvzf redis-stable.tar.gz
```

```bash
$ cd redis-stable
```
```bash
$ make
```

```bash
$ make install
```

#### Mac Üzerine
```bash
brew install redis
```

Note: Redis kullanmak için Ruby 2.2.2 yüklenmiş olmalıdır.


### Sunucuları Başlatma

1. `./bin/setup`
2. `./bin/cable`
3. Yeni bir terminal açın ve çalıştırın: `./bin/rails server`
4. Redis serveri çalıştırmak için de yeni bir terminal açın: `redis-server`
4. Browserda `http://localhost:3000`

### Live comments example

1. Ayrı cookies kullanan 2 tarayıcı açın(Biri normal diğeri gizli oturum gibi.)
2. İki farklı tarayıcıda iki farklı kişiymiş gibi davranın.
3. İki kullanıcıdan da aynı mesaja geçin.
4. Her iki tarayıcıda yorum ekleyin. Gerçekzamanlı çalıştığını göreceksiniz.
