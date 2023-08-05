1. File => Project Structure => Dependencise => app => + => Library Dependency => com.android.volley 검색해서 모듈가져오기?
2. 코드
     public class MainActivity extends AppCompatActivity {
    
      RequestQueue queue;
      TextView textView;
    
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_main);
    
    
          textView = findViewById(R.id.textView); //text 연결
          Button button = findViewById(R.id.button); // button 연결
    
          if(queue == null){
              queue = Volley.newRequestQueue(this); //
          }
    
          String url = "http://202.31.147.129:25003/weater.php"; // URL
    
          StringRequest stringRequest = new StringRequest(Request.Method.GET, url, new Response.Listener<String>() {
              @Override
              public void onResponse(String response) {
                  // 응답
                  textView.setText(response);
              }
          }, new Response.ErrorListener() {
              @Override
              public void onErrorResponse(VolleyError error) {
                  //에러
                  textView.setText("에러 : "+error.toString());
              }
          });
          button.setOnClickListener(new View.OnClickListener() {
              @Override
              public void onClick(View v) {
                  queue.add(stringRequest);
              }
          });
      }
    }
