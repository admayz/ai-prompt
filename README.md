[Antigravity Kit](https://github.com/vudovn/antigravity-kit)

- **agent** (frontend-specialist, security-auditor, backend-engineer vb.)
- **skill** (bilgi modülleri – görev bağlamına göre otomatik yüklenir)
- **workflow** (`/brainstorm`, `/create`, `/debug`, `/deploy` gibi)
- **Çalışma alanı kuralları** (rules – davranışları yönlendiren yönergeler)

## Klasör Yapısı

```text
.agent/
├── agents/              # Uzman AI kişilikleri (agent tanımları)
│   └── ...              # frontend-specialist.md, security-auditor.md vb.
├── commit/              # Commit mesajı kuralları ve şablonları
├── frontend-design/     # Frontend odaklı tasarım rehberleri / pattern'ler
├── rules/               # Genel çalışma alanı kuralları
│   └── GEMINI.md        # En önemli kural dosyası (genellikle buraya bakılır)
├── skills/              # Otomatik yüklenen bilgi/beceri modülleri
│   └── ...              # documentation-templates, testing-strategy vb.
└── workflows/           # Slash komutlarıyla tetiklenen iş akışları
    └── ...              # /create, /refactor, /debug gibi akış tanımları
