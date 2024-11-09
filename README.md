# MiniTwitter Back-End

MiniTwitterApp, Twitter benzeri bir sosyal medya uygulamasının back-end tarafını .NET ile geliştiren bir projedir. Bu uygulama, kullanıcıların içerik oluşturmasını, diğer kullanıcıları takip etmesini, postları beğenmesini ve repost yapmasını sağlamak için RESTful bir API sağlar.

## Proje Özeti

MiniTwitterApp’in amacı, Twitter benzeri bir sosyal medya platformu oluşturmak ve kullanıcıların aşağıdaki temel işlevleri gerçekleştirmesine izin vermektir:

- **Kullanıcı Yönetimi:** Kullanıcı kaydı, giriş işlemleri, profil görüntüleme ve güncelleme.
- **Post Yönetimi:** Post oluşturma, düzenleme, silme, beğenme ve repost özellikleri.
- **Takip Sistemi:** Kullanıcıların birbirini takip edebilmesi ve akışlarını bu ilişkiler doğrultusunda görebilmesi.
- **Etkileşimler:** Post beğenme, kaydetme ve repost yapma gibi sosyal medya etkileşimleri.

## Kullanılan Teknolojiler

### Back-End
- **.NET 8**: Projenin çekirdek geliştirme platformu. Uygulamanın RESTful API mimarisinde servis tabanlı bir yapı sunuyor.
- **Entity Framework Core**: Veritabanı işlemleri için kullanılan ORM. .NET uygulaması ile PostgreSQL arasında veri etkileşimini sağlar.
- **AutoMapper**: Model ve DTO’lar arasında veri haritalandırması yapar, kodun daha temiz ve düzenli kalmasını sağlar.
- **JWT Authentication**: Kullanıcı kimlik doğrulaması için JSON Web Token (JWT) tabanlı kimlik doğrulama sistemi.

### Veritabanı
- **PostgreSQL**: Kullanıcı, post, takip ve etkileşim gibi uygulama verilerinin saklandığı, yüksek performanslı ve güvenilir bir SQL veritabanı.

## Proje Mimarisi

MiniTwitterApp, **Temiz Mimari (Clean Architecture)** prensiplerine göre yapılandırılmıştır. Bu yapıda her katman, belirli bir işlevi yerine getirir ve katmanlar arası bağımlılıklar dıştan içe doğru olacak şekilde düzenlenmiştir.

### 1. API Katmanı (MiniTwitterApp.WebApi)

- **Görevi**: Uygulamanın dış dünyaya açılan kapısıdır. Tüm HTTP isteklerini alır, işler ve uygun `Application` servislerine yönlendirir.
- **İçerik**: Kullanıcı işlemleri, post yönetimi ve etkileşimler gibi tüm API endpoint'leri burada tanımlıdır. `Controllers` klasöründe API kontrolörleri bulunur.
- **Bağımlılıklar**: Yalnızca `Application` katmanına bağımlıdır, iş mantığına ait servisleri çağırır ve veriyi işleyerek istemciye döner.

### 2. Use Cases Katmanı (MiniTwitterApp.Application)

- **Görevi**: Uygulamanın iş mantığını ve iş kurallarını içerir. Burada `Domain` varlıkları üzerinde çalışarak belirli işlemleri gerçekleştiren servisler bulunur.
- **İçerik**: `Interfaces` klasöründe servis ve repository arayüzleri, `Services` klasöründe ise iş mantığını yöneten servisler (örneğin `UserService`, `PostService`) bulunur. Ayrıca `Mappings` klasöründe veri transferi ve model dönüşümleri yapılır.
- **Bağımlılıklar**: `Domain` ve `Infrastructure` katmanlarına bağımlıdır. İş mantığı ile veri erişimi arasında köprü görevi görür.

### 3. Domain Katmanı (MiniTwitterApp.Domain)

- **Görevi**: Uygulamanın temel iş modellerini ve kurallarını tanımlar. Domain Katmanı, uygulamanın iş kurallarını temsil eder ve diğer katmanlardan bağımsızdır.
- **İçerik**: `Entities` klasöründe `User`, `Post`, `Follow` gibi veritabanı varlıkları bulunur. `Enums` klasöründe uygulama genelinde kullanılan sabit türler ve enum’lar yer alır.
- **Bağımlılıklar**: Bu katman tamamen bağımsızdır ve diğer katmanlara bağımlı değildir. Bu, iş kurallarının dış etkenlerden etkilenmeden değiştirilebilmesini sağlar.

### 4. Altyapı Katmanı (MiniTwitterApp.Infrastructure)

- **Görevi**: Veritabanı gibi dış sistemlerle etkileşimi sağlar. `Domain` katmanındaki iş modelleri üzerinde veri işlemlerini gerçekleştiren repository sınıflarını içerir.
- **İçerik**: `Data` klasöründe veritabanı bağlamı (`AppDbContext`) ve migration işlemleri, `Repositories` klasöründe repository sınıfları (örneğin `UserRepository`, `PostRepository`), `Configurations` klasöründe ise veritabanı konfigürasyonları yer alır.
- **Bağımlılıklar**: `Domain` katmanına bağımlıdır, çünkü veritabanı işlemleri için `Domain` varlıklarını kullanır.

### 5. Ortak Katman (MiniTwitterApp.Common)

- **Görevi**: Tüm katmanlarda kullanılabilecek yardımcı yapı ve genel sabitleri içerir.
- **İçerik**: `Helpers` klasöründe JWT oluşturma gibi yardımcı sınıflar, `Extensions` klasöründe genişletme metotları ve `Constants` klasöründe genel sabitler bulunur.
- **Bağımlılıklar**: `Common` katmanı herhangi bir katmana doğrudan bağımlı değildir; fakat diğer katmanlar `Common` içerisindeki genel kullanımlık yapıları kullanabilir.

### 6. Test Katmanı (MiniTwitterApp.Tests)

- **Görevi**: Uygulamanın iş mantığı ve veri erişim katmanlarının doğru çalışıp çalışmadığını kontrol eden testleri içerir.
- **İçerik**: `UnitTests` klasöründe birim testler ve `IntegrationTests` klasöründe entegrasyon testleri bulunur.
- **Bağımlılıklar**: `Application`, `Infrastructure` ve `Domain` katmanlarına bağımlıdır.

---

Bu yapı, temiz mimari prensipleri doğrultusunda projenizi modüler, sürdürülebilir ve test edilebilir bir yapıya kavuşturur. Katmanlar arasındaki bağımlılıklar dıştan içe doğru düzenlenmiş olup, iş mantığı ve veri erişimi birbirinden izole edilmiştir. Bu sayede uygulamanızın bakımı, genişletilmesi ve test edilmesi kolaylaşır.


## Proje Özellikleri

- **Kullanıcı Yönetimi**: Kayıt olma, giriş yapma, şifre sıfırlama ve profil düzenleme gibi temel kullanıcı işlemlerini sağlar.
- **Post Yönetimi**: Kullanıcıların metin tabanlı post oluşturma, düzenleme, silme gibi işlemleri yapmalarını sağlar.
- **Beğeni ve Repost**: Kullanıcıların postları beğenmesini ve repost yapmasını mümkün kılar.
- **Takip ve Akış Yönetimi**: Kullanıcılar birbirlerini takip ederek, takip ettikleri kişilerin postlarını kendi akışlarında görebilirler.
- **Kimlik Doğrulama ve Yetkilendirme**: JWT ile kullanıcı kimlik doğrulaması yapılır, her kullanıcının yalnızca kendi verilerine erişmesi sağlanır.
