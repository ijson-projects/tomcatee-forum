# 🚨 Tomcat Startup Issues Troubleshooting

This guide helps you diagnose and resolve common Tomcat startup problems in TomcatEE.

## 🔍 Quick Diagnosis

### Check Instance Status

1. **Open TomcatEE view** in VSCode
2. **Look at instance status indicator**:
   - 🟢 **Running** - Instance is healthy
   - 🟡 **Starting** - Instance is in startup process
   - 🔴 **Stopped** - Instance is not running
   - ⚠️ **Error** - Instance encountered an error

### View Startup Logs

1. **Right-click your instance**
2. **Select "View Logs"**
3. **Choose "Catalina Log"** for startup information
4. **Look for error messages** and stack traces

## 🚨 Common Startup Issues

### 1. Port Already in Use

#### Symptoms
```
Error: Port 8080 already in use
java.net.BindException: Address already in use
```

#### Solutions

**Option A: Use Different Ports**
1. Right-click instance → "Configure Instance"
2. Go to "Port Settings"
3. Click "Suggest Available Ports"
4. Apply new port configuration

**Option B: Find and Stop Conflicting Process**
```bash
# On Windows
netstat -ano | findstr :8080
taskkill /PID <process_id> /F

# On macOS/Linux
lsof -i :8080
kill -9 <process_id>
```

**Option C: Use TomcatEE Port Detection**
1. Enable "Auto Port Detection" in global settings
2. TomcatEE will automatically find available ports

### 2. Invalid JRE Path

#### Symptoms
```
Error: JAVA_HOME is not set
Error: Cannot find Java executable
java.lang.ClassNotFoundException
```

#### Solutions

**Check JRE Configuration**
1. Right-click instance → "Configure Instance"
2. Go to "JVM Settings"
3. Verify "JRE Path" points to valid Java installation
4. Click "Detect JRE" for automatic detection

**Valid JRE Paths Examples**
```
Windows: C:\Program Files\Java\jdk-11.0.1
macOS: /Library/Java/JavaVirtualMachines/jdk-11.0.1.jdk/Contents/Home
Linux: /usr/lib/jvm/java-11-openjdk
```

**Test JRE Installation**
```bash
# Test Java installation
java -version
javac -version

# Check JAVA_HOME
echo $JAVA_HOME  # macOS/Linux
echo %JAVA_HOME% # Windows
```

### 3. Invalid Tomcat Installation

#### Symptoms
```
Error: Catalina.sh not found
Error: Invalid Tomcat installation
ClassNotFoundException: org.apache.catalina.startup.Bootstrap
```

#### Solutions

**Verify Tomcat Installation**
1. Check Tomcat directory structure:
   ```
   tomcat/
   ├── bin/
   │   ├── catalina.sh (macOS/Linux)
   │   ├── catalina.bat (Windows)
   │   └── startup.sh/startup.bat
   ├── conf/
   │   ├── server.xml
   │   └── web.xml
   ├── lib/
   │   └── catalina.jar
   └── webapps/
   ```

**Update Tomcat Path**
1. Right-click instance → "Configure Instance"
2. Update "Base Tomcat Path"
3. Point to root Tomcat directory (not bin/)

**Download Valid Tomcat**
- Download from [Apache Tomcat](https://tomcat.apache.org/)
- Use version 8.5+ or 9.0+
- Extract to accessible location

### 4. Memory Issues

#### Symptoms
```
java.lang.OutOfMemoryError: Java heap space
java.lang.OutOfMemoryError: Metaspace
Error occurred during initialization of VM
```

#### Solutions

**Increase Memory Allocation**
1. Right-click instance → "Configure Instance"
2. Go to "JVM Settings"
3. Adjust memory settings:
   ```
   Min Heap Size: 512m
   Max Heap Size: 2g
   Metaspace Size: 256m
   ```

**Memory Recommendations**
```
Small Applications:
- Min Heap: 256m
- Max Heap: 1g
- Metaspace: 128m

Large Applications:
- Min Heap: 1g
- Max Heap: 4g
- Metaspace: 512m
```

### 5. Permission Issues

#### Symptoms
```
Permission denied
Access is denied
Cannot create directory
Cannot write to file
```

#### Solutions

**Windows Solutions**
1. Run VSCode as Administrator
2. Check folder permissions
3. Disable antivirus temporarily
4. Use different working directory

**macOS/Linux Solutions**
```bash
# Fix permissions
chmod +x tomcat/bin/*.sh
chown -R $USER:$USER tomcat/
chmod -R 755 tomcat/

# Check directory permissions
ls -la tomcat/
```

### 6. Firewall/Antivirus Blocking

#### Symptoms
```
Connection refused
Port blocked
Process terminated unexpectedly
```

#### Solutions

**Windows Firewall**
1. Open Windows Defender Firewall
2. Allow Java through firewall
3. Add exception for Tomcat ports
4. Add exception for VSCode

**Antivirus Software**
1. Add Tomcat directory to exclusions
2. Add Java executable to exclusions
3. Temporarily disable real-time protection
4. Check quarantine for blocked files

### 7. Configuration File Issues

#### Symptoms
```
XML parsing error in server.xml
Invalid configuration
Configuration file not found
```

#### Solutions

**Reset Configuration Files**
1. Right-click instance → "Reset Configuration"
2. Or manually restore from Tomcat installation:
   ```bash
   cp tomcat/conf/server.xml instance/conf/
   cp tomcat/conf/web.xml instance/conf/
   ```

**Validate XML Files**
1. Open server.xml in VSCode
2. Check for XML syntax errors
3. Validate against Tomcat schema
4. Fix malformed XML elements

## 🔧 Advanced Troubleshooting

### Enable Debug Logging

**Increase Log Level**
1. Edit `conf/logging.properties`
2. Set log level to FINE or FINEST:
   ```properties
   org.apache.catalina.level = FINE
   org.apache.coyote.level = FINE
   ```

**Add JVM Debug Arguments**
1. Right-click instance → "Configure Instance"
2. Add to "Additional JVM Args":
   ```
   -Djava.util.logging.config.file=conf/logging.properties
   -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager
   ```

### Check System Resources

**Monitor System Resources**
```bash
# Check available memory
free -h  # Linux
vm_stat # macOS

# Check disk space
df -h

# Check CPU usage
top
htop
```

**Java Process Monitoring**
```bash
# List Java processes
jps -v

# Monitor Java process
jstat -gc <pid>
jmap -histo <pid>
```

### Network Diagnostics

**Test Port Connectivity**
```bash
# Test if port is accessible
telnet localhost 8080
nc -zv localhost 8080

# Check listening ports
netstat -tlnp | grep :8080  # Linux
netstat -an | grep :8080    # macOS
netstat -an | findstr :8080 # Windows
```

## 📋 Startup Checklist

Before starting Tomcat, verify:

- [ ] **JRE Path** is valid and accessible
- [ ] **Tomcat Path** points to valid installation
- [ ] **Ports** are available and not blocked
- [ ] **Memory Settings** are appropriate
- [ ] **Permissions** allow read/write access
- [ ] **Configuration Files** are valid XML
- [ ] **Firewall/Antivirus** allows Java and Tomcat
- [ ] **System Resources** are sufficient

## 🆘 Getting Help

### Collect Diagnostic Information

When asking for help, provide:

1. **TomcatEE Version**: Check in Extensions view
2. **VSCode Version**: Help → About
3. **Java Version**: `java -version`
4. **Tomcat Version**: Check tomcat/RELEASE-NOTES
5. **Operating System**: Windows/macOS/Linux version
6. **Error Messages**: Copy exact error text
7. **Log Files**: Relevant portions of catalina.log
8. **Configuration**: Instance configuration details

### Log File Locations

```
Instance Logs:
~/.vscode/extensions/ijson.tomcatee-*/instances/<instance-id>/logs/
├── catalina.out          # Main output log
├── catalina.YYYY-MM-DD.log # Daily catalina log
├── localhost.YYYY-MM-DD.log # Localhost log
└── manager.YYYY-MM-DD.log   # Manager app log

TomcatEE Extension Logs:
VSCode → Help → Toggle Developer Tools → Console
```

### Community Support

1. **Search existing solutions** in [discussions](../../discussions)
2. **Ask in troubleshooting category** [here](../../discussions/categories/troubleshooting)
3. **Report bugs** in [bug reports](../../discussions/categories/bug-reports)
4. **Check documentation** in [user guides](../user-guides/)

## 🔗 Related Resources

- [Instance Configuration Guide](../configuration/instance-configuration.md)
- [Port Management Guide](../configuration/port-management.md)
- [Debug Issues](debug-issues.md)
- [Performance Tuning](performance-tuning.md)

---

**Still having issues? Don't hesitate to ask for help in our [community forum](../../discussions)!**
