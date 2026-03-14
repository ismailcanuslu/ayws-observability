# 👁️ AYWS Observability Service

**AYWS altyapısı** için özel olarak geliştirilmiş, sistemin kalbini dinleyen ve tüm bileşenlerin (Proxmox node'ları, Docker konteynerleri, servisler) sağlık durumunu anlık olarak izleyen merkezi **gözlem (observability)** ve **telemetri** servisidir.

Bu sistem, dağıtık mimaride çalışan altyapınızın ürettiği devasa metrik ve log verilerini tek bir merkezde toplar, analiz eder ve görselleştirir. Olası darboğazları (bottleneck) ve hataları sistem çökmeden önce tespit etmenizi sağlayarak %100 görünürlük (visibility) sunar. 📈🔍

---

## ⚡ Sistem Neler Yapabiliyor?

Bu servis, altyapıdaki kör noktaları ortadan kaldırarak aşağıdaki işlemleri otomatik ve sürekli olarak gerçekleştirir:

### 📊 Merkezi Metrik Toplama (Metrics Collection)
Sistemin donanımsal ve yazılımsal nefes alışverişini saniyesi saniyesine takip eder.
* **Fiziksel & Sanal Kaynaklar:** Proxmox host'larının ve Sanal Makinelerin (VM) CPU, RAM, Disk I/O ve ağ bant genişliği kullanımlarını anlık olarak ölçümler.
* **Konteyner Düzeyinde İzleme:** Docker üzerinde koşan her bir uygulamanın (mikroservisin) ayrı ayrı kaynak tüketimini raporlar.
* **Uygulama Telemetrisi:** Diğer AYWS servislerinin (Örn: Compute Service) ürettiği API yanıt süreleri (latency) ve işlem hacimleri gibi özel metrikleri toplar.

### 📝 Bütünleşik Log Yönetimi (Log Aggregation)
Dağıtık sistemlerdeki log karmaşasına son verir, hata takibini kolaylaştırır.
* **Merkezi Log Havuzu:** Farklı sunucu ve konteynerlere dağılmış tüm standart çıktıları (stdout/stderr) ve log dosyalarını tek bir merkezde (stream halinde) indeksler.
* **Hızlı Arama ve Filtreleme:** Milyonlarca log satırı arasında anomali, hata (Error/Fatal) veya spesifik IP/kullanıcı araması yapılmasına olanak tanır.
* **Bağlamsal İz Sürme:** Mikroservisler arası isteklerin (request) rotasını takip ederek yavaşlıkların veya çökmelerin kök nedenini (root cause) nokta atışı bulur.

### 🚨 Dinamik Uyarı ve Alarm (Alerting) Mekanizması
Sorunlardan kullanıcıdan önce haberdar olmanızı ve proaktif davranmanızı sağlar.
* **Kural Tabanlı Tetikleyiciler:** "CPU kullanımı %90'ı geçerse", "API 500 hatası verirse" veya "Kritik bir konteyner durursa" gibi senaryolara özel eşik değerleri (threshold) tanımlanır.
* **Çoklu Kanal Bildirimleri:** Eşik değerleri aşıldığında anında Webhook'lar üzerinden diğer sistemleri veya haberleşme kanallarını (Slack, Discord, Telegram vb.) uyarır.
* **Self-Healing (Otokontrol) Altyapısı:** Alarm durumlarında diğer AYWS servislerine (Örn: Compute Service) komut göndererek arızalı birimin yeniden başlatılması gibi otomatik kurtarma süreçlerini tetikleyebilir.

### 🔌 API Entegrasyonu ve Veri Sunumu
Sadece pasif bir izleme ekranı değil, aynı zamanda veriyi diğer servislerle paylaşan aktif bir entegrasyon noktasıdır.
* **RESTful Telemetri Uç Noktaları:** Toplanan sağlık ve performans verilerini, AYWS ekosistemindeki diğer yönetim servislerinin kararlar (örn: yük dengeleme) alabilmesi için standart JSON/HTTP formatında dışarı açar.
* **Geçmişe Dönük Analiz:** Tarihsel verileri güvenle saklayarak gelecek kapasite planlaması ve kaynak optimizasyonu yapılmasına veri tabanı sağlar.

---

## 🛠️ Temel Teknolojiler

Bu yüksek performanslı gözlem altyapısının arkasındaki güçler:
* 🔭 **Metrik Motoru:** Prometheus / VictoriaMetrics (Zaman serisi veri tabanı ve scraping).
* 📈 **Görselleştirme:** Grafana (Dinamik dashboardlar ve anlık izleme panelleri).
* 📝 **Log ve Trace:** Loki / ELK Stack (Logların hafif ve verimli indekslenmesi).
* 🌐 **İletişim Katmanı:** REST API & Webhooks (Servisler arası alarm ve veri transferi).
* 🐳 **Altyapı:** Docker (Tüm monitoring stack'inin izole konteynerler halinde çalıştırılması).

---
