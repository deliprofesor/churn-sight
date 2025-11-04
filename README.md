#  TELEKOM-CHURN-OPERASYONEL-OPTİMİZASYON

**Müşteri Kaybı (CHURN) Analizi ve Haberleşme Mühendisliği Kararlarına Dönüşümü**

<img width="1012" height="567" alt="image" src="https://github.com/user-attachments/assets/9f3c92c3-b986-4338-8901-6b6595f5e690" />


---

##  Proje Özeti  
Bu proje, bir **telekomünikasyon şirketinin müşteri veri setini** kullanarak **Müşteri Kaybını (CHURN)** tahmin etme ve **kaybı en çok tetikleyen operasyonel (şebeke) ve finansal faktörleri** belirleme üzerine odaklanmıştır.  

Geleneksel tahmin modellerinin ötesine geçilerek, analiz sonuçları doğrudan **Şebeke Operasyonları** ve **Hizmet Kalitesi birimlerinin** alacağı **stratejik kararlara** dönüştürülmüştür.

---

##  Teknik Yaklaşım ve Kullanılan Metotlar

- **Sınıf Dengesizliği Yönetimi:**  
  Veri setindeki yüksek sınıf dengesizliği (CHURN oranının düşük olması) nedeniyle, modelin **kayıp yapan müşterileri bulma yeteneği (Recall)** önceliklendirilmiştir.

- **Veri Mühendisliği (Feature Engineering):**  
  Ham abone sayıları yerine aşağıdaki operasyonel risk metrikleri oluşturulmuştur:
  - `NotActive_Ratio`: Aktif Olmayan Abone Oranı  
  - `Mobile_Revenue_Share`: Mobil gelir payı  

- **Sınıf Dengeleme:**  
  `SMOTE (Synthetic Minority Over-sampling Technique)` algoritması ile veri dengelenmiştir.

- **Tahmin Modeli:**  
  Özellik önem skorlarını belirlemek için **Random Forest Classifier** algoritması kullanılmıştır.

- **Değerlendirme Metriği:**  
  İş başarısı için en kritik metrik olan **Recall (CHURN yapan müşteriyi bulma oranı)** odak noktası olmuştur.

---

##  Analiz ve Mühendislik Çıktıları

### A. Kaybı Tetikleyen En Önemli 5 Faktör (Özellik Önemi)

| Sıra | Özellik (Faktör)         | Önem Skoru | Operasyonel Çıkarım |
|------|--------------------------|-------------|----------------------|
| 1 | `ARPU` | En Yüksek | Müşteri başına gelirin düşmesi, kayıp için en güçlü sinyaldir. Finansal değer kaybı, operasyonel müdahale gerektirir. |
| 2 | `AvgMobileRevenue` | Yüksek | Kayıp kararının mobil şebeke/servis kalitesiyle ilgili olduğunu gösterir. |
| 3 | `TotalRevenue` | Yüksek | Müşterinin genel finansal değeri kritik bir faktördür. |
| 4 | `Total_SUBs` | Orta | Toplam abone sayısındaki değişimler risk göstergesidir. |
| 5 | `Active_subscribers` | Orta | Aktif abone sayısındaki düşüş, risk artışını gösterir. |

---

### B. Kritik Operasyonel Risk Analizi

| Kategori | En Riskli Tespitler | Mühendislik Aksiyonu |
|-----------|--------------------|-----------------------|
| **Segment Riskleri** | `SME`, `Platinum`, `Gold` | **Yüksek Değer Odaklı Müdahale:** En değerli segmentlere yönelik şebeke önceliklendirmesi (QoS) uygulanmalıdır. |
| **Coğrafi Riskler (Top ZIP’ler)** | `6673.0`, `7800.0` (100% CHURN) | **Kritik Şebeke İncelemesi:** Bu bölgelerde kapasite, sinyal gücü ve arıza kayıtları incelenmelidir. |
| **Hizmet Kalitesi** | Yüksek `NotActive_Ratio` | **Proaktif Kalite Kontrolü:** Müşteri hizmeti kullanmayı bırakmadan önce kalite analizi yapılmalıdır. |

---

## 📁 Proje Yapısı

