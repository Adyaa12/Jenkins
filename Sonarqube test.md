
# SonarQube Installation Guide (Ubuntu)

## Step 1: Install Java

SonarQube requires **Java 11** or **17**.

**Update the package index:**
```bash
sudo apt update
```

**Install OpenJDK 17:**
```bash
sudo apt install -y openjdk-17-jdk
```

**Verify Java installation:**
```bash
java -version
```

---

## Step 2: Install and Configure PostgreSQL

**Install PostgreSQL:**
```bash
sudo apt install -y postgresql postgresql-contrib
```

**Switch to the PostgreSQL user:**
```bash
sudo -i -u postgres
```

**Create a database and user for SonarQube:**
```bash
psql
CREATE DATABASE sonarqube;
CREATE USER sonar WITH ENCRYPTED PASSWORD 'sonar';
GRANT ALL PRIVILEGES ON DATABASE sonarqube TO sonar;
\q
exit
```

---

## Step 3: Download SonarQube

**Download the latest SonarQube version:**
```bash
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.9.2.50663.zip
```

**Install unzip and extract SonarQube:**
```bash
sudo apt install -y unzip
unzip sonarqube-9.9.2.50663.zip
sudo mv sonarqube-9.9.2.50663 /opt/sonarqube
```

---

## Step 4: Configure SonarQube

**Edit the configuration file:**
```bash
sudo nano /opt/sonarqube/conf/sonar.properties
```

**Update database connection details:**
```properties
sonar.jdbc.url=jdbc:postgresql://localhost:5432/sonarqube
sonar.jdbc.username=sonar
sonar.jdbc.password=sonar
```

---

## Step 5: Create a Systemd Service for SonarQube

**Create the service file:**
```bash
sudo nano /etc/systemd/system/sonarqube.service
```

**Paste the following configuration (replace `<your_user>` with your system username):**
```ini
[Unit]
Description=SonarQube service
After=syslog.target network.target

[Service]
Type=simple
User=<your_user>
Group=<your_user>
ExecStart=/opt/sonarqube/bin/linux-x86-64/sonar.sh start
ExecStop=/opt/sonarqube/bin/linux-x86-64/sonar.sh stop
Restart=always
LimitNOFILE=65536

[Install]
WantedBy=multi-user.target
```

**Reload systemd and start the service:**
```bash
sudo systemctl daemon-reload
sudo systemctl start sonarqube
sudo systemctl enable sonarqube
```

---

## Step 6: Access SonarQube

Open your web browser and go to:

```
http://<your_server_ip>:9000
```

**Login Credentials:**

- **Username:** `admin`  
- **Password:** `admin`
