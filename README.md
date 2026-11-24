# Zombi Dalgası

Tarayıcıda çalışan, kuş bakışı (2.5D) bir zombi hayatta kalma oyunu. Kurulum gerektirmez: oyun `index.html` dosyasında (HTML + CSS + JavaScript, Canvas API), görseller ve sesler `assets/` klasöründe.

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
| Duraklat | `ESC` veya `P` | Sağ üstteki duraklat butonu |
| Ses aç/kapa | `M` | Sağ üstteki hoparlör butonu |
| Özellik seçimi | Kartlara tıklama veya `1` `2` `3` tuşları | Karta dokunma |

Sesler tarayıcı kuralları gereği ilk tıklama ya da dokunuştan sonra başlar. Ses tercihi tarayıcıda saklanır.

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
- Bir dalgada son 5 zombi kaldığında, ekran dışındakiler kenardaki kırmızı oklarla gösterilir. En yüksek skor tarayıcıda saklanır.

### Özellikler (15 tane)

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

## Ayarları değiştirmek

Bütün ayarlar `index.html` içindeki `<script>` bloğunun başında, **`CONFIG`** objesinde duruyor:

- `CONFIG.player`: can (100), hız, atış hızı (3/sn), mermi hasarı (10), ölümsüzlük süresi (0,5 sn), çarpışma yarıçapı.
- `CONFIG.zombies`: her türün canı, hızı, çarpışma yarıçapı (`radius`, ayaklarda), mermi isabet alanı (`hitRadius`, `hitLift`: gövdenin ortası), hasarı, puanı; boss'un atılma ayarları.
- `CONFIG.sprites`: sprite'ların büyütme oranları (1 sanat pikseli = kaç dünya pikseli), ağaç/çalı/kaya/çit boyutları, zemin piksel boyutu.
- `CONFIG.anim`: zombi animasyonu. Tür başına `freq` (saniyedeki zıplama), `bob` (zıplama yüksekliği), `squash` (ezilme/uzama), `sway` (sallanma açısı); dururken hız çarpanı (`idleFactor`); oyuncunun yürüme karesi hızı.
- `CONFIG.audio`: genel ses, müzik ve her efektin ses seviyesi.
- `CONFIG.waves`: dalga başına zombi sayıları (`counts`: 10 → 62), dalga başına can/hız artışı, doğma aralıkları, koşucu ve tankların hangi dalgadan itibaren çıkacağı.
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
  audio/     Müzik ve efekt sesleri
  unused/    Oyunda kullanılmayan dosyalar
```

Hangi parça nerede kullanılıyor:

- **Karakter:** Player1–3 yürüme animasyonu. Silah sprite'tan ayrı kesilip nişan yönüne döndürülüyor, gövde sağa/sola çevriliyor.
- **Zombiler:** ZombiePack'te yürüme animasyonu yok. Normal, tank ve boss için kodla sinüs zıplama, squash & stretch ve sallanma eklendi; her zombi farklı zamanda zıplıyor, gölge yerde sabit kalıyor. Koşucu, Zombie1/2'nin 2 kareli yürüyüşünü kullanıyor.
- **Harita:** FreeEnvironment'tan çam ağaçları, kuru ağaç, kaya, çalılar ve renkli çalılar; Background'dan demir çit; Zombie paketinden mezar taşı.
- **Arayüz:** Pixel UI pack 3 parçaları 9-slice (CSS `border-image` ve canvas) ile butonlarda, panellerde, kart çerçevelerinde, can barlarında, boss barında ve joystick düğmelerinde kullanılıyor.
- **Sesler:** tık (butonlar), adım sesi (isabet), patlama 1 (zombi ölümü), patlama 2 (boss ölümü, patlayıcı mermi), hitHurt (hasar), powerUp 4 (dalga başlangıcı), powerUp 5 (dalga bitişi, özellik seçimi), jump (boss atılma uyarısı), arka plan müziği.

Paketlerde karşılığı olmayan parçalar aynı piksel stilinde kodla çiziliyor:

- **Zemin:** `Tiles/Tilemap` bir zemin karosu değil, Kenney'nin fare imleci paketi. Bu yüzden zemin (çimen, toprak, çakıl, çiçek) piksel piksel üretiliyor; imleç paketinden nişangah ve el imleçleri kullanılıyor.
- **Özellik ikonları:** PowerUps'ta 15 özelliğe karşılık 3 farklı ikon var. Kalan 12 ikon, PowerUps'taki 16x16 çerçeve ve renk paletiyle çiziliyor.
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

## Lisanslar

| Paket | Kaynak / Lisans |
|---|---|
| Tiles / Tilemap (Cursor Pixel Pack) | Kenney (www.kenney.nl), **CC0**: kişisel ve ticari kullanım serbest. Lisans dosyası: `assets/ui/cursors/License-Kenney.txt` |
| ZombiePack | Özel lisans: `assets/zombies/LICENSE-ZombiePack.txt`. Oyunun parçası olarak ticari kullanım ve değiştirme serbest. Asset'lerin tek başına dağıtılması, satılması ve **ham dosyaların başkalarının indirebileceği şekilde sunulması yasak**. |
| Player, Zombie, FreeEnvironment, Background, Pixel UI pack 3, PowerUps, Overlay, Menu, Logo, Audio | Zip'te lisans dosyası yok. Lisansı ve gerekli atıfı, paketleri indirdiğiniz yerden kontrol edin. |

> **Dikkat:** Bu depo herkese açıksa, `assets/` içindeki ham dosyalar (ZombiePack dahil) herkes tarafından indirilebilir. Bu, ZombiePack lisansındaki "ham dosyaları indirilebilir şekilde sunma" yasağıyla çelişebilir. Depoyu gizli tutmanızı ya da paketin sahibine danışmanızı öneririm.

Oyun kodu (`index.html`) bu projeye aittir.

## Teknik notlar

- Zemin 500x500'lük parçalar halinde, düşük çözünürlükte bir kez üretiliyor ve pikselli büyütülerek çiziliyor. Ekranın dışında kalan nesneler çizilmiyor.
- Nesneler ve karakterler ayak noktalarına göre sıralanıyor (2.5D). Çarpışma ayaklarda, mermi isabeti gövdenin ortasında hesaplanıyor.
- Zombiler oyuncudan dışa doğru hesaplanan bir akış alanını (40 px'lik ızgarada Dijkstra) takip ederek engellerin etrafından dolaşıyor.
- `file://` ile açıldığında görseller canvas'a yalnızca çiziliyor, pikselleri okunmuyor; böylece tarayıcı güvenlik kısıtlamalarına takılmıyor.
- Otomatik testte 10 dalganın tamamı bot ile oynandı. 45 zombi aynı anda ekrandayken bir karenin güncellemesi en fazla ~2 ms, çizimi ~4 ms sürüyor.
