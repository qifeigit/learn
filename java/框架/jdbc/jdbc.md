 A.载入JDBC驱动程序

String driver = "oracle.jdbc.driver.OracleDriver";

B.定义连接URL

String url = "jdbc:oracle:thin:@127.0.0.1:1521:DB_NAME";

C.建立连接



String username= "zhouchuandong";

String password = "xiaodong728";

Connection conn = DriverManager.getConnection(url,username,password);

D.创建Statement对象

Statement stmt = conn.createStatement();

 E.执行查询或更新SQL

String sql = "insert into student1 (id , name,sex ) values (1002,'黄国国','男')";

stmt.addBatch(sql);

F.结果处理

int[] count =stmt.executeBatch();
if(count.length>0){
System.out.println("加入成功！");
}

 G.关闭连接

conn.rollback();
stmt.close();

conn.close();