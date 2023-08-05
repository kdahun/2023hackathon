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



잘 모르겠으면 googole 액티비티? google맵 선택후 API만 Manifest에 넣어주기


## 메인 엑티비티 정리
        public class MapsActivity extends FragmentActivity implements OnMapReadyCallback {
        
            private GoogleMap mMap;
            private ActivityMapsBinding binding;
        
            @Override
            protected void onCreate(Bundle savedInstanceState) {
                super.onCreate(savedInstanceState);
        
                // 엑티비티에 연결된 레이아웃 파일인 activity_maps.xml을 사용하여 데이터 바인딩을 수행한다.
                // 데이터 바인딩을 사용하면 레이아웃의 뷰들을 쉽게 참조하고 조작할 수 있다.
                binding = ActivityMapsBinding.inflate(getLayoutInflater());
        
                // 엑티비티에 보여질 레이아웃을 설정한다.
                // bind.getRoot()는 데이터 바인딩을 통해 생성된 레이아웃의 최상위 뷰를 반환하는 메서드이다.
                // 따라서 이 코드로 인해 activity_maps.xml의 내용이 화면에 보여지게 된다.
                setContentView(binding.getRoot());
        
                // SupportMapFragment를 생성하고 지도를 보여주기 위해 사용할 지도 플래그먼트를 찾는다.
                // getSupportFragmentManager()를 통해 액티비티의 지도 플래그먼트 관리자를 가져온다.
                // findFragmentById(R.id.map)를 사용하여 레이아웃 파일에서 정의된 R.id.map ID를 가진 플래그먼트를 찾는다.
                SupportMapFragment mapFragment = (SupportMapFragment) getSupportFragmentManager()
                        .findFragmentById(R.id.map);
        
                // getMapAsync() 메서드를 호출하여 비동기적으로 Google 지도를 로드한다.
                // 로드가 완료되면 this로 지정된 현재 액티비티를 통해 onMapReady() 메서드를 호출한다.
                // 이를 통해 지도가 사용 가능한 상태가 되었을 때 앱에서 원하는 작업을 수행할 수 있다.
                mapFragment.getMapAsync(this);
            }
        
            // 안드로이드 앱에서 Google지도를 사용할때 onMapReady 메서드 내에서 호출되는 콜백 함수이다.
            // onMapReady는 지도가 완전히 로드외었을 때 호출되며, 이때 지도의 초기 설정과 마커 추가, 카메라 이동 등 초기화 작업을 수행할 수 있다.
            @Override
            public void onMapReady(GoogleMap googleMap) {
                //mMap 변수에 GoogleMap 객체를 할당.(이 객체는 지도를 조작할 수 있는 메서드를 제공)
                mMap = googleMap;
        
        
                // Lating 클레스를 사용하여 위도와 경도입력
                LatLng sydney = new LatLng(-34, 151);
        
                // mMap.addMarker() 메서드를 사용하여 sydney위치에 마커 추가
                // 마커는 지도상에 특정 위치를 나타내는 아이콘을 표시하는 역할을 한다.(마커 이름 : Marker in Sydeny)
                mMap.addMarker(new MarkerOptions().position(sydney).title("Marker in Sydney"));
        
                // mMap.moveCamera() 메서드를 사용하여 카메라를 sydeny 위치로 이동시킨다.
                // 이렇게 하면 지도가 해당 위치를 중심으로 보여지게 된다.
                mMap.moveCamera(CameraUpdateFactory.newLatLng(sydney));
            }
        }
