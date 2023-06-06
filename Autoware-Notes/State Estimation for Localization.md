[Referans](https://gitlab.com/ApexAI/autowareclass2020/-/blob/master/lectures/10_Localization/State_Estimation_algorithms.pdf)

Durum tahmini teknikleri, aracın 3B dünyadaki konumu ve oryantasyonunu hesaplamamıza olanak sağlar
- Kalman Filtesi
- Doğrusal olmayan Filtreler (Non-Linear)
- Partikül Filtreleri vb

#### Kalman Filtreleri
[1](https://www.kalmanfilter.net/default.aspx) [2](https://en.wikipedia.org/wiki/Kalman_filter)
- Kalman filtreleri doğrusal sistemlerde kullanılırlar
- Genellikle verideki gürültüyü azaltmak ve hata oranını düşürmek için kullanılırlar
- Tahmin ve düzelt şeklinde iki ana kısımdan oluşmaktadır

![[kf.png]]

#### Doğrusal Olmayan Fİltreler 

Kalman filtereleri doğrusal sistemler içindir. Aksi durumlarda:
- Extended Kalmal Filte (EKF) ->Genişletilmiş Kalman Filtresi
- Unscented Kalman Filter (UKF)
tekniklerini kullanmamız gerekir

#### Autoware Odometry Konfigrasyonu

![[autoware-odom.png]]