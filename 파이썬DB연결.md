
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

