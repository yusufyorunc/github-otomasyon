GitHub Actions kullanarak bunu ücretsiz ve kolay bir şekilde yapabiliriz. GitHub Actions, public repolar için tamamen ücretsizdir ve private repolar için de ayda 2000 dakika ücretsiz kullanım sunar.

**ÖNEMLİ GÜVENLİK UYARISI:** Paylaştığınız Personal Access Token'ı hemen iptal edip yenisini oluşturmanızı şiddetle tavsiye ediyorum! Token'ınız artık public olarak görünüyor ve kötü niyetli kişiler tarafından kullanılabilir.

İşte adım adım yapmanız gerekenler:

## 1. Yeni Personal Access Token Oluşturma

1. GitHub'a giriş yapın
2. Sağ üstteki profil fotoğrafınıza tıklayın → Settings
3. Sol menüden "Developer settings" → "Personal access tokens" → "Tokens (classic)"
4. "Generate new token" → "Generate new token (classic)"
5. Token'a bir isim verin (örn: "Daily Update Bot")
6. Süre olarak 90 gün veya "No expiration" seçin
7. Şu yetkileri seçin:
   - `repo` (tüm repo yetkisi)
   - `workflow` (workflow dosyalarını güncelleme yetkisi)
8. "Generate token" butonuna tıklayın ve token'ı kopyalayın

## 2. Repository Secret Ekleme

1. GitHub'da otomatik güncelleme yapacağınız repoya gidin
2. Settings → Secrets and variables → Actions
3. "New repository secret" butonuna tıklayın
4. Name: `PAT_TOKEN`
5. Value: Yeni oluşturduğunuz token'ı yapıştırın
6. "Add secret" butonuna tıklayın

## 3. GitHub Actions Workflow Dosyası Oluşturma

Repository'nizde şu klasör yapısını oluşturun:
```
.github/workflows/daily-update.yml
```

İşte `daily-update.yml` dosyasının içeriği:## 4. Workflow'u Test Etme

1. Yukarıdaki YAML dosyasını repository'nize ekleyin
2. GitHub'da Actions sekmesine gidin
3. Sol taraftan "Daily README Update" workflow'unu seçin
4. Sağ taraftan "Run workflow" butonuna tıklayın
5. "Run workflow" ile manuel olarak test edin

## 5. Önemli Notlar

### Zaman Ayarı
- Cron ifadesi `'0 12 * * *'` UTC 12:00'yi temsil eder
- Türkiye UTC+3 olduğu için bu saat Türkiye'de 15:00'e denk gelir
- İsterseniz farklı bir saat ayarlayabilirsiniz

### Cron Sözdizimi
```
┌───────────── dakika (0-59)
│ ┌───────────── saat (0-23)
│ │ ┌───────────── ayın günü (1-31)
│ │ │ ┌───────────── ay (1-12)
│ │ │ │ ┌───────────── haftanın günü (0-6)
│ │ │ │ │
│ │ │ │ │
* * * * *
```

### Alternatif Saatler
- UTC 00:00 için: `'0 0 * * *'`
- UTC 06:00 için: `'0 6 * * *'`
- UTC 18:00 için: `'0 18 * * *'`

## 6. İzleme ve Kontrol

1. **Actions sekmesinden** workflow çalışmalarını izleyebilirsiniz
2. **Email bildirimleri** almak için Settings → Notifications'dan ayarlayabilirsiniz
3. Hata durumunda otomatik email alırsınız

## Ek Özellikler (Opsiyonel)

Eğer isterseniz README'ye daha fazla bilgi ekleyebilirsiniz:
- Commit sayısı
- Repository istatistikleri
- Hava durumu
- Random quote

Bu özellikleri eklemek isterseniz workflow dosyasını güncelleyebilirim.

**Tekrar hatırlatma:** Lütfen paylaştığınız Personal Access Token'ı hemen iptal edin ve yenisini oluşturun! GitHub Settings → Developer settings → Personal access tokens'dan eski token'ı revoke edebilirsiniz.