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
