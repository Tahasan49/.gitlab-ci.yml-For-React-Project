Project CI/CD Documentation

This .gitlab-ci.yml file is designed to manage the CI/CD pipelines for your Vite/React frontend projects. Its primary purpose is to install dependencies, generate optimized production bundles, and deploy them to a Windows IIS server based on the active branch.
Branch Management

  - Main Branch (Development): Pushing to the main branch triggers an automated process. The app is built in development mode and deployed to the test environment.

  - Prod Branch (Production): Pushing to the prod branch triggers the pipeline. The app is built in production mode and transferred to the live environment.

Build Stage

In this stage, your React project is transformed into static assets:

  - Dependency Installation: Runs npm install to fetch project packages.

  - Vite Build: Uses npx vite build to compile and optimize the project into the dist folder. The --mode flag ensures environment-specific configurations are applied.

  - Artifacts: The dist folder is stored on GitLab for 1 hour to be used by the deployment stage.

Deploy Stage (IIS Deployment)

Static files are transferred to the IIS directory using PowerShell:

  - Service Suspension: The IIS service (W3SVC) is stopped to prevent file-in-use errors.

  - Cleanup and Copying: Existing files in the DEPLOY_PATH are removed, and the new build files are copied over.

  - Restart: The service is restarted to bring the updated web application online.
    
*****************************************************
FOR TURKISH
*****************************************************

Proje CI/CD Dokümantasyonu

Bu .gitlab-ci.yml dosyası; Vite/React tabanlı ön yüz (frontend) projelerinizin CI/CD süreçlerini yönetmek için tasarlanmıştır. Temel amacı, projenin bağımlılıklarını kurmak, optimize edilmiş çıktıları (bundle) oluşturmak ve bunları Windows IIS sunucusuna otomatik veya kontrollü bir şekilde dağıtmaktır.
Dallara Göre Ayrılmış Senaryo (Branch Management)

  - Main Branch (Geliştirme): main dalına kod gönderildiğinde süreç otomatik başlar. development moduyla derleme yapılır ve test sunucusuna dağıtılır.

  - Prod Branch (Canlı): prod dalına kod gönderildiğinde süreç tetiklenir. production moduyla derleme yapılır ve canlı sunucuya aktarılır.

Build (Derleme) Aşaması

Bu aşamada React projeniz tarayıcının anlayabileceği statik dosyalara dönüştürülür:

  - Bağımlılık Kurulumu: npm install ile gerekli paketler yüklenir.

  - Vite Build: npx vite build komutu ile proje dosyaları optimize edilerek dist klasörüne çıkarılır. --mode parametresi ile ortama özel (dev/prod) ayarlar yüklenir.

  - Artifacts: Oluşturulan dist klasörü, dağıtım aşamasında kullanılmak üzere 1 saat süreyle GitLab üzerinde saklanır.

Deploy (IIS Sunucusuna Dağıtım) Aşaması

Statik dosyalar PowerShell aracılığıyla IIS'in yayın klasörüne aktarılır:

  - Hizmet Durdurma: Dosya kilitlenmelerini önlemek için IIS servisi (W3SVC) durdurulur.

  - Temizlik ve Kopyalama: DEPLOY_PATH içindeki eski dosyalar silinir ve yeni dist içeriği buraya kopyalanır.

  - Yeniden Başlatma: Servis tekrar başlatılarak web uygulaması yayına alınır.
