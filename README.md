# Docker ve Laravel

#### 1. Laravel 6 Install
Terminal üzerinde projemizi kurmak istediğimiz dizine gelerek **composer create-project --prefer-dist laravel/laravel proje_ismi "6.*"** kodunu çalıştırıyoruz.
ğer sistemimizde composer yok ise https://getcomposer.org/download/ adresini ziyaret edebilirsiniz. Not : Composer bazen **php composer.phar** şeklinde çalışabilir.

#### 2. Docker Install
https://docs.docker.com/docker-for-windows/install/  adresine giderek kullanmakta olduğumuz işletim sistemine uygun olanı sistemimize yüklüyoruz.

#### 3.Create Dockerfile
Dockerfile :  Kullancağımız docker containerlar için projeye uygun uzantıları(extensions) tanımlamamızı ve kurmamızı sağlar.
Örneğin biz laravel projeyi docker içerisinde çalıştırmayı planlıyoruz.
Laravel çalışacağı ortamda  aşağıdaki uzantılara ihtiyaç duyar işte biz bu ihtiyaçları dockerfile içerisinde tanımlıyoruz.
- BCMath PHP Extension
- Ctype PHP Extension
- Fileinfo PHP extension
- JSON PHP Extension
- Mbstring PHP Extension
- OpenSSL PHP Extension
- PDO PHP Extension
- Tokenizer PHP Extension
- XML PHP Extension

dockerfile indirmiş olduğumuz Laravel projenin ana dizini içerisine oluşturulur.
Örnek dockerfile içeriğine adresinden ulaşabilirsiniz.

#### 4.Create Docker-Compose
Docker-Compose : Docker projemiz içerisinde farklı containerların birlikte çalışmasını sağlayan bir yapıdır.
Ana projemiz içerisine Docker-compose.yml dosyası oluşturulur ve gerekli tanımlamalar yapılır.
Örnek içerik ve açıklamaları için :


#### 5. Projemiz için docker image oluşturuyoruz.
Terminal kısmına **docker build -t senin-docker-image-ismin . ** yazarak çalıştırıyoruz.
sonrasında belirlemiş olduğumuz isme uygun docker image oluşuyor.
Çalışan docker image listesini terminale **docker image ls** yazarak alabiliriz.
Not : Docker image Dockerfile içeriğine uygun olarak oluşturulur.
Eğer sadece oluşturduğumuz bu image için container oluşturmak istiyorsak **docker run -p 8000:8000 senin-docker-image-ismin** yazarak çalıştırıyoruz.
Fakat biz bunu tercih etmiyoruz.
Container oluşturma işlemini Docker-compose.yml içerisine yapmış olduğumuz tanımlamalar ile yapcağız.

#### 6. Containerlar oluşsun ve Proje docker üzerinden yağı kalksın.
Terminale **docker-compose up -d --build**  yazarak çalıştırırsak yml dosyasına uygun olarak containerlarımız oluşur ve arka planda çalışacak şekilde ayağım kalkar.
