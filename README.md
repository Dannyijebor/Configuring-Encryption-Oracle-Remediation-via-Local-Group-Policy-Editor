# **Configuring Encryption Oracle Remediation via Local Group Policy Editor**

## **Repository Name:** `Encryption-Oracle-Remediation-Policy-Config`  

### **Overview**  
This repository provides a detailed guide and necessary scripts to configure **Encryption Oracle Remediation** settings in the **Local Group Policy Editor (gpedit.msc)** on Windows systems. The configuration is critical for resolving issues related to **CredSSP (Credential Security Support Provider) encryption vulnerabilities**, which may cause Remote Desktop Protocol (RDP) authentication failures due to mismatched encryption policies.

---

### **Why This Configuration is Important**
The **Encryption Oracle Remediation** policy controls how Windows validates credentials in **CredSSP**-based authentication (e.g., Remote Desktop connections). If not configured properly, users may encounter errors like:  

> "An authentication error has occurred. The function requested is not supported. This could be due to CredSSP encryption oracle remediation."  

This setting became crucial after Microsoft released security updates to patch **CVE-2018-0886**, which introduced stricter CredSSP security policies.

---

### **Steps to Configure Encryption Oracle Remediation**
#### **Method 1: Using Local Group Policy Editor (GUI)**
1. **Open Group Policy Editor**  
   - Press `Win + R`, type `gpedit.msc`, and press **Enter**.

2. **Navigate to the Policy Setting**  
   - Go to:  
     ```
     Computer Configuration → Administrative Templates → System → Credentials Delegation
     ```

3. **Modify the Encryption Oracle Remediation Policy**  
   - Find **Encryption Oracle Remediation** in the right-hand panel.  
   - Double-click it to open the settings window.  
   - Change the setting to:
     - `Enabled`
     - Select **Vulnerable** (if compatibility is required) or **Mitigated** (recommended for security).  

4. **Apply and Save Changes**  
   - Click **Apply** → **OK** → Close the editor.  

5. **Restart Your Computer**  
   - Restart to apply the new policy settings.

---

#### **Method 2: Using Windows Registry Editor (For Non-Pro Versions)**
For Windows **Home Edition**, where `gpedit.msc` is unavailable, use the **Registry Editor**:

1. **Open Registry Editor** (`Win + R`, type `regedit`, press **Enter**).
2. Navigate to:
   ```
   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
   ```
3. Right-click **System**, select **New** → **DWORD (32-bit) Value**.
4. Name it:  
   ```
   AllowEncryptionOracle
   ```
5. Set its **value**:
   - `2` (Vulnerable – Least Secure)
   - `1` (Mitigated – Recommended)
   - `0` (Force Updated Clients – Most Secure)
6. Restart the system.

---

### **Repository Contents**
- `README.md` – This guide explaining the **CredSSP Encryption Oracle Remediation** policy.
- `enable_encryption_oracle_regedit.reg` – Preconfigured registry file to apply settings in Windows Home.
- `gpedit-config-screenshot.png` – Screenshot showing how to navigate and configure the policy.
- `troubleshooting.md` – Common issues and troubleshooting steps.

---

### **Use Cases**
✔ Fixes **Remote Desktop Connection** authentication issues.  
✔ Enhances security for **CredSSP-based authentication**.  
✔ Helps organizations **comply with Microsoft's security updates**.  

---

### **Contributing**
Feel free to submit issues, suggestions, or pull requests to improve this guide! 🚀

---

### **License**
This project is licensed under the **MIT License**.

---

### **Final Notes**
This configuration is **crucial** for administrators who manage **RDP access** in secured environments. If you're facing issues with remote desktop authentication due to Microsoft’s security updates, this guide provides a structured solution.
