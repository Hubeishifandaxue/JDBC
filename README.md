//STEP 1. 导入必需的软件包
import java.sql.*;

public class FirstExample {
   // JDBC驱动程序名称和数据库URL 
   static final String JDBC_DRIVER = "com.mysql.jdbc.Driver";  
   static final String DB_URL = "jdbc:mysql://localhost/jdbc_a";

   //  数据库凭据 
   static final String USER = "root";
   static final String PASS = "nihao";

   public static void main(String[] args) {
   Connection conn = null;
   Statement stmt = null;
   try{
      //STEP 2: 注册JDBC驱动程序
      Class.forName(JDBC_DRIVER);

      //STEP 3: 打开连接 
      System.out.println("Connecting to database...");
      conn = DriverManager.getConnection(DB_URL,USER,PASS);

      //STEP 4: 执行查询 
      System.out.println("Creating statement...");
      stmt = conn.createStatement();
      String sql;
      sql = "SELECT id, name, email FROM custoner_tb1";
      ResultSet rs = stmt.executeQuery(sql);

      //STEP 5: 从结果集中提取数据 
      while(rs.next()){
         //按列检索 
         int id  = rs.getInt(1);
         String name = rs.getString(2);
         String email = rs.getString(3);

         //显示值 
         System.out.print("ID: " + id);
         System.out.print(", name: " + name);
         System.out.print(", email: " + email);
         System.out.println();
      }
      //STEP 6: 净化环境 
      rs.close();
      stmt.close();
      conn.close();
   }catch(SQLException se){
      //处理JDBC错误
      se.printStackTrace();
   }catch(Exception e){
      //处理类名称的错误 
      e.printStackTrace();
   }finally{
      //最后使用块来关闭资源
      try{
         if(stmt!=null)
            stmt.close();
      }catch(SQLException se2){
      }// 我们无能为力 
      try{
         if(conn!=null)
            conn.close();
      }catch(SQLException se){
         se.printStackTrace();
      }//最后尝试 
   }//end try
   System.out.println("There are so thing wrong!");
}//end main
}//end FirstExample