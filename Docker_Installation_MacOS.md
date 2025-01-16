# Cyber Forenics
Here’s how to install Docker on macOS and set up the Cyber Forensics environment:

---

### **Step 1: Download Docker Desktop for macOS**
1. Visit the official Docker website: [Docker Desktop for Mac](https://www.docker.com/products/docker-desktop/).
2. Download the appropriate installer for macOS (Intel or Apple Silicon).

---

### **Step 2: Install Docker Desktop**
1. Open the downloaded `.dmg` file.
2. Drag and drop the Docker icon into the Applications folder.
3. Open Docker Desktop from Applications or Spotlight Search.
4. Follow the setup process and grant permissions as needed.

---

### **Step 3: Start Docker Desktop**
1. Ensure Docker Desktop is running.
2. Verify the installation by opening a terminal and running:
   ```bash
   docker --version
   ```
   You should see the Docker version printed.

---

### **Step 4: Create a Dockerfile**
#### **Option A: Using Terminal**
1. Open the terminal and navigate to your project directory:
   ```bash
   cd ~/Desktop/CYB_Foren
   ```
2. Create an empty `Dockerfile`:
   ```bash
   touch Dockerfile
   ```
3. Open the file with a text editor (e.g., nano, vim, or Visual Studio Code):
   ```bash
   nano Dockerfile
   ```

#### **Option B: Using Finder**
1. Navigate to the desired folder (e.g., `Desktop/CYB_Foren`).
2. Right-click and select **New File** (or use your text editor to create a new file named `Dockerfile`).

---

### **Step 5: Add Content to the Dockerfile**
Paste the following content into the `Dockerfile` using your preferred editor:

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

Save and close the file.

---

### **Step 6: Build the Docker Image**
1. Open the terminal.
2. Navigate to the directory containing the Dockerfile:
   ```bash
   cd ~/Desktop/CYB_Foren
   ```
3. Build the Docker image:
   ```bash
   docker build -t cyberforensics-class .
   ```

---

### **Step 7: Run the Docker Container**
1. Start the container interactively:
   ```bash
   docker run -it --name cyberforensics cyberforensics-class
   ```
2. You are now inside the container’s terminal with all the tools installed.

---

### **Step 8: Verify the Tools**
1. Inside the container, test the tools:
   ```bash
   autopsy --help
   binwalk --version
   volatility --info
   ```

---

### **Step 9: Save and Reuse the Container**
1. Stop the container:
   ```bash
   exit
   ```
2. Restart the container later:
   ```bash
   docker start -ai cyberforensics
   ```

---

