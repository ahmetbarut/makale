# Supervisor
## Supervisord Nedir ? 
Supervisord unix benzeri işletim sistemlerinde bir dizi işlemi kontrol etmesine izin veren bir istemci/sunucu sistemidir.

### Basit
Süpervizör, öğrenmesi kolay, INI tarzı basit bir yapılandırma dosyasıyla yapılandırılır. Başarısız işlemleri yeniden başlatmak ve otomatik günlük rotasyonu gibi hayatınızı kolaylaştıran birçok işlem başına seçenek sunar.

### Merkezileştirilmiş
Supervisor, süreçlerinizi başlatmak, durdurmak ve izlemek için size tek bir yer sağlar. Süreçler tek tek veya gruplar halinde kontrol edilebilir. Supervisor'ı yerel veya uzak bir komut satırı ve web arayüzü sağlayacak şekilde yapılandırabilirsiniz.

## Kurulum 
Öncelikle ben kurulumu Centos 7'de kuracam. Resmi dökümana göre kulurum ve konfigürasyonu yapıyorum.

```bash pip install supervisord```

## Konfigürasyon
Kurulum işlemi bittikten sonra öncelikle ```echo_supervisord_conf``` komutunu çalıştırıyoruz bu komut supervisord konfig dosyası oluşturması için.

Sonra ```echo_supervisord_conf > /etc/supervisord.conf``` Eğer ```/etc``` dizinine koymayı tercih etmiyorsanız kendi dizininize koyabilirsiniz.

## Program Ekleme
Supervisor program eklemek için ```/etc/supervisord.conf```  dosyasından eklemeniz gerekiyor. Ben laravel için bir program ekledim.
```bash
    [program:laravel-worker]
    process_name=%(program_name)s_%(process_num)02d
    command=php /dizininiz/alan_adi.../artisan queue:work --sleep=1 --tries=10
    autostart=true
    autorestart=true
    user=kullanici_adi
    numprocs=8
    redirect_stderr=true
    stdout_logfile=/dizininiz/alan_adi.../worker.log

```
kaydedip çıkıyorum

#### supervisord çalıştırma
```bash 
    sudo supervisordctl reread
    sudo supervisordctl update
    sudo superciordctl start laravel-worker:*
```
bu şekilde çalışmaya başladı 
```sudo supervisorctl status``` komutunu çalıştırdığınızda eğer hata yoksa
```bash
    [root@server ~] supervisorctl status laravel-worker:*
    laravel-worker:laravel-worker_00   RUNNING   pid 27814, uptime 0:21:31
    laravel-worker:laravel-worker_01   RUNNING   pid 27815, uptime 0:21:31
    laravel-worker:laravel-worker_02   RUNNING   pid 27816, uptime 0:21:31
    laravel-worker:laravel-worker_03   RUNNING   pid 27817, uptime 0:21:31
    laravel-worker:laravel-worker_04   RUNNING   pid 27818, uptime 0:21:31
    laravel-worker:laravel-worker_05   RUNNING   pid 27819, uptime 0:21:31
    laravel-worker:laravel-worker_06   RUNNING   pid 27820, uptime 0:21:31
    laravel-worker:laravel-worker_07   RUNNING   pid 27821, uptime 0:21:31

```
buna benzer bir çıktı alırsınız eğer bir sorun varsa zaten bildirir