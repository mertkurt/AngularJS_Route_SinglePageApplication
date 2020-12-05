Arkadaşlar Merhaba,

 

Bu yazımızda sizlere AngularJS ile Route kütüphanesini kullanarak basit ve kullanışlı bir Single Page Application anlatacağım.

 

İlk olarak herzamanki gibi Visual Studio uygulamamızı açıyorum ve boş bir Web Projesi başlatıyorum. Başlattığınız projenin MVC veya Asp.Net olması hiç farketmeycektir. Biz zaten sadece html uzantılı sayfalarla çalışacağımız için isteyen arkadaşlarımız Visual Studio yerine başka bir IDE veya NotePad++ benzeri uygulama kullanabilirler.

 

Biz Visual Studio ile başladığımız için kod geliştirmeye boş projemiz açıldığı anda ilk olarak Manage Nuget Packages yardımıyla AngularJS kütüptanesini aratıp hiç uğraşmadan full versiyonunu seçip projemize hemen ekliyoruz. Ekleme işlemi tamamlanınca Hemen projemize sağ tıklayıp New bölümünden Index isimli yeni bir html sayfa ekliyoruz projemize. Biz Visual studio ile proje başlattığımız için projemize otomatik olarak bootstrap kütüphaneleri ekli geliyor. Eğer başka bir kod geliştirme uygulaması kullanıyorsanız bootstrap kütüphanesinide projenize eklemeniz gerekecektir.

 

AngularJS ve Bootstrap için kütüphaneleri indirebileceğiniz adresleri aşağıda paylaşıyorum. Visual Studio ile geliştirme yapmayan arkadaşlarmız bu adreslerden kütüphaneleri indirip sayfalarına ekleyebilirler.

 

AngularJS : https://angularjs.org/

Bootstrap : https://getbootstrap.com/

 

Biz şimdi ilk olarak aşağıda örnek olarak koyduğum satırlar gibi oluşturduğumuz Index.html sayfamızı açıp kullanmak istediğimiz bütün kütüphaneleri ve CSS dosyalarını <head></head> tagleri arasına ekliyoruz.

 

    <link href="Content/bootstrap.css" rel="stylesheet" />

    <link href="Content/scrolling-nav.css" rel="stylesheet" />

    <script src="Scripts/angular.min.js"></script>

    <script src="Scripts/angular-route.min.js"></script>

 

Bir diğer kütüphane ekleyeceğimiz yer ise </body> etiketinin bitiş alanı. </body> tag i ni bulup bir satır üstüne aşağıdaki gibi javascript kütüphanelerimizi ekliyoruz.

 

    <script src="Scripts/jquery-1.9.1.min.js"></script>

    <script src="Scripts/bootstrap.min.js"></script>

    <script src="Scripts/jquery.easing.min.js"></script>

 

Kütüphane ekleme işlemlerimiz bittiğine göre artık sayfamızın kodlamasına geçebiliriz. İlk olarak AngularJS in sayfanın hangi analarında çalışacağını belirten 'ng-app' kodumuzu ekleyerek başlayalım. Ben sayfanın tamamında AngularJS i kullanmak istediğim için bu kodu aşağıdaki gibi <html> etiketine ekleyerek başlayacağım.

 

<html ng-app="myApp">

 

ng-app attributesinin yanına yazdığımız isim ise bizim AngularJS kullanırken kullanacağımız genel isim gibi düşünülebilir. 

 

Sayfamızın body bölümünde ise bootstrap sayesinde ekrana bir menü ekleyerek o menü elemanlarını kullanıp Single Page Application projemizi hazırlayacağız. Body bölümün için hazırladığım kodlarda aşağıdaki gibidir.

 

<body id="page-top" data-spy="scroll" data-target=".navbar-fixed-top">

    <nav class="navbar navbar-default navbar-fixed-top" role="navigation">

        <div class="container">

            <div class="navbar-header page-scroll">

                <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-ex1-collapse">

                    <span class="sr-only">Toggle navigation</span>

                    <span class="icon-bar"></span>

                    <span class="icon-bar"></span>

                    <span class="icon-bar"></span>

                </button>

                <a class="navbar-brand page-scroll" href="/">Anasayfa</a>

            </div>

            <div class="collapse navbar-collapse navbar-ex1-collapse">

                <ul class="nav navbar-nav">

                    <li>

                        <a class="page-scroll" href="/hakkimizda">Hakkımızda</a>

                    </li>

                    <li>

                        <a class="page-scroll" href="/urunler">Ürünler</a>

                    </li>

                    <li>

                        <a class="page-scroll" href="/iletisim">İletişim</a>

                    </li>

                </ul>

            </div>

        </div>

    </nav>

    <ng-view>

    </ng-view>

 

 

Yukarıdaki kodumuzda asıl dikkat edilmesi gereken nokta     <ng-view> </ng-view> etiketleri. Bu etiketler içerisine biz AngularJS Route kütüphanesini kullanarak hazırladığımız diğer html sayfaları çağırabileceğiz.

 

Index.html sayfamızdaki html bölümü kodlamalarımız bitti. Şimdi artık AngularJS kullanrak dinamik olarak Single Page Application umuzu hazırlayacağımız kodlarımızı yazmaya geldi. Ben bu kodları html taglerinin bitişine en alta ekleyerek yazmayı tercih ediyorum. 

 

<script>

    var app = angular.module("myApp", ['ngRoute']);

    app.config(RouteConfig);

 

    RouteConfig.$inject = ["$routeProvider", "$locationProvider"];

 

    function RouteConfig($routeProvider, $locationProvider, $location) {

        $routeProvider

            .when("/", {

                templateUrl: "anasayfa.html"

            })

            .when("/hakkimizda", {

                templateUrl: "hakkimizda.html"

            })

            .when("/urunler", {

                templateUrl: "urunler.html"

            })

            .when("/iletisim", {

                templateUrl: "iletisim.html"

            })

            .otherwise({

                redirectTo:"/"

            })

 

        $locationProvider.html5Mode({

            enabled: true,

            requireBase: false

        });

    }

</script>

 

 

 

Yukarıdaki kodumuzda sayfamızı ilk açtığımızda oluşturduğumuz ng-app ismimizle bir module başlatıp o modüle AngularJS içerisinden route kütüphanesini kullanmak için ['ngRoute'] etiketini yazdık. Bu eklenti sayesinde artık sayfamız route kütüphanesinin bütün özelliklerini kullanabilecek duruma gelecektir.

 

Daha sonra RouteConfig ayarlarını yaparak birazdan oluşturacağımız menü sayfalarımızın hangi isimlerde olacağını ve ekrana gelirken adres satırında nasıl görüneceklerini tanımladık.

 

Son olarakta locationProvider içerisinde html5Mode özelliklerini aktif ederek adres satırından yapılacak yönlendirmelerin çalışmasını sağlıyoruz.

 

AngularJS kodumuzuda hazırladıktan sonra artık kod içerisinde htlml sayfa olarak yazdığımız sayfaları oluşturup kodlayabiliriz.

 

İlk olarak anasayfa.html sayfamızı oluşturup içerisini aşağıdaki gibi kodladım.

 

<section id="about" class="about-section">

    <div class="container">

        <div class="row">

            <div class="col-lg-12">

                <h1>Anasayfa</h1>

            </div>

        </div>

    </div>

</section>

 

 

hakkimizda.html

<section id="about" class="about-section">

    <div class="container">

        <div class="row">

            <div class="col-lg-12">

                <h1>Hakkımızda</h1>

            </div>

        </div>

    </div>

</section>

 

 

urunler.html

 

<section id="about" class="about-section">

    <div class="container">

        <div class="row">

            <div class="col-lg-12">

                <h1>Ürünler</h1>

            </div>

        </div>

    </div>

</section>

 

 

 

iletisim.html

 

<section id="about" class="about-section">

    <div class="container">

        <div class="row">

            <div class="col-lg-12">

                <h1>İletişim</h1>

            </div>

        </div>

    </div>

</section>

 

 

Bütün sayfalarımızı hazırladığımıza göre artık Index.html sayfamızı çalıştırıp Single Page Application uygulamamızın nasıl çalıştığını görebiliriz.

Ekrandaki linklerimize tıklayarak sayfamızın yenilenmeden oluşturduğumuz diğer sayfalarımızı açtığını görebiliriz.

Artık size kalan tek işlem istediğiniz gibi açılan sayfaların içeriklerini doldurmak oluyor. 

 
