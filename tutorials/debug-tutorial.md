# 🐛 Debug Tutorial for TomcatEE

Learn how to effectively debug your Java web applications using TomcatEE's integrated debugging features.

## 🎯 What You'll Learn

- Setting up debug configuration
- Using breakpoints effectively
- Debugging different types of applications
- Troubleshooting debug connection issues
- Advanced debugging techniques

## 📋 Prerequisites

- TomcatEE extension installed
- Java web project (Maven/Gradle)
- Basic understanding of Java debugging concepts
- VSCode with Java Extension Pack

## 🚀 Quick Start Debugging

### Step 1: Enable Debug Mode

1. **Select your Tomcat instance** in the TomcatEE view
2. **Click the 🐛 Debug button** (not the regular Start button)
3. **Wait for the instance to start** in debug mode
4. **Look for debug port information** in the output

### Step 2: Set Breakpoints

1. **Open your Java source file**
2. **Click on the line number** where you want to pause execution
3. **A red dot appears** indicating a breakpoint is set
4. **Set multiple breakpoints** as needed

### Step 3: Connect Debugger

1. **Press F5** or go to Run → Start Debugging
2. **VSCode will automatically connect** to the debug port
3. **If prompted, select the debug configuration** (auto-created)
4. **You should see "Debugger attached" message**

### Step 4: Trigger Breakpoints

1. **Access your web application** in the browser
2. **Navigate to pages** that execute your breakpoint code
3. **VSCode will pause execution** when breakpoints are hit
4. **Inspect variables and step through code**

## 🔧 Debug Configuration

### Automatic Configuration

TomcatEE automatically creates debug configurations:

```json
{
    "type": "java",
    "name": "Debug Tomcat (MyInstance)",
    "request": "attach",
    "hostName": "localhost",
    "port": 5005,
    "projectName": "my-web-project"
}
```

### Manual Configuration

If automatic configuration doesn't work:

1. **Open .vscode/launch.json**
2. **Add debug configuration**:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "java",
            "name": "Debug Tomcat",
            "request": "attach",
            "hostName": "localhost",
            "port": 5005,
            "projectName": "your-project-name"
        }
    ]
}
```

### Debug Port Configuration

1. **Right-click your instance** → Configure Instance
2. **Go to JVM Settings**
3. **Enable Debug Mode**
4. **Set Debug Port** (default: 5005)
5. **Choose Debug Suspend** option:
   - **Yes**: Wait for debugger before starting
   - **No**: Start immediately, debugger can attach later

## 🎯 Debugging Different Application Types

### Spring Boot Applications

#### Configuration
```java
// application.properties
debug=true
logging.level.org.springframework=DEBUG
```

#### Common Breakpoints
- Controller methods
- Service layer methods
- Configuration classes
- Exception handlers

#### Example Debug Session
```java
@RestController
public class UserController {
    
    @GetMapping("/users/{id}")
    public User getUser(@PathVariable Long id) {
        // Set breakpoint here
        User user = userService.findById(id);
        // Set another breakpoint here
        return user;
    }
}
```

### JSP/Servlet Applications

#### Servlet Debugging
```java
@WebServlet("/hello")
public class HelloServlet extends HttpServlet {
    
    protected void doGet(HttpServletRequest request, 
                        HttpServletResponse response) {
        // Set breakpoint here
        String name = request.getParameter("name");
        // Set breakpoint here
        response.getWriter().println("Hello " + name);
    }
}
```

#### JSP Debugging
- Set breakpoints in scriptlets `<% %>`
- Debug included JSP files
- Inspect request/session attributes

### Maven Multi-Module Projects

#### Module Dependencies
1. **Ensure all modules are compiled** with debug info
2. **Check source attachment** for dependencies
3. **Verify classpath** includes all modules

#### Debug Configuration
```xml
<!-- In parent pom.xml -->
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <configuration>
        <debug>true</debug>
        <debuglevel>lines,vars,source</debuglevel>
    </configuration>
</plugin>
```

## 🔍 Advanced Debugging Techniques

### Conditional Breakpoints

1. **Right-click on a breakpoint**
2. **Select "Edit Breakpoint"**
3. **Add condition**:
   ```java
   user.getId() == 123
   user.getName().equals("admin")
   request.getParameter("debug") != null
   ```

### Logpoints

1. **Right-click on line number**
2. **Select "Add Logpoint"**
3. **Enter log message**:
   ```
   User ID: {user.getId()}, Name: {user.getName()}
   Request URI: {request.getRequestURI()}
   ```

### Exception Breakpoints

1. **Go to Run → Add Configuration**
2. **Add exception breakpoint**:
   ```json
   {
       "type": "java",
       "name": "Debug Exceptions",
       "request": "attach",
       "hostName": "localhost",
       "port": 5005,
       "stopOnEntry": false,
       "exceptionBreakpoints": [
           "java.lang.NullPointerException",
           "java.sql.SQLException"
       ]
   }
   ```

### Remote Debugging

For debugging on remote servers:

```json
{
    "type": "java",
    "name": "Debug Remote Tomcat",
    "request": "attach",
    "hostName": "remote-server.com",
    "port": 5005,
    "timeout": 30000
}
```

## 🛠️ Debug Tools and Features

### Variable Inspection

- **Variables Panel**: View local variables and their values
- **Watch Panel**: Monitor specific expressions
- **Call Stack**: See method call hierarchy
- **Breakpoints Panel**: Manage all breakpoints

### Step Controls

- **Step Over (F10)**: Execute current line
- **Step Into (F11)**: Enter method calls
- **Step Out (Shift+F11)**: Exit current method
- **Continue (F5)**: Resume execution

### Debug Console

Execute expressions during debugging:
```java
// Evaluate expressions
user.getName()
request.getSession().getAttribute("userId")
System.getProperty("java.version")

// Modify variables
user.setName("newName")
```

### Hot Code Replace

1. **Modify Java code** while debugging
2. **Save the file** (Ctrl+S)
3. **VSCode will hot-swap** the code if possible
4. **Continue debugging** with new code

## 🆘 Troubleshooting Debug Issues

### Debug Port Connection Failed

**Problem**: Cannot connect to debug port
**Solutions**:
1. Check if Tomcat started in debug mode
2. Verify debug port is not blocked by firewall
3. Ensure no other process is using the debug port
4. Check if debug port matches configuration

### Breakpoints Not Hit

**Problem**: Breakpoints are ignored
**Solutions**:
1. Verify source code matches deployed code
2. Check if classes are compiled with debug info
3. Ensure breakpoints are in executable code
4. Verify classpath and source paths

### Source Code Not Found

**Problem**: "Source not found" during debugging
**Solutions**:
1. Check source attachment in project settings
2. Verify project build path
3. Ensure source folders are correctly configured
4. Check if JAR files have source attachments

### Debug Session Disconnects

**Problem**: Debugger disconnects unexpectedly
**Solutions**:
1. Increase debug timeout settings
2. Check network connectivity (for remote debugging)
3. Verify Tomcat instance stability
4. Check for memory issues

## 📊 Debug Performance Tips

### Optimize Debug Performance

1. **Limit breakpoints**: Remove unnecessary breakpoints
2. **Use conditional breakpoints**: Reduce breakpoint hits
3. **Disable hot code replace**: If not needed
4. **Increase memory**: For large applications

### Debug Configuration Tuning

```json
{
    "type": "java",
    "name": "Optimized Debug",
    "request": "attach",
    "hostName": "localhost",
    "port": 5005,
    "timeout": 30000,
    "stepFilters": {
        "skipClasses": ["java.*", "javax.*"],
        "skipSynthetics": true
    }
}
```

## 🎯 Best Practices

### Development Workflow

1. **Start with simple breakpoints**
2. **Use logging for complex scenarios**
3. **Test debug configuration early**
4. **Keep debug sessions short**
5. **Document debug procedures**

### Team Debugging

1. **Share debug configurations** in version control
2. **Document debug procedures** for team members
3. **Use consistent debug ports** across team
4. **Create debug profiles** for different environments

### Production Debugging

1. **Never enable debug in production**
2. **Use remote debugging carefully**
3. **Limit debug access** to authorized personnel
4. **Monitor debug performance impact**

## 🔗 Related Resources

- [Instance Configuration](../configuration/instance-configuration.md)
- [Hot Deployment Guide](hot-deployment-guide.md)
- [Multi-Module Projects](multi-module-projects.md)
- [Troubleshooting Guide](../troubleshooting/)

## 🤝 Getting Help

If you encounter debugging issues:

1. **Check the [Troubleshooting Guide](../troubleshooting/debug-issues.md)**
2. **Search [community discussions](../../discussions)**
3. **Ask for help** in the [forum](../../discussions)
4. **Report bugs** in [bug reports](../../discussions/categories/bug-reports)

---

**Happy debugging with TomcatEE! 🐛**

*Master debugging to become more productive in your Java web development workflow.*
