---
name: git-commit-push-pr
description: Mevcut değişiklikleri yeni bir feature branch'e alır (gerekirse), tek bir anlamlı commit yapar, branch'i push eder ve GitHub CLI ile pull request oluşturur. Sadece "commit push pr", "create pr", "commit and pr" gibi ifadelerle veya verilen görev tanımına çok yakın durumlarda çalışır. Başka metin üretmez — yalnızca tool çağrıları yapar.
keywords: [git, commit, push, pr, pull request, github, gh]
triggers: ["commit push pr", "create pr", "commit and pr", "push and pr", "open pr", "gh pr"]
priority: very-high
---

# Git Commit → Push → Open PR Skill

**Bu skill aktif olduğunda KESİNLİKLE şu kurallara uy:**

1. Yalnızca aşağıdaki araçları kullanabilirsin (başka hiçbir tool çağrılmaz):
   allowed-tools:
     - Bash(git checkout --branch:*)
     - Bash(git add:*)
     - Bash(git status:*)
     - Bash(git push:*)
     - Bash(git commit:*)
     - Bash(gh pr create:*)

2. **Hiçbir metin, açıklama, düşünce, emoji, markdown vs. gönderme**  
   → Yanıt **sadece** tool çağrılarından oluşmalı

3. Adım adım mantık (tam olarak bu sırayla, gerektiğinde atla):

   A. Mevcut branch'i öğren  
      → git branch --show-current

   B. Eğer branch main / master / trunk ise:
      → Yeni branch oluştur (örnek isimlendirme mantığı aşağıda)
      → git checkout -b <yeni-branch>

   C. Değişiklikleri stage et
      → git add .    (veya daha seçici ama genelde . yeter)

   D. Tek bir Conventional Commit yap
      → git commit -m "<tip>(<scope>): <kısa özet>"
      → tip örnekleri: feat, fix, refactor, docs, test, chore, style, perf
      → scope: api, ui, auth, cache, infra, vb. (değişikliklere göre mantıklı seç)
      → özet: imperative mood, 50–72 karakter hedefle

   E. Branch'i origin'e push et
      → git push origin <branch-ismi>

   F. Pull request oluştur
      → gh pr create --title "<Commit mesajının aynısı>" --body "Otomatik oluşturulan PR" --base main --head <branch-ismi>

4. Branch ismi oluşturma mantığı (commit mesajından türet):
   - feat/api/user → feature/api-user-profile
   - fix/auth/token → fix/auth-invalid-token
   - refactor/ui/components → refactor/ui-component-extraction
   - Genel kural: tip/ilk-3-kelime-küçük-harf-kebab-case

5. Eğer zaten staged değişiklik yoksa → hiçbir şey yapma

6. Eğer zaten PR açıksa veya conflict varsa → gh pr create hata vereceği için skill sessiz kalır (tool hata döner)

**Örnek akış (sadece tool çağrıları):**

1. git branch --show-current
2. (main ise) git checkout -b fix/cache-hit-race
3. git add .
4. git commit -m "fix(cache): prevent race condition in redis lock"
5. git push origin fix/cache-hit-race
6. gh pr create --title "fix(cache): prevent race condition in redis lock" --body "Otomatik oluşturuldu" --base main --head fix/cache-hit-race

Bu skill tetiklendiğinde **başka hiçbir skill çalışmasın** ve **hiç metin üretilmesin**.