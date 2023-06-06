Lokalizasyon aracın dünya üzerinde nerede olduğunu belirleryen sistemlerdir

##### Global Localization

Dünyaya göre konum (enlem, boylam, irtifa vs)

- GNSS
	- GPS (USA)
	- BeiDou (Çin)
	- GLONASS (Rusya)
	- Galileo (EU)

- GNSS Corrections
	- Ground-based RTK
	- Satellite-based Subscription Services (TERRASTAR)

##### Absolute Local Localization

Belli bir bölgeye göre konum(map). X,Y,Z RPY, Quaternion
- [[NDT]]
- Lidar
- Radar
- Kameralar

##### Relative Local Localization

Belli bir başlangıç noktasına göre konum (orijin)
- X, Y, Z, RPY, Quaternion
- Slam
- VO
- IMU
- Enkoder (Wheel Odometry)
- Kamera

[[State Estimation for Localization]]

##### Autoware.AUTO TF

![[TF.png]]