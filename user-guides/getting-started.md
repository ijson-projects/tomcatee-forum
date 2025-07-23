# 🚀 Getting Started with TomcatEE

Welcome to TomcatEE! This guide will help you get up and running with the TomcatEE VSCode extension in just a few minutes.

## 📋 Prerequisites

Before you begin, make sure you have:

- **VSCode** 1.74.0 or higher
- **Apache Tomcat** 8.5+ or 9.0+
- **Java** 8 or higher (JDK recommended)
- **Maven** or **Gradle** (for project building)

## 🔧 Installation

### Step 1: Install the Extension

1. Open VSCode
2. Go to Extensions view (`Ctrl+Shift+X`)
3. Search for "TomcatEE"
4. Click "Install" on the TomcatEE extension by ijson

Alternatively, install from the [VSCode Marketplace](https://marketplace.visualstudio.com/items?itemName=ijson.tomcatee).

### Step 2: Verify Installation

After installation, you should see:
- TomcatEE icon in the Activity Bar (left sidebar)
- "Tomcat EE" commands in the Command Palette (`Ctrl+Shift+P`)

## 🏗️ First-Time Setup

### Step 1: Configure Global Settings

1. Open Command Palette (`Ctrl+Shift+P`)
2. Run "Tomcat EE: Open Settings"
3. Configure the following:

#### Default Paths
- **Default Tomcat Path**: Point to your Tomcat installation directory
  ```
  Example: /usr/local/tomcat or C:\apache-tomcat-9.0.100
  ```
- **Default JRE Path**: Point to your Java installation
  ```
  Example: /usr/lib/jvm/java-11-openjdk or C:\Program Files\Java\jdk-11.0.1
  ```

#### Port Configuration
- **Port Range**: Default ports for new instances (usually 8080-8090)
- **Auto Port Detection**: Enable automatic port conflict resolution

### Step 2: Create Your First Tomcat Instance

1. Click the TomcatEE icon in the Activity Bar
2. Click the "+" button or run "Tomcat EE: Create Instance"
3. Follow the Instance Creation Wizard:

#### Basic Information
- **Instance Name**: Give your instance a descriptive name (e.g., "MyWebApp")
- **Description**: Optional description for the instance

#### Paths Configuration
- **Tomcat Path**: Use default or browse to specific Tomcat installation
- **JRE Path**: Use default or browse to specific Java installation
- **Working Directory**: Choose where instance files will be stored

#### Port Configuration
- **HTTP Port**: Default 8080 (will auto-adjust if occupied)
- **HTTPS Port**: Default 8443
- **AJP Port**: Default 8009
- **JMX Port**: Default 8050
- **Shutdown Port**: Default 8005

#### JVM Settings
- **Min Heap Size**: 256m (adjust based on your needs)
- **Max Heap Size**: 512m (adjust based on your needs)
- **Additional JVM Args**: Optional JVM parameters

4. Click "Create Instance"

## 📦 Deploy Your First Project

### For Maven Projects

1. **Open your Maven web project** in VSCode
2. **Right-click on the project folder** in Explorer
3. **Select "Deploy to Tomcat"**
4. **Choose your Tomcat instance**
5. **Wait for deployment to complete**

### For Gradle Projects

1. **Open your Gradle web project** in VSCode
2. **Right-click on the project folder** in Explorer
3. **Select "Deploy to Tomcat"**
4. **Choose your Tomcat instance**
5. **Wait for deployment to complete**

### Manual Deployment

1. **Build your project** to generate a WAR file
2. **Right-click on your Tomcat instance**
3. **Select "Deploy WAR File"**
4. **Browse and select your WAR file**
5. **Choose deployment context path**

## 🚀 Start Your Application

### Normal Mode

1. **Select your Tomcat instance** in the TomcatEE view
2. **Click the ▶️ Start button**
3. **Wait for startup to complete** (watch the status indicator)
4. **Access your application** at `http://localhost:8080/your-app`

### Debug Mode

1. **Set breakpoints** in your Java code (click line numbers)
2. **Select your Tomcat instance**
3. **Click the 🐛 Debug button**
4. **Press F5** when prompted to connect the debugger
5. **Access your application** to trigger breakpoints

## 🔥 Enable Hot Deployment

Hot deployment automatically redeploys your application when files change.

### Enable Hot Deploy

1. **Right-click your Tomcat instance**
2. **Select "Configure Instance"**
3. **Go to "Deploy Settings" tab**
4. **Enable "Hot Deploy"**
5. **Configure file watching patterns**:
   - **Watch Extensions**: `java,jsp,html,css,js,xml,properties`
   - **Exclude Directories**: `target,build,node_modules,.git`
   - **Deploy Delay**: 1000ms (adjust as needed)

### How It Works

1. **Make changes** to your source files
2. **Save the files** (`Ctrl+S`)
3. **Watch the automatic rebuild** in the output panel
4. **See your changes** reflected immediately in the browser

## 🌐 Browser Integration

### Auto-Open Browser

1. **Configure browser settings** in instance configuration
2. **Choose browser type**:
   - System Default
   - Chrome
   - Firefox
   - Edge
   - Custom (specify path)
3. **Set default page** (e.g., `/index.jsp`)
4. **Enable auto-open** on startup

### Manual Browser Opening

- **Right-click instance** → "Open in Browser"
- **Use the 🌐 browser button** in the instance view
- **Access directly** at `http://localhost:[port]/[context]`

## 📊 Monitor Your Application

### Instance Status

Monitor your instance status in real-time:
- 🟢 **Running** - Instance is active and serving requests
- 🟡 **Starting** - Instance is in startup process
- 🔴 **Stopped** - Instance is not running
- ⚠️ **Error** - Instance encountered an error

### View Logs

1. **Right-click your instance**
2. **Select "View Logs"**
3. **Choose log type**:
   - **Catalina Log** - Main Tomcat log
   - **Application Log** - Your application's log output
   - **Access Log** - HTTP request log

### Performance Monitoring

- **Memory Usage** - Monitor JVM heap usage
- **Thread Count** - Active thread monitoring
- **Request Statistics** - HTTP request metrics (if JMX enabled)

## 🔧 Common Tasks

### Restart Instance
- **Right-click instance** → "Restart"
- **Or use the 🔄 restart button**

### Stop Instance
- **Right-click instance** → "Stop"
- **Or use the ⏹️ stop button**

### Clean Deployment
- **Right-click instance** → "Clean Deploy"
- **Removes old deployment** and redeploys fresh

### Update Configuration
- **Right-click instance** → "Configure Instance"
- **Modify settings** as needed
- **Apply changes** (may require restart)

## 🆘 Troubleshooting

### Common Issues

#### Port Already in Use
- **Check port availability** in instance configuration
- **Use "Suggest Available Ports"** feature
- **Manually change ports** if needed

#### Startup Failures
- **Check JRE path** is correct
- **Verify Tomcat installation** is valid
- **Review startup logs** for error details

#### Deployment Failures
- **Ensure project builds successfully**
- **Check WAR file is generated**
- **Verify deployment permissions**

#### Hot Deploy Not Working
- **Check file watching patterns**
- **Verify build tools are configured**
- **Ensure deployment delay is appropriate**

### Getting Help

If you encounter issues:

1. **Check the [Troubleshooting Guide](../troubleshooting/)**
2. **Search [existing discussions](../../discussions)**
3. **Ask for help** in the [community forum](../../discussions)
4. **Report bugs** in [bug reports](../../discussions/categories/bug-reports)

## 🎯 Next Steps

Now that you have TomcatEE set up:

1. **Explore [Advanced Configuration](../configuration/)**
2. **Learn about [Multi-Module Projects](../tutorials/multi-module-projects.md)**
3. **Master [Debug Features](../tutorials/debug-tutorial.md)**
4. **Optimize with [Hot Deployment](../tutorials/hot-deployment-guide.md)**

## 🤝 Join the Community

- 💬 **Join discussions** at [TomcatEE Forum](../../discussions)
- 🐛 **Report issues** to help improve TomcatEE
- 💡 **Suggest features** for future versions
- 📚 **Share your experiences** with other users

---

**Happy coding with TomcatEE! 🚀**

*Need more help? Visit our [community forum](../../discussions) or check out more [user guides](../user-guides/).*
