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

                
데이터베이스 출력

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



# 테이블 생성

        import pymysql
        
        conn = pymysql.connect(
            host='202.31.147.129',
            user='jisung',
            password='Wldnjs981212@@',
            db='weater',
            port=13306
        )
        
        sql = """CREATE TABLE IF NOT EXISTS wave (
        latitude FLOAT,
        longitude FLOAT,
        wavesize FLOAT,
        waveway VARCHAR(255),
        wavecycle FLOAT,
        windspeed FLOAT,
        windway VARCHAR(255)
        )"""
        
        try:
            with conn:
                with conn.cursor() as cur:
                    cur.execute(sql)
                    print("테이블 생성에 성공하였습니다.")
        except pymysql.err.InternalError as e:
            if e.args[0] == 1050:  # 1050은 'Table already exists' 오류 코드입니다.
                print("테이블이 이미 존재합니다. 기존 테이블을 사용합니다.")
            else:
                print("오류가 발생하여 테이블을 생성하지 못했습니다:", e)

# with을 사용함으로써 conn이 close되어서
# 다시 conn으로 연결을 해줘야된다.

        conn = pymysql.connect(
            host='202.31.147.129',
            user='jisung',
            password='Wldnjs981212@@',
            db='weater',
            port=13306
        )

# 테이블 확인
        with conn:
            with conn.cursor() as cur:
                cur.execute('SHOW TABLES')
                for data in cur:
                    print(data)
