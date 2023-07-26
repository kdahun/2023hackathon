## 1. Google Play services 설치
Tools - SDK Manager에서 SDK Tools 탭을 눌러 Google Play service가 설치되어 있는지 확인

## 2. 인증을 위한 SHA1 코드 알아내기
Open JDK 폴더(C:\Program Files\Android\Android Studio\jre\bin)로 이동하여 'keytool.exe -list -v -keystore C:\Users\dahun\.android\debug.keystore' 명령을 사용한다
(JDK가 안깔려있으면 안된다. => JDK 깔고 환경변수 설정까지)

## 3. Google Maps Platform으로 와서 키 및 사용자 인증 정보에 들어간다.

## 4. 애플리케이션 제한사항 설정 후 패키지 이름과 SHA-1 인증서 디지털 지문을 채워 넣는다.
![image](https://github.com/kdahun/2023hackathon/assets/101082485/9d168045-22d0-41c2-91e4-9361c5cfe0e1)

## 5. 안드로이드 스튜디오로 돌아와 Gradle Scripts -> build.gradle(2번째꺼) -> dependencies 부분에 다음 코드를 추가한다.
    implementation 'com.google.android.gms:play-services-location:17.0.0'
    implementation 'com.google.android.gms:play-services-maps:17.0.0'
## 6. AndroidManifest.xml 파일을 편집한다.
