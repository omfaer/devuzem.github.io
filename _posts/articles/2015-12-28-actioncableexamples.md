---
layout: post
title:  "Action Cable Examples"
excerpt: ""
author: omfaer
date:   2015-12-28
categories: articles
tags: [docker]
comments: true
share: true
---

# Ubuntu

Docker aşağıdaki Ubuntu işletim sistemlerinde desteklenir.

Ubuntu Wily 15.10
Ubuntu Trusty 14.04 (LTS)
Ubuntu Precise 12.04 (LTS)

Bu sayfa Docker-yönetim sürüm paketleri ve yükleme mekanizması hakkında bilgilendirir.
Bu paketleri kullanarak Docker'ın son sürümünü elde etmenizi sağlar.
Eğer Ubuntu-yönetim paketleri kullanarak yüklemek isterseniz, Ubuntu dokümantasyonuna bakınız.

Not: Docker'da Ubuntu Utopic 14.10 ve 15.04 de APT repoları bulunuyordu ancak artık resmen destenklenmektedir.

# Prerequisites (Ön Koşullar)

Docker'ın olmazsa olmazı Ubuntu'nun 64-bit kurulmuş versiyonudur. Ayrıca kernel sürümünün minimum 3.10 olması gerekir. En az 3.10 sürümü veya daha yeni bir desteklenen versiyonu da kabul edilebilir.

3.10 dan daha eski kernel versiyonları Docker container larını çalıştırmak için gerekli olan bazı özelliklerden yoksundur. Bu eski sürümlerin bazı durumlarda veri kaybına ve sık sık panik haline yol açtığı bilinmektedir.

Mevcut kernel versiyonunu kontrol etmek için bir terminal açın ve `uname -r` komutuyla kernel sürümünü görüntüleyin.

```bash
$ uname -r
3.19.0-49-generic
```

Not: Eğer daha önce APT kullanarak Docker yüklediyseniz, yeni Docker reponun APT kaynaklarını güncellediğinizden emin olun.

## Update your apt sources (APT kaynaklarını güncellemek)

Docker'ın APT reposu Docker 1.7.1 ve üstü versiyonları içermektedir. Yeni repo paketlerini kullanmak için APT ayarlarını yapın:

1. Yetkili bir kullanıcıyla Ubuntu'ya giriş yapın.

2. Yeni bir terminal açın.

3. Paket bilgilerini güncelleyin, CA sertifikalarının yüklü olduğundan emin olun.

```bash
$ apt-get update
$ apt-get install apt-transport-https ca-certificates
```

4. Yeni bir GPG anahtarı ekleyin.

```bash
$ sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
```

5. `/etc/apt/sources.list.d/docker.list` dosyasını terminalde açın. Eğer dosya yoksa oluşturun.

6. Tüm girdileri silin.

7. Ubuntu işletim sistemi için aşağıdaki satırlardan ilgili olanı ekleyin.

* On Ubuntu Precise 12.04 (LTS)

```bash
deb https://apt.dockerproject.org/repo ubuntu-precise main
```

* On Ubuntu Trusty 14.04 (LTS)

```bash
deb https://apt.dockerproject.org/repo ubuntu-trusty main
```

* Ubuntu Wily 15.10

```bash
deb https://apt.dockerproject.org/repo ubuntu-wily main
```

Not: Docker tüm mimariler için paket sağlamamaktadır. Multi-architecture bir sisteme Docker yüklemek için [arch=...] cümlesini ekleyin. Ayrıntılar için Debian Multiarch wiki'sine bakınız.

8. /etc/apt/sources.list.d/docker.list dosyasını kaydedin ve kapatın.

9. APT paket index güncelleyin.

```bash
$ apt-get update
```

10. Varsa eski repoları temizleyin.

```bash
$ apt-get purge lxc-docker
```

11. Bu apt reposunu doğrulayın.

```bash
$ apt-cache policy docker-engine
```

Bundan sonra `apt-get upgrade` komutunu çalıştırdığınızda yeni depodan çeker.

## Prerequisites by Ubuntu Version (Ubuntu Versiyonu Önkoşullar)

* Ubuntu Wily 15.10
* Ubuntu Vivid 15.04
* Ubuntu Trusty 14.04 (LTS)

Ubuntu Trusty, Vivid, ve Wily versiyoları için `linux-image-extra` kernel paketini indirmeniz tavsiye edilir. `linux-image-extra` paketi [aufs](https://docs.docker.com/engine/userguide/storagedriver/aufs-driver/) storage driver kullanabilmenizi sağlar.

Kernel versiyonuna göre `linux-image-extra` paketini yükleyin:

1. Ubuntu ana bilgisayarda bir terminal açın.

2. Paket yöneticisini güncelleyin.

```bash
$ sudo apt-get update
```

3. Tavsiye edilen paketi yükleyin.

```bash
$ sudo apt-get install linux-image-extra-$(uname -r)
```

4. Devam edin ve Docker yükleyin.

Eğer Ubuntu 14.04 veya 12.04 kullanıyorsanız `apparmor` gereklidir.

```bash
$ sudo apt-get install apparmor
```

ile yükleyebilirsiniz.

## Ubuntu Precise 12.04 (LTS)

Ubuntu 12.04 için başka bağımlılıklarda vardır. Bakınız: (https://docs.docker.com/engine/installation/linux/ubuntulinux/)

# Install (Kurulum)

Ubuntu için önkoşulların ve bağımlılıkların yüklü olduğundan emin olun.

Daha sonra aşağıdaki komutları kullanarak Docker'ı yükleyin.

1. Sudo haklarına sahip bir kullanıcı olarak giriş yapın.

2. Paket yöneticisini güncelleyin.

```bash
$ sudo apt-get update
```

3. Docker yükleyin.

```bash
$ sudo apt-get install docker-engine
```

4. `docker` çalıştırın.

```bash
$ sudo service docker start
```

5. Doğru kurulduğunda emin olmak için Hello World!.

```bash
$ sudo docker run hello-world
```

###### References:https://docs.docker.com/engine/installation/linux/ubuntulinux/
