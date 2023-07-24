# 데이터베이스 만들기
        mydb = pymysql.connect(
            host="202.31.147.129",
            user='jisung',
            password="Wldnjs981212@@",
            port = 13306
        )
        
        mycursor = mydb.cursor()
        
        mycursor.execute("CREATE DATABASE weater")
* connect에 아이피, 사용자, 비밀번호, 포트번호를 넣어준다
* cursor() 메서드는 데이터베이스 연결 객체에서 커서를 생성하는 메서드이다. 커서는 SQL쿼리를 실행하고 데이터베이스와 상호작용하는데 사용되는 객체이다.
    1. SQL쿼리 실행 : 커서는 데이터베이스에 SQL 쿼리를 실행하는 데 사용된다. execute() 메서드를 통해 SQL 쿼리를 실행할 수 있으며, 결과를 반환받거나 데이터를 조작할 수 있다.
    2. 데이터 검색 : SELECT 문을 사용하여 데이터베이스에서 데이터를 검색할 때, 커서를 사용하여 검색된 결과를 읽을 수 있다.
    3. 데이터 추가/수정/삭제 : INSERT, UPDATE, DELETE 등의 쿼리를 실행하여 데이터를 추가,수정, 삭제하는데 사용된다.
    4. 트랜잭션 관리 : 커서를 사용하여 트랜잭션을 시작하고 커밋 또는 롤백하는 등의 트랜잭션 관리를 할 수 있다.

                mydb = pymysql.connect(
                    host="202.31.147.129",
                    user='jisung',
                    password="Wldnjs981212@@",
                    port = 13306
                )
                
                mycursor = mydb.cursor()
                
                mycursor.execute("SHOW DATABASES")
                
                for x in mycursor:
                    print(x)
  데이터베이스 출력

# 테이블 생성
    import pymysql
    
    conn = pymysql.connect(host = 'localhost',user = 'testuser', password = 'pas1234', db = 'testdb' , charset = 'utf8')
    
    sql = '''CREATE TABLE user(
      id int(11) NOT NULL AUTO_INCREMENT PRIMARY KEY,
      name varchar(255),
      email varchar(255)
      )'''
    
    with conn:
      with conn.cursor() as cur:
        cur.excute(sql)
        conn.comit()

