# 🧠 Yapay Zeka Eğitim Veri Seti Yönetim Sistemi

## 🎯 Proje Amacı
Bu proje, yapay zeka araştırmacılarının veya öğrencilerin veri setlerini yükleyip yönetebileceği, makine öğrenmesi modelleri eğitebileceği ve sonuçları görüntüleyebileceği bir platform oluşturmayı amaçlar.  
Sistem hem **kullanıcılar** hem de **yöneticiler (admin)** için farklı yetkilendirmelere sahip olacak şekilde tasarlanmıştır.

---

## 👤 Kullanıcı Gereksinimleri

### 🔹 Genel Kullanıcı Gereksinimleri
- **Kayıt ve Giriş İşlemleri:** Kullanıcılar e-posta, şifre ve ad-soyad bilgileriyle sisteme kayıt olup giriş yapabilir.  
- **Profil Güncelleme:** Kullanıcılar e-posta ve şifre gibi profil bilgilerini güncelleyebilir.  
- **Veri Seti Arama ve Filtreleme:** Veri setlerini isme, kategoriye veya etikete göre arayabilir ve filtreleyebilir.  
- **Veri Seti Yükleme:** Yeni veri setleri (başlık, açıklama, kategori, boyut) ekleyebilir.  
- **Yorum Yapma:** Veri setlerine yorum ekleyebilir ve yorumları görüntüleyebilir.  
- **Eğitim Başlatma:** Seçtikleri veri setleriyle yeni bir makine öğrenmesi eğitimi başlatabilir.  
- **Eğitim Takibi:** Eğitim durumlarını (Başladı, Tamamlandı, Hata) takip edebilir.  
- **Sonuç Görüntüleme:** Tamamlanan eğitimlerin doğruluk oranı, kayıp oranı ve model versiyonlarını görüntüleyebilir.  

---

## 🛠️ Yönetici (Admin) Gereksinimleri
- **Veri Seti Yönetimi:** Kullanıcıların yüklediği veri setlerini görüntüleyebilir, düzenleyebilir veya silebilir.  
- **Kategori Yönetimi:** Yeni kategoriler ekleyebilir, mevcutları güncelleyip silebilir.  
- **Etiket Yönetimi:** Veri setlerine eklenen etiketleri yönetebilir (birleştirme, düzeltme vb.).  
- **Kullanıcı Yönetimi:** Tüm kullanıcıları listeleyebilir, rollerini (User / Admin) değiştirebilir.  
- **Yorum Yönetimi:** Uygunsuz yorumları inceleyip silebilir.  
- **Eğitim Gözetimi:** Eğitim süreçlerini izleyebilir ve gerektiğinde müdahale edebilir.  

---

## 🏷️ Varlıklar ve Nitelikleri

### 1️⃣ Kullanıcılar (Users)
| Alan Adı | Açıklama |
|-----------|-----------|
| KullaniciID (PK) | Benzersiz kullanıcı kimliği |
| AdSoyad | Kullanıcının adı-soyadı |
| Eposta | Kullanıcının e-posta adresi |
| Sifre | Şifre (hash’lenmiş) |
| Rol | Kullanıcı türü (User / Admin) |
| KayitTarihi | Kayıt tarihi |

---

### 2️⃣ Kategoriler (Categories)
| Alan Adı | Açıklama |
|-----------|-----------|
| KategoriID (PK) | Benzersiz kategori kimliği |
| KategoriAdi | Kategorinin adı |
| Aciklama | Kategori açıklaması |

---

### 3️⃣ Veri Setleri (Datasets)
| Alan Adı | Açıklama |
|-----------|-----------|
| VeriSetID (PK) | Benzersiz veri seti kimliği |
| VeriSetAdi | Veri setinin başlığı |
| Aciklama | Veri seti açıklaması |
| OlusturanID (FK → Kullanıcılar) | Veri setini yükleyen kullanıcı |
| KategoriID (FK → Kategoriler) | Veri setinin ait olduğu kategori |
| YuklemeTarihi | Yükleme tarihi |
| VeriBoyutuMB | Veri seti boyutu (MB) |

---

### 4️⃣ Etiketler (Tags)
| Alan Adı | Açıklama |
|-----------|-----------|
| EtiketID (PK) | Etiket kimliği |
| EtiketAdi | Etiketin adı |
| VeriSetID (FK → VeriSetleri) | Ait olduğu veri seti |

> **Not:** Eğer bir etiket birden fazla veri setinde kullanılacaksa “VeriSet_Etiket” ara tablosu eklenebilir.

---

### 5️⃣ Eğitimler (Trainings)
| Alan Adı | Açıklama |
|-----------|-----------|
| EgitimID (PK) | Eğitim kimliği |
| ModelAdi | Modelin adı |
| VeriSetID (FK → VeriSetleri) | Kullanılan veri seti |
| EgitimiYapanID (FK → Kullanıcılar) | Eğitimi başlatan kullanıcı |
| BaslangicTarihi | Başlangıç tarihi |
| BitisTarihi | Bitiş tarihi |
| Durum | Eğitim durumu (Başladı, Tamamlandı, Hata) |

---

### 6️⃣ Model Versiyonları (ModelVersions)
| Alan Adı | Açıklama |
|-----------|-----------|
| VersiyonID (PK) | Model versiyonu kimliği |
| EgitimID (FK → Eğitimler) | Ait olduğu eğitim |
| VersiyonAdi | Versiyon adı |
| ParametreSayisi | Modeldeki parametre sayısı |
| KayitTarihi | Versiyon kaydedilme tarihi |

---

### 7️⃣ Sonuçlar (Results)
| Alan Adı | Açıklama |
|-----------|-----------|
| SonucID (PK) | Sonuç kimliği |
| EgitimID (FK → Eğitimler) | İlgili eğitim süreci |
| DogrulukOrani | Accuracy oranı |
| KayipOrani | Loss oranı |
| TestVeriBoyutu | Test veri sayısı |
| RaporTarihi | Rapor tarihi |

---

### 8️⃣ Yorumlar (Comments)
| Alan Adı | Açıklama |
|-----------|-----------|
| YorumID (PK) | Yorum kimliği |
| KullaniciID (FK → Kullanıcılar) | Yorumu yapan kullanıcı |
| VeriSetID (FK → VeriSetleri) | Yorum yapılan veri seti |
| YorumMetni | Yorum içeriği |
| Tarih | Yorum tarihi |

---

## 🔗 İlişkiler

| İlişki | Türü |
|--------|------|
| Kullanıcılar ↔ VeriSetleri | 1 - n |
| Kategoriler ↔ VeriSetleri | 1 - n |
| VeriSetleri ↔ Etiketler | 1 - n |
| VeriSetleri ↔ Eğitimler | 1 - n |
| Eğitimler ↔ ModelVersiyonları | 1 - n |
| Eğitimler ↔ Sonuçlar | 1 - 1 |
| VeriSetleri ↔ Yorumlar | 1 - n |

---

## ⚙️ Ek Notlar
- Tablolar arası bütünlük **Foreign Key** yapısıyla korunmuştur.  
- Her varlık, sistemdeki farklı rollerin görevlerini destekleyecek şekilde tasarlanmıştır.  
- İleride **model indirme**, **paylaşım** ve **API erişimi** gibi özelliklerle genişletilebilir.  
