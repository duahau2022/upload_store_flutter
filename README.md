# upload_store_flutter

https://support.shopgate.com/hc/en-us/articles/204812698-Optimizing-your-app-information-for-the-app-stores

A: Release Android

1. Tạo file key jks ( dùng Android studio )
2. Lưu file vào folder project/android/app
3. Trong file project/android/gradle.properties thay đổi các thông số sau:
MYAPP_RELEASE_STORE_FILE=kename.jks (tên file key jks vừa tạo)
MYAPP_RELEASE_KEY_ALIAS=key0 (Tên key)
MYAPP_RELEASE_STORE_PASSWORD=password	(mật khẩu store)
MYAPP_RELEASE_KEY_PASSWORD=password  (mật khẩu key)
 
4. Thêm đoạn sau vào file project/android/app/build.gradle :
android { // thẻ android chứa compileSdkVersion 28
    signingConfigs {
       debug {
           if (project.hasProperty('MYAPP_RELEASE_STORE_FILE')) {
               storeFile file(MYAPP_RELEASE_STORE_FILE)
               storePassword MYAPP_RELEASE_STORE_PASSWORD
               keyAlias MYAPP_RELEASE_KEY_ALIAS
               keyPassword MYAPP_RELEASE_KEY_PASSWORD
           }
       }
       release {
           if (project.hasProperty('MYAPP_RELEASE_STORE_FILE')) {
               storeFile file(MYAPP_RELEASE_STORE_FILE)
               storePassword MYAPP_RELEASE_STORE_PASSWORD
               keyAlias MYAPP_RELEASE_KEY_ALIAS
               keyPassword MYAPP_RELEASE_KEY_PASSWORD
           }
       }
   }
   buildTypes {
       release {
           signingConfig signingConfigs.release
           proguardFiles getDefaultProguardFile('proguard-android.txt'), 'app/proguard-rules.pro'
       }
   }
}
5. Mở terminal project gõ lệnh : flutter build apk để lấy file apk -> Vào thư mục project/build/app/outputs/flutter-apk/ : để lấy apk flutter build appbundle --target-platform android-arm,android-arm64,android-x64 để lấy file appbundle -> Vào thư mục project/build/app/outputs/bundle/release/ : để lấy appbundle

B. Release Ios:
B1: Đổi bundle id trong xcode, add app mới trên firebase (đồng thời cập nhật file GoogleService-Info.plist)
B2:Config push noti trên firebase: Vào app => Settings => Cloud messaging => thêm APNs Authentication Key (lấy trên acc dev) trong app ios
B3: Tạo key config trên máy theo guide: https://bitbar.com/blog/tips-and-tricks-how-to-build-ipa-for-ios-app-testing/
B4: Cài đặt flutter và run
Chạy lệnh lấy lib về: flutter package get Đóng gói dart sang native: flutter build ios Mở xcode lên build và upstore như native

**. IOS:
https://help.apple.com/app-store-connect/#/devd274dd925
- 1 screen short: 
  1.1 6.5 inch (iPhone 13 Pro Max, iPhone 12 Pro Max, iPhone 11 Pro Max, iPhone 11, iPhone XS Max, iPhone XR)
               2688 x 1242 pixels (19.5:9 aspect ratio)
  1.2 5.5 inch (iPhone 6s Plus, iPhone 7 Plus, iPhone 8 Plus) 
              2208 x 1242 pixels (Rendered Pixels)
              1920 x 1080 pixels (Physical Pixels)
  1.3 12.9 inch (iPad Pro (3rd generation)) 
              2732 x 2048 pixels (4:3 aspect ratio)
Icon: tool icon: https://appiconmaker.co/
** Android
1 screen short: đẹp là đc
2 icon: 512x512
3 image: 1024x500
4 onesignale icon http://romannurik.github.io/AndroidAssetStudio/icons-notification.html
Tạo icon https://makeappicon.com/
* More
** Up app:
1 kiểm tra config ads, debug, link appstore
2 kiểm tra firebase config
3 kiểm tra term, privacy
4 Thay server dev vs product
5 Kiểm tra inapp config appstore
6 create privacy and term: https://app-privacy-policy-generator.firebaseapp.com
7 tạo web privacy:
https://www.blogger.com/about/
google site
https://developers.google.com/youtube/terms/developer-policies-guide
** Up store success:
1 Android Login fb: config sh1, hash key:
sh1: lấy trên store ch play
hash key: run git bash trên windown: sh echo <sh1> | xxd -r -p | openssl base64
mac: sh echo -n "abc"| openssl sha1 -binary | base64
2 Android Firebase auth: config sh1
** May ảo
this copy of the install macos mojave application is damaged and can‘t be used to install macos: date 010101002018
Resolving duplicate serial numbers for macOS Virtual Machines.: https://support.watchmanmonitoring.com/hc/en-us/articles/213487906-Resolving-duplicate-serial-numbers-for-macOS-Virtual-Machines-
**: Android: install .apk programmatically [duplicate]
https://stackoverflow.com/a/4969421/10819917
*Note: Ảnh dùng theo 3 size: low: 100px, medium: 300px, high: 500px
**: Create drawble android:
https://www.img-bak.in/tbjNPVCqVzjxLZVIvfGHUT8nMvLhDyIr/
