# Zombi Dalgası

Tarayıcıda çalışan, kuş bakışı (2.5D), Doom tarzı hızlı tempolu bir zombi hayatta kalma oyunu: üç silah, dash, infaz, kombo, zincirleme patlayan variller. Kurulum gerektirmez: oyun `index.html` dosyasında (HTML + CSS + JavaScript, Canvas API), görseller ve sesler `assets/` klasöründe.

## Nasıl çalıştırılır?

`index.html` dosyasına çift tıklayın, oyun tarayıcıda açılır. `assets/` klasörü `index.html` ile aynı yerde durmalı. İnternet bağlantısı gerekmez.

`assets/` klasörü bulunamazsa oyun yine açılır; eksik görsellerin yerine eski, kodla çizilmiş grafikleri kullanır.

Telefonda oynamak için klasörü olduğu gibi bir statik sunucuya (ör. GitHub Pages) koyup telefon tarayıcısından açabilirsiniz. Dokunmatik cihaz otomatik algılanır.

## Kontroller

| | Bilgisayar | Telefon / Tablet |
|---|---|---|
| Hareket | `W A S D` veya ok tuşları | Sol alttaki joystick (ekranın sol yarısında herhangi bir yere dokunun) |
| Nişan | Mouse | Sağ alttaki joystick |
| Ateş | Sol tık (basılı tutunca sürekli ateş) | Sağ joystick'i çekince otomatik ateş |
| Silah değiştir | `1` tabanca, `2` pompalı, `3` roketatar; `Q` veya fare tekerleği sıradaki | SİLAH butonu (sıradaki silah) |
| Dash | `Shift` veya `Boşluk` | DASH butonu |
| İnfaz | `E` (parlayan zombinin yakınında) | İNFAZ butonu (hedef varken turuncu yanar) |
| Duraklat | `ESC` veya `P` | Sağ üstteki duraklat butonu |
| Müzik | Sağ üstteki nota butonu (oyun durmaz) veya duraklatma menüsü | Aynı |
| Ses aç/kapa | `M` | Sağ üstteki hoparlör butonu |
| Hitbox debug | `H`: hitbox dairelerini gösterir/gizler | – |
| Özellik seçimi | Kartlara tıklama veya `1` `2` `3` tuşları | Karta dokunma |

Sesler tarayıcı kuralları gereği ilk tıklama ya da dokunuştan sonra başlar. Ses ve müzik tercihleri tarayıcıda saklanır.

## Oyun

- Amaç **10 dalga** boyunca hayatta kalmak. Zombiler harita kenarlarından, ekran dışından gelir ve engellerin etrafından dolaşarak size doğru yürür.
- Oyunun başında ve her dalganın sonunda **3 rastgele özellik kartı** çıkar. Kart çerçevesinin rengi nadirliği gösterir: Sıradan (yeşil), Nadir (mavi), Efsanevi (turuncu). Aynı özellik birden çok kez alınabilir ve etkisi üst üste biner.
- Zombi türleri:
  - **Normal:** orta hız, orta can. Görünümü ZombiePack'teki 60 farklı zombiden rastgele seçilir.
  - **Koşucu:** hızlı ama az canlı. 4. dalgadan itibaren çıkar.
  - **Tank:** yavaş, büyük, çok canlı (itfaiyeci zombi). 6. dalgadan itibaren çıkar.
  - **Dev Zombi (Boss):** 10. dalgada gelir (korsan kaptan). Ekranın üstünde kendi can barı var. Ara ara kırmızı bir uyarı alanı gösterip o yöne hızla atılır; kırmızı alandan çekilin. Canı yarıya inince öfkelenir.
- Ağaçlar, kayalar ve demir çitler hem sizi hem zombileri hem de mermileri durdurur. Çalılar, mezar taşları, tabelalar ve çiçekler sadece süs.
- Nesneler derinliğe göre sıralanır. Bir ağacın arkasına geçtiğinizde ağaç yarı saydam olur ve karakteriniz görünür kalır. Oyuncunun başladığı orta alan açık.
- **Karanlık atmosfer:** gece. Oyuncunun etrafında küçük bir ışık halkası var; nişan yönünde, kenarları yumuşak bir el feneri konisi yanıyor. Ateş edince namlu parlaması etrafı kısa süre aydınlatıyor, patlamalar da ışık saçıyor. Renkler soğuk ve soluk (hafif mavi-yeşil), ekran kenarlarında vinyet var, yerde hafif sis kayıyor. Karanlıktaki zombilerin gözleri parlıyor (boss'unki kırmızı).
- **Kan izleri:** ölen zombi yerde, son vuruş yönüne uzanan bir kan izi bırakır ve iz yavaşça kaybolur. Yaralı zombiler yürürken kan damlatır.
- Bir dalgada son 5 zombi kaldığında, ekran dışındakiler kenardaki kırmızı oklarla gösterilir. En yüksek skor tarayıcıda saklanır.

### Doom modu

- **Tempo:** karakter hızlı (300 px/sn), zombiler daha hızlı ve kalabalık (dalga başına 16 → 90, aynı anda 70'e kadar). Yakına gelen zombiler kısa süre hızlanıp size atılır; sürekli hareket etmeniz gerekir.
- **Silahlar:**

  | Silah | Özellik | Mermi |
  |---|---|---|
  | Tabanca | Hızlı (saniyede 5 atış); özellik kartlarının çoğu buna etki eder | Sınırsız |
  | Pompalı | 9 saçmalı geniş atış, yakından devasa hasar, zombileri geriye uçurur, sizi geri iter | 16 ile başlar, en fazla 48 |
  | Roketatar | Alan hasarlı patlama, zombileri savurur | 5 ile başlar, en fazla 15 |

  Ölen zombilerden mermi kutusu düşer (yeşil: saçma, kırmızı: roket; tank ve boss daha sık düşürür). Kutular yakındayken size doğru çekilir. Mermi bitince tabancaya geçilir.
- **Dash:** kısa ve hızlı bir atılma. Dash sırasında hasar almazsınız. Dolum süresi silah panelinin altındaki mavi çubukta görünür.
- **İnfaz:** canı %25'in altına düşen zombi turuncu parlar (boss için %10). Yanındayken `E`'ye basınca karakter atılıp onu parçalar; 20 can ve kısa bir ölümsüzlük kazanırsınız.
- **Kombo:** arka arkaya öldürmeler kombo sayacını artırır. Her 5 öldürmede skor çarpanı 1 artar (en fazla x8). 5, 10, 20, 35 ve 50. öldürmelerde "BRUTAL!", "SAVAGE!", "UNSTOPPABLE!", "MASSACRE!", "GODLIKE!" yazıları çıkar. 3 saniye öldürme olmazsa kombo sıfırlanır.
- **Patlayıcı variller:** haritaya dağılmış kırmızı variller vurulunca ya da bir patlamaya yakalanınca patlar ve yakındaki varilleri zincirleme patlatır. Yakınındaysanız size de hasar verir. Her dalga başında birkaç yeni varil eklenir.
- **Vuruş hissi:**
  - Pompalı isabetlerinde, roket ve varil patlamalarında, tank/boss ölümlerinde ve infazda 30–60 ms hit-stop (oyun kısacık donar).
  - Ekran sarsıntısı ve geri tepme silaha göre değişir.
  - Vurulan zombi beyaz parlar ve geri itilir. Ölen zombi et parçalarına ayrılır; parçalar yere düşüp kan izi bırakır.
  - Patlamalarda ateş topu, duman, şok dalgası, kıvılcım ve yanık izi oluşur.
  - Hasar sayıları fırlar; kritik vuruşlar büyük ve sarıdır.
- **Müzik:** `assets/music/` içindeki 8 parça çalma listesinde. Sağ üstteki nota butonu oyunu durdurmadan bir panel açar: şarkı listesi, önceki/sonraki, oynat/durdur, karışık çal, tekrarla, ayrı müzik ve efekt ses kaydırıcıları. Seçimler kaydedilir. Şarkılar arasında yumuşak geçiş var. Müzik dalga aralarında kısılır, kombo yükselince veya boss gelince hafifçe yükselir.

### Özellikler (21 tane)

| Özellik | Nadirlik | Etki |
|---|---|---|
| Güçlü Mermi | Sıradan | +%25 hasar |
| Çevik Adımlar | Sıradan | +%15 hareket hızı |
| Seri Atış | Sıradan | +%20 atış hızı |
| Sağlam Beden | Sıradan | +30 maksimum can ve 30 iyileşme |
| Yenilenme | Sıradan | Saniyede +1 can |
| Sarsıcı Mermi | Sıradan | Mermiler zombileri daha çok geri iter |
| Hızlı Mermi | Sıradan | +%20 mermi hızı ve menzili |
| Çift Mermi | Nadir | Her atışta +1 paralel mermi |
| Yayılma Atışı | Nadir | Üçlü yayılma, sonra her seviyede +2 mermi |
| Delici Mermi | Nadir | Mermi +1 zombinin içinden geçer |
| Kritik Vuruş | Nadir | +%10 kritik şansı (2x hasar) |
| Vampir | Nadir | Öldürülen her zombi +2 can verir |
| Koruyucu Bıçaklar | Efsanevi | Etrafınızda dönen +1 bıçak |
| Patlayıcı Mermi | Efsanevi | İsabet eden mermi patlar, çevreye hasar verir |
| İkinci Şans | Efsanevi | Ölünce bir kez %50 canla dirilirsiniz |
| Dolu Fişek | Nadir | Pompalıya +2 saçma |
| Büyük Patlama | Nadir | Roketin patlama alanı %30 büyür |
| Koçbaşı | Nadir | Dash çarptığı zombilere hasar verir |
| Zincirleme | Efsanevi | Öldürülen zombiler patlar |
| Soğukkanlı | Sıradan | Kombo süresi +1 saniye uzar |
| Kan Bedeli | Sıradan | İnfaz +15 daha fazla can verir |

Çift Mermi, Yayılma Atışı ve Delici Mermi yalnızca tabancaya etki eder.

## Ayarları değiştirmek

Bütün ayarlar `index.html` içindeki `<script>` bloğunun başında, **`CONFIG`** objesinde duruyor:

- `CONFIG.player`: can (100), hız (300), tabancanın atış hızı (5/sn) ve hasarı (11), ölümsüzlük süresi (0,5 sn), çarpışma yarıçapı.
- `CONFIG.weapons`: pompalı ve roketatarın atış hızı, saçma sayısı, yayılma, yakın/uzak hasar çarpanı, menzil, geri itme, geri tepme, ekran sarsıntısı, hit-stop, patlama yarıçapı, başlangıç/en fazla mermi ve kutudan gelen mermi.
- `CONFIG.ammo`: mermi kutusu düşme olasılıkları, roket/saçma oranı, kutunun ömrü, mıknatıs ve toplama mesafesi.
- `CONFIG.dash`: dash hızı, süresi, dolum süresi; "Koçbaşı" kartının hasarı.
- `CONFIG.glory`: infaz eşikleri (%25, boss %10), menzil, verdiği can, ölümsüzlük süresi, hit-stop, sarsıntı.
- `CONFIG.combo`: kombo süresi, skor çarpanı adımı ve üst sınırı, ekranda çıkan yazılar.
- `CONFIG.barrels`: varil sayısı, canı, patlama hasarı ve yarıçapı, zincirleme gecikme, oyuncuya hasarı (`playerDamage: 0` ile kapatılır).
- `CONFIG.feel`: hit-stop üst sınırı (60 ms), hasar sayıları, et parçası sayısı, "Zincirleme" kartının patlaması.
- `CONFIG.music`: varsayılan müzik/efekt sesi, şarkı geçiş süresi, menü/savaş/yoğun savaş/dalga arası/duraklatma ses çarpanları.
- `CONFIG.zombies`: her türün canı, hızı, ayaktaki hareket çarpışması (`radius`), hasarı, puanı; boss'un atılma ayarları; yakındaki zombilerin atılması (`lunge`).
- `CONFIG.hitbox.scale`: hitbox dairesinin görsele göre oranı (0.85 = görselden biraz küçük).
- `CONFIG.light`: karanlık oranı (`darkness`), oyuncunun etrafındaki ışık yarıçapı (`radius`), fener menzili ve açısı (`coneRange`, `coneAngle`), namlu ışığı (`muzzleRadius`, `muzzleTime`), vinyet, soluklaşma (`desaturate`), soğuk ton (`tint`), sis (`fogAlpha`, `fogSpeed`), göz parlaklığı (`eyeGlow`). Karanlığı kapatmak için `darkness: 0`.
- `CONFIG.effects`: kan izinin ömrü (`decalLife`), damla sıklığı ve ömrü, parçacık sınırı (dolunca en eski parçacıkların yerine yazılır).
- `CONFIG.sprites`: sprite'ların büyütme oranları (1 sanat pikseli = kaç dünya pikseli), ağaç/çalı/kaya/çit boyutları, zemin piksel boyutu.
- `CONFIG.anim`: zombi animasyonu. Tür başına `freq` (saniyedeki zıplama), `bob` (zıplama yüksekliği), `squash` (ezilme/uzama), `sway` (sallanma açısı); dururken hız çarpanı (`idleFactor`); oyuncunun yürüme karesi hızı.
- `CONFIG.audio`: genel ses, müzik ve her efektin ses seviyesi.
- `CONFIG.waves`: dalga başına zombi sayıları (`counts`: 16 → 90), aynı anda en fazla zombi (70), dalga başına can/hız artışı, doğma aralıkları, koşucu ve tankların hangi dalgadan itibaren çıkacağı.
- `CONFIG.upgrades.rarityWeights`: kartların nadirlik olasılıkları.
- `CONFIG.world`: harita boyutu (3000x3000), engel ve dekor sayıları, ortadaki açık alanın yarıçapı.
- `CONFIG.camera`: yakınlaştırma ve kamera takip yumuşaklığı.

Özelliklerin seviye üst sınırları ve etkileri `UPGRADES` listesinde tanımlı.

## Asset'ler

```
assets/
  player/    Player paketi: 3 yürüme karesi, mermi, namlu parlaması
  zombies/   ZombiePack sprite sayfası (+ lisansı), Zombie1/2 (koşucu)
  map/       FreeEnvironment sayfası (ağaç, kaya, çalı), demir çit, mezar taşı
  ui/        Pixel UI pack 3 parçaları (buton, panel, kart çerçevesi, bar, kalp, joystick düğmesi),
             Menu görselleri (Play, Upgrade, pano, logo), Overlay ikonları (duraklat, devam, çıkış, ateş),
             cursors/ (Kenney Cursor Pixel Pack: nişangah ve el imleci)
  icons/     PowerUps ikonları (can, alev, hız)
  weapons/   Pompalı ve roketatar görselleri
  audio/     Efekt sesleri (boom.mp3 dahil)
  music/     Çalma listesi (8 parça, MP3)
  unused/    Oyunda kullanılmayan dosyalar
```

Hangi parça nerede kullanılıyor:

- **Karakter:** Player1–3 yürüme animasyonu. Silah sprite'tan ayrı kesilip nişan yönüne döndürülüyor, gövde sağa/sola çevriliyor.
- **Zombiler:** ZombiePack'te yürüme animasyonu yok. Normal, tank ve boss için kodla sinüs zıplama, squash & stretch ve sallanma eklendi; her zombi farklı zamanda zıplıyor, gölge yerde sabit kalıyor. Koşucu, Zombie1/2'nin 2 kareli yürüyüşünü kullanıyor.
- **Harita:** FreeEnvironment'tan çam ağaçları, kuru ağaç, kaya, çalılar ve renkli çalılar; Background'dan demir çit; Zombie paketinden mezar taşı.
- **Arayüz:** Pixel UI pack 3 parçaları 9-slice (CSS `border-image` ve canvas) ile butonlarda, panellerde, kart çerçevelerinde, can barlarında, boss barında ve joystick düğmelerinde kullanılıyor.
- **Silahlar:** tabanca karakterin kendi silahı (Player sprite'ından kesiliyor), pompalı `shotgun.png`, roketatar `rpg.png` (`rocket_launcher.png`). Silahlar nişan yönüne döner; namlu ve egzoz noktaları sprite üzerinden hesaplanıyor.
- **Sesler:** tık (butonlar), adım sesi (isabet), patlama 1 (zombi ölümü), patlama 2 (boss ölümü, patlayıcı mermi), hitHurt (hasar), powerUp 4 (dalga başlangıcı), powerUp 5 (dalga bitişi, özellik seçimi), jump (boss atılma uyarısı), arka plan müziği.

Paketlerde karşılığı olmayan parçalar aynı piksel stilinde kodla çiziliyor:

- **Zemin:** `Tiles/Tilemap` bir zemin karosu değil, Kenney'nin fare imleci paketi. Bu yüzden zemin (çimen, toprak, çakıl, çiçek) piksel piksel üretiliyor; imleç paketinden nişangah ve el imleçleri kullanılıyor.
- **Özellik ikonları:** PowerUps'ta 15 özelliğe karşılık 3 farklı ikon var. Kalan 12 ikon, PowerUps'taki 16x16 çerçeve ve renk paletiyle çiziliyor.
- **Doom modu:** patlayıcı varil, mermi kutuları, roket mermisi, ateş topu/duman/şok dalgası/et parçası efektleri ve müzik notası simgesi pakette yok, kodla çiziliyor.
- **Sentezlenmiş sesler (Web Audio):** patlamalar gürültü + alçak geçiren filtre + derin bas ile üretiliyor ve türüne göre farklı tonda: roket derin ve uzun, varil daha ağır ve çatırtılı, öldürme patlaması kısa ve tiz, boss en derini. Pompalı, roket ateşleme, dash, infaz, mermi toplama, boş tetik ve kombo yazısı sesleri de sentezleniyor. Ayrıca `boom.mp3` boss ölümünde sentezle birlikte çalıyor. Tüm efektler bir kompresörden geçiyor; üst üste binen patlamalar cızırdamıyor.
- **Diğerleri:** tahta tabelalar, ses butonu simgesi, ateş sesi (Web Audio ile üretilen kısa "pew"), kan ve parçacık efektleri, boss uyarı alanı, koruyucu bıçaklar.
- **Font:** Pixel UI pack 3'te font dosyası yok. Metinlerde sistem fontu, piksel tarzı sert gölgelerle kullanılıyor.

`assets/unused/` klasöründeki kullanılmayan dosyalar:

- Background'daki bina ve platform zemini görselleri (yan görünüş platform oyunu için)
- Overlay'deki 5 parçalı can barı, zıplama ve sol ok ikonları
- "Press anywhere to start" yazısı
- 1000 piksellik logo
- Health ile birebir aynı olan PowerUps1
- Tek tek `Tiles/` karoları (aynı içerik `ui/cursors/tilemap.png`'de)
- ZombiePack'in tek tek sprite dosyaları (oyun sprite sayfasını kullanıyor)
- `weapons/`: hafif makineli, saldırı tüfeği ve iki el bombası atar görseli (oyunda üç silah var)

## Lisanslar

| Paket | Kaynak / Lisans |
|---|---|
| Tiles / Tilemap (Cursor Pixel Pack) | Kenney (www.kenney.nl), **CC0**: kişisel ve ticari kullanım serbest. Lisans dosyası: `assets/ui/cursors/License-Kenney.txt` |
| ZombiePack | Özel lisans: `assets/zombies/LICENSE-ZombiePack.txt`. Oyunun parçası olarak ticari kullanım ve değiştirme serbest. Asset'lerin tek başına dağıtılması, satılması ve **ham dosyaların başkalarının indirebileceği şekilde sunulması yasak**. |
| Player, Zombie, FreeEnvironment, Background, Pixel UI pack 3, PowerUps, Overlay, Menu, Logo, Audio, silah görselleri, `boom.mp3` | Lisans dosyası yok. Lisansı ve gerekli atıfı, dosyaları indirdiğiniz yerden kontrol edin. |
| `assets/music/` (Orman Gecesi hariç) | **Telifli ticari müzikler:** Mick Gordon (Doom Eternal OST), Doom OST, John Williams (Duel of the Fates), Krutikov Music ve çeşitli phonk parçaları. Dosya meta verilerine göre YouTube kaynaklı. Kişisel kullanım dışında yayınlamak için hak sahiplerinden izin gerekir. |

> **Dikkat:** Bu depo herkese açıksa, `assets/` içindeki ham dosyalar herkes tarafından indirilebilir. Bu, ZombiePack lisansındaki "ham dosyaları indirilebilir şekilde sunma" yasağıyla çelişebilir. Daha da önemlisi, `assets/music/` içindeki telifli şarkıların herkese açık bir depoda veya yayınlanmış bir oyunda dağıtılması telif ihlali sayılabilir. Depoyu gizli tutmanızı; oyunu yayınlayacaksanız bu şarkıları telifsiz ya da lisanslı müziklerle değiştirmenizi öneririm (`PLAYLIST` listesinden kolayca değiştirilir).

Oyun kodu (`index.html`) bu projeye aittir.

## Teknik notlar

- Zemin 500x500'lük parçalar halinde, düşük çözünürlükte bir kez üretiliyor ve pikselli büyütülerek çiziliyor. Ekranın dışında kalan nesneler çizilmiyor.
- Nesneler ve karakterler ayak noktalarına göre sıralanıyor (2.5D). Engellerle ve birbirleriyle çarpışma ayaklardaki küçük dairelerle hesaplanıyor.
- **Hitbox:** her zombi sprite'ı (ZombiePack'in 64 karesi, Zombie1/2) ve oyuncu gövdesi için hitbox, görünen (opak) piksellerden önceden ölçüldü. Merkez opak piksellerin ortalaması, yarıçap aynı alana sahip dairenin yarıçapı; şeffaf kenarlar sayılmıyor. Daire zıplama animasyonunu da takip ediyor. Mermi isabeti, oyuncuya temas (hasar ve itme), bıçaklar ve patlamalar aynı hitbox'ı kullanıyor. `H` tuşu bu daireleri gösteriyor: kırmızı zombi, yeşil oyuncu, sarı kesikli ayak çarpışması.
- **Işık:** düşük çözünürlüklü (ekranın %30'u) bir katman karanlıkla dolduruluyor, ışıklar yumuşak gradyanlarla bu katmandan siliniyor (oyuncu, fener, namlu, patlamalar, roketler, yanan variller). Fener konisinin yumuşak kenarı, farklı genişlikteki 4 koninin üst üste binmesiyle elde ediliyor. Soluk renkler için pahalı `saturation` karıştırması yerine ucuz bir gri-mavi örtü kullanılıyor.
- **Hit-stop:** güncelleme kısa süre atlanır, çizim devam eder; arka arkaya donmaları önlemek için bekleme süresi var.
- **Takılma koruması:** yarım saniyede 10 pikselden az ilerleyen zombi engelin kenarı boyunca yana kayar. 8 saniye takılı kalan ve ekran dışında olan zombi harita kenarında yeniden doğar; dalgalar kilitlenmez.
- **Müzik:** iki ses elemanı arasında çapraz geçiş yapılıyor. Dosyalar her tarayıcıda çalışsın diye MP3 (bazı Chromium sürümleri AAC/m4a çalamıyor).
- Zombiler oyuncudan dışa doğru hesaplanan bir akış alanını (40 px'lik ızgarada Dijkstra) takip ederek engellerin etrafından dolaşıyor.
- `file://` ile açıldığında görseller canvas'a yalnızca çiziliyor, pikselleri okunmuyor; böylece tarayıcı güvenlik kısıtlamalarına takılmıyor.
- Otomatik testte 10 dalganın tamamı, üç silahı ve infazı kullanan bir bot ile oynandı; aynı anda 70 zombi oldu. GPU'suz test tarayıcısında 60 zombi ve tüm efektler açıkken ~57 FPS ölçüldü; GPU'lu cihazlarda daha hızlı çalışması beklenir.
