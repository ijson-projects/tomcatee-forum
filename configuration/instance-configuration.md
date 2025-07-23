# ⚙️ Instance Configuration Guide

This guide covers all aspects of configuring individual Tomcat instances in TomcatEE.

## 🏗️ Accessing Instance Configuration

### Method 1: Right-Click Menu
1. Right-click on any Tomcat instance in the TomcatEE view
2. Select "Configure Instance"
3. The configuration panel will open

### Method 2: Instance Actions
1. Select a Tomcat instance
2. Click the ⚙️ settings icon in the instance toolbar
3. The configuration panel will open

## 📋 Configuration Sections

### 🔧 Basic Settings

#### Instance Information
- **Name**: Display name for the instance
- **Description**: Optional description for documentation
- **Instance Path**: Working directory for this instance
- **Base Tomcat Path**: Path to the Tomcat installation

#### Status Information
- **Current Status**: Running/Stopped/Starting/Error
- **Process ID**: System process ID when running
- **Created**: Instance creation timestamp
- **Last Modified**: Last configuration change

### 🌐 Port Configuration

#### HTTP Ports
- **HTTP Port**: Main web server port (default: 8080)
- **HTTPS Port**: Secure web server port (default: 8443)
- **AJP Port**: Apache JServ Protocol port (default: 8009)

#### Management Ports
- **JMX Port**: Java Management Extensions port (default: 8050)
- **Shutdown Port**: Tomcat shutdown command port (default: 8005)
- **Debug Port**: Java debug wire protocol port (auto-assigned)

#### Port Management Features
- **Auto-Detection**: Automatically find available ports
- **Conflict Resolution**: Suggest alternative ports when conflicts occur
- **Port Validation**: Real-time validation of port availability

### ☕ JVM Configuration

#### Memory Settings
- **Min Heap Size**: Initial heap memory allocation
  ```
  Examples: 256m, 512m, 1g, 2g
  ```
- **Max Heap Size**: Maximum heap memory allocation
  ```
  Examples: 512m, 1g, 2g, 4g
  ```
- **PermGen Size**: Permanent generation memory (Java 7 and below)
  ```
  Examples: 128m, 256m, 512m
  ```
- **Metaspace Size**: Metaspace memory (Java 8+)
  ```
  Examples: 128m, 256m, 512m
  ```

#### JRE Settings
- **JRE Path**: Path to Java Runtime Environment
- **Java Version Detection**: Automatic detection of Java version
- **Compatibility Check**: Verify JRE compatibility with Tomcat

#### JVM Arguments
- **Additional JVM Args**: Custom JVM parameters
  ```
  Examples:
  -Dfile.encoding=UTF-8
  -Djava.awt.headless=true
  -Dspring.profiles.active=dev
  -Duser.timezone=UTC
  ```

#### Debug Configuration
- **Enable Debug**: Enable Java debugging support
- **Debug Port**: Port for debugger connection
- **Debug Suspend**: Wait for debugger before starting
- **JDWP Options**: Java Debug Wire Protocol settings

### 🌐 Browser Configuration

#### Browser Selection
- **System Default**: Use system default browser
- **Chrome**: Google Chrome
- **Firefox**: Mozilla Firefox
- **Edge**: Microsoft Edge
- **Custom**: Specify custom browser path

#### Browser Behavior
- **Auto Open**: Automatically open browser on startup
- **Default Page**: Initial page to load
  ```
  Examples: /, /index.jsp, /app/home
  ```
- **Custom Path**: Path to custom browser executable

### 🚀 Deployment Settings

#### Hot Deploy Configuration
- **Enable Hot Deploy**: Automatic redeployment on file changes
- **Watch Extensions**: File types to monitor
  ```
  Default: java,jsp,html,css,js,xml,properties
  ```
- **Exclude Directories**: Directories to ignore
  ```
  Default: target,build,node_modules,.git,.idea,.vscode
  ```
- **Deploy Delay**: Delay before redeployment (milliseconds)
  ```
  Recommended: 1000-3000ms
  ```

#### Build Settings
- **Auto Build**: Automatically build before deployment
- **Build Command**: Custom build command
- **Build Timeout**: Maximum build time (seconds)
- **Incremental Build**: Only rebuild changed modules

### 📊 Advanced Settings

#### Startup Configuration
- **Startup Timeout**: Maximum startup time (seconds)
- **Shutdown Timeout**: Maximum shutdown time (seconds)
- **Startup Args**: Additional startup arguments

#### Logging Configuration
- **Log Level**: Tomcat logging level
  ```
  Options: SEVERE, WARNING, INFO, CONFIG, FINE, FINER, FINEST
  ```
- **Log File Path**: Custom log file location
- **Log Rotation**: Enable log file rotation

#### Performance Tuning
- **Thread Pool Size**: HTTP connector thread pool
- **Connection Timeout**: HTTP connection timeout
- **Keep-Alive**: Enable HTTP keep-alive
- **Compression**: Enable response compression

## 🔧 Configuration Best Practices

### 🎯 Memory Configuration

#### Development Environment
```
Min Heap: 256m
Max Heap: 1g
Metaspace: 256m
```

#### Production Environment
```
Min Heap: 1g
Max Heap: 4g
Metaspace: 512m
```

#### Large Applications
```
Min Heap: 2g
Max Heap: 8g
Metaspace: 1g
```

### 🌐 Port Management

#### Single Instance
- Use default ports (8080, 8443, etc.)
- Enable auto-detection for conflicts

#### Multiple Instances
- Use port ranges (8080-8090, 8443-8453, etc.)
- Enable automatic port assignment
- Document port assignments

#### Production Deployment
- Use standard ports (80, 443)
- Configure reverse proxy if needed
- Secure management ports

### 🚀 Hot Deploy Settings

#### Small Projects
```
Deploy Delay: 1000ms
Watch Extensions: java,jsp,html,css,js
Build Timeout: 30s
```

#### Large Projects
```
Deploy Delay: 3000ms
Watch Extensions: java,jsp,html
Build Timeout: 300s
Incremental Build: Enabled
```

#### Multi-Module Projects
```
Deploy Delay: 5000ms
Watch Extensions: java,xml,properties
Build Timeout: 600s
Auto Build: Enabled
```

## 🔍 Configuration Validation

### Automatic Validation
TomcatEE automatically validates:
- Port availability and conflicts
- JRE path and version compatibility
- Tomcat installation validity
- Memory allocation limits
- File path accessibility

### Manual Validation
You can manually validate:
- **Test Ports**: Check if ports are available
- **Validate JRE**: Verify Java installation
- **Test Tomcat**: Validate Tomcat installation
- **Check Paths**: Verify all file paths exist

## 🆘 Common Configuration Issues

### Port Conflicts
**Problem**: Port already in use
**Solution**: 
1. Use "Suggest Available Ports" feature
2. Manually assign different ports
3. Stop conflicting services

### Memory Issues
**Problem**: OutOfMemoryError
**Solution**:
1. Increase max heap size
2. Increase metaspace size
3. Add memory monitoring

### JRE Compatibility
**Problem**: Unsupported Java version
**Solution**:
1. Update to supported Java version
2. Use compatible Tomcat version
3. Check version compatibility matrix

### Hot Deploy Problems
**Problem**: Changes not detected
**Solution**:
1. Check file watching patterns
2. Verify build configuration
3. Increase deploy delay
4. Check exclude patterns

## 📁 Configuration Files

### Instance Configuration
TomcatEE stores instance configuration in:
```
~/.vscode/extensions/ijson.tomcatee-*/instances/
├── instance-id.json          # Instance configuration
├── server.xml                # Tomcat server configuration
├── context.xml               # Application context
└── tomcat-users.xml          # User authentication
```

### Global Configuration
Global settings are stored in:
```
~/.vscode/extensions/ijson.tomcatee-*/config/
├── global-config.json        # Global settings
├── port-assignments.json     # Port allocations
└── user-preferences.json     # User preferences
```

## 🔄 Configuration Import/Export

### Export Configuration
1. Right-click instance → "Export Configuration"
2. Choose export location
3. Save as JSON file

### Import Configuration
1. Right-click in TomcatEE view → "Import Configuration"
2. Select configuration file
3. Review and confirm import

### Backup Configuration
1. Use "Export All Configurations" command
2. Save to version control
3. Regular backup schedule

## 🎯 Next Steps

- Learn about [Global Settings](global-settings.md)
- Explore [Port Management](port-management.md)
- Master [Hot Deployment](../tutorials/hot-deployment-guide.md)
- Understand [Debug Configuration](../tutorials/debug-tutorial.md)

---

**Need help with configuration? Visit our [community forum](../../discussions) or check the [troubleshooting guide](../troubleshooting/).**
