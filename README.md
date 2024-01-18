# BitirmeProje
# Raspberry Pi Mobil İstasyon Kurulumu
## Yol haritası
### Raspberry Pi işletim sistemi kurulması

### GSM Modülünün kurulması

### Veri Tabanı deposunun kurulması

### Sensörlerin Çalıştırılması

# Raspberry Pi Kurulumu
Raspberry pi OS other kısmından Raspberry Pi(64-bit) olan versiyonu Raspberry pi imaj yöneticisi ile kurun. Raspberrydeki kullanıcı adı mutlaka pi olmalı değiştirilirse çalışmayacaktır.

![1](https://github.com/suhavural/BitirmeProje/assets/77546710/a294eb81-cf81-49ce-8c3a-a8ec4cc0a59a)

![2](https://github.com/suhavural/BitirmeProje/assets/77546710/00b916a8-e215-4e8d-8daf-f281e3f377e9)

![3](https://github.com/suhavural/BitirmeProje/assets/77546710/0c3d8ce4-b46d-4f94-bd73-0306ca86f4e3)

![44](https://github.com/suhavural/BitirmeProje/assets/77546710/792827a8-6a2d-490c-a46e-ed5849f837ff)




pi kullanıcısının şifresini girin daha sonra lazım olacak not alın. Bu ayarlar wifiye otomatik bağlanması için yapılmıştır. ssh ile bağlantı almak için yapılmaktadır. Monitörlü kurulumda wifiye monitör ile bağlanılabilir.

# Gsm Modülün Kurulması
Gsm modülün ilk kurulumunda internete ihtiyaç vardır bu yüzden wifi ile veya ethernet kablosu ile internete bağlayın.
Önemli not : Çıkartılan gsmsetup isimli klasör mutlaka /home/pi dizininde olmalı ve kurulumdan sonra silinmemeli !

gsmsetup.zip dosyasını raspberry pi'nin /home/pi dizinine aktarın

wget https://github.com/bartinbu/gsmsetup/raw/main/gsmsetup.zip

/home/pi dizininde terminal açın Zip dosyasını çıkartın

unzip gsmsetup.zip

/home/pi/gsmsetup dizinine gidin

cd gsmsetup

Tüm .sh uzantılı dosyalara +x yetkisi verin

sudo chmod +x *.sh

sudo haklarıyla install.sh dosyasını çalıştırın.

sudo ./install.sh

GSM shiled üzerindeki ışıklar yanmaya başlayacaktır. İnternet bağlantısı için hat takılı olmalıdır. Hat takılı değilken de kurulum yapılabilir.

GSM bağlantısını kontrol etmek için pingtest.sh scriptini çalıştırabilirsiniz.(zorunlu değil) Eğer ppp0 arayüzü gelmiyorsa hat çekmiyordur çeken bir yerlerde kendisi otoatik olarak gelecektir.
Eğer yine de gelmediyse yeniden başlatmayı deneyebilirsiniz.

# Firebase Veri Tabanı Kurulumu

Öncelikle Firebase'e üye olun ve kullanacağınız "Realtime Database" oluşturun

Firebase'e veri göndermek istediğiniz kod için öncelikle "Project Settings" kısmından "Service Accounts" kısmına girin ve "Generate new private key" butonuna tıklayın ardından bir JSON dosyası inecektir dosyanızın yolunu bulun ve koda şu şekilde ekleyin.
Bunu kodunuzda şu şekilde göstereceksiniz

 cred = credentials.Certificate("/home/pi/Downloads/raspberrypi7474-firebase-adminsdk-kqrrl-a642f17d92.json") # Firebase Console'dan indirdiğiniz JSON dosyasını belirtin

 firebase_admin.initialize_app(cred, {'databaseURL': 'https://raspberrypi7474-default-rtdb.firebaseio.com/'})  # Bu URL'yi kendi Firebase proje URL'nizle değiştirin Örnek aşağıda verilmiştir.

![4](https://github.com/suhavural/BitirmeProje/assets/77546710/7b706b4c-c7d9-4d26-904b-ae46d79360a8)




Veri gönderimi içinde örnek kod aşağıda verilmiştir.


            ref = db.reference('/veriler')  # Firebase Realtime Database'deki bir referans
            ref.set({
                'veri1': 10,
                'veri2': 20
            })
            

# Sensörlerin Çalıştırılması
## Kullanılan sensörler: RS-WS-N01-TR-1 & RK400-01
DİKKAT! Çalıştıracağınız sensörün datasheetindeki bilgilere bakmayı unutmayın her sensör için farklı değerler kullanılıyor(Örn. Baudrate)

İlk önce çalıştıracağınız sensörü "Modbus Poll" uygulamasında deneyin sensörü test etmek için NOT! RS-485 kullanıyorsanız Windows bilgisayarınızda deneyebilirsiniz

RS-485 ve sensör bağlantınızı gerçekleştirdikten sonra RS-485 i bilgisayarınızı USB portuna takın.

Daha sonra Setup'a tıklayın oradanda Read/Write Definition a tıklayın (KISAYOL:F8) oradaki ayarları sensörünüzün datasheetine göre değiştirdikten sonra Ok tuşuna basın

![5](https://github.com/suhavural/BitirmeProje/assets/77546710/441cd82c-9ead-42a3-8d91-1962e572d292)




Ardından Connectiondan Connect yapın (KISAYOL:F3)  oradaki değerleride yine sensörünüzün datasheetine göre değiştirin. (Serial Settings kısmı USBnizin bağlı olduğu portu gösteriyor.)

![6](https://github.com/suhavural/BitirmeProje/assets/77546710/355f0b09-29c0-44b8-adda-ebad19155fa8)



VE SONUÇ VERİLER GELİYOR

NOT: Raspberry Pi da sensörünüzü çalıştırırken yine datasheetine göre değiştirmeyin unutmayın. Gerekli bilgiler sensörünüzün datasheetinde yazıyor.
