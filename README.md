# Zombi Dalgası

Tarayıcıda çalışan, kuş bakışı 2D bir zombi hayatta kalma oyunu. Tamamı tek bir `index.html` dosyasında (HTML + CSS + JavaScript, Canvas API). Kurulum yok, dış kütüphane ya da hazır resim yok. Bütün grafikler kodla çiziliyor.

## Nasıl çalıştırılır?

`index.html` dosyasına çift tıklayın, oyun tarayıcıda açılır. İnternet bağlantısı gerekmez.

Telefonda oynamak için dosyayı herhangi bir statik sunucuya (ör. GitHub Pages) koyup telefon tarayıcısından açabilirsiniz. Dokunmatik cihaz otomatik algılanır.

## Kontroller

| | Bilgisayar | Telefon / Tablet |
|---|---|---|
| Hareket | `W A S D` veya ok tuşları | Sol alttaki joystick (ekranın sol yarısında herhangi bir yere dokunun) |
| Nişan | Mouse | Sağ alttaki joystick |
| Ateş | Sol tık (basılı tutunca sürekli ateş) | Sağ joystick'i çekince otomatik ateş |
| Duraklat | `ESC` veya `P` | Sağ üstteki **II** butonu |
| Özellik seçimi | Kartlara tıklama veya `1` `2` `3` tuşları | Karta dokunma |

## Oyun

- Amaç **10 dalga** boyunca hayatta kalmak. Zombiler harita kenarlarından, ekran dışından gelir ve engellerin etrafından dolaşarak size doğru yürür.
- Oyunun başında ve her dalganın sonunda **3 rastgele özellik kartı** çıkar. Kartlar Sıradan (gri), Nadir (mavi) ve Efsanevi (altın) olabilir. Aynı özellik birden çok kez alınabilir ve etkisi üst üste biner.
- Zombi türleri:
  - **Normal:** orta hız, orta can.
  - **Koşucu:** hızlı ama az canlı. 4. dalgadan itibaren çıkar.
  - **Tank:** yavaş, büyük, çok canlı. 6. dalgadan itibaren çıkar.
  - **Dev Zombi (Boss):** 10. dalgada gelir. Ekranın üstünde kendi can barı var. Ara ara kırmızı bir uyarı alanı gösterip o yöne hızla atılır; kırmızı alandan çekilin. Canı yarıya inince öfkelenir.
- Ağaçlar, kayalar ve çitler hem sizi hem zombileri hem de mermileri durdurur. Çalılar, çiçekler ve tabelalar sadece süs. Bir ağacın altına girince tepesi yarı saydam olur.
- Bir dalgada son 5 zombi kaldığında, ekran dışındakiler kenardaki kırmızı oklarla gösterilir.
- En yüksek skor tarayıcıda saklanır.

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

## Dengeyi değiştirmek

Bütün denge değerleri `index.html` içindeki `<script>` bloğunun başında, **`CONFIG`** objesinde duruyor:

- `CONFIG.player`: can (100), hız, atış hızı (3/sn), mermi hasarı (10), ölümsüzlük süresi (0,5 sn) vb.
- `CONFIG.zombies`: her zombi türünün canı, hızı, boyutu, hasarı, puanı; boss'un atılma ayarları.
- `CONFIG.waves`: dalga başına zombi sayıları (`counts`: 10 → 62), dalga başına can/hız artışı, doğma aralıkları, koşucu ve tankların hangi dalgadan itibaren çıkacağı.
- `CONFIG.upgrades.rarityWeights`: kartların nadirlik olasılıkları.
- `CONFIG.world`: harita boyutu (3000x3000), engel sayıları, ortadaki açık alanın yarıçapı.
- `CONFIG.camera`: yakınlaştırma ve kamera takip yumuşaklığı.

Özelliklerin seviye üst sınırları ve etkileri `UPGRADES` listesinde tanımlı.

## Teknik notlar

- Zemin 500x500'lük parçalar halinde önceden çiziliyor ve önbellekte tutuluyor. Ekranın dışında kalan nesneler çizilmiyor.
- Zombiler oyuncudan dışa doğru hesaplanan bir akış alanını (40 px'lik ızgarada Dijkstra) takip ederek engellerin etrafından dolaşıyor. Birbirlerinin içine girmemeleri ve mermi çarpışmaları için uzamsal ızgara kullanılıyor.
- Otomatik testte 10 dalganın tamamı bot ile oynandı. 45 zombi aynı anda ekrandayken bile bir oyun karesinin güncellemesi yaklaşık 1 ms sürüyor.
