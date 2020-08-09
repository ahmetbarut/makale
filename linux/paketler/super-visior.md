# Supervisor
## Supervisord Nedir ? 
Supervisord unix benzeri işletim sistemlerinde bir dizi işlemi kontrol etmesine izin veren bir istemci/sunucu sistemidir.
## Kurulum 
Öncelikle ben kurulumu Centos 7'de kuracam. Resmi dökümana göre kulurum ve konfigürasyonu yapıyorum.
    
### Kurulum 
```bash pip install supervisord```
## Konfigürasyon
Kurulum işlemi bittikten sonra öncelikle ```echo_supervisord_conf``` komutunu çalıştırıyoruzbu komut supervisord konfig dosyası oluşturması için.

Sonra ```echo_supervisord_conf > /etc/supervisord.conf``` Eğer ```/etc``` dizinine koymayı tercih etmiyorsanız kendi dizininize koyabilirsiniz.

## Program Ekleme
Supervisor program eklemek için ```/etc/supervisord.conf```  dosyasını açıp eklemek istediğiniz işlemi ben örnek için *_/tmp_* dizininde worker.log diye bir dosyaya bişeyler yazdıracam.
```bash
    [program:visord-test]
    command= echo "supervisord test" > /tmp/worker.log
```
kaydedip çıkıyorum

#### supervisord çalıştırma
```bash 
    sudo supervisordctl reread
    sudo supervisordctl update
    sudo superciordctl start visord-test
```