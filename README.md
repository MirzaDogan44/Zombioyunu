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
| Silah değiştir | `1` tabanca, `2` pompalı, `3` roketatar, `4` makineli, `5` keskin nişancı; `Q` veya fare tekerleği sıradaki | SİLAH butonu (sıradaki silah) |
| Şarjör değiştir | `R` (şarjör boşalınca otomatik) | ŞARJ butonu |
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
  - **Azrail (Boss):** 10. dalgada gelir; tırpanlı, süzülen bir ölüm meleği. Ekranın üstünde kendi can barı var. Animasyonları duruma göre oynar: süzülme, tırpan savurma (yakındaysanız 30 hasar), kırmızı uyarı alanından sonra karanlık hamleyle atılma ve etrafına 4 gölge yaratık çağırma. Canı yarıya inince öfkelenir. Ölünce ölüm animasyonu, zincirleme büyük patlama, güçlü ekran sarsıntısı ve kısa bir ağır çekim olur.
- Ağaçlar, kayalar ve demir çitler hem sizi hem zombileri hem de mermileri durdurur. Çalılar, mezar taşları, tabelalar ve çiçekler sadece süs.
- Nesneler derinliğe göre sıralanır. Bir ağacın arkasına geçtiğinizde ağaç yarı saydam olur ve karakteriniz görünür kalır. Oyuncunun başladığı orta alan açık.
- **Atmosfer:** karartma ve el feneri yok, harita tamamen görünür. Sadece hafif bir kenar vinyeti ve hafif soğuk bir renk tonu var (`CONFIG.light`).
- **Kan izleri:** ölen zombi yerde, son vuruş yönüne uzanan bir kan izi bırakır ve iz yavaşça kaybolur. Yaralı zombiler yürürken kan damlatır.
- Bir dalgada son 5 zombi kaldığında, ekran dışındakiler kenardaki kırmızı oklarla gösterilir. En yüksek skor tarayıcıda saklanır.

### Doom modu

- **Tempo:** karakter hızlı (300 px/sn), zombiler daha hızlı ve kalabalık (dalga başına 24 → 135, aynı anda 100'e kadar; doğma aralığı 0,5 → 0,13 sn). Yakına gelen zombiler kısa süre hızlanıp size atılır; sürekli hareket etmeniz gerekir.
- **Silahlar:**

  | Tuş | Silah | Özellik | Şarjör / yedek |
  |---|---|---|---|
  | 1 | Tabanca | Hızlı (saniyede 5 atış); özellik kartlarının çoğu buna etki eder | 12 / sınırsız |
  | 2 | Pompalı | 9 saçmalı geniş atış, yakından devasa hasar, zombileri geriye uçurur, sizi geri iter | 6 / 18 (en fazla 48) |
  | 3 | Roketatar | Duman izli roket, alan hasarlı patlama, zombileri savurur | 1 / 5 (en fazla 15) |
  | 4 | Makineli (AK-47) | Saniyede 11 atış, biraz dağınık | 30 / 60 (en fazla 210) |
  | 5 | Keskin Nişancı (KAR98) | 130 hasar, 8 zombiyi delip geçer, yavaş | 5 / 10 (en fazla 30) |

  Silah elde tutulur, fareye doğru döner, sola nişan alınca dikey çevrilir. Mermi her silahın kendi namlu noktasından çıkar; her silahın mermisi farklı (küçük mermi, saçma, duman izli roket). Ateşte namlu parlaması, hafif geri tepme ve yere düşen boş kovan var; sprite sayfalarındaki ateş ve şarjör değiştirme animasyonları oynatılır. Silah değiştirirken kısa bir indirme/kaldırma animasyonu var. Sağ altta silah ikonu, şarjördeki ve yedekteki mermi sayısı görünür; şarjör değiştirirken dolum çubuğu çıkar.

  Ölen zombilerden mermi kutusu düşer (pompalı, makineli, keskin nişancı veya roket için; tank ve boss daha sık düşürür). Kutular yakındayken size doğru çekilir. Bir silahın hiç mermisi kalmayınca tabancaya geçilir.
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
- `CONFIG.weapons`: her silah için hasar (`damage`), atış hızı (`fireRate`), şarjör (`mag`), şarjör değiştirme süresi (`reloadTime`), mermi hızı (`bulletSpeed`), menzil, yayılma, saçma sayısı, yakın/uzak hasar çarpanı, delme (`pierce`), patlama yarıçapı ve hasarı, geri itme, geri tepme, ekran sarsıntısı, hit-stop, başlangıç/en fazla yedek mermi, kutudan gelen mermi ve eldeki boyut (`scale`).
- `CONFIG.weaponAnim`: silah değiştirme süresi ve ateş animasyonunun kare hızı.
- `CONFIG.ammo`: mermi kutusu düşme olasılıkları, silahlara göre dağılım (`shares`), kutunun ömrü, mıknatıs ve toplama mesafesi.
- `CONFIG.dash`: dash hızı, süresi, dolum süresi; "Koçbaşı" kartının hasarı.
- `CONFIG.glory`: infaz eşikleri (%25, boss %10), menzil, verdiği can, ölümsüzlük süresi, hit-stop, sarsıntı.
- `CONFIG.combo`: kombo süresi, skor çarpanı adımı ve üst sınırı, ekranda çıkan yazılar.
- `CONFIG.barrels`: varil sayısı, canı, patlama hasarı ve yarıçapı, zincirleme gecikme, oyuncuya hasarı (`playerDamage: 0` ile kapatılır).
- `CONFIG.feel`: hit-stop üst sınırı (60 ms), hasar sayıları, et parçası sayısı, "Zincirleme" kartının patlaması.
- `CONFIG.music`: varsayılan müzik/efekt sesi, şarkı geçiş süresi, menü/savaş/yoğun savaş/dalga arası/duraklatma ses çarpanları.
- `CONFIG.zombies`: her türün canı, hızı, ayaktaki hareket çarpışması (`radius`), hasarı, puanı; boss'un atılma, tırpan savurma (`meleeDamage`, `meleeRadius`), çağırma (`summonCount`) ve ölüm ağır çekimi (`deathSlowmo`, `slowmoTime`) ayarları; çağrılan yaratıklar (`minion`); yakındaki zombilerin atılması (`lunge`).
- `CONFIG.hitbox.scale`: hitbox dairesinin görsele göre oranı (0.85 = görselden biraz küçük).
- `CONFIG.light`: kenar vinyeti (`vignette`, 0.32), hafif soğuk ton (`tint`, `'#ffffff'` = kapalı), soluklaşma (`desaturate`). Karartma ve el feneri kapalı (`darkness: 0`); eski gece modu için `darkness: 0.86`, `fogAlpha` ve `eyeGlow` değerleri artırılabilir.
- `CONFIG.effects`: kan izinin ömrü (`decalLife`), damla sıklığı ve ömrü, parçacık sınırı (dolunca en eski parçacıkların yerine yazılır).
- `CONFIG.sprites`: sprite'ların büyütme oranları (1 sanat pikseli = kaç dünya pikseli), ağaç/çalı/kaya/çit boyutları, zemin piksel boyutu.
- `CONFIG.anim`: zombi animasyonu. Tür başına `freq` (saniyedeki zıplama), `bob` (zıplama yüksekliği), `squash` (ezilme/uzama), `sway` (sallanma açısı); dururken hız çarpanı (`idleFactor`); oyuncunun yürüme karesi hızı.
- `CONFIG.audio`: genel ses, müzik ve her efektin ses seviyesi.
- `CONFIG.waves`: dalga başına zombi sayıları (`counts`: 24 → 135), aynı anda en fazla zombi (`maxAlive`: 100), doğma aralığı (`spawnIntervalFirst`/`Last`: 0,5 → 0,13 sn), dalga başına can/hız artışı, doğma aralıkları, koşucu ve tankların hangi dalgadan itibaren çıkacağı.
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
  weapons/   pistol, shotgun, rocket, rifle, sniper: ateş/şarjör sprite sayfaları, namlu parlaması, mermi
  boss/      Azrail: süzülme, saldırı, yetenek, çağırma, ölüm; gölge yaratık animasyonları
  audio/     Efekt sesleri (boom.mp3 dahil)
  music/     Çalma listesi (8 parça, MP3)
  unused/    Oyunda kullanılmayan dosyalar
```

Hangi parça nerede kullanılıyor:

- **Karakter:** Player1–3 yürüme animasyonu. Silah sprite'tan ayrı kesilip nişan yönüne döndürülüyor, gövde sağa/sola çevriliyor.
- **Zombiler:** ZombiePack'te yürüme animasyonu yok. Normal, tank ve boss için kodla sinüs zıplama, squash & stretch ve sallanma eklendi; her zombi farklı zamanda zıplıyor, gölge yerde sabit kalıyor. Koşucu, Zombie1/2'nin 2 kareli yürüyüşünü kullanıyor.
- **Harita:** FreeEnvironment'tan çam ağaçları, kuru ağaç, kaya, çalılar ve renkli çalılar; Background'dan demir çit; Zombie paketinden mezar taşı.
- **Arayüz:** Pixel UI pack 3 parçaları 9-slice (CSS `border-image` ve canvas) ile butonlarda, panellerde, kart çerçevelerinde, can barlarında, boss barında ve joystick düğmelerinde kullanılıyor.
- **Silahlar (assets3/weapons):** tabanca "Pistol - Second version" (80x48, efektsiz ateş + şarjör boşaltma), pompalı ve KAR98 V1.00 paketinden (ayrı namlu parlaması sayfası ile), makineli AK-47 ve roketatar (Bazooka M20) Guns V1.01 paketinden. El, namlu ve kovan çıkış noktaları her silahın karesi üzerinde ölçüldü (`WSPR`). HUD ikonu ateş sayfasının ilk karesinden kesiliyor.
- **Boss (assets3/boss):** Azrail sprite sayfaları (100x100 kare) ve gölge yaratık (50x50). Hitbox görünen piksellerden ölçüldü.
- **Sesler:** tık (butonlar), adım sesi (isabet), patlama 1 (zombi ölümü), patlama 2 (boss ölümü, patlayıcı mermi), hitHurt (hasar), powerUp 4 (dalga başlangıcı), powerUp 5 (dalga bitişi, özellik seçimi), jump (boss atılma uyarısı), arka plan müziği.

Paketlerde karşılığı olmayan parçalar aynı piksel stilinde kodla çiziliyor:

- **Zemin:** `Tiles/Tilemap` bir zemin karosu değil, Kenney'nin fare imleci paketi. Bu yüzden zemin (çimen, toprak, çakıl, çiçek) piksel piksel üretiliyor; imleç paketinden nişangah ve el imleçleri kullanılıyor.
- **Özellik ikonları:** PowerUps'ta 15 özelliğe karşılık 3 farklı ikon var. Kalan 12 ikon, PowerUps'taki 16x16 çerçeve ve renk paletiyle çiziliyor.
- **Doom modu:** patlayıcı varil, mermi kutuları, roket mermisi, ateş topu/duman/şok dalgası/et parçası efektleri ve müzik notası simgesi pakette yok, kodla çiziliyor.
- **Sentezlenmiş sesler (Web Audio):** patlamalar gürültü + alçak geçiren filtre + derin bas ile üretiliyor ve türüne göre farklı tonda: roket derin ve uzun, varil daha ağır ve çatırtılı, öldürme patlaması kısa ve tiz, boss en derini. Pompalı, makineli, keskin nişancı, roket ateşleme, silah değiştirme, şarjör değiştirme, boss tırpanı ve çağırma, dash, infaz, mermi toplama, boş tetik ve kombo yazısı sesleri de sentezleniyor. Ayrıca `boom.mp3` boss ölümünde sentezle birlikte çalıyor. Tüm efektler bir kompresörden geçiyor; üst üste binen patlamalar cızırdamıyor.
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
- `weapons/`: eski silah görselleri (hafif makineli, saldırı tüfeği, iki el bombası atar, eski pompalı ve roketatar)
- `weapons-pack/`: assets3 silah paketinin kullanılmayan dosyaları (Glock, Revolver, MP5, kalın bazuka, tek tek sprite'lar, GIF'ler, tasarım görselleri)
- `boss/`: Azrail'in Aseprite proje dosyaları ve tek satırlık yedek sayfa

## Lisanslar

| Paket | Kaynak / Lisans |
|---|---|
| Tiles / Tilemap (Cursor Pixel Pack) | Kenney (www.kenney.nl), **CC0**: kişisel ve ticari kullanım serbest. Lisans dosyası: `assets/ui/cursors/License-Kenney.txt` |
| ZombiePack | Özel lisans: `assets/zombies/LICENSE-ZombiePack.txt`. Oyunun parçası olarak ticari kullanım ve değiştirme serbest. Asset'lerin tek başına dağıtılması, satılması ve **ham dosyaların başkalarının indirebileceği şekilde sunulması yasak**. |
| Player, Zombie, FreeEnvironment, Background, Pixel UI pack 3, PowerUps, Overlay, Menu, Logo, Audio, silah görselleri, assets3 silah ve boss paketleri, `boom.mp3` | Lisans dosyası yok. Lisansı ve gerekli atıfı, dosyaları indirdiğiniz yerden kontrol edin. |
| `assets/music/` (Orman Gecesi hariç) | **Telifli ticari müzikler:** Mick Gordon (Doom Eternal OST), Doom OST, John Williams (Duel of the Fates), Krutikov Music ve çeşitli phonk parçaları. Dosya meta verilerine göre YouTube kaynaklı. Kişisel kullanım dışında yayınlamak için hak sahiplerinden izin gerekir. |

> **Dikkat:** Bu depo herkese açıksa, `assets/` içindeki ham dosyalar herkes tarafından indirilebilir. Bu, ZombiePack lisansındaki "ham dosyaları indirilebilir şekilde sunma" yasağıyla çelişebilir. Daha da önemlisi, `assets/music/` içindeki telifli şarkıların herkese açık bir depoda veya yayınlanmış bir oyunda dağıtılması telif ihlali sayılabilir. Depoyu gizli tutmanızı; oyunu yayınlayacaksanız bu şarkıları telifsiz ya da lisanslı müziklerle değiştirmenizi öneririm (`PLAYLIST` listesinden kolayca değiştirilir).

Oyun kodu (`index.html`) bu projeye aittir.

## Teknik notlar

- Zemin 500x500'lük parçalar halinde, düşük çözünürlükte bir kez üretiliyor ve pikselli büyütülerek çiziliyor. Ekranın dışında kalan nesneler çizilmiyor.
- Nesneler ve karakterler ayak noktalarına göre sıralanıyor (2.5D). Engellerle ve birbirleriyle çarpışma ayaklardaki küçük dairelerle hesaplanıyor.
- **Hitbox:** her zombi sprite'ı (ZombiePack'in 64 karesi, Zombie1/2) ve oyuncu gövdesi için hitbox, görünen (opak) piksellerden önceden ölçüldü. Merkez opak piksellerin ortalaması, yarıçap aynı alana sahip dairenin yarıçapı; şeffaf kenarlar sayılmıyor. Daire zıplama animasyonunu da takip ediyor. Mermi isabeti, oyuncuya temas (hasar ve itme), bıçaklar ve patlamalar aynı hitbox'ı kullanıyor. `H` tuşu bu daireleri gösteriyor: kırmızı zombi, yeşil oyuncu, sarı kesikli ayak çarpışması.
- **Işık:** varsayılan olarak karartma katmanı hiç çizilmiyor; sadece radyal gradyanlı bir kenar vinyeti ve `multiply` ile soğuk ton uygulanıyor. `darkness` 0'dan büyük yapılırsa düşük çözünürlüklü ışık katmanı (oyuncu, fener, namlu, patlamalar) yeniden devreye girer.
- **Ağır çekim:** boss ölünce oyun zamanı `deathSlowmo` (0.3) hızına iner ve `slowmoTime` sonunda yumuşakça normale döner.
- **Hit-stop:** güncelleme kısa süre atlanır, çizim devam eder; arka arkaya donmaları önlemek için bekleme süresi var.
- **Takılma koruması:** yarım saniyede 10 pikselden az ilerleyen zombi engelin kenarı boyunca yana kayar. 8 saniye takılı kalan ve ekran dışında olan zombi harita kenarında yeniden doğar; dalgalar kilitlenmez.
- **Müzik:** iki ses elemanı arasında çapraz geçiş yapılıyor. Dosyalar her tarayıcıda çalışsın diye MP3 (bazı Chromium sürümleri AAC/m4a çalamıyor).
- Zombiler oyuncudan dışa doğru hesaplanan bir akış alanını (40 px'lik ızgarada Dijkstra) takip ederek engellerin etrafından dolaşıyor.
- `file://` ile açıldığında görseller canvas'a yalnızca çiziliyor, pikselleri okunmuyor; böylece tarayıcı güvenlik kısıtlamalarına takılmıyor.
- Otomatik testte 10 dalganın tamamı, üç silahı ve infazı kullanan bir bot ile oynandı; aynı anda 70 zombi oldu. GPU'suz test tarayıcısında 60 zombi ve tüm efektler açıkken ~57 FPS ölçüldü; GPU'lu cihazlarda daha hızlı çalışması beklenir.
