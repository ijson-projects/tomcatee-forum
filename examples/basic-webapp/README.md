# 📦 Basic Web Application Example

This example demonstrates how to create and deploy a simple Java web application using TomcatEE.

## 🎯 What You'll Learn

- Creating a basic Maven web project
- Configuring TomcatEE for deployment
- Setting up hot deployment
- Basic debugging setup

## 📋 Prerequisites

- TomcatEE extension installed in VSCode
- Java 8+ installed
- Maven 3.6+ installed
- Apache Tomcat 9.0+ installed

## 🏗️ Project Structure

```
basic-webapp/
├── pom.xml                     # Maven configuration
├── src/
│   └── main/
│       ├── java/
│       │   └── com/
│       │       └── example/
│       │           ├── HelloServlet.java
│       │           └── UserController.java
│       ├── resources/
│       │   └── application.properties
│       └── webapp/
│           ├── WEB-INF/
│           │   └── web.xml
│           ├── index.jsp
│           ├── hello.html
│           └── css/
│               └── style.css
└── README.md
```

## 🚀 Quick Start

### Step 1: Create Maven Project

```bash
mvn archetype:generate \
  -DgroupId=com.example \
  -DartifactId=basic-webapp \
  -DarchetypeArtifactId=maven-archetype-webapp \
  -DinteractiveMode=false
```

### Step 2: Update pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    
    <groupId>com.example</groupId>
    <artifactId>basic-webapp</artifactId>
    <version>1.0.0</version>
    <packaging>war</packaging>
    
    <name>Basic Web Application</name>
    <description>A simple web application for TomcatEE demonstration</description>
    
    <properties>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <servlet.version>4.0.1</servlet.version>
        <jsp.version>2.3.3</jsp.version>
    </properties>
    
    <dependencies>
        <!-- Servlet API -->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>${servlet.version}</version>
            <scope>provided</scope>
        </dependency>
        
        <!-- JSP API -->
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>javax.servlet.jsp-api</artifactId>
            <version>${jsp.version}</version>
            <scope>provided</scope>
        </dependency>
        
        <!-- JSTL -->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>
    </dependencies>
    
    <build>
        <finalName>basic-webapp</finalName>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>11</source>
                    <target>11</target>
                    <debug>true</debug>
                    <debuglevel>lines,vars,source</debuglevel>
                </configuration>
            </plugin>
            
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>3.2.3</version>
                <configuration>
                    <failOnMissingWebXml>false</failOnMissingWebXml>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

### Step 3: Create HelloServlet

```java
package com.example;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import java.time.LocalDateTime;

@WebServlet("/hello")
public class HelloServlet extends HttpServlet {
    
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) 
            throws ServletException, IOException {
        
        response.setContentType("text/html;charset=UTF-8");
        
        String name = request.getParameter("name");
        if (name == null || name.trim().isEmpty()) {
            name = "World";
        }
        
        try (PrintWriter out = response.getWriter()) {
            out.println("<!DOCTYPE html>");
            out.println("<html>");
            out.println("<head>");
            out.println("<title>Hello Servlet</title>");
            out.println("<link rel='stylesheet' type='text/css' href='css/style.css'>");
            out.println("</head>");
            out.println("<body>");
            out.println("<div class='container'>");
            out.println("<h1>Hello, " + name + "!</h1>");
            out.println("<p>Current time: " + LocalDateTime.now() + "</p>");
            out.println("<p><a href='index.jsp'>Back to Home</a></p>");
            out.println("</div>");
            out.println("</body>");
            out.println("</html>");
        }
    }
    
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) 
            throws ServletException, IOException {
        doGet(request, response);
    }
}
```

### Step 4: Create index.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE html>
<html>
<head>
    <title>Basic Web Application</title>
    <link rel="stylesheet" type="text/css" href="css/style.css">
</head>
<body>
    <div class="container">
        <h1>Welcome to Basic Web Application</h1>
        <p>This is a simple demonstration of TomcatEE deployment.</p>
        
        <div class="form-section">
            <h2>Try the Hello Servlet</h2>
            <form action="hello" method="get">
                <label for="name">Enter your name:</label>
                <input type="text" id="name" name="name" placeholder="Your name">
                <button type="submit">Say Hello</button>
            </form>
        </div>
        
        <div class="links-section">
            <h2>Quick Links</h2>
            <ul>
                <li><a href="hello">Hello Servlet (default)</a></li>
                <li><a href="hello?name=TomcatEE">Hello with parameter</a></li>
                <li><a href="hello.html">Static HTML page</a></li>
            </ul>
        </div>
        
        <div class="info-section">
            <h2>Application Info</h2>
            <p><strong>Server Info:</strong> <%= application.getServerInfo() %></p>
            <p><strong>Context Path:</strong> <%= request.getContextPath() %></p>
            <p><strong>Session ID:</strong> <%= session.getId() %></p>
        </div>
    </div>
</body>
</html>
```

### Step 5: Create CSS Styles

```css
/* css/style.css */
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 20px;
    background-color: #f5f5f5;
}

.container {
    max-width: 800px;
    margin: 0 auto;
    background-color: white;
    padding: 30px;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

h1 {
    color: #333;
    text-align: center;
    margin-bottom: 30px;
}

h2 {
    color: #555;
    border-bottom: 2px solid #007acc;
    padding-bottom: 10px;
}

.form-section {
    margin: 30px 0;
    padding: 20px;
    background-color: #f9f9f9;
    border-radius: 5px;
}

.form-section label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
}

.form-section input[type="text"] {
    width: 200px;
    padding: 8px;
    margin-right: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
}

.form-section button {
    padding: 8px 16px;
    background-color: #007acc;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.form-section button:hover {
    background-color: #005a9e;
}

.links-section ul {
    list-style-type: none;
    padding: 0;
}

.links-section li {
    margin: 10px 0;
}

.links-section a {
    color: #007acc;
    text-decoration: none;
    padding: 5px 10px;
    border: 1px solid #007acc;
    border-radius: 3px;
    display: inline-block;
}

.links-section a:hover {
    background-color: #007acc;
    color: white;
}

.info-section {
    margin-top: 30px;
    padding: 20px;
    background-color: #e8f4f8;
    border-radius: 5px;
}

.info-section p {
    margin: 5px 0;
}
```

## 🔧 TomcatEE Setup

### Step 1: Create Tomcat Instance

1. Open VSCode with your project
2. Open TomcatEE view (click TomcatEE icon in sidebar)
3. Click "+" to create new instance
4. Configure instance:
   - **Name**: "BasicWebApp"
   - **Tomcat Path**: Your Tomcat installation
   - **JRE Path**: Your Java installation
   - **HTTP Port**: 8080 (or auto-assign)

### Step 2: Deploy Project

1. Right-click on project folder in VSCode Explorer
2. Select "Deploy to Tomcat"
3. Choose "BasicWebApp" instance
4. Wait for deployment to complete

### Step 3: Start Instance

1. In TomcatEE view, select "BasicWebApp" instance
2. Click ▶️ Start button
3. Wait for startup to complete
4. Access application at `http://localhost:8080/basic-webapp`

## 🔥 Hot Deployment Setup

### Enable Hot Deploy

1. Right-click "BasicWebApp" instance
2. Select "Configure Instance"
3. Go to "Deploy Settings" tab
4. Enable "Hot Deploy"
5. Configure settings:
   ```
   Watch Extensions: java,jsp,html,css,js,xml,properties
   Exclude Directories: target,build,.git,.idea,.vscode
   Deploy Delay: 2000ms
   ```

### Test Hot Deploy

1. Start the instance
2. Open `src/main/webapp/index.jsp`
3. Modify the welcome message
4. Save the file (Ctrl+S)
5. Refresh browser to see changes immediately

## 🐛 Debug Setup

### Enable Debug Mode

1. Set breakpoints in `HelloServlet.java`
2. Click 🐛 Debug button (not Start)
3. Press F5 when prompted to connect debugger
4. Access `http://localhost:8080/basic-webapp/hello`
5. Debugger will pause at breakpoints

### Debug Configuration

TomcatEE automatically creates `.vscode/launch.json`:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "java",
            "name": "Debug BasicWebApp",
            "request": "attach",
            "hostName": "localhost",
            "port": 5005,
            "projectName": "basic-webapp"
        }
    ]
}
```

## 🧪 Testing the Application

### Manual Testing

1. **Home Page**: `http://localhost:8080/basic-webapp/`
2. **Hello Servlet**: `http://localhost:8080/basic-webapp/hello`
3. **With Parameter**: `http://localhost:8080/basic-webapp/hello?name=YourName`
4. **Static HTML**: `http://localhost:8080/basic-webapp/hello.html`

### Expected Results

- Home page displays welcome message and form
- Hello servlet responds with personalized greeting
- CSS styles are applied correctly
- Hot deployment works for file changes
- Debug breakpoints trigger correctly

## 🆘 Troubleshooting

### Common Issues

**Build Failures:**
```bash
# Clean and rebuild
mvn clean compile war:war
```

**Port Conflicts:**
- Use TomcatEE's "Suggest Available Ports" feature
- Check for other running Tomcat instances

**Deployment Issues:**
- Verify WAR file is generated in `target/` directory
- Check Tomcat logs for deployment errors
- Ensure proper file permissions

### Getting Help

- Check [Troubleshooting Guide](../../troubleshooting/)
- Ask in [Community Forum](../../discussions)
- Report issues in [Bug Reports](../../discussions/categories/bug-reports)

## 🎯 Next Steps

- Try [Spring Boot Integration](../spring-boot-example/)
- Learn [Multi-Module Projects](../multi-module-maven/)
- Explore [Advanced Features](../../tutorials/advanced-features.md)

---

**Happy coding with TomcatEE! 🚀**
