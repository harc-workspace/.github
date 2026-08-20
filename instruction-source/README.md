# Instruction Source

Bu klasör, `harc-workspace` organization'ındaki repository'lere dağıtılacak ortak instruction dosyalarını içerir.

## Hedef repository yapısı

Her proje repository'sinde aşağıdaki dosyalar bulunmalıdır:

```text
.github/
├── copilot-instructions.md
└── instructions/
    ├── coding.instructions.md
    ├── architecture.instructions.md
    ├── security.instructions.md
    └── documentation.instructions.md
```

Repository kökünde ayrıca `AGENTS.md` bulunması, farklı AI agent ve IDE'lerde uyumluluğu artırır.

## Senkronizasyon

Bu klasördeki ortak dosyalar hedef repository'lere kopyalanmalıdır. Proje-özel talimatlar hedef repository'de ayrıca tutulur; ortak dosyalar üzerine yazılmamalıdır.

Önerilen hedef dosya:

```text
.github/copilot-instructions.md
```

Bu dosya ortak talimatları ve proje-özel kuralları birleştiren ana giriş noktasıdır. Markdown linkleri gerçek bir import mekanizması değildir; dağıtım sırasında ortak içerik hedef repository'ye alınmalıdır.
