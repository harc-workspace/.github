# HARC Shared Instructions

Bu dosya, HARC organization'ındaki tüm projelere uygulanması hedeflenen ortak talimatların ana giriş noktasıdır.

## Uygulama sırası

Projeye ait ana instruction dosyası bu dosyayı ve aşağıdaki context'leri birlikte kullanmalıdır:

1. `coding.instructions.md`
2. `architecture.instructions.md`
3. `security.instructions.md`
4. `documentation.instructions.md`
5. İlgili repository'nin proje-özel talimatları

Bu dosyalar otomatik olarak import edilmez. Sync işlemi sırasında içerikleri hedef repository'ye kopyalanmalı veya hedef dosyada açıkça birleştirilmelidir.

## Genel kurallar

- Önce ilgili kodu, testleri, configuration dosyalarını ve dokümantasyonu incele.
- Mevcut mimariyi ve public sözleşmeleri gereksiz yere değiştirme.
- Değişiklikleri küçük, doğrulanabilir ve geri alınabilir parçalarda tut.
- Secret, token, connection string veya kişisel veriyi source code'a yazma.
- Değişiklik sonrası uygun build, test ve lint kontrollerini çalıştır.
- Gerçek kod davranışı ile dokümantasyon çelişirse kodu doğrula ve dokümantasyonu güncelle.
- Yapılmayan doğrulamaları yapılmış gibi raporlama.
