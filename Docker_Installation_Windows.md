# Cyber_Forensics
### How to Install Docker on Windows and Set Up the Cyber Forensics Environment

---

### **Step 1: Download Docker Desktop**
1. Go to the official Docker website: [Docker Desktop](https://www.docker.com/products/docker-desktop/).
2. Download the installer for Windows.

---

### **Step 2: Install Docker Desktop**
1. Double-click the downloaded file (`Docker Desktop Installer.exe`).
2. Follow the on-screen instructions:
   - Accept the license agreement.
   - Choose to use **WSL 2 backend** during installation.
3. Wait for the installation to complete.

---

### **Step 3: Start Docker Desktop**
1. After installation, open Docker Desktop from the Start Menu.
2. Wait for Docker to initialize.
3. **Enable WSL 2:** If prompted, follow the steps to enable WSL 2:
   - Open PowerShell as Administrator and run:
     ```powershell
     wsl --install
     wsl --set-default-version 2
     ```
4. Restart your computer if prompted.

---

### **Step 4: Create a Dockerfile**
#### **Option A: Using PowerShell**
1. Open PowerShell.
2. Navigate to your desired directory:
   ```powershell
   cd "C:\Users\sande\Desktop\CYB Foren"
   ```
3. Create an empty Dockerfile:
   ```powershell
   New-Item -Path . -Name "Dockerfile" -ItemType "File"
   ```
4. Open the Dockerfile in Notepad for editing:
   ```powershell
   notepad Dockerfile
   ```

#### **Option B: Using CMD**
1. Open CMD.
2. Navigate to your desired directory:
   ```cmd
   cd "C:\Users\sande\Desktop\CYB Foren"
   ```
3. Create an empty Dockerfile:
   ```cmd
   echo. > Dockerfile
   ```
4. Open the Dockerfile in Notepad:
   ```cmd
   notepad Dockerfile
   ```

---

### **Step 5: Add Content to the Dockerfile**
Copy and paste the following code into your Dockerfile:

```dockerfile
FROM kalilinux/kali-rolling

# Update and install essential cyber forensics tools
RUN apt-get update && apt-get install -y \
    autopsy \
    sleuthkit \
    binwalk \
    foremost \
    testdisk \
    scalpel \
    hashdeep \
    exiftool \
    volatility3 \
    tshark \
    tcpdump \
    nmap \
    netcat \
    whois \
    curl \
    wget \
    python3-pip \
    steghide \
    outguess \
    stegsnow \
    zsteg \
    && apt-get clean

# Install Python tools for forensic tasks
RUN pip3 install pytsk3 yara-python pefile pandas

# Allow passwordless sudo
RUN echo "root ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers

CMD ["/bin/bash"]
```

Save the file and close Notepad.

---

### **Step 6: Build the Docker Image**
1. Open a terminal (PowerShell or CMD).
2. Navigate to the directory containing the Dockerfile:
   ```powershell
   cd "C:\Users\sande\Desktop\CYB Foren"
   ```
3. Build the Docker image:
   ```powershell
   docker build -t cyberforensics-class .
   ```

---

### **Step 7: Run the Docker Container**
1. Start the container interactively:
   ```powershell
   docker run -it --name cyberforensics cyberforensics-class
   ```
2. You are now inside the container’s terminal with all the tools installed.

---

### **Step 8: Verify the Tools**
1. Inside the container, run commands to ensure the tools are installed:
   ```bash
   autopsy --help
   binwalk --version
   volatility --info
   ```

---

### **Step 9: Save and Reuse the Container**
1. To stop the container:
   ```bash
   exit
   ```
2. To restart the container later:
   ```powershell
   docker start -ai cyberforensics
   ```

---
