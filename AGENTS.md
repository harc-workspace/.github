# Organization Instructions Repository

Bu repository, `harc-workspace` organization'ındaki ortak AI/developer talimatlarının merkezi kaynağıdır.

## Yapı

- `instruction-source/main.instructions.md`: Ortak talimatların ana giriş noktası.
- `instruction-source/*.instructions.md`: Coding, architecture, security ve documentation context'leri.
- `agents/`: Organization seviyesinde kullanılacak Copilot custom agent profilleri.
- `profile/README.md`: Organization profilinde görünen açıklama.

Bu repository'deki dosyalar diğer repository'lere otomatik olarak miras alınmaz. Ortak talimatlar her projeye `.github/copilot-instructions.md`, `.github/instructions/` ve gerektiğinde `AGENTS.md` olarak senkronize edilmelidir.

## Değişiklik kuralları

- Ortak kuralları `instruction-source/` altında tut.
- HARC'a özgü kuralları genel kurallardan ayrı yaz.
- Bir talimat birden fazla projede geçerli değilse ortak dosyaya ekleme.
- Talimat dosyalarında secret, token veya environment-specific değer bulundurma.
- Değişiklikten sonra dosya yollarını ve örnekleri kontrol et.
