# Windows Part 3

## Windows Updates

**Windows Update** is a service provided by Microsoft to deliver security updates, feature enhancements, and patches for the Windows operating system and other Microsoft products, such as Microsoft Defender.

Updates are typically released on the second Tuesday of each month, commonly known as **Patch Tuesday**. However, critical updates do not necessarily wait until the next Patch Tuesday. If an update is urgent, Microsoft may release it immediately through the Windows Update service to affected Windows devices.

Windows Update can be accessed through the **Settings** application. Another way to open Windows Update is by using the **Run** dialog box and entering the following command: `control /name Microsoft.WindowsUpdate`
 
Throughout the years, many Windows users became accustomed to postponing or completely ignoring Windows Updates. Several factors contributed to this behavior, one of which was the requirement to reboot the system after installing updates.

Microsoft addressed this issue with Windows 10. Updates can no longer be indefinitely ignored or dismissed. While they may be postponed temporarily, they must eventually be installed, and the system will restart as required. Microsoft enforces these updates to help ensure that devices remain secure and protected.

## Windows Security

According to Microsoft, **"Windows Security is your home to manage the tools that protect your device and your data."**

Windows Security can be accessed through the **Settings** application. It includes four main protection areas:
- **Virus & threat protection**
- **Firewall & network protection**
- **App & browser control**
- **Device security**

## Virus & Threat Protections
This area is divided into two parts:
- Current Threats 
- Virus & threats protection settings

### Current Threats

**Scan Options**

- **Quick scan** — Scans locations on your system where threats are commonly found.
- **Full scan** — Scans all files and running programs on your hard drive. This scan may take more than one hour to complete.
- **Custom scan** — Allows you to select specific files and locations to scan.

**Threat History**

- **Last scan** — Windows Defender Antivirus automatically scans your device for viruses and other threats to help maintain system security.
- **Quarantined threats** — Identified threats that have been isolated and prevented from running on your device. These items are periodically removed.
- **Allowed threats** — Items identified as threats that you have explicitly allowed to run on your device.


### Virus & threat protection settings

**Manage Settings**

- **Real-time protection** — Detects and prevents malware from installing or running on your device.

- **Cloud-delivered protection** — Provides faster and enhanced protection by accessing the latest threat intelligence data from the cloud.

- **Automatic sample submission** — Sends sample files to Microsoft to help improve detection and protect you and other users from potential threats.

- **Controlled folder access** — When enabled, this feature protects files, folders, and memory areas from unauthorized changes by malicious or unknown applications. Only approved and trusted applications are allowed to modify files within protected folders. To enable this feature, click **Manage Controlled Folder Access** and turn it on.

- **Exclusions** — Allows specific files or folders to be excluded from antivirus scanning, typically to reduce false positives. Administrators may exclude certain files or directories to prevent them from being scanned. To add exclusions, click **Add or remove exclusions** and specify the desired files or folders.

- **Notifications** — Sends alerts containing critical information about the health and security status of your device.

Excluded items may contain threats that could compromise your device. Only use exclusions if you are completely certain of their safety.


## Firewall and Network Protection

According to Microsoft, "Traffic flows into and out of devices through what we call ports. A firewall controls what is — and more importantly, what is not — allowed to pass through those ports. You can think of it as a security guard standing at the door, checking the ID of everything that tries to enter or exit."

Windows Firewall uses three network profiles:

- **Domain** — Applies to networks where the system can authenticate to a domain controller.
- **Private** — A user-assigned profile used for trusted networks, such as home or internal networks.
- **Public** — The default profile, used for untrusted public networks such as Wi-Fi hotspots in coffee shops, airports, and other public locations.

### App & Browser Control

According to Microsoft, "Microsoft Defender SmartScreen protects against phishing and malware websites and applications, as well as the download of potentially malicious files."

### Check apps and files

- **Windows Defender SmartScreen** helps protect your device by checking unrecognized applications and files downloaded from the web before they are allowed to run.

### Exploit protection

- **Exploit protection** is built into Windows 10 and helps safeguard your device against various types of exploits and attack techniques.

## TPM (Trusted Platform Module)

According to Microsoft, "Trusted Platform Module (TPM) technology is designed to provide hardware-based, security-related functions. A TPM chip is a secure cryptoprocessor designed to perform cryptographic operations. The chip includes multiple physical security mechanisms to make it tamper-resistant, and malicious software cannot interfere with the security functions of the TPM."

## Bitlocker

According to Microsoft, "BitLocker Drive Encryption is a data protection feature that integrates with the operating system and addresses the threats of data theft or exposure from lost, stolen, or improperly decommissioned computers."

On devices equipped with a TPM, BitLocker provides enhanced protection.

Microsoft states, "BitLocker provides the most protection when used with a Trusted Platform Module (TPM) version 1.2 or later. The TPM is a hardware component installed in many newer computers by manufacturers. It works with BitLocker to help protect user data and ensure that the system has not been tampered with while offline."

## Volume Shadow Copy Service

**Volume Shadow Copy Service (VSS)** coordinates the necessary actions to create a consistent shadow copy (also known as a snapshot or point-in-time copy) of data to be backed up.

Volume Shadow Copies are stored in the **System Volume Information** folder on each drive where protection is enabled.

If VSS is enabled (System Protection turned on), you can perform the following tasks through **Advanced System Settings**:

- Create a restore point
- Perform a system restore
- Configure restore settings
- Delete restore points

From a security perspective, malware authors are aware of this Windows feature and often design malware to locate and delete shadow copies. By removing these backups, attackers prevent recovery after a ransomware attack, unless an offline or off-site backup is available.


