[Referans](https://gitlab.com/ApexAI/autowareclass2020/-/tree/master/lectures/07_Object_Perception_LIDAR)

### Lidar Object Detection Stack

![[lidar-stack.png]]

#### Ground Filtering

Obje tespitinin temel amacı engellerden kaçınmaktır ve verilerimizi obje tespiti algoritmalarına göndermeden önce yüzey noktalarını ayıklamamız gereklidir, çünkü

- Zemine çarpamayız bu yüzden kullanılması gereksizdir
- Algoritmalara olabildiğince az veri göndermeliyiz

Olası bazı zemin ayıklama teknikleri

- Eğri/normallere bakmak -> Yavaş
- Sahneye büyük yüzey sığdırmak (RANSAC) -> Hızlı, kararsız ve yüzey modeli her şarta uygun değil
- Derinlik resminden ışın(ray) saçmak -> Oldukça hızlı ve kararlı ama isabet eksikliği var, ayrıca yüksek çözürnülüğe ihtiyaç duyar

Autoware ışın tabanlı yöntemi kullanmaktadır

##### Işın Yöntemi

![[ray-filtering-1.png]]
Öncelikle noktalar şekildeki gibi çevresel bölgelere ayrılır  

![[ray-filtering-2.png]]

1- Her bölgede, sensöre en yakın ayrıca yüzeyde olduğunu bildiğimiz noktadan başlarız ve o noktaya `ground` etiketi veririz, yani yüzey olarak kabul görür
2- Bir sonraki her nokta için bir önceki noktanın `local_max_slope` (local cone) oluşturduğu üçgenin içinde olup olmadığına bakarız
2.a- Eğer içindeyse önceki noktanın etiketini alır
2.b- İçinde değilse sensörün `general_max_slope` (global cone) ile oluşturduğu üçgenin içinde olup olmadığına bakarız ve içindeyse 'ground' etiketini olur

Yukarıdaki örneğe p0 ile başlarsak:
- p0 araca en yakın nokta ve global cone'un içinde bu yüzden yüzeyden sayılır
- p1 p0 noktasının oluşturduğu üçgenin içinde değil ama sensörün üçgeninde oluğu için yüzey sayılır
- Bu aynı durum p2, p3 ve p4 için geçerlidir
- p5 ve p6 global cone'un içinde olmadığı için zemin değildir

#### Object Detection

Zemin filtresinden geçen nokta bulutundaki olasu objeleri belirlememiz gerekir. Bunun için noktaları  gruplandırmalıyız(clustering/segmentation)

##### Euclidean Clustrering

Klasik segmantation algoritmalarındandır 
- P nokta bulutundan kd-tree oluştur
- boş cluster seti oluştur C, ve noktalar için queue oluştur Q
- P deki her nokta p için
	- p noktatına Q'e ekle
	- Q deki her pq için
		- pq nun belli bir r mesafasindeki komşularını bul ve bu noktalar işlenmemişse Q'ya ekle
	- Q'deki hern oktayı C'ye ekle ve Q'yu sıfırla

Bu algoritmanın hızlanması için `Integer lattice/Spatial hash` veriyapıları kullanılabilir
[1](https://autowarefoundation.gitlab.io/autoware.auto/AutowareAuto/geometry-spatial-hash.html#:~:text=The%20spatial%20hash%20is%20a,neighbor%20queries%20in%20low%20dimensions.&text=Where%20in%20this%20case%20'd,r%60%20is%20the%20fixed%20radius.)
[2](https://en.wikipedia.org/wiki/Integer_lattice)

#### Shape Extraction

Oluşturual clusterlar daha sonra bu clusterları dünyada daha basdit bir şekilde temsil etmek ve collision detection algoritmalarında kullanılmaları için kutulaştırılmalılar(daha iyi bi tabir bulamadım)

![[bbx3.png]]

![[bbx.png]] 

Bu `bounding box` denen kutular basit bir yapıya sahip olmaları önemlidirler ve bunları yapmanın çeşitli teknikleri vardır. Bunlardan biri yukarıdaki şekilde kullanılan, her cluster için [PCA](https://en.wikipedia.org/wiki/Principal_component_analysis) hesaplamaktır. Bu teknikle algoritma O(n) seviyesine düşürebilir (Convex hull O(nl og n) ile çalışır) lakin yeterince optimal sonuçlar veremez ve hatalara sebep olabilir 

![[bbx2.png]]

Autoware.Auto bu durumu algoritmayı hafif değiştirerek çözer
- Sadece blob eksenini hesaplar
- Noktaları hesaplanan blob eksenine göre sıralar
- Sıralanmış noktaların uç kısımları kutu köşelerini oluşturur

#### Şekilleri Kullanmak

Oluşturulan kutuları kullanmalıyız
- Classification
- Feature extraction
- Tracking
- Collision detection

##### Collision Detection

Olası Algoritmalar
- [SAT](https://en.wikipedia.org/wiki/Hyperplane_separation_theorem#Use_in_collision_detection)
- [GJK](https://en.wikipedia.org/wiki/Gilbert%E2%80%93Johnson%E2%80%93Keerthi_distance_algorithm) [(+EPA)](http://www.dyn4j.org/2010/05/epa-expanding-polytope-algorithm/)

Uygulamalar
- [Mirtich, 1997](https://www.merl.com/publications/docs/TR97-23.pdf)
- [Lin and Gottschalk](https://pdfs.semanticscholar.org/ca4b/fcf1df1728cff8ffbf28dba52b5741514f4b.pdf)
![[collision.png]]

##### Tracking

- Tracking by assingment
	-  Veri eşleştırme teknikleri [Hungarian algortimasi](https://en.wikipedia.org/wiki/Hungarian_algorithm) [GNN](https://www.researchgate.net/publication/228601003_A_study_of_a_target_tracking_algorithm_using_global_nearest_neighbor_approach) 
	- Durum tahmini [Kalman filtreleri](https://en.wikipedia.org/wiki/Kalman_filter), [Partikül filtreleri](https://en.wikipedia.org/wiki/Particle_filter)
- Birleştirilmiş teknikler
	- Multiple Hypothesis Tracking [(Kim et al)](https://web.engr.oregonstate.edu/~lif/MHT_ICCV15.pdf)


![[lidar-sum.png]]