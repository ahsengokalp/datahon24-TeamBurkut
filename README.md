# datahon24-TeamBurkut
Datahon24 - Degerlendirme Puani Tahmini
Bu depo, Datahon24 yarışmasına katılımımız için hazırlanan kodları içermektedir. Projenin amacı, verilen veri setine dayanarak bireylerin Degerlendirme Puani (Değerlendirme Puanı) tahminini yapmaktır.

Proje Yapısı
train.csv: 65.125 satır ve 44 sütundan oluşan eğitim veri seti.
test_x.csv: Degerlendirme Puani tahminlerinin yapılacağı test veri seti.
submission.csv: Tahmin sonuçlarını içeren ve yarışmaya gönderilen dosya.
Bağımlılıklar
Projeyi çalıştırmak için aşağıdaki kütüphanelerin yüklenmesi gerekmektedir:

pip install numpy pandas matplotlib seaborn scikit-learn

Veri Ön İşleme
Eksik Veri Yönetimi:

%50'den fazla eksik veriye sahip sütunlar çıkarıldı.
Daha az eksik veriye sahip sütunlar için ortalama veya mod kullanılarak eksik veriler dolduruldu.
Metin verileri küçük harfe dönüştürüldü.

Tarih Formatlama:
Dogum Tarihi (Doğum Tarihi) sütunundan yalnızca yıl bilgisi çıkartılarak standart hale getirildi.

Kategorik Değişkenler:
Kategorik veriler, benzersiz değerleri sayısal değerlere eşleştirilerek kodlandı.

Özellik Mühendisliği
Dogum Yeri (Doğum Yeri) ve Ikametgah Sehri (İkamet Şehri) gibi sütunlar, analizde daha az önemli olduğu düşünülerek veri setinden çıkarıldı.
Basvuru Yili (Başvuru Yılı) sütununda eksik değerler ortalama ile dolduruldu, çünkü bu sütunda uç değer bulunmamaktaydı.

Model Eğitimi
Tahmin modeli olarak scikit-learn kütüphanesinden RandomForestRegressor kullanıldı.
from sklearn.ensemble import RandomForestRegressor
model = RandomForestRegressor(random_state=42)
model.fit(X_train, y_train)

Model, doğrulama seti üzerinde Ortalama Kare Hata (MSE) ile değerlendirildi:
from sklearn.metrics import mean_squared_error
mse = mean_squared_error(y_val, y_pred)
print(f"Validation MSE: {mse}")

Nihai Tahminler
Test veri seti üzerinde aynı ön işleme adımları tekrarlandı ve tahminler üretildi:
test_predictions = model.predict(test_x)

Gönderim
Tahminler, yarışmaya gönderilmek üzere submission.csv dosyasına kaydedildi:
submission = pd.DataFrame({
    "id": test_x["id"],
    "Degerlendirme Puani": test_predictions
})
submission.to_csv("submission.csv", index=False)

Sonuç
Bu proje, eksik veri yönetimi, kategorik değişken işleme ve yapılandırılmış veri üzerinde bir makine öğrenimi modelinin eğitilmesini göstermektedir. RandomForestRegressor kullanarak değerlendirme puanlarını tahmin ettik ve doğrulama seti üzerinde 361.42 MSE değeri elde ettik.

Doğruluk Skoru olarak 19.1 değeri elde edildi

