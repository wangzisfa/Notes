# 【Java核心技术】之JDBC初步

## 什么是JDBC

> JDBC 是 java 中的用来连接数据库的 应用程序接口

早期 JDBC 为 **双层结构**

![image-20200428215256978](C:\Users\hp\AppData\Roaming\Typora\typora-user-images\image-20200428215256978.png)

后来有了中间层服务

![image-20200428215427963](C:\Users\hp\AppData\Roaming\Typora\typora-user-images\image-20200428215427963.png)





## 具体操作

这里使用 idea intellij + SQLite作为集成环境演示



要完成 java 中的数据库处理，需要“三层包装“ 数据库 ，

步骤：

1. 获取数据库所在位置（本地文件或服务器地址）的url
2. 加载驱动连接数据库
3. 增删改查







```java
package MyDatabase;

import java.sql.*;

public class TestBD {
	public static void main(String[] args) {
		Connection connection = null;
		Statement statement = null;
		ResultSet resultSet = null;
		try {
			Class.forName("org.sqlite.JDBC");//找到jar驱动
			connection = DriverManager.getConnection("jdbc:sqlite:C:\\Users\\hp\\IdeaProjects\\MyDB\\src\\MyDatabase\\Mydb.sqlite");
			statement = connection.createStatement();//连接

            //更改
			statement.executeUpdate("UPDATE example set name = 'fuck' WHERE id = 1;");
			//查询
            resultSet = statement.executeQuery("SELECT * FROM main.example");
			while (resultSet.next()) {
				System.out.println(resultSet.getInt("id") + " " + resultSet.getString("name"));
				System.out.println("------------------------------");
			}
		}catch (ClassNotFoundException | SQLException e) {
			e.getCause();
		}finally {
			try {
				statement.close();
				connection.close();
			}catch (SQLException e) {
				e.getErrorCode();
			}
		}
	}
}

```







