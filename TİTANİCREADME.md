# Titanic Veri Ön İşleme Ödevi

Bu repo, derste işlediğimiz `5.ipynb` uygulama notundaki veri ön işleme (data preprocessing) adımlarını Kaggle'daki **Titanic - Machine Learning from Disaster** yarışmasının `train.csv` ve `test.csv` veri setlerine uyarlamak için hazırladığım ödev çalışmasını içeriyor[cite: 1, 2]. 

Dersteki akışa sadık kalarak sadece veri analizi, eksik verilerin doldurulması, yeni özellik türetme (Feature Engineering) ve korelasyon incelemesi yaptım[cite: 1, 2]. Dersteki örnekte herhangi bir makine öğrenmesi modeli eğitilmediği için bu çalışmada da model kurulumu yer almıyor, sadece veriyi modele hazır hale getirip kaydettim[cite: 1, 2].

## Çalışmada Neler Yaptım?

1. **Veri İnceleme ve Görselleştirme:** Eğitim (891 satır, 12 sütun) ve test (418 satır, 11 sütun) verilerini yükleyip eksik değerleri kontrol ettim[cite: 1, 2]. Hayatta kalma durumunun cinsiyet ve yolcu sınıfına (`Pclass`) göre dağılımlarını grafiklerle inceledim[cite: 1, 2].
2. **Eksik Verileri Doldurma:** Veri sızıntısı (data leakage) olmaması için doldurma değerlerini sadece eğitim verisinden hesapladım:
   * `Age` (Yaş) sütunundaki boşlukları eğitim verisinin medyanı (**28**) ile doldurdum[cite: 1, 2].
   * `Embarked` (Biniş limanı) kısmındaki eksikleri en çok tekrar eden değer olan **S** (mod) ile tamamladım[cite: 1, 2].
   * Test verisinde ekstra olarak `Fare` (Bilet ücreti) sütununda 1 tane eksik değer çıktı, onu da yine eğitim verisinin medyanı (**14.4542**) ile doldurdum[cite: 1, 2].
3. **Özellik Türetme ve Dönüşüm:** 
   * `SibSp` ve `Parch` sütunlarını toplayıp kişiyi de ekleyerek (`SibSp + Parch + 1`) **`FamilySize`** (Aile Büyüklüğü) adında yeni bir sütun oluşturdum[cite: 1, 2]. Sonrasında eski iki sütunu ve modele etkisi olmayacak `Name`, `Ticket`, `Cabin`, `PassengerId` sütunlarını tablodan çıkardım.
   * Kategorik olan `Sex` ve `Embarked` sütunlarını `get_dummies` kullanarak **One-Hot Encoding** yöntemiyle sayısal hale getirdim[cite: 1, 2].
4. **Korelasyon ve Çıktı Alma:** Son adımda sayısal değişkenlerin `Survived` ile olan ilişkisini görmek için korelasyon matrisi (heatmap) çizdirdim ve temizlenmiş tabloları CSV olarak dışa aktardım[cite: 1, 2].

## Elde Ettiğim Özet Sonuçlar

* Ön işleme adımlarından sonra hem eğitim hem de test setinde **9 adet özellik (feature)** kaldı ve hiç eksik veri kalmadı (`(891, 9)` ve `(418, 9)`)[cite: 1, 2].
* Eğitim verisine göre genel hayatta kalma oranı **%38.4**[cite: 1, 2]. 
* Kadınların hayatta kalma oranı (**%74.2**), erkeklere (**%18.9**) göre oldukça yüksek. Aynı şekilde 1. sınıf yolcuların kurtulma oranı (**%63.0**), 3. sınıfa (**%24.2**) göre çok daha fazla[cite: 1].

## Colab'da Çalıştırma Adımları

1. `titanic_colab_on_isleme.ipynb` dosyasını Google Colab üzerinden açın[cite: 2].
2. Üst menüden **Çalışma Zamanı -> Tümünü çalıştır** seçeneğine tıklayın[cite: 2].
3. İlk kod hücresi çalıştığında eğer dosyalar yüklü değilse sizden `train.csv` ve `test.csv` dosyalarını seçmenizi isteyecektir[cite: 1, 2]. Kaggle'dan indirdiğiniz dosyaları buradan yükleyebilirsiniz (`gender_submission.csv` dosyasına gerek yoktur)[cite: 1, 2].
4. Tüm hücreler çalıştığında temizlenmiş veriler `X_train_preprocessed.csv`, `y_train.csv` ve `X_test_preprocessed.csv` isimleriyle kaydedilir[cite: 1, 2]. Sol taraftaki dosya menüsünden bilgisayarınıza indirebilirsiniz[cite: 1, 2].
