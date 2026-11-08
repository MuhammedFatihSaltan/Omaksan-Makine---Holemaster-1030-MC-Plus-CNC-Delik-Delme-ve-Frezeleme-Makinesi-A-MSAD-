# Holemaster 1030 MC Plus — Siber Güvenlik ve Fonksiyonel Emniyet Çalışması

> Inspecco × Kriptarium **Safety 4.0 Bootcamp** kapsamında, **Omaksan Makine Holemaster 1030 MC Plus** CNC delik delme ve frezeleme makinesi üzerinde hazırladığım yedi laboratuvar çalışması.

**Hazırlayan:** Muhammed Fatih Saltan
**Tarih:** 22.10.2026

---

## Projenin amacı

Bir CNC makinede siber güvenlik, yalnızca verinin korunması demek değildir. Bir saldırı zinciri en sonunda makinenin başındaki insanı etkileyebilir. Bu çalışmada tek bir makineyi baştan sona ele alarak şu soruya cevap aradım:

**Bir siber saldırı, bu makinede çalışan kişinin güvenliğini nasıl tehlikeye atabilir ve bunu nasıl önleriz?**

Yedi laboratuvarın hepsinde aynı makineyi kullandım. Böylece emniyet mimarisinden olay müdahalesine ve yapay zekâya kadar tüm konuları aynı örnek üzerinde birbirine bağlayabildim.

## Makine hakkında

Holemaster 1030 MC Plus, delik delme ve kanal açma işlemini frezeleme yeteneğiyle birleştiren bir CNC makinedir. Çalışmada ele aldığım başlıca tehlike kaynakları:

- Dönen iş mili ve delme kafaları
- Hareketli eksenler (portal/gantri)
- Pnömatik kıskaç ve bastırma elemanları

Bu tehlikelerden zarar görebilecek kişiler operatör ve bakım personelidir.

## Laboratuvar çalışmaları

### Lab 1 · Safety Architecture
Makinenin normal kontrol yolunu (CNC kontrolcü, sürücü, iş mili) ve ayrı bir safety yolunu (E-stop → Safety PLC → STO) birbirinden ayırdım. Emniyet fonksiyonlarının hangi dijital bileşenlere bağlı olduğunu çıkardım ve bir saldırganın bu fonksiyonu hangi noktalardan bozabileceğini belirledim.
**Çıktı:** Safety Function Map

### Lab 2 · IEC 62443 Mini Workshop
Makine çevresindeki varlıkları bölgelere ayırdım: Safety, Makine kontrol, Hazırlık, Kurumsal ve DMZ. Bölgeler arası geçişleri (conduit) ve her geçişte uygulanacak kontrolleri tanımladım. Uzak erişim için jump server, VPN, MFA, kişisel hesap, tam oturum kaydı ve varsayılan kapalı yaklaşımını seçtim.
**Çıktı:** Zone / Conduit Diagram

### Lab 3 · Threat & Risk + Risk Matrix
Üç saldırı senaryosu kurdum ve **L × S × E** yöntemiyle puanladım. Önemli kural: şiddeti 3 olan (ağır yaralanma) senaryo, skoru düşük olsa bile listede öne alınır. Böylece insana zarar verme ihtimali gözden kaçmaz.
**Çıktı:** Risk Register

### Lab 4 · Secure Remote Access
Mevcut (varsayılan) uzak erişim durumunu hedef mimariyle karşılaştırdım. Erişim güvenliğinin yanında, saldırgan içeri girse bile emniyet fonksiyonlarının çalışmaya devam etmesi için gereksinimleri yazdım. Burada çözüm değil, gereksinim tanımlamaya odaklandım.
**Çıktı:** Secure Architecture

### Lab 5 · SBOM / CVE / Patch
Bir CVE'nin makineyi gerçekten etkileyip etkilemediğini üç şartla değerlendirdim: bileşen var mı, sürüm etkileniyor mu, açık ulaşılabilir mi. Yama öncesi test, safety validation etkisi ve yama mümkün değilse telafi edici önlemler konusunda karar akışı oluşturdum.
**Çıktı:** Vulnerability Decision

### Lab 6 · CRA Incident Simulation
Servis hesabında yetkisiz erişim tespit edilen bir senaryoda, ilk 15 dakikadan 14 günlük son rapora kadar olay müdahale akışını çıkardım. CRA'nın 24 saat / 72 saat / 14 gün yükümlülüklerini iyi bir müdahalenin doğal kilometre taşları olarak ele aldım. Çalışmanın ana mesajı: önce emniyet, hemen sonra kanıt; "resetleyip devam edelim" demeden önce kanıtı korumak gerekir.
**Çıktı:** Incident Workflow

### Lab 7 · AI Safety Challenge
Makineye isteğe bağlı bir kamera/YZ modülü eklendiği varsayımıyla üç başarısızlık durumunu inceledim: yanlış sınıflandırma, manipüle edilmiş girdi ve düşük güven. Temel ilke **Prediction ≠ Safety**: yapay zekâ karar üretir, güvenliği garanti eden mimari ise YZ'nin dışında tanımlanır.
**Çıktı:** AI Fail-Safe Decision

## Çalışmadan çıkardığım sonuçlar

1. **Emniyet fonksiyonu kontrol sisteminden bağımsız olmalı.** E-stop, kapı kilidi ve STO donanım devresi olarak çalışmalı; uzak bir oturum bunları devre dışı bırakamamalı.
2. **Erişim güvenliği tek başına yetmez.** Savunma iki katmandır: girişi zorlaştırmak ve girilse bile insanı korumak.
3. **Risk skoru her şeyi anlatmaz.** Ağır yaralanma ihtimali olan senaryo, puanı düşük olsa da görünür kalmalıdır.
4. **Yüksek CVSS puanı otomatik olarak üretimi durdurmak anlamına gelmez.** Karar bağlama göre verilir; önce ulaşılabilirlik kapatılır.
5. **Olayda zaman ve kanıt en değerli iki şeydir.** Kanıt korunmadan yapılan reset, olayın incelenmesini imkânsız hale getirir.
6. **Yapay zekâ çıktısı öneridir.** Makine hareketini doğrudan sürmemeli, insan onayı ve sabit sınırlar YZ'nin dışında çalışmalıdır.

## Kullanılan kavramlar

`Fonksiyonel emniyet` · `Safety PLC` · `STO` · `PLr / SIL` · `IEC 62443` · `Zone / Conduit` · `Risk matrisi` · `Jump server` · `VPN` · `MFA` · `SBOM` · `CVE / CVSS` · `Compensating control` · `CRA` · `Olay müdahalesi` · `Fail-safe` · `Human override`

---

*Safety 4.0 Bootcamp · Inspecco × Kriptarium*
