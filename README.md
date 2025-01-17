# proje-5
Tiva C Mikrodenetleyicide Floating-Point İşlemleri ve Matematiksel İşlevler
Bu proje, Tiva C LaunchPad (TM4C123) kullanılarak floating-point işlemleri ve math.h kütüphanesinin temel matematiksel işlevlerini içeren bir uygulama örneğidir. Uygulama, floating-point işlem birimi (FPU) etkinleştirilerek çeşitli matematiksel işlemlerin gerçekleştirilmesini ve belirli bir koşula bağlı olarak bir GPIO pini üzerindeki LED'in yakılmasını içermektedir.

Projenin Amacı
Bu projede:
Floating-point işlem biriminin (FPU) nasıl etkinleştirileceği ve kullanılacağı gösterilmiştir.
math.h kütüphanesi kullanılarak temel ve gelişmiş matematiksel işlemler gerçekleştirilmiştir.
Bir sinyalin örneklenmesi ve sinüs sinyali oluşturma işlemi gösterilmiştir.
Hesaplanan bir sonuç üzerinden GPIO pini kontrol edilerek LED yakma/söndürme işlemi gerçekleştirilmiştir.

Donanım Gereksinimleri
Tiva C LaunchPad (TM4C123 veya benzeri bir model)
On-board kırmızı LED (GPIO_PIN_1, Port F) ya da harici bir LED.

Kodun Çalışma Mantığı
1. Sistem Saatinin Ayarlanması
Sistem saati, 16 MHz kristal osilatör kullanılarak yapılandırılmıştır. Bu, tüm çevresel birimlerin çalışması için temel saat kaynağını sağlar.

3. Floating-Point İşlem Biriminin (FPU) Etkinleştirilmesi
FPU, floating-point işlemleri donanım seviyesinde hızlandırır.
FPUEnable() ve FPULazyStackingEnable() fonksiyonları ile FPU etkinleştirilir.

5. Floating-Point Değişkenlerle Temel Matematiksel İşlemler
Floating-point türündeki değişkenler üzerinde toplama, çıkarma, çarpma ve bölme gibi temel işlemler gerçekleştirilmiştir.

7. Gelişmiş Matematiksel İşlemler
Dereceyi radyana dönüştürme: angle * (M_PI / 180.0) formülüyle derece cinsinden verilen açı radyana çevrilmiştir.
Trigonometrik işlemler: sinf(), cosf(), tanf().
Üstel ve logaritmik işlemler: expf(), logf(), log10f().
Üs alma ve karekök: powf(), sqrtf().
Mutlak değer ve yuvarlama işlemleri: fabsf(), ceilf(), floorf().

9. Özel Durumların Kontrolü
Bölme sıfıra bölünme durumunda Infinity (Sonsuzluk) oluşturur.
Negatif bir sayının karekökü alınmaya çalışıldığında NaN (Not a Number) değeri oluşturulur.

11. Sinyal Üretimi (Sinüs Sinyali)
Bir sinüs sinyali, örnekleme frekansı (samplingRate) ve frekansı (frequency) verilerek üretilmiştir.
Bu işlem, sinf() fonksiyonu ve Fourier dönüşümünde kullanılabilecek temel sinyal üretim tekniklerini göstermektedir.

13. LED Kontrolü
Hesaplanan karekök değeri (squareRoot) bir eşik değeriyle karşılaştırılır.
Eğer karekök değeri 2.0'dan büyükse, GPIO pini (GPIO_PIN_1) kullanılarak LED yakılır.
Aksi durumda LED söndürülür.

15. Sonsuz Döngü
İşlemler tamamlandıktan sonra mikrodenetleyici bir sonsuz döngüye girer.
Fonksiyonlar ve Tanımlamalar
SysCtlClockSet(): Sistem saatini yapılandırır.
FPUEnable(): Floating-point işlem birimini etkinleştirir.
FPULazyStackingEnable(): FPU'nun yığın yönetimi performansını artırır.
sinf(), cosf(), tanf(): Trigonometrik fonksiyonlar.
expf(): Üstel fonksiyon (e^x).
logf(), log10f(): Logaritma işlemleri (doğal ve taban 10).
powf(): Üs alma işlemi (a^b).
sqrtf(): Kare kök.
fabsf(): Mutlak değer.
ceilf(), floorf(): Yuvarlama işlemleri (yukarı/aşağı).
GPIOPinWrite(): GPIO pinine lojik 1 veya lojik 0 yazmak için kullanılır.
Projenin Çalıştırılması
Hazırlık:

Tiva C LaunchPad'iniz geliştirme ortamına (ör. Code Composer Studio) bağlanır.
Kod, geliştirme ortamında derlenir ve mikrodenetleyiciye yüklenir.
Çalışma Adımları:

Sistem saati ve FPU etkinleştirilir.
Matematiksel işlemler gerçekleştirilir ve sinüs sinyali üretilir.
Kare kök değeri eşik değeriyle karşılaştırılarak LED kontrolü yapılır.

Sonuç:
Hesaplama sonucuna bağlı olarak kırmızı LED yanar veya söner.

Dikkat Edilmesi Gerekenler
FPU'nun Etkinliği: Floating-point işlemleri FPU etkinleştirilmeden yapılmaya çalışılırsa performans kaybı yaşanabilir.
Math.h Kullanımı: Matematiksel işlemler sırasında doğru fonksiyonların seçildiğinden emin olun (ör. sinf() yerine sin() kullanılmamalıdır).
Donanım Bağlantıları: LED'in doğru GPIO pinine bağlandığından emin olun (GPIO_PIN_1, Port F).
