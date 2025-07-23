# 🐛 TomcatEE 调试教程

学习如何使用 TomcatEE 的集成调试功能有效调试您的 Java Web 应用程序。

## 🎯 您将学到

- 设置调试配置
- 有效使用断点
- 调试不同类型的应用程序
- 排除调试连接问题
- 高级调试技巧

## 📋 前置要求

- 已安装 TomcatEE 扩展
- Java Web 项目（Maven/Gradle）
- 基本的 Java 调试概念理解
- 安装了 Java Extension Pack 的 VSCode

## 🚀 快速开始调试

### 步骤 1：启用调试模式

1. **在 TomcatEE 视图中选择您的 Tomcat 实例**
2. **点击 🐛 调试按钮**（不是常规的启动按钮）
3. **等待实例以调试模式启动**
4. **在输出中查看调试端口信息**

### 步骤 2：设置断点

1. **打开您的 Java 源文件**
2. **点击要暂停执行的行号**
3. **出现红点表示断点已设置**
4. **根据需要设置多个断点**

### 步骤 3：连接调试器

1. **按 F5** 或转到 运行 → 开始调试
2. **VSCode 将自动连接**到调试端口
3. **如果提示，选择调试配置**（自动创建）
4. **您应该看到"调试器已连接"消息**

### 步骤 4：触发断点

1. **在浏览器中访问您的 Web 应用程序**
2. **导航到执行断点代码的页面**
3. **当断点被触发时，VSCode 将暂停执行**
4. **检查变量并逐步执行代码**

## 🔧 调试配置

### 自动配置

TomcatEE 自动创建调试配置：

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

### 手动配置

如果自动配置不起作用：

1. **打开 .vscode/launch.json**
2. **添加调试配置**：

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

### 调试端口配置

1. **右键点击您的实例** → 配置实例
2. **转到 JVM 设置**
3. **启用调试模式**
4. **设置调试端口**（默认：5005）
5. **选择调试暂停选项**：
   - **是**：启动前等待调试器连接
   - **否**：立即启动，调试器可以稍后连接

## 🎯 调试不同类型的应用程序

### Spring Boot 应用程序

#### 配置
```java
// application.properties
debug=true
logging.level.org.springframework=DEBUG
```

#### 常见断点位置
- 控制器方法
- 服务层方法
- 配置类
- 异常处理器

#### 调试会话示例
```java
@RestController
public class UserController {
    
    @GetMapping("/users/{id}")
    public User getUser(@PathVariable Long id) {
        // 在此处设置断点
        User user = userService.findById(id);
        // 在此处设置另一个断点
        return user;
    }
}
```

### JSP/Servlet 应用程序

#### Servlet 调试
```java
@WebServlet("/hello")
public class HelloServlet extends HttpServlet {
    
    protected void doGet(HttpServletRequest request, 
                        HttpServletResponse response) {
        // 在此处设置断点
        String name = request.getParameter("name");
        // 在此处设置断点
        response.getWriter().println("Hello " + name);
    }
}
```

#### JSP 调试
- 在脚本片段 `<% %>` 中设置断点
- 调试包含的 JSP 文件
- 检查 request/session 属性

### Maven 多模块项目

#### 模块依赖
1. **确保所有模块都编译**包含调试信息
2. **检查依赖项的源码附件**
3. **验证类路径**包含所有模块

#### 调试配置
```xml
<!-- 在父 pom.xml 中 -->
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <configuration>
        <debug>true</debug>
        <debuglevel>lines,vars,source</debuglevel>
    </configuration>
</plugin>
```

## 🔍 高级调试技巧

### 条件断点

1. **右键点击断点**
2. **选择"编辑断点"**
3. **添加条件**：
   ```java
   user.getId() == 123
   user.getName().equals("admin")
   request.getParameter("debug") != null
   ```

### 日志点

1. **右键点击行号**
2. **选择"添加日志点"**
3. **输入日志消息**：
   ```
   用户 ID: {user.getId()}, 姓名: {user.getName()}
   请求 URI: {request.getRequestURI()}
   ```

### 异常断点

1. **转到 运行 → 添加配置**
2. **添加异常断点**：
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

### 远程调试

用于调试远程服务器：

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

## 🛠️ 调试工具和功能

### 变量检查

- **变量面板**：查看局部变量及其值
- **监视面板**：监控特定表达式
- **调用堆栈**：查看方法调用层次结构
- **断点面板**：管理所有断点

### 步进控制

- **单步跳过 (F10)**：执行当前行
- **单步进入 (F11)**：进入方法调用
- **单步跳出 (Shift+F11)**：退出当前方法
- **继续 (F5)**：恢复执行

### 调试控制台

在调试期间执行表达式：
```java
// 评估表达式
user.getName()
request.getSession().getAttribute("userId")
System.getProperty("java.version")

// 修改变量
user.setName("newName")
```

### 热代码替换

1. **在调试时修改 Java 代码**
2. **保存文件** (Ctrl+S)
3. **如果可能，VSCode 将热交换**代码
4. **使用新代码继续调试**

## 🆘 调试问题排除

### 调试端口连接失败

**问题**：无法连接到调试端口
**解决方案**：
1. 检查 Tomcat 是否以调试模式启动
2. 验证调试端口未被防火墙阻止
3. 确保没有其他进程使用调试端口
4. 检查调试端口是否与配置匹配

### 断点未被触发

**问题**：断点被忽略
**解决方案**：
1. 验证源代码与部署的代码匹配
2. 检查类是否使用调试信息编译
3. 确保断点在可执行代码中
4. 验证类路径和源路径

### 找不到源代码

**问题**：调试时"找不到源"
**解决方案**：
1. 检查项目设置中的源附件
2. 验证项目构建路径
3. 确保源文件夹配置正确
4. 检查 JAR 文件是否有源附件

### 调试会话断开

**问题**：调试器意外断开连接
**解决方案**：
1. 增加调试超时设置
2. 检查网络连接（用于远程调试）
3. 验证 Tomcat 实例稳定性
4. 检查内存问题

## 📊 调试性能提示

### 优化调试性能

1. **限制断点**：删除不必要的断点
2. **使用条件断点**：减少断点触发
3. **禁用热代码替换**：如果不需要
4. **增加内存**：用于大型应用程序

### 调试配置调优

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

## 🎯 最佳实践

### 开发工作流程

1. **从简单断点开始**
2. **对复杂场景使用日志记录**
3. **尽早测试调试配置**
4. **保持调试会话简短**
5. **记录调试程序**

### 团队调试

1. **在版本控制中共享调试配置**
2. **为团队成员记录调试程序**
3. **在团队中使用一致的调试端口**
4. **为不同环境创建调试配置文件**

### 生产调试

1. **永远不要在生产中启用调试**
2. **谨慎使用远程调试**
3. **限制调试访问**给授权人员
4. **监控调试性能影响**

## 🔗 相关资源

- [实例配置](../configuration/instance-configuration.md)
- [热部署指南](hot-deployment-guide-zh.md)
- [多模块项目](multi-module-projects-zh.md)
- [故障排除指南](../troubleshooting/)

## 🤝 获取帮助

如果遇到调试问题：

1. **查看 [故障排除指南](../troubleshooting/debug-issues-zh.md)**
2. **搜索 [社区讨论](../../discussions)**
3. **在 [论坛](../../discussions) 寻求帮助**
4. **在 [问题报告](../../discussions/categories/bug-reports) 中报告错误**

---

**使用 TomcatEE 愉快调试！🐛**

*掌握调试技能，提高您的 Java Web 开发工作流程效率。*
