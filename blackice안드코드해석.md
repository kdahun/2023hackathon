    private float distCondition(){
            float distance = nowLocate.distanceTo(markerLocate);
            Log.i("distance", "distance = " + distance);
            return distance;
    }
이 코드는 두 지점 간의 거리를 계간하는 함수이다.
nowLocate와 markerLocate는 안드로이드의 Location 객체로, 각각 현재 위치와 특정 마커(목표지점)의 위치를 나타낸다. 이 함수는 이 두 지점 사이의 거리를 계산하여 그 값을 반환한다.
distanceTo() 메서드는 Location 객체에서 제공하는 메서드로, 두 지점 간의 직선 거리를 계산한다. 이 거리는 미터 단위로 반환된다. 함수가 실행되면 거리가 계산되고, Log.i를 통해 Logcat에 거리가 출력된다.
앱에서 이 함수를 사용하면 현재 위치와 특정 마커와의 거리를 쉽게 알 수 있다. 이를 활용하여 사용자의 상호작용이나 위치 기반 기능을 구현할 수 있다. 
예를 들어, 특정 거리 이내에 마커가 있는지를 체크하여 특정 동작을 수행하거나, 가까운 마커를 찾는 등의 기능을 구현할 수 있다.

    private void getBlackIce() {
          new Thread(){
              @Override
              public void run() {
                  Spinner sItems = findViewById(R.id.spinner);
    
                  while (true) {
    
                      float dist = 10000.0f;
                      try {
    
                          long now = System.currentTimeMillis();
                          Date date = new Date(now);
                          SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd H");
                          String getTime = sdf.format(date);
    //                        Log.i("test", printDate());
                          Document doc = Jsoup.connect(URL).timeout(5000).get();
                          JSONObject json = new JSONObject(doc.body().text());
                          JSONArray blackiceArray = json.getJSONArray("blackice");
                          try {
                              mapView.removeAllPOIItems();
                          }catch (Exception e){
    
                          }
                          ArrayList<String> dateList = new ArrayList<String>();
    
                          for (int i = 0; i < blackiceArray.length(); i++) {
                              JSONObject blackiceObj = blackiceArray.getJSONObject(i);
                              blackiceData bld = new blackiceData();
                              double markerLatitude = Float.parseFloat(blackiceObj.getString("latitude"));
                              double markerLongtitude = Float.parseFloat(blackiceObj.getString("longitude"));
                              bld.setDatetime(blackiceObj.getString("datetime"));
                              bld.setLatitude(Float.parseFloat(blackiceObj.getString("latitude")));
                              bld.setLongitude(Float.parseFloat(blackiceObj.getString("longitude")));
                              bld.setIce_type(blackiceObj.getString("ice_type"));
                              try {
                                  markerLocate.setLatitude(markerLatitude);
                                  markerLocate.setLongitude(markerLongtitude);
    //                                Log.i("test","passed");
                                  String testValue = mapView.getCurrentLocationTrackingMode().toString();
                                  Log.i("test location", testValue);
    
                                  //                                nowLocate.setLatitude(35.94521);
                                  nowLocate.setLatitude(userLatitude);
                                  nowLocate.setLongitude(userLongitude);
    //                                nowLocate.setLongitude(126.68297);
                              }catch(Exception e){
    
                              }
    
                              blackiceList.add(bld);
                              // blackiceData 는 getter and setter 함수가 있어 저장함.
                              // 저장후에 blackiceList에 추가해 저장해줌
    
    
                              marker = new MapPOIItem();
                              marker.setTag(0);
                              try {
                                  marker.setMapPoint(
                                          MapPoint.mapPointWithGeoCoord(Float.parseFloat(blackiceObj.getString("latitude")),
                                                  Float.parseFloat(blackiceObj.getString("longitude")))
                                  );
                              }catch (Exception e) {
    
                              }
    
    
    
                              dateList.add(blackiceObj.getString("datetime"));
                              switch (blackiceObj.getString("ice_type")) {
    
                                  case "water":
                                      try {
                                          if (sItems.getSelectedItem().toString().substring(0,13).equals(blackiceObj.getString("datetime").substring(0,13))) {
                                              marker.setItemName("water");
                                              marker.setMarkerType(MapPOIItem.MarkerType.BluePin);
                                              marker.setSelectedMarkerType(MapPOIItem.MarkerType.RedPin);
                                              mapView.addPOIItem(marker);
                                              dist = distCondition();
                                              Log.d("except" , "distance:"+dist);
                                          }
                                      }
                                      catch(Exception e){
    //                                        Log.d("except", "except");
                                      }
    
                                      break;
    
                                  case "ice":
                                      try {
                                          if (sItems.getSelectedItem().toString().substring(0,13).equals(blackiceObj.getString("datetime").substring(0, 13))) {
                                              marker.setItemName("ice");
                                              marker.setMarkerType(MapPOIItem.MarkerType.YellowPin);
                                              marker.setSelectedMarkerType(MapPOIItem.MarkerType.RedPin);
                                              mapView.addPOIItem(marker);
                                              dist = distCondition();
                                              Log.d("except" , "distance:"+dist);
                                          }
                                      }catch (Exception e){
    //                                        Log.d("except" , "Except");
                                      }
    
                                      break;
    
                                  default:
                                      break;
                              }
                              if(dist < 100 && getTime.substring(0,13).equals(sItems.getSelectedItem().toString().substring(0, 13))){ // 만약 water 혹은 ice가 50m이내에 있을경우
                                  tone.startTone(ToneGenerator.TONE_DTMF_S, 1000);
                                  marker.setMarkerType(MapPOIItem.MarkerType.RedPin);
                                  mapView.addPOIItem(marker);
                              }
                          } // for문 끝
                          runOnUiThread(new Runnable(){
                              @Override
                              public void run() {
                                  returnSpinner(dateList);
                              }
                          });
    
    
                      } catch (IOException | JSONException e) {
    //                    Log.i("test", " error ");
                          e.printStackTrace();
                      }
    
                      try { // 시간지연
                          Thread.sleep(2000);
                      }catch (InterruptedException e){
                          Log.d("test", "time Error");
                      }
    
                  }
    
    
              }
    
    
          }.start();
    
      }
1. getBlackIce() 함수는 UI 스레드에서 호출된다. 함수 안에서는 새로운 쓰레드를 생성하여 네트워크 작업을 실행한다.(이렇게 별도의 쓰레드를 사용하는 이유는, 네트워크 작업의 시간이 오래 걸리는 경우에 메인 UI스레드를 블로킹하지 않고 앱이 끊김 없이 동작할 수 있도록 하기 위함이다.)
  * new Tread()를 통해 새로운 쓰레드를 생성한다.
2. 새로운 스레드의 run() 메서드에서는 무한루프를 톨면서 주기적으로 서버로부터 데이터를 가져온다.
    * System.current
