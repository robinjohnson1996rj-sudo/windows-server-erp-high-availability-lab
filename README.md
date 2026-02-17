# windows-server-erp-high-availability-lab
Enterprise-style ERP deployment built in a virtual lab environment using Active Directory, IIS, SQL Server, and HAProxy load balancing.

##  Project Goals
- Simulate production-level ERP infrastructure
- Implement domain-based authentication
- Deploy redundant IIS application servers
- Configure HAProxy load balancing
- Test failover and high availability

##  Lab Architecture

| Server | Role |
|--------|------|
| DC1 | Domain Controller + DNS |
| SQL1 | SQL Database Server |
| APP1 | IIS ERP Application Server |
| APP2 | IIS ERP Application Server |
| LB1 | HAProxy Load Balancer |
| Client | Windows 10 Test Machine |


##  Network Configuration

- Domain: corp.local
- Network: 10.10.10.0/24

| Component | IP |
|-----------|----|
| DC1 | 10.10.10.10 |
| SQL1 | 10.10.10.20 |
| APP1 | 10.10.10.31 |
| APP2 | 10.10.10.32 |
| LB1 | 10.10.10.50 |


##  IIS ERP Deployment (APP1 & APP2)

- Installed IIS Web Server
- Installed ASP.NET Core Hosting Bundle
- Created IIS site on port 8080
- Application Pool set to "No Managed Code"
- Deployed published ASP.NET Core ERP application
- Connected application to SQL1 database


##  SQL Server Configuration (SQL1)

- Installed SQL Server 2022
- Created ERP database
- Configured SQL Authentication for application access


##  HAProxy Load Balancer Configuration (LB1)

sudo apt update
sudo apt install haproxy -y

frontend http_front
    bind *:80
    default_backend app_servers

backend app_servers
    balance roundrobin
    option httpchk
    server app1 10.10.10.31:8080 check
    server app2 10.10.10.32:8080 check


### Test URL
http://erp.corp.local

##  High Availability Validation

Failover testing was performed by:

- Stopping IIS on APP1
- Confirming traffic continued through APP2
- Verifying HAProxy health checks

### Expected Behavior
If one application server becomes unavailable, HAProxy automatically routes traffic to the remaining healthy server without user interruption.


## 🛠 Troubleshooting (Issues & Fixes)

| Issue |   Root Cause | Fix |

| Untrusted domain login | Authentication mismatch | Switched to SQL Authentication |
| Add-Migration not recognized | EF tools missing | Installed EF Core Tools |
| dotnet-ef not found | Global tool missing | Installed dotnet-ef |
| DNS not resolving | Missing A record | Created DNS A record |
| 502 Bad Gateway | Hosting bundle missing | Installed Hosting Bundle & restarted IIS |

##  Skills Demonstrated

- Active Directory & DNS Administration
- Windows Server configuration
- IIS deployment
- SQL Server management
- HAProxy configuration
- Load balancing & health checks
- High availability concepts
- Production troubleshooting

  ##  Technologies Used

- Windows Server 2025
- Active Directory
- SQL Server 2022
- IIS
- ASP.NET Core
- HAProxy
- Ubuntu Server
- VMware Workstation

---











