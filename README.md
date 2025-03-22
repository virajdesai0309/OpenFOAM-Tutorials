### **🚀 Installing OpenFOAM on Linux Mint**

To set up **OpenFOAM 12** on **Linux Mint**, follow this step-by-step guide.

🔗 **Official Download Page:** [OpenFOAM 12 - Ubuntu](https://openfoam.org/download/12-ubuntu/)

---

## **📌 Installation Steps**

### **1️⃣ Add Repository and Public Key**

Open a terminal (`Applications → Accessories → Terminal`) and run:

```bash
sudo sh -c "wget -O - https://dl.openfoam.org/gpg.key > /etc/apt/trusted.gpg.d/openfoam.asc"
sudo add-apt-repository http://dl.openfoam.org/ubuntu
```

### **2️⃣ Update Package List**

```bash
sudo apt update
```

### **3️⃣ Install OpenFOAM 12**

To install **OpenFOAM 12** along with **ParaView** (if not already installed):

```bash
sudo apt -y install openfoam12
```

✅ **OpenFOAM is now installed in `/opt/`**

---

## **🔧 Post-Installation Setup**

### **1️⃣ Add OpenFOAM to the Shell Environment**

Modify your **`.bashrc`** file to source OpenFOAM on startup.

```bash
cd ~  # Navigate to home directory
nano .bashrc  # Open .bashrc file in a text editor
```

📌 **Add the following line at the end of the file:**

```bash
source /opt/openfoam12/etc/bashrc
```

💾 **Save and exit** (For Nano: Press `CTRL + X`, then `Y`, then `Enter`).

---

### **2️⃣ Apply Changes**

Close the terminal and open a new one. Then, run:

```bash
foamRun -help
```

🔹 **If you don’t want to restart the terminal**, apply changes instantly:

```bash
. $HOME/.bashrc
```

📌 **Note:** If `.bashrc` already contains an older OpenFOAM version, remove or comment (`#`) the previous line before adding the new one.

---

## **🏗️ Getting Started with OpenFOAM**

### **1️⃣ Create a Project Directory**

Set up your working directory inside `$HOME/OpenFOAM`:

```bash
mkdir -p $FOAM_RUN
```

### **2️⃣ Copy Example Case and Run Simulation**

1️⃣ Navigate to your working directory:

```bash
cd $FOAM_RUN
```

2️⃣ Copy the **pitzDailySteady** example case:

```bash
cp -r $FOAM_TUTORIALS/incompressibleFluid/pitzDailySteady .
```

3️⃣ Move into the case directory:

```bash
cd pitzDailySteady
```

4️⃣ Generate the mesh:

```bash
blockMesh
```

5️⃣ Run the simulation:

```bash
foamRun
```

6️⃣ View results in **ParaView**:

```bash
paraFoam
```

✅ **Congratulations! You have successfully installed and run OpenFOAM. 🎉**

![image](https://github.com/user-attachments/assets/b4c3a4ac-b600-467c-9716-bceab7ed19a3)
