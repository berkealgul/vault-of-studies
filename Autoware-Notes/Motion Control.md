
![[motion-control.png]]
![[motion-control-2.png]]

#### Route Planner

Rota hesaplanır. Rota, belli başlı x-y koordinatlarıdır. Teknikler:

- Hedef odaklı (A*)
- Ayrıştırma odaklı (vertex graphs)
- Hiyerarşik (otoyol ağları, daha geniş yollar önceliklidir)
- Bounded hop (kestirmeler, mesafe önceden hesaplanır)

#### Path Planner

Rotalar arasındaki patika hesaplanır

- Graph search (A*, Dijksra, occupancy map)
- Curve interpolation (rotadaki hedeflar arasında noktalar bulmaya dayanır)

#### Behavior selector

Patika seçerek aracın nereye gideceğini seçer
- Aracı yoda tutmak
- Kesişimleri yönetmek
- Trafik kuralları vs.

Teknikler:
- Finite State Machine (Sonru kurallar geliştirilebilir ama belirsizliğe karşı dezavantajlıdır)
- Ontology-based (Mesela karmaşık yol ağında kurallara göre hareket etmek)
- Markov decision processes 

#### Motion Planner

Behaviour Planner tarafından seçilen patikayı bazı kurallar çerçevesinde takip eder
- Komfort, eco-driving
- Güvenlik
- Kinematik sınırlar

Metotlar: 
- Graph search (A*, state lattice, elastic band)
- Sampling-based (RRT)
- Curve interpolation 
- Numerical optimization

#### Obstacle Avoider

Patika engellere göre değiştirilebilir.
Genelde yavaşlaş
