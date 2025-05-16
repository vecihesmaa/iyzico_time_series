# 📊 Iyzico İşlem Hacmi Tahmini Projesi

Bu proje, Iyzico adlı finansal teknoloji şirketinin e-ticaret iş yerleri için günlük işlem hacmini tahmin etmeye yönelik zaman serisi tahmin modelini kapsamaktadır. Projede LightGBM modeli ile geçmiş işlem verileri kullanılarak ileriye dönük tahminler yapılmaktadır.

---

## 🧠 Problem Tanımı

Iyzico, e-ticaret siteleri ve bireysel kullanıcılar için ödeme altyapısı sunan bir finansal teknoloji şirketidir. Bu projede, **2020 yılının son 3 ayı** için her bir `merchant_id`'ye özel **günlük toplam işlem hacminin tahmin edilmesi** amaçlanmaktadır.

---

## 📁 Veri Seti

Veri seti 2018-2020 yılları arasını kapsamaktadır. 5 değişken ve 7667 gözlem içerir:

- `transaction_date`: Satış tarihi
- `merchant_id`: Üye iş yeri ID’si
- `Total_Transaction`: Günlük işlem sayısı
- `Total_Paid`: Toplam ödeme miktarı
- `Category`: İş yeri kategorisi

---

## 🚀 Proje Akışı

### Görev 1: 📌 Veri Keşfi (EDA)

- Veri tipi dönüşümleri (`transaction_date`)
- Başlangıç ve bitiş tarihleri
- Kategorisel dağılımlar
- İşlem ve ödeme istatistikleri
- Zaman bazlı işlem trendlerinin görselleştirilmesi

### Görev 2: 🧱 Özellik Mühendisliği (Feature Engineering)

- **Tarihsel özellikler:** Ay, hafta, çeyrek, tatil kontrolü
- **Lag/shift özellikleri:** Önceki günlerin işlem sayıları
- **Hareketli ortalama (Rolling Mean):** Geçmiş pencerelerdeki işlem trendleri
- **Exponentially Weighted Mean:** Daha yakın geçmişe ağırlık verilerek ortalama hesaplama
- **Özel gün etkileri:** Black Friday, yaz gündönümü
- **One-Hot Encoding**: Kategorik değişkenlerin sayısallaştırılması

### Görev 3: ⚙️ Modelleme

- Veri seti zaman bazlı olarak `train` ve `validation` olarak ayrılmıştır.
- **Özel başarı metriği olarak SMAPE** tanımlanmıştır.
- LightGBM kullanılarak model eğitilmiş, erken durdurma (early stopping) uygulanmıştır.

### Görev 4: 📈 Değerlendirme

- SMAPE skoru ile değerlendirme yapılmıştır.
- Öznitelik önem düzeyleri görselleştirilmiştir.

---

## 📦 Kullanılan Teknolojiler

- Python
- Pandas, NumPy
- Matplotlib, Seaborn
- LightGBM
- Scikit-learn
- Jupyter Notebook

---

## 🧪 Değerlendirme Metriği

**SMAPE (Symmetric Mean Absolute Percentage Error)**  
Bu metrik, öngörülen ve gerçek değerler arasındaki orantılı hatayı ölçer. Aşağıdaki şekilde hesaplanır:

```python
SMAPE = 200 * |y_pred - y_true| / (|y_pred| + |y_true|)
