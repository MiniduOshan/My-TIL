📘 **TIL – NTP (Network Time Protocol) & Active Directory**

📅 02 November 2026

Today I learned about **NTP (Network Time Protocol)** and its importance in Windows Server environments, especially when working with **Active Directory (AD)**.

### Key points I learned:

- **NTP:** A protocol used to synchronize system clocks across computers and network devices.
- **UDP Port 123:** NTP uses UDP port 123 for time synchronization.
- **Time Synchronization:** Ensures all devices maintain accurate and consistent time.
- **Stratum Levels:** Represent the hierarchy of time sources.

### NTP & Active Directory

- **Kerberos Authentication:** Active Directory uses Kerberos, which relies on time synchronization between clients and domain controllers.
- **Time Difference:** Significant clock differences can cause Kerberos authentication failures. The default maximum tolerance in Windows domains is typically 5 minutes.
- **Domain Controller:** Domain controllers participate in the domain time hierarchy.
- **PDC Emulator:** The PDC Emulator in the forest root domain usually acts as the primary time source for the domain hierarchy.
- **Windows Time Service (W32Time):** Windows uses this service to synchronize system clocks.

💡 **Important takeaway:** Proper time synchronization is essential for Active Directory authentication, security, event logs, and reliable communication between domain-joined computers.

#TIL #NTP #ActiveDirectory #WindowsServer #Kerberos #Networking #SystemAdministration #Learning
