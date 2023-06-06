#### Lidarla Lokalizasyon
![[NDT.png]]
Neden?
- Lidarlar 3B veriyi çok iyi bir şekilde çıkarabilir
- GNSS iç ortamlarda işlevsizdir ayrıca dış etkenlerle engellenebilir
- Lidar ile eşleştirme yüksek çözünürlülüğe sahip haritalarda etkilidir

#### 2B NDT (Normal Distrobution Transform)

![[NDT-2.png]]

 - Haritayı eş karelere ayrılır
 - Her kare noktaların normal dağılımı temsil eder
 - Ortalama ve kovaryans her hücre için, o hücredeki her `x` noktası ile hesaplanır (N toplam nokta sayısı)
 ![[NDT-3.png]]
 Optimal eşleştirme için score(p) fonksiyonu minimalize edilmelidir
 ![[NDT-4.png]]
 Burada T(x, p), sensöre göre ölçülen x noktasının p pozu ile haritaya yansıtılmış halidir.

#### NDT Algoritması

- Haritayı hücrelere ayır
- Her hücre için ortalama ve kovaryansı hesapla
- Alınan her tarama için
	- Poz `p` tahmini çıkart
	- Her optimizasyon adımı için
		- score(p), H ve g yi hesapla 
		- dp  yi Newton'un yöntemi ile hesapla $$\triangle p = H^{-1}g$$
		- Adım uzunluğu `a` yı hesapla [(More & thuente, 1994)](https://www.ii.uib.no/~lennart/drgrad/More1994.pdf) 
		- Pozu güncelle $$p = p + \alpha \triangle p$$
		- Bu işlemi sistem yakınsana kadar veya iterasyon limitini aşana kadar devam et
- Spn `p` değerini yayınla

![[NDT-5.png]]