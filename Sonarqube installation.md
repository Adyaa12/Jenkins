# SonarQube Installation Guide (v9.4.0.54424)

This guide walks you through the installation of SonarQube on a Linux system using OpenJDK 11.

---

## Step 1: Install Java

Update your system and install OpenJDK 11:

```bash
sudo apt-get update && sudo apt-get install openjdk-11-jdk -y
```

---

## Step 2: Install Unzip Utility

```bash
sudo apt install unzip -y
```

---

## Step 3: Create a New User for SonarQube

Switch to root and add a new user:

```bash
sudo adduser sonarqube
```

---

## Step 4: Download and Extract SonarQube (as `sonarqube` user)

Switch to the `sonarqube` user:

```bash
su - sonarqube
```

Download SonarQube:

```bash
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.4.0.54424.zip
```

Unzip the archive:

```bash
unzip sonarqube-9.4.0.54424.zip
```

---

## Step 5: Set Permissions (as root)

Switch back to root and set proper permissions:

```bash
sudo chmod -R 755 /home/sonarqube/sonarqube-9.4.0.54424
sudo chown -R sonarqube:sonarqube /home/sonarqube/sonarqube-9.4.0.54424
```

---

## Step 6: Start SonarQube

Switch to the `sonarqube` user and start the service:

```bash
su - sonarqube
cd sonarqube-9.4.0.54424/bin/linux-x86-64/
./sonar.sh start
```

---

## 🎉 SonarQube is Now Running!

Open your browser and navigate to:

```
http://<your-server-ip>:9000
```

Default credentials:

- **Username:** `admin`
- **Password:** `admin`

---

> 💡 Tip: For production, consider configuring SonarQube as a systemd service and using a reverse proxy like Nginx.
