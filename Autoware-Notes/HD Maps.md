
![[HD-MAPS.png]]

"High Definition Maps" otonom sürüş sistemlerin daha verimli çalışması için kullanılırlar
Zira araçlar ortamı insanlar kadar iyi tanıyamazlar bu yüzden detaylı bir haritaya sahip olmak algoritmaları daha işlevsel hale getirebilir

- Otonom sürüşün her adımında kullanılabilirler (Perception, Localization vs)
- Bazı sensörlerin yerini alabilirler
- Lokalizasyon optimizasyonu
- Planlama (regulasyon, trafik kuralları vs)

Ne tür bilgi taşırlar:
- Geometrik -> Ortamın yapısal bilgisi (poligonlar, nokta bulutu, yol çizgileri vs)
- Semantik -> Geometrik katmana anlam veren etiketleri içerir (trafik sembolleri, yaya geçidi vs)
- Yol ağı -> Yollar arasındaki bağlantıları içerir
- Deneysel -> Yollar hakkında tecrübeye odaklı çeşitli bilgiler içerir (trafik akışı, yolun kullanılma miktarı, kaza oranı vs) Bu katman araçlar sürüş yaptıkça güncellenir
- Gerçek zaman -> Gerçek zamanlı trafik bilgisi, kaza, yolun durumu gibi her an olup, değişebilen bilen bilgi katmanıdır

Depolama, API
- Navigation Data Standarts (NDS)
- OpenDrive
- Lanelet2

Harita oluşum katmanı (aşağıdan yukarıya doğru)

- Gerçek zaman katmanı
- Deneysel katman
- Semantik katman
- Geomatrik katman
- Temel harita