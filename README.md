Android Signature Pad
====================

Android Signature Pad 라이브러리는 안드로이드에서 필기 서명을 할 수 있도록 합니다.
[Square](https://squareup.com)님의 포스팅 [Smoother Signatures](http://corner.squareup.com/2012/07/smoother-signatures.html)을 참조한 가변 폭 베지어 곡선 보간법을 사용합니다.

![Screenshot](https://github.com/gcacace/android-signaturepad/raw/master/header.png)

## 특징
 * 베지어 곡선 보간법을 이용한 부드러운 곡선
 * 누르는 압력 및 속도에 따른 선의 폭 변화
 * 필기 펜의 색과 너비 커스터마이징
 * Bitmap과 SVG 형식을 지원
 * 데이터 바인딩(Data Binding on Android XML)

## 설치

Maven Central을 통해 최신 배포판을 사용하실수 있습니다.

### Gradle

`build.gradle` 파일을 열고, `repositories` 항목에 추가하세요:
```gradle
repositories {
    mavenCentral()
}
```
그리고 dependency에 추가해주세요:
```gradle
compile 'com.github.gcacace:signature-pad:1.2.1'
```

### Maven

`pom.xml` 파일에 아래와 같이 추가해주세요:
```xml
<dependency>
  <groupId>com.github.gcacace</groupId>
  <artifactId>signature-pad</artifactId>
  <version>1.2.1</version>
  <type>aar</type>
</dependency>
```

## 사용법

*`/SignaturePad-Example` 프로젝트를 참고하시면 더 다양한 예제와 상세한 사용법을 확인하실 수 있습니다.*

1. `SignaturePad` 뷰 객체를 레이아웃에 추가해주세요.
```xml
 <com.github.gcacace.signaturepad.views.SignaturePad
     xmlns:android="http://schemas.android.com/apk/res/android"
     xmlns:app="http://schemas.android.com/apk/res-auto"
     android:id="@+id/signature_pad"
     android:layout_width="match_parent"
     android:layout_height="match_parent"
     app:penColor="@android:color/black"
     />
```

2. 설정값은 아래와 같습니다.
 * `penMinWidth` - 최소 선 굵기 (default: 3dp).
 * `penMaxWidth` - 최대 선 굵기 (default: 7dp).
 * `penColor` - 필기 펜 색상 (default: Color.BLACK).
 * `velocityFilterWeight` - 속도 가중치 값 (default: 0.9).
 * `clearOnDoubleClick` - 뷰 객체를 두번 터치할때 뷰를 초기화 하는지에 대한 여부 (default: false)

3. 서명 객체의 이벤트 핸들링

 `OnSignedListener` 예제입니다:
 ```java
 mSignaturePad = (SignaturePad) findViewById(R.id.signature_pad);
 mSignaturePad.setOnSignedListener(new SignaturePad.OnSignedListener() {

      @Override
      public void onStartSigning() {
          // 서명 뷰 객체가 터치되어 그려지기 시작할때
      }

     @Override
     public void onSigned() {
         // 터치가 끝났을때
     }

     @Override
     public void onClear() {
         // 서명 뷰 객체가 초기화(Clear)될 때
     }
 });
 ```

4. 서명 뷰 객체에서 이미지를 출력하는 메소드입니다.
 * `getSignatureBitmap()` - Bitmap 형태로 서명 이미지를 얻습니다.
 * `getTransparentSignatureBitmap()` - 배경이 투명한 서명 이미지를 Bitmap 형태로 얻습니다.
 * `getSignatureSvg()` - 벡터 서명 이미지를 얻습니다. 이미지 형태는 Svg 입니다.

## XML 데이터 바인딩(Data Binding)

`SignaturePad` 뷰 객체에 XML 속성으로 이벤트 핸들링이 가능합니다:

```xml
 <com.github.gcacace.signaturepad.views.SignaturePad
     xmlns:android="http://schemas.android.com/apk/res/android"
     xmlns:bind="http://schemas.android.com/apk/res-auto"
     android:id="@+id/signature_pad"
     android:layout_width="match_parent"
     android:layout_height="match_parent"
     bind:onStartSigning="@{activity.onStartSigning}"
     bind:onSigned="@{activity.onSigned}"
     bind:onClear="@{activity.onClear}" />
```

## Cordova 플러그인

[netinhoteixeira](https://github.com/netinhoteixeira/)님 감사합니다.
우리의 라이브러리를 사용한 Cordova 플러그인입니다.
https://github.com/netinhoteixeira/cordova-plugin-signature-view 링크를 확인하세요.

## NativeScript 플러그인
[bradmartin](https://github.com/bradmartin)님 감사합니다.
NativeScript 플러그인입니다.
[https://github.com/bradmartin/nativescript-signaturepad](https://github.com/bradmartin/nativescript-signaturepad) 링크를 확인하세요.

## 주의사항

현재 화면 돌림 상황에서 정상 작동을 기대하기 어렵습니다.
누군가 풀 리퀘스트(Pull Request) 해주시면 감사하겠습니다!

## 라이센스

    Copyright 2014-2016 Gianluca Cacace

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
