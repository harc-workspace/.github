# HARC

HARC, çalışan profili ve izin süreçlerini yöneten kurumsal bir İK portalıdır. Proje; React frontend, YARP gateway, .NET 10 Web API, PostgreSQL ve .NET Aspire ile birlikte çalışır.

## Mimari

```text
React / Vite
    │ /api/*
    ▼
YARP Gateway
    │ reverse proxy
    ▼
FastEndpoints API ─── EF Core / Npgsql ─── PostgreSQL
```

`harc-aspire-host`, bu servisleri ve PostgreSQL’i tek bir geliştirme ortamında orkestre eder.

## Mevcut özellikler

- Google ID token ile oturum doğrulama.
- Kullanıcı profili, rolü, takımı, unvanı ve yöneticisini görüntüleme.
- İzin talebi oluşturma.
- İzin belgelerini multipart upload ile kaydetme.
- Aylık izin takvimi ve takım izinlerini görüntüleme.
- Deneyim süresine göre izin bakiyesi hesaplama.
- Türkçe/İngilizce arayüz ve tema seçimi.

Payroll ve documents sayfaları frontend route’u olarak vardır; tamamlanmış backend akışları değildir.

## Gereksinimler

- .NET 10 SDK
- Node.js veya Bun
- Docker Desktop (PostgreSQL için)
- Google OAuth client ID
- Aspire workload/SDK (Aspire ile çalıştırmak için)

## Hızlı başlangıç

### 1. PostgreSQL’i başlatın

```bash
cd harc-api
docker compose up -d
```

Bu compose dosyası PostgreSQL’i `localhost:5433` üzerinde yayınlar.

### 2. API yapılandırmasını hazırlayın

Gerçek secret’ları source control’e yazmayın. `harc-api/appsettings.Development.json` veya user secrets üzerinden aşağıdaki ayarları sağlayın:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Host=localhost;Port=5433;Database=harc_db;Username=harc_user;Password=change-me"
  },
  "Authentication": {
    "Google": {
      "ClientId": "your-google-client-id.apps.googleusercontent.com"
    }
  }
}
```

### 3. API’yi çalıştırın

```bash
cd harc-api
dotnet run
```

API portları `harc-api/Properties/launchSettings.json` içindeki profile göre belirlenir. API Development ortamında Scalar/OpenAPI arayüzü sunar.

### 4. Gateway’i çalıştırın

```bash
cd harc-gateway
dotnet run
```

Gateway’in backend destination’ı varsayılan olarak `http://localhost:5100` adresidir. API farklı portta çalışıyorsa `harc-gateway/appsettings.json` güncellenmelidir.

### 5. Frontend’i çalıştırın

```bash
cd harc-fe
copy .env.example .env   # Windows; macOS/Linux: cp .env.example .env
bun install
bun run dev
```

`.env` içinde en az `VITE_GOOGLE_CLIENT_ID` ve `VITE_GATEWAY_BASE_URL` bulunmalıdır.

## Aspire ile çalıştırma

```bash
cd harc-aspire-host
dotnet run --project Harc.AppHost
```

Aspire PostgreSQL, API, gateway ve frontend’i birlikte başlatır. Sabit portlar yerine Aspire dashboard’ında gösterilen endpoint’leri kullanın. Aspire SDK/workload kurulumu veya NuGet erişimi eksikse AppHost build’i ortam kaynaklı olarak başarısız olabilir.

## API özeti

| Method | Endpoint | Açıklama |
|---|---|---|
| GET | `/api/identity/me` | Kimliği ve profil ilişkilerini getirir |
| POST | `/api/leave` | İzin ve opsiyonel belgeleri oluşturur |
| GET | `/api/leave/calendar?year=YYYY&month=M` | Kişisel/takım izin takvimini getirir |
| GET | `/api/leave/my-balance` | İzin bakiyesini getirir |

Endpoint’ler Bearer Google ID token bekler. Kullanıcı, `identity.Users` tablosunda email ile önceden tanımlı olmalıdır.

## Geliştirme komutları

```bash
# API
dotnet build harc-api/harc-api.csproj

# Gateway
dotnet build harc-gateway/harc-gateway.csproj

# Frontend
cd harc-fe
bun run build
bun run lint
```

Migration güncellemek için API klasöründe `dotnet ef` kullanılır; migration üretmeden önce `IdentityDbContext` mapping’i incelenmelidir.

## Klasörler ve ilgili README’ler

- [AI teknik proje rehberi]()
- [API README](https://github.com/harc-workspace/harc-api/README.md)
- [Gateway README](https://github.com/harc-workspace/harc-gateway/README.md)
- [Frontend README](https://github.com/harc-workspace/harc-fe/README.md)

## Önemli sınırlamalar

- `POST /api/leave` henüz çakışma, hafta sonu, resmi tatil, bakiye ve tarih doğrulamalarını uygulamaz.
- Kullanıcılar authentication sırasında otomatik oluşturulmaz.
- Gateway CORS mevcut kodda tüm origin’lere açıktır; production’da sınırlandırılmalıdır.
- Dosya yükleme için boyut/tür/virüs doğrulaması sınırlıdır.
- Payroll ve documents frontend ekranları tamamlanmış backend özellikleri değildir.
- Otomatik test projesi bulunmamaktadır.
- Mevcut frontend toolchain’inde `bun run build`, kullanılan TypeScript sürümünün `tsconfig.app.json` içindeki kaldırılmış `baseUrl` seçeneğini reddetmesi nedeniyle ayrıca düzenleme gerektirebilir.

Kaynak kodun ayrıntılı mimarisi, veri modeli, auth akışı ve AI çalışma kuralları için `AI_PROJECT_GUIDE.md` dosyasına bakın.
