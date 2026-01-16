---
name: prompt-enhancer
description: Kullanıcının verdiği prompt'u analiz eder, belirsizlikleri giderir, detaylandırır ve Gemini 3 / Claude / Grok gibi LLM'lerin en iyi performans göstereceği şekilde yeniden yapılandırır. "Daha iyi prompt yaz" veya "bu prompt'u optimize et" gibi taleplerde otomatik devreye girer. Çıktı: iyileştirilmiş prompt + kısa açıklama (neler değişti, neden daha iyi olur).
keywords: [prompt, optimize, enhance, improve, better prompt, prompt engineering, refine]
triggers: ["optimize et", "daha iyi yaz", "enhance", "improve prompt", "prompt'ümü düzelt", "daha etkili yap"]
priority: high
---

# Prompt Enhancer Skill

Bu skill aktif olduğunda, kullanıcıdan gelen **herhangi bir prompt'u** (ya da "şu prompt'u iyileştir" gibi bir isteği) şu adımlarla sistematik olarak geliştir:

## 1. Analiz Aşaması (Step-by-Step Reasoning)

1. **Görev Tipini Belirle**  
   - Kod yazma / refactor / debug  
   - SQL / performans optimizasyonu  
   - Mimari tasarım / pattern  
   - Test yazma  
   - Dokümantasyon / açıklama  
   - Genel sohbet / araştırma  
   - Başka bir LLM'ye prompt hazırlama (meta-prompt)

2. **Belirsizlikleri Tespit Et**  
   - Hangi dil / framework? (.NET 8, ASP.NET Core, Dapper, EF Core, Redis vs.)  
   - Hedef: performans, okunabilirlik, güvenlik, test edilebilirlik?  
   - Input/output örnekleri var mı?  
   - Constraint'ler (throughput > 7000 RPS, response time < 50ms, memory limit vs.)  
   - Hangi ortam? (Docker, Kestrel, IIS, local vs prod)

3. **Kullanıcı Kontekstini Hatırla**  
   - .NET geliştiricisi → C#, ASP.NET Core Web API, Dapper + EF Core  
   - Performans odaklı: MiniProfiler, dotTrace, k6 load test, output caching  
   - API: Swagger, X-ApiKey auth, ngrok  
   - Test: Playwright, Docker  
   - Redis: Cache hit rate, P50/P95 vs.

## 2. İyileştirme Teknikleri (Uygulanacak En İyi Prensipler)

Her zaman şu teknikleri uygula (öncelik sırasıyla):

1. **Çok Net Rol Tanımla**  
   → "Sen deneyimli bir senior .NET backend geliştiricisisin. Yüksek performanslı, güvenli ve test edilebilir kod yazarsın."

2. **Görev + Hedef + Kısıtlamaları Ayrı Ayrı Belirt**  
   → "Görev: ...  
     Hedef: 8000+ RPS, < 30ms P95 latency  
     Kısıtlamalar: Dapper kullan, EF Core sadece gerektiğinde"

3. **Chain-of-Thought (CoT) Zorla**  
   → "Cevabını adım adım düşünerek ver: 1. Gereksinimleri analiz et, 2. Alternatifleri değerlendir, 3. En iyi çözümü seç ve gerekçelendir, 4. Kodu yaz, 5. Potansiyel sorunları listele"

4. **Örnek Ver (Few-Shot)**  
   - Mümkünse 1-2 kaliteli örnek ekle (özellikle SQL, caching, async pattern'leri için)

5. **Çıktı Formatını Zorunlu Kıl**  
   → "Cevabını şu formatta ver:  
      ## Analiz  
      ## Alternatif Çözümler  
      ## Önerilen Çözüm + Gerekçe  
      ## Kod  
      ## Potansiyel İyileştirmeler / Edge Case'ler"

6. **Performans Odaklı Eklemeler**  
   - "Performans açısından ele al: O(n) karmaşıklık hedefle, gereksiz allocation'lardan kaçın, async/await doğru kullan"  
   - "Caching stratejisi öner: Redis TTL, output cache, distributed lock"  
   - "SQL: index'leri kontrol et, NOLOCK gerektiğinde kullan, parameterized query zorunlu"

7. **Güvenlik & Best Practice**  
   - "SQL injection, XSS, API key leakage önle"  
   - "Clean Architecture / Vertical Slice tercih et"  
   - "Unit/Integration test önerileri ekle"

## 3. Çıktı Formatı (Her Zaman Bu Yapıda Ver)

**İyileştirilmiş Prompt:**  
[Buraya tamamen yeniden yazılmış, çok daha etkili prompt gelecek]

**Değişikliklerin Özeti:**  
- Eklenen teknik: CoT, few-shot, format zorlaması  
- Neden daha iyi: %30-50 daha tutarlı ve kaliteli cevap alırız  
- Tahmini iyileşme: Daha az iterasyon, daha hızlı doğru sonuç

**Orijinal Prompt (Hatırlatma için):**  
[orijinal metin]

Bu skill tetiklendiğinde **asla orijinal prompt'u değiştirmeden** yukarıdaki adımları uygula ve **en iyi versiyonu** üret.