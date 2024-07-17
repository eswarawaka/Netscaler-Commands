### Comprehensive Guide on Citrix Management and Calculations

#### 1. Calculating the Load Evaluator Index on Delivery Controller (DDC)
The Load Evaluator Index (LEI) is calculated using the following formula:
\[ \text{Load Evaluator Index} = \text{Disk} + \left(\frac{\text{CPU} + \text{Memory} + \text{Session Count}}{3}\right) \times 0.05 \]

Example Command:
```powershell
PS C:\Windows\system32> Get-BrokerMachine XD\XenApp4
```
Example Output:
```plaintext
LoadIndex                   : 9848
LoadIndexes                 : {CPU:7267, Memory:661, Disk:9633, SessionCount:5000}
```
Calculation:
\[ \text{LEI Total} = 9633 + \left(\frac{7267 + 661 + 5000}{3}\right) \times 0.05 = 9633 + 215.46 = 9848.46 \]

#### 2. Formula to Calculate Disk Space for MCS Deployed Non-Persistent VMs
The required disk space for Machine Creation Services (MCS) deployed non-persistent VMs can be calculated as follows:

\[ (\text{number of storages} \times 2 \times \text{image size}) + (\text{number of users} \times 15\% \times \text{image size}) + (\text{number of users} \times 16 \text{MB}) \]

For VMware environments, include swap files:
\[ (\text{number of storages} \times 2 \times \text{image size} \times \text{number of machine catalog}) + (\text{number of users} \times 15\% \times \text{image size}) + (\text{number of users} \times 16 \text{MB}) + (\text{number of users} \times \text{VM swap file}) + (\text{number of users} \times \text{VM video swap file}) \]

#### 3. Calculating USER/DEVICE Licenses Needed
To calculate the number of USER/DEVICE licenses needed:
\[ A - C + B = \text{Number of USER/DEVICE Licenses Needed} \]
Where:
- \( A \) = Total Number of Users
- \( B \) = Total Number of Shared Devices
- \( C \) = Number of Users that will ONLY use Shared Devices

#### 4. Capacity of a Single Delivery Controller
A single delivery controller with 4 vCPUs and 4GB RAM can support more than 5,000 VDAs. For high availability, an additional delivery controller should be added:
\[ \# \text{of DCs} = \left(\frac{\# \text{of VDAs}}{5,000}\right) + 1 \]

#### 5. Database Recommendations
- 2 Cores / 4 GB RAM for environments up to 5,000 users
- 4 Cores / 8 GB RAM for environments up to 15,000 users
- 8 Cores / 16 GB RAM for environments with 15,000+ users

The database files and transaction logs should be hosted on separate disk subsystems to handle high transaction volumes.

#### 6. Booting Devices with Provisioning Services
Provisioning Services can boot 500 devices simultaneously. The time required to boot can be calculated as follows:
\[ \text{Seconds to boot} = \left(\frac{\text{number of targets} \times \text{MB usage}}{\text{network throughput (MB/sec)}}\right) \]

For example:
- Booting 500 devices on a 1 Gbps network:
  \[ \text{Seconds to boot} = \frac{500 \times 178}{125} = 712 \text{ seconds} = 12 \text{ minutes} \]

- Booting 500 devices on a 10 Gbps network:
  \[ \text{Seconds to boot} = \frac{500 \times 178}{1250} = 71.2 \text{ seconds} = 1.2 \text{ minutes} \]

#### Provisioning Services Streaming Capacity
The number of streams a Provisioning Services server can run concurrently:
\[ \text{Max number of streams} = \text{number of ports} \times \text{number of threads/port} \]
With default settings of 20 ports and 8 threads per port:
\[ \text{Max number of streams} = 20 \times 8 = 160 \text{ concurrent targets} \]

### Citrix Documentation Resources
For a more comprehensive cheat sheet and additional details, refer to the Citrix Community resources:
- [Citrix ADC - nsconmsg Commands Cheat Sheet](https://community.citrix.com/docs/DOC-47468)
- [Citrix TechZone - Diagrams and Posters](https://community.citrix.com/docs/DOC-40282)
