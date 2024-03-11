Step 1: Update System Packages
sudo apt update && sudo apt upgrade -y
Step 2: Install Java Development Kit (JDK)
sudo apt install openjdk-11-jdk
java -version
Step 3: Create Tomcat User
sudo useradd -r -m -U -d /opt/tomcat -s /bin/false tomcat
Step 4: Download and Extract Tomcat 10
wget https://downloads.apache.org/tomcat/tomcat-10/v10.1.19/bin/apache-tomcat-10.1.19.tar.gz
sudo tar xzf apache-tomcat-*.tar.gz -C /opt/tomcat
sudo -i
cd /opt/tomcat/apache-tomcat-10.1.19
Step 5: Set Permissions
sudo chown -R tomcat: /opt/tomcat
sudo sh -c 'chmod +x /opt/tomcat/apache-tomcat-10.1.19/bin/*.sh'
Step 6: Create Tomcat Application Accounts

sudo nano /opt/tomcat/apache-tomcat-10.1.19/conf/tomcat-users.xml

<!-- user manager can access only the manager section -->
<role rolename="manager-gui" />
<user username="manager" password="manager@123" roles="manager-gui" />

<!-- user admin can access manager and admin section both -->
<role rolename="admin-gui" />
<user username="admin" password="admin@123" roles="manager-gui,admin-gui" />

Step 7: Allow Remote Hosts to Access Tomcat
sudo nano /opt/tomcat/apache-tomcat-10.1.19/webapps/manager/META-INF/context.xml
----------
<Context antiResourceLocking="false" privileged="true" >
  <CookieProcessor className="org.apache.tomcat.util.http.Rfc6265CookieProcessor"
                   sameSiteCookies="strict" />
  <Valve className="org.apache.catalina.valves.RemoteAddrValve"
         allow=".*" />
  <Manager sessionAttributeValueClassNameFilter="java\.lang\.(?:Boolean|Integer|Long|Number|String)|org\.apache\.catalina\.filters\.CsrfPreventionFilter\$L></Context>
 

sudo nano /opt/tomcat/apache-tomcat-10.1.19/webapps/host-manager/META-INF/context.xml
edit same like Above:
         allow=".*" />

Step 8: Create a Systemd Service File:

sudo nano /etc/systemd/system/tomcat.service
------------
Description=Apache Tomcat 10 Web Application Server
After=network.target

[Service]
Type=forking

User=tomcat
Group=tomcat

Environment="JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64"
Environment="CATALINA_HOME=/opt/tomcat/apache-tomcat-10.1.19"
Environment="CATALINA_BASE=/opt/tomcat/apache-tomcat-10.1.19"
Environment="CATALINA_PID=/opt/tomcat/apache-tomcat-10.1.19/temp/tomcat.pid"
Environment="CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC"

ExecStart=/opt/tomcat/apache-tomcat-10.1.19/bin/startup.sh
ExecStop=/opt/tomcat/apache-tomcat-10.1.19/bin/shutdown.sh

[Install]
WantedBy=multi-user.target
--------
Step 9: Start and Enable Tomcat

sudo systemctl daemon-reload
sudo systemctl start tomcat
sudo systemctl status tomcat
sudo systemctl enable tomcat
Access the browser page : see the results:
