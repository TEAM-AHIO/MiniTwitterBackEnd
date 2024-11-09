# MiniTwitter Back-End

MiniTwitterApp, Twitter benzeri bir sosyal medya uygulamasının back-end tarafını .NET ile geliştiren bir projedir. Bu uygulama, kullanıcıların içerik oluşturmasını, diğer kullanıcıları takip etmesini, postları beğenmesini ve repost yapmasını sağlamak için RESTful bir API sağlar.

## Proje Özeti

MiniTwitterApp’in amacı, Twitter benzeri bir sosyal medya platformu oluşturmak ve kullanıcıların aşağıdaki temel işlevleri gerçekleştirmesine izin vermektir:

- **Kullanıcı Yönetimi:** Kullanıcı kaydı, giriş işlemleri, profil görüntüleme ve güncelleme.
- **Post Yönetimi:** Post oluşturma, düzenleme, silme, beğenme ve repost özellikleri.
- **Takip Sistemi:** Kullanıcıların birbirini takip edebilmesi ve akışlarını bu ilişkiler doğrultusunda görebilmesi.
- **Etkileşimler:** Post beğenme ve repost yapma gibi sosyal medya etkileşimleri.

## Kullanılan Teknolojiler

### Back-End
- **.NET 8**: Projenin çekirdek geliştirme platformu. Uygulamanın RESTful API mimarisinde servis tabanlı bir yapı sunuyor.
- **Entity Framework Core**: Veritabanı işlemleri için kullanılan ORM. .NET uygulaması ile PostgreSQL arasında veri etkileşimini sağlar.
- **AutoMapper**: Model ve DTO’lar arasında veri haritalandırması yapar, kodun daha temiz ve düzenli kalmasını sağlar.
- **JWT Authentication**: Kullanıcı kimlik doğrulaması için JSON Web Token (JWT) tabanlı kimlik doğrulama sistemi.

### Veritabanı
- **PostgreSQL**: Kullanıcı, post, takip ve etkileşim gibi uygulama verilerinin saklandığı, yüksek performanslı ve güvenilir bir SQL veritabanı.

## Proje Mimarisi

MiniTwitterApp, katmanlı bir mimari yapıyı takip eder:

1. **API Katmanı**: Tüm HTTP isteklerini alır ve yönlendirir. Kullanıcı işlemleri, post yönetimi ve etkileşimler gibi tüm API endpoint’leri burada bulunur.
2. **Business (Service) Katmanı**: Uygulamanın iş mantığını içerir. Veritabanı işlemleri ile kullanıcı etkileşimleri bu katmanda gerçekleştirilir.
3. **Data Access (Repository) Katmanı**: Veritabanı ile etkileşimi yöneten katmandır. Entity Framework Core kullanılarak PostgreSQL üzerinde CRUD işlemleri gerçekleştirilir.
4. **Model Katmanı**: Uygulamanın temel veri modelleri ve DTO'ları bu katmanda yer alır.

## Proje Özellikleri

- **Kullanıcı Yönetimi**: Kayıt olma, giriş yapma, şifre sıfırlama ve profil düzenleme gibi temel kullanıcı işlemlerini sağlar.
- **Post Yönetimi**: Kullanıcıların metin tabanlı post oluşturma, düzenleme, silme gibi işlemleri yapmalarını sağlar.
- **Beğeni ve Repost**: Kullanıcıların postları beğenmesini ve repost yapmasını mümkün kılar.
- **Takip ve Akış Yönetimi**: Kullanıcılar birbirlerini takip ederek, takip ettikleri kişilerin postlarını kendi akışlarında görebilirler.
- **Kimlik Doğrulama ve Yetkilendirme**: JWT ile kullanıcı kimlik doğrulaması yapılır, her kullanıcının yalnızca kendi verilerine erişmesi sağlanır.
