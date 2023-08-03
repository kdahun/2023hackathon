    # Userinfo.php
    <?php
        $con = mysqli_connect("localhost", "DB아이디", "DB비밀번호", "DB이름(스키마이름)");
        mysqli_query($con, 'SET NAMES utf8'); 
        
        $userName = $_POST["userName"]; //입력받음
        $userAge = $_POST["userID"]; //입력받음
    
        $statement = mysqli_prepare($con, "INSERT INTO USER VALUES (?, ?)"); //DB에 값 저장
        mysqli_stmt_bind_param($statement, "ss", $userName, $userID); 
        mysqli_stmt_execute($statement);
    
        $response = array();
        $response["success"] = true;
    
        echo json_encode($response);
    ?> 
주어진 코드는 안드로이드 앱에서 전송한 사용자 정보를 PHP파일에서 MySQL 데이터베이스에 저장하는 코드이다.
안드로이드 앱에서 POST 방식으로 userName과 userID라는 키로 값을 봰면 PHP 파일에서 해당 값을 가져와서 MySQL 데이터베이스에 INSERT 한다.
해당 코드는 사용자 정보를 저장하기 위한 기본적인 형태의 PHP 코드이며
