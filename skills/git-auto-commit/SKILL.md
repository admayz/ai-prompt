---
name: git-auto-commit
description: Değişiklikleri analiz eder, uygun dosyaları stage eder ve tek bir anlamlı Conventional Commit mesajıyla commit yapar. Sadece "create a git commit", "commit changes", "git commit" gibi taleplerde veya allowed-tools bağlamında otomatik devreye girer. Başka hiçbir metin/çıktı üretmez — yalnızca tool çağrıları yapar.
keywords: [git, commit, stage, push, conventional commits]
triggers: ["commit", "git commit", "create commit", "stage and commit", "auto commit"]
priority: very-high
---

# Git Auto Commit Skill

Bu skill **sadece** şu durumlarda aktif olur:
- Kullanıcı açıkça "commit", "git commit", "create a git commit" gibi bir şey söyler
- Veya görev tam olarak şuna benzer: "Based on the above changes, create a single git commit."
- Context'te git status, diff, branch, log gibi bilgiler sağlanmışsa

**Kesin Kurallar — Asla İhlal Etme:**

1. **SADECE** izin verilen araçları kullan:  
   - Bash(git add:*)  
   - Bash(git status:*)  
   - Bash(git commit:*)

2. **Hiçbir zaman** şu araçları çağırma: web search, browse, code execution, x search vb.

3. **Yanıtta metin gönderme** — sadece tool çağrıları olsun. Hiçbir açıklama, düşünce, emoji, markdown vs. yok.

4. **Adım adım mantık (tool çağrı sırası):**

   a. Önce mevcut durumu doğrula  
      → Bash(git status:*)

   b. Eğer unstaged değişiklik varsa → hepsini stage et  
      → Bash(git add .)   ya da daha güvenli: Bash(git add -u) + yeni dosyalar için ayrı add

   c. Commit mesajı oluştur:  
      - Conventional Commits formatı kullan (feat:, fix:, refactor:, docs:, chore: vb.)  
      - Mesaj kısa, net, imperative mood  
      - Değişiklikleri özetle (diff ve status'tan bakarak)  
      - Örnek: "refactor: split auth service into smaller modules"  
      - Türkçe istiyorsan: "düzelt: login hatası için null check eklendi"

   d. Tek commit yap  
      → Bash(git commit -m "mesaj buraya")

5. **Eğer zaten staged yoksa veya hiçbir değişiklik yoksa**  
   → Hiçbir şey yapma (tool çağırma)

6. **Branch koruması**  
   - main/master üzerinde çalışıyorsan → commit etme, uyarı verme (ama metin yok → sessiz kal)

**Örnek Tool Çağrı Akışı (tam olarak bu mantıkla):**

1. git status kontrolü
2. git add .   (veya seçici add)
3. git commit -m "fix: resolve undefined user in profile endpoint"

**Bu skill aktifken başka hiçbir skill'i tetikleme veya metin üretme.**