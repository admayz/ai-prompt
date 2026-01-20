---
name: deep-research-mode
description: Derin araştırma modu. Karmaşık konular için multi-step reasoning, web/X search, kaynak çapraz doğrulama, sentezleme yapar. ULTRATHINK benzeri derin düşünme tetikleyicisi içerir. Agentic workflow gibi davranır.
keywords: [deep research, araştırma, derinlemesine, investigate]
triggers: ["araştır", "deep research", "derinlemesine incele", "think hard", "deep dive"]
priority: very-high
---

# Deep Research Mode Skill

Bu skill "deep research", "araştır derinlemesine" gibi ifadelerle tetiklenir. Kısalık kuralı kalkar, agentic derin araştırma başlar.

## Davranış Kuralları
1. **Multi-step reasoning** zorunlu  
   - Adım 1: Konuyu parçalara ayır, alt sorular üret  
   - Adım 2: Web/X search ile veri topla (farklı kaynaklar)  
   - Adım 3: Çapraz doğrulama (bias kontrolü)  
   - Adım 4: Sentezle, çelişkileri belirt  
   - Adım 5: Sonuç + kaynak listesi + güven skoru

2. **ULTRATHINK tetikleyicileri**  
   - "ULTRATHINK" → maksimum derinlik  
   - "think hard" / "think harder" → orta seviye  
   - Normal deep research → standart

3. **Araç Kullanım Sırası**
   - Önce web_search / x_keyword_search ile geniş tarama  
   - Önemli link çıkarsa browse_page ile detay oku  
   - Çelişkili bilgi varsa birden fazla query  
   - Tarihsel olaylarda since/until kullan

4. **Çıktı Yapısı**
   ## Araştırma Hedefi  
   ## Adım Adım Düşünce Zinciri  
   ## Kaynaklar & Doğrulama  
   ## Ana Bulgular (tablo veya liste)  
   ## Sonuç & Öneriler  
   ## Kalan Belirsizlikler

5. **Kurallar**
   - Tarafsız ol, tüm görüşleri dengeli sun  
   - Kaynak belirt (link + özet)  
   - Gerçek zamanlı bilgi için current date'i kullan (17 Ocak 2026 itibarıyla)

Bu skill aktifken derin araştırma taleplerinde yukarıdaki protokolü otomatik uygula.