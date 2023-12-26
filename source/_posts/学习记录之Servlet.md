---
title: 学习记录之Servlet
date: 2023-12-20 19:36:59
tags: java
---

# 1 Servlet

## 1.2 调用流程

1. **客户端发起请求：** 客户端通过浏览器或其他客户端发送 HTTP 请求到服务器。
2. **Web服务器接收请求：** Web 服务器（如Tomcat）接收到客户端的请求。
3. **Servlet容器处理请求：** Servlet 容器（如Tomcat的Catalina）负责解析 HTTP 请求，确定请求的 Servlet，并调用相应的 Servlet。
4. **加载和实例化 Servlet：** 如果请求的 Servlet 尚未加载或实例化，Servlet 容器将加载并实例化相应的 Servlet 类。
5. **调用Servlet的service方法：** Servlet 容器调用 Servlet 的 `service` 方法，并将请求和响应对象传递给该方法。
6. **Servlet处理请求：** 在 `service` 方法中，开发人员编写的 Servlet 处理客户端的请求，生成响应内容。
7. **生成响应：** Servlet 通过操作响应对象生成 HTML 页面或其他类型的响应内容。
8. **发送响应给客户端：** Servlet 将生成的响应通过响应对象发送回客户端。
9. **Servlet容器处理响应：** Servlet 容器接收到 Servlet 生成的响应后，将其发送给客户端，完成整个请求-响应周期。

## 1.3 service（）

- `service` 方法是Servlet中处理请求的主要入口，负责分发请求到具体的处理方法。
- `doGet` 方法用于处理GET请求，适合从服务器获取数据。
- `doPost` 方法用于处理POST请求，适合向服务器提交数据。
- 一般情况下，如果你只关心一种请求类型，你可以选择只覆盖 `doGet` 或 `doPost` 中的一个。如果你需要处理两者，你可以覆盖 `service` 方法。

```java
import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class MyServlet extends HttpServlet {
    protected void service(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        if (request.getMethod().equals("GET")) {
            // 处理GET请求的逻辑
            doGet(request, response);
        } else if (request.getMethod().equals("POST")) {
            // 处理POST请求的逻辑
            doPost(request, response);
        }
        // 可以添加其他请求类型的处理逻辑
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // 处理GET请求的具体逻辑
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // 处理POST请求的具体逻辑
    }
}

```



# 2 第一个尝试

在webapp的包里创建一个html，设置好post请求以便于触发servlet。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form action="myweb" method="post">
        <div>
            <span>姓名:</span>
            <input name="name">

        </div>
        <div>
            <span>密码:</span>
            <input name="password">
        </div>
        <button type="submit">提交</button>
    </form>

</body>
</html>
```

在src/main/java/com/example/demo1这个目录下创建myweb.java实现doPost请求

```java
package com.example.demo1;

import com.sun.nio.sctp.AbstractNotificationHandler;
import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;

public class myweb extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //super.doPost(req, resp);
        String name = req.getParameter("name");
        String password = req.getParameter("password");
        System.out.println(name);
        System.out.println(password);
    }
}

```

在webapp下的WEB-INF中的web.xml配置好关联信息

```xml
		<servlet>
            <servlet-name>myweb</servlet-name>
            <servlet-class>com.example.demo1.myweb</servlet-class>
        </servlet>

        <servlet-mapping>
            <servlet-name>myweb</servlet-name>
            <url-pattern>/myweb</url-pattern>
        </servlet-mapping>

        <welcome-file-list>
            <welcome-file>myweb.html</welcome-file>
        </welcome-file-list>
```

==servlet-class在这里是全限定名==

启动tomcat之后可以观察到运行效果。

![image-20231220200342786](../images/image-20231220200342786.png)

证明我的post请求已经获取到了，开始进一步的学习。

## 2.2 页面跳转

服务端跳转

```java
package com.example.demo1;

import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;

public class tiaozhuan extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String name = req.getParameter("name");
        String password = req.getParameter("password");
        if(name.equals("姓名") && password.equals("123")){
            req.getRequestDispatcher("success.html").forward(req,resp);
        }else{
            req.getRequestDispatcher("fail.html").forward(req, resp);
        }
    }
}

```

客户端跳转

```java
package com.example.demo1;

import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;

public class tiaozhuan extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String name = req.getParameter("name");
        String password = req.getParameter("password");
        if(name.equals("姓名") && password.equals("123")){
            
            resp.sendRedirect("success.html");
        }else{
            
            resp.sendRedirect("fail.html");
        }
    }
}
```

## 2.3 自启动配置

在Servlet的`web.xml`配置文件中，`<load-on-startup>` 元素用于指定Servlet在应用启动时被加载的顺序。

```xml
<servlet>
    <servlet-name>MyServlet</servlet-name>
    <servlet-class>com.example.MyServlet</servlet-class>
    <load-on-startup>10</load-on-startup>
</servlet>
```

这里的 `<load-on-startup>` 元素中的值是一个整数，表示Servlet的加载顺序。当应用启动时，容器会按照 `<load-on-startup>` 的值的升序来加载Servlet。值越小，加载的越早。如果多个Servlet有相同的 `<load-on-startup>` 值，容器可以自由选择加载的顺序。

使用 `<load-on-startup>` 的情况通常包括：

1. **初始化操作：** 如果Servlet在启动时需要执行一些初始化工作，可以通过在 `<load-on-startup>` 中指定一个值，确保在应用启动时就加载该Servlet。(比如要加载数据库等等操作)
2. **确保顺序：** 在一些特定的场景，可能需要确保一些Servlet在应用启动时按照指定的顺序加载，以确保它们正确初始化。

## 2.4 request常用方法

`HttpServletRequest` 接口提供了一系列用于获取客户端请求信息的方法。以下是一些 `HttpServletRequest` 中常用的方法：

1. **获取请求行信息：**
   - `getMethod()`: 获取HTTP请求的方法，如GET、POST等。
   - `getRequestURI()`: 获取请求的URI，不包含查询字符串。
   - `getQueryString()`: 获取请求的查询字符串部分。
2. **获取请求头信息：**
   - `getHeader(String name)`: 获取指定名称的请求头的值。
   - `getHeaders(String name)`: 获取指定名称的请求头的所有值。
   - `getHeaderNames()`: 获取所有的请求头名称。
3. **获取请求参数：**
   - `getParameter(String name)`: 获取指定名称的请求参数的值。
   - `getParameterValues(String name)`: 获取指定名称的请求参数的所有值。
   - `getParameterMap()`: 获取所有请求参数的映射。
   - `getParameterNames()`: 获取所有请求参数的名称。
4. **获取客户端信息：**
   - `getRemoteAddr()`: 获取客户端的IP地址。
   - `getRemotePort()`: 获取客户端的端口号。
   - `getRemoteHost()`: 获取客户端的主机名。
5. **获取会话信息：**
   - `getSession()`: 获取与请求关联的会话对象。
   - `getSession(boolean create)`: 获取与请求关联的会话对象，如果不存在并且 `create` 为 `true`，则创建一个新的会话。
6. **获取其他信息：**
   - `getLocale()`: 获取客户端请求的语言环境。
   - `getInputStream()`: 获取请求的输入流，用于读取请求体的数据。
   - `getReader()`: 获取请求的Reader，用于读取请求体的数据。
   - `getServletContext()`: 获取Servlet上下文对象。

## 2.5 response常用方法

`HttpServletResponse` 接口提供了一系列用于设置响应的方法。以下是一些 `HttpServletResponse` 中常用的方法：

1. **设置响应内容类型和字符编码：**
   - `setContentType(String type)`: 设置响应的内容类型（MIME类型）。
   - `setCharacterEncoding(String charset)`: 设置响应的字符编码。
2. **设置响应状态和头信息：**
   - `setStatus(int sc)`: 设置响应的状态码，例如200表示成功。
   - `sendError(int sc, String msg)`: 发送一个错误响应。
   - `sendRedirect(String location)`: 发送一个重定向响应。
   - `addHeader(String name, String value)`: 添加一个响应头。
   - `setHeader(String name, String value)`: 设置一个响应头。
3. **设置响应内容：**
   - `getWriter()`: 获取一个 PrintWriter 对象，用于向客户端写入字符数据。
   - `getOutputStream()`: 获取一个 ServletOutputStream 对象，用于向客户端写入二进制数据。
   - `setCharacterEncoding(String charset)`: 设置字符编码。
   - `setContentLength(int len)`: 设置响应内容长度。
   - `setContentLengthLong(long len)`: 设置响应内容长度（长整型）。
   - `setBufferSize(int size)`: 设置响应缓冲区的大小。
4. **缓存控制：**
   - `setDateHeader(String name, long date)`: 设置响应头中日期字段的值。
   - `addDateHeader(String name, long date)`: 添加响应头中日期字段的值。
   - `setExpires(long expires)`: 设置响应过期的日期。
   - `addHeader(String name, String value)`: 添加响应头。
5. **Cookie：**
   - `addCookie(Cookie cookie)`: 添加一个Cookie到响应。
6. **重定向和错误处理：**
   - `sendRedirect(String location)`: 发送一个重定向响应。
   - `sendError(int sc)`: 发送一个错误响应。
7. **其他方法：**
   - `flushBuffer()`: 强制将响应的缓冲区内容发送到客户端。
   - `reset()`: 重置响应，清除所有设置。

# servlet配合JDBC的使用案例

## 制作查询

英雄类的创建

```java
package com.example.newgzwithjdbc;

public class Hero {
    private  int id;
    private String name;
    private float hp;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public float getHp() {
        return hp;
    }

    public void setHp(float hp) {
        this.hp = hp;
    }

    public int getDamage() {
        return damage;
    }

    public void setDamage(int damage) {
        this.damage = damage;
    }

    private int damage;

}

```

数据库链接

```java
package com.example.newgzwithjdbc;

import java.sql.*;
import java.util.ArrayList;
import java.util.List;

public class HeroDao {
    public HeroDao() {
        try{
            Class.forName("com.mysql.jdbc.Driver");
        }catch (ClassNotFoundException e){
            e.printStackTrace();
        }
    }

    public Connection getConnection() throws SQLException{
        return DriverManager.getConnection(
                "jdbc:mysql://127.0.0.1:3306/db_hero?characterEncoding=UTF-8",
                "root", "");	//密码就不放了
    }
    /**
     * 获取数量
     *
     * */
    public int getTotal(){
        int total = 0;
        try(Connection c = getConnection(); Statement s = c.createStatement()){
            String sql = "select count(*) from hero";
            ResultSet rs = s.executeQuery(sql);
            while(rs.next()){
                total = rs.getInt(1);
            }
            System.out.println("total:" + total);
        }catch (SQLException e){
            e.printStackTrace();
        }
        return total;
    }
    /**
     * 插入新英雄
     *
     * */
    public void addHero(Hero hero){
        String sql = "insert into hero values(null,?,?,?)";
        try(Connection c =getConnection(); PreparedStatement s = c.prepareStatement(sql);){
            s.setString(1, hero.getName());
            s.setFloat(2, hero.getHp());
            s.setInt(3, hero.getDamage());

            s.execute();

            ResultSet rs = s.getGeneratedKeys();
            if(rs.next()){
                int id = rs.getInt(1);
                hero.setId(id);
            }
        }catch (SQLException e){
            e.printStackTrace();
        }
    }
    /**
     * 更新操作
     *
     * */
    public void updateHero(Hero hero){
        String sql = "update hero set name= ?, hp = ?, damage = ? where id = ?";
        try(Connection c = getConnection(); PreparedStatement s = c.prepareStatement(sql)){
            s.setString(1, hero.getName());
            s.setFloat(2, hero.getHp());
            s.setInt(3, hero.getDamage());
            s.setInt(4, hero.getId());

            s.execute();
        }catch (SQLException e){
            e.printStackTrace();
        }
    }

    /**
     * 删除英雄
     *
     * */
    public void deleteHero(int id){
        try(Connection c = getConnection(); Statement s = c.createStatement();){
            String  sql = "delete from hero where id = " + id;
            s.execute(sql);
        }catch (SQLException e){
            e.printStackTrace();
        }
    }

    /*
    * 获取英雄
    *
    *
    * */
    public Hero get(int id) {
        Hero hero = null;

        try (Connection c = getConnection(); Statement s = c.createStatement();) {

            String sql = "select * from hero where id = " + id;

            ResultSet rs = s.executeQuery(sql);

            if (rs.next()) {
                hero = new Hero();
                String name = rs.getString(2);
                float hp = rs.getFloat("hp");
                int damage = rs.getInt(4);
                hero.setName(name);
                hero.setHp(hp);
                hero.setDamage(damage);
                hero.setId(id);
            }

        } catch (SQLException e) {

            e.printStackTrace();
        }
        return hero;
    }

    public List<Hero> list() {
        return list(0, Short.MAX_VALUE);
    }

    public List<Hero> list(int start, int count) {
        List<Hero> heros = new ArrayList<Hero>();

        String sql = "select * from hero order by id desc limit ?,? ";

        try (Connection c = getConnection(); PreparedStatement ps = c.prepareStatement(sql);) {

            ps.setInt(1, start);
            ps.setInt(2, count);

            ResultSet rs = ps.executeQuery();

            while (rs.next()) {
                Hero hero = new Hero();
                int id = rs.getInt(1);
                String name = rs.getString(2);
                float hp = rs.getFloat("hp");
                int damage = rs.getInt(4);
                hero.setName(name);
                hero.setHp(hp);
                hero.setDamage(damage);
                hero.setId(id);
                heros.add(hero);
            }
        } catch (SQLException e) {

            e.printStackTrace();
        }
        return heros;
    }



}

```

页面

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>111</title>
</head>
<body>
    <div style="color: green">这是数据</div>
    <form action="firstpage" method="post">
        <button>这是按钮</button>
    </form>

</body>
</html>
```

相应页面的servlet

```java
package com.example.newgzwithjdbc;

import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;
import java.util.List;

public class HelloListServlet extends HttpServlet {
    HeroDao heroDao = new HeroDao();
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
       List<Hero> heros = heroDao.list();

       StringBuffer sb = new StringBuffer();
       sb.append("<table align='center' border='1' cellspacing='0'>\r\n");
       sb.append("<tr><td>id</td><td>name</td><td>hp</td><td>damage</td></tr>\r\n");
       String trFormat = "<tr><td>%d</td><td>%s</td><td>%f</td><td>%d</td></tr>\r\n";
       for(Hero hero: heros){
           String tr = String.format(trFormat, hero.getId(), hero.getName(), hero.getHp(), hero.getDamage());
            sb.append(tr);
       }
       sb.append("</table>");
       resp.getWriter().print(sb.toString());
    }
}
```

进行xml映射

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
         version="5.0">
    <servlet>
        <servlet-name>HelloListServlet</servlet-name>
        <servlet-class>com.example.newgzwithjdbc.HelloListServlet</servlet-class>
    </servlet>
    
    <servlet-mapping>
        <servlet-name>HelloListServlet</servlet-name>
        <url-pattern>/firstpage</url-pattern>
    </servlet-mapping>
    <welcome-file-list>
        <welcome-file>firstpage.html</welcome-file>
    </welcome-file-list>
</web-app>
```

最终可以看到效果

![image-20231222094945598](../images/image-20231222094945598.png)

![image-20231222094953549](../images/image-20231222094953549.png)

## 英雄增加

准备要使用的英雄添加页面

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>addhero</title>
</head>
<body>
  <form method="post" action="addhero">
    <span>姓名：</span>
    <input type="text" name="name">
    <span>HP：</span>
    <input type="text" name="hp">
    <span>DAMAGE：</span>
    <input type="number" name="damage">
    <button type="submit" name="btn">
      提交
    </button>
  </form>
</body>
</html>
```

编写调addhero的action的servlet

```java
package com.example.newgzwithjdbc;

import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;

public class HeroAddServlet extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        Hero hero = new Hero();
        hero.setName(req.getParameter("name"));
        hero.setHp(Float.parseFloat(req.getParameter("hp")));
        hero.setDamage(Integer.parseInt(req.getParameter("damage")));

        HeroDao heroDao = new HeroDao();
        heroDao.addHero(hero);
        System.out.println(hero.getName());
        System.out.println(hero.getHp());
        System.out.println(hero.getDamage());

        resp.setContentType("text/html;charSet=UTF-8");
        StringBuffer sb = new StringBuffer();
        sb.append("<span>");
        sb.append(hero.getName());
        sb.append("</span>");
        resp.getWriter().print(sb.toString());


        try {
            Thread.sleep(2);
        }catch (InterruptedException e){
            e.printStackTrace();
        }
        /*最后重定向的是当前的上下文的根目录*/
        resp.sendRedirect(req.getContextPath()+ "/");

    }
}

```

添加xml配置

```xml
	<servlet>
        <servlet-name>AddHeroServlet</servlet-name>
        <servlet-class>com.example.newgzwithjdbc.HeroAddServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>AddHeroServlet</servlet-name>
        <url-pattern>/addhero</url-pattern>
    </servlet-mapping>
```



## 英雄删除

修改展示的servlet，提供删除的超连接

```java
	String trFormat = "<tr><td>%d</td><td>%s</td><td>%f</td><td>%d</td>" +
               "<td><a href='deleteHeroid?id=%d'>delete</a></td>" +
               "</tr>\r\n";
       for(Hero hero: heros){
           String tr = String.format(trFormat, hero.getId(), hero.getName(), hero.getHp(), hero.getDamage(), hero.getId());
            sb.append(tr);
       }
```

编写点击超连接删除的servlet

```java
package com.example.newgzwithjdbc;

import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;

public class HeroDeleteServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        int id = Integer.parseInt(req.getParameter("id"));

        new HeroDao().deleteHero(id);

        resp.sendRedirect(req.getContextPath() + "/firstpage");
    }
}
```

在xml文件中实现配置

```xml
	<servlet>
        <servlet-name>HeroDeleteServlet</servlet-name>
        <servlet-class>com.example.newgzwithjdbc.HeroDeleteServlet</servlet-class>
    </servlet>


    <servlet-mapping>
        <servlet-name>HeroDeleteServlet</servlet-name>
        <url-pattern>/deleteHeroid</url-pattern>
    </servlet-mapping>
```

## 英雄修改

对于每一个英雄表格，增加一个edit来修改，再将修改后的信息，存储，展示

修改展示的servlet

```java
	String trFormat = "<tr><td>%d</td><td>%s</td><td>%f</td><td>%d</td>" +
               "<td><a href='deleteHeroid?id=%d'>delete</a></td>" +
               "<td><a href='editHeroid?id=%d'>edit</a>" +
               "</tr>\r\n";
       for(Hero hero: heros){
           String tr = String.format(trFormat, hero.getId(), hero.getName(), hero.getHp(), hero.getDamage(), hero.getId(), hero.getId());
            sb.append(tr);
       }	
```

```java
package com.example.newgzwithjdbc;

import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;
import java.util.List;

public class HelloListServlet extends HttpServlet {
    HeroDao heroDao = new HeroDao();


    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
       List<Hero> heros = heroDao.list();

       StringBuffer sb = new StringBuffer();
       sb.append("<table align='center' border='1' cellspacing='0'>\r\n");
       sb.append("<tr><td>id</td><td>name</td><td>hp</td><td>damage</td></tr>\r\n");
       String trFormat = "<tr><td>%d</td><td>%s</td><td>%f</td><td>%d</td>" +
               "<td><a href='deleteHeroid?id=%d'>delete</a></td>" +
               "<td><a href='editHeroid?id=%d'>edit</a>" +
               "</tr>\r\n";
       for(Hero hero: heros){
           String tr = String.format(trFormat, hero.getId(), hero.getName(), hero.getHp(), hero.getDamage(), hero.getId(), hero.getId());
            sb.append(tr);
       }
       sb.append("</table>");
       resp.getWriter().print(sb.toString());
    }
}

```

每一次点击会调用不同的editHeroid？id=%d那么，首先是修改的servlet，能够获取修改后的信息

```java
package com.example.newgzwithjdbc;

import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;

public class HeroUpdateServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        int id = Integer.parseInt(req.getParameter("id"));
        HeroDao heroDao = new HeroDao();
        Hero hero = heroDao.get(id);

        StringBuffer sb = new StringBuffer();
        resp.setContentType("text/html; charSet=UTF-8");
        sb.append("<!DOCTYPE html>");

        sb.append("<form action='updateHero' method='post'>");
        sb.append("名字 ： <input type='text' name='name' value='%s' > <br>");
        sb.append("血量 ： <input type='text' name='hp'  value='%f' > <br>");
        sb.append("伤害： <input type='text' name='damage'  value='%d' > <br>");
        sb.append("<input type='hidden' name='id' value='%d'>");
        sb.append("<input type='submit' value='更新'>");
        sb.append("</form>");

        String html = String.format(sb.toString(), hero.getName(), hero.getHp(), hero.getDamage(), hero.getId());
        resp.getWriter().write(html);
    }
}

```

在上面的表格中完成修改后，点击更新之后就会调用updateHero的action，那么要再编写能处理updateHero的servlet。

```java
package com.example.newgzwithjdbc;

import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;

public class HeroUpdateToServlet extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        HeroDao heroDao = new HeroDao();
        Hero hero = new Hero();
        hero.setId(Integer.parseInt(req.getParameter("id")));
        hero.setName(req.getParameter("name"));
        hero.setHp(Integer.parseInt(req.getParameter("hp")));
        hero.setDamage(Integer.parseInt(req.getParameter("damage")));
        heroDao.updateHero(hero);

        resp.sendRedirect(req.getContextPath() + "/");
    }
}
```

在xml中进行配置

```xml
<servlet>
    <servlet-name>HeroUpdateServlet</servlet-name>
    <servlet-class>com.example.newgzwithjdbc.HeroUpdateServlet</servlet-class>
</servlet>

<servlet-mapping>
    <servlet-name>HeroUpdateServlet</servlet-name>
    <url-pattern>/editHeroid</url-pattern>
</servlet-mapping>

<servlet>
    <servlet-name>HeroUpdateToServlet</servlet-name>
    <servlet-class>com.example.newgzwithjdbc.HeroUpdateToServlet</servlet-class>
</servlet>

<servlet-mapping>
    <servlet-name>HeroUpdateToServlet</servlet-name>
    <url-pattern>/updateHero</url-pattern>
</servlet-mapping>
```

## 效果

初始页面（要的是逻辑，效果丑就丑点）

![image-20231226144359248](../images/image-20231226144359248.png)

添加数据

![image-20231226144426177](../images/image-20231226144426177.png)

查看数据

![image-20231226144507734](../images/image-20231226144507734.png)

删除id=11

![image-20231226144522865](../images/image-20231226144522865.png)

修改id=10

![image-20231226144542424](../images/image-20231226144542424.png)

![image-20231226144603734](../images/image-20231226144603734.png)
