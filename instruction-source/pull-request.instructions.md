# Automated Pull Request Instructions

Automation tarafından açılan her synchronization PR'ı, değişikliğin amacını ve kapsamını reviewer'ın ek bağlam aramasına gerek bırakmadan açıklamalıdır.

## Zorunlu bölümler

- **Summary**: Bu PR'ın neden açıldığını tek paragrafta açıkla.
- **Target**: Etkilenen repository'yi ve branch'i belirt.
- **Changes**: Kopyalanan veya güncellenen dosyaları listele.
- **Preserved**: Proje-özel dosyaların ve uygulama source code'unun değiştirilmediğini belirt.
- **Validation**: Workflow'un yaptığı kontrolleri ve yapılmayan testleri açıkla.
- **Review checklist**: Reviewer'ın kontrol etmesi gereken maddeleri ekle.

## HARC synchronization PR kuralları

- PR başlığı `chore: sync shared AI instructions` formatını korumalıdır.
- PR açıklaması otomasyon tarafından oluşturulduğunu belirtmelidir.
- Ortak instruction dosyaları ile proje-özel instruction dosyalarını birbirine karıştırma.
- Uygulama kodu, dependency, configuration veya secret değişikliği varmış gibi ifade kullanma.
- Değişiklik yoksa PR açma; mevcut açık PR varsa yeni PR yerine onu güncelle.
