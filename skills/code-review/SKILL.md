---
name: code-review
description: Kod değişikliklerini bug, güvenlik açığı, okunabilirlik, performans ve takım standartlarına göre inceler. PR yorumu yazarken, kod kalitesini yükseltmek istediğinde veya refactor sırasında kullan. Objektif, yapıcı ve açıklayıcı yorumlar üretir.
---

# Code Review Skill

Bu skill aktif olduğunda, kod parçalarını / diff'leri / dosyaları şu prensiplerle değerlendir:

## 1. Temel İnceleme Sırası (her zaman bu sırayı takip et)

1. **Doğruluk / Correctness**  
   - Kod gerçekten istenen işi yapıyor mu?  
   - Beklenen input → output eşleşiyor mu?  
   - Logic hataları, off-by-one, yanlış koşullar var mı?

2. **Güvenlik (Security)**  
   - SQL injection, XSS, command injection riski?  
   - Hard-coded secret, API key vs. var mı?  
   - Kullanıcı girdisi yeterince sanitize ediliyor mu?  
   - Yetkilendirme / authentication kontrolleri eksik mi?

3. **Edge Case & Hata Yönetimi**  
   - Null / undefined / empty değerler nasıl ele alınıyor?  
   - Hata durumları (exceptions, error responses) yakalanıyor mu?  
   - Timeout, network failure, rate-limit gibi durumlar düşünülmüş mü?

4. **Okunabilirlik & Bakım Kolaylığı (Readability & Maintainability)**  
   - Değişken / fonksiyon isimleri anlamlı ve tutarlı mı?  
   - Kod "self-documenting" mi, yoksa yorum eksik mi?  
   - Çok uzun fonksiyon / metod var mı? (→ extract öner)  
   - Magic number / string yerine constant kullanılmış mı?

5. **Performans & Verimlilik**  
   - Gereksiz döngü / tekrar eden işlem var mı?  
   - O(n²) yerine O(n log n) veya daha iyi alternatif mümkün mü?  
   - Gereksiz bellek kullanımı / kopyalama var mı?

6. **Stil & Konvansiyonlar**  
   - Proje dilinin style guide'ına uyuyor mu? (ör. black, prettier, google-java-format)  
   - Import'lar düzenli mi, kullanılmayan import temizlenmiş mi?  
   - Tip hint / annotation eksik mi? (özellikle Python, TypeScript)

7. **Test Edilebilirlik**  
   - Fonksiyonlar pure mı, yoksa çok fazla side-effect mi var?  
   - Kolayca unit test yazılabilir mi?

## 2. Yorum Yazma Tarzı

- Her yoruma **konum belirt** (dosya yolu + satır no aralığı)
- **Sorun → Neden kötü → Öneri** formatını kullan
  Örnek:  
  `main.py:42-45`  
  `Burada user_input doğrudan concat ediliyor → SQL injection riski taşıyor.`  
  `Öneri: parameterized query kullanın veya input’u escaping fonksiyonundan geçirin:`

- Olumlu yönleri de belirt (sandwich feedback): iyi olanı önce söyle, sonra iyileştirme öner, sonra tekrar olumlu bitir
- Alternatif çözüm önerirken kısa kod parçası verebilirsin
- "Bence", "bana göre" yerine objektif konuş: "Bu potansiyel bir race condition yaratabilir çünkü..."

## 3. Ekstra Tavsiyeler

- Büyük refactor öneriyorsan, önce küçük adımlarla ilerlemeyi tavsiye et
- Eğer kod çok kötüyse önce "high-level summary" ver, sonra detaya gir
- Proje-spesifik kurallar varsa (örneğin "her public method’a docstring zorunlu"), onları da hatırla

Bu skill tetiklendiğinde yukarıdaki checklist'i sistematik olarak uygula ve mümkün olduğunca yapılandırılmış, okunabilir yorumlar üret.