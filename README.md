<div align="center">

  <h1> Secure Network Controls: NSG & ASG Implementation</h1>

  <p><strong>FuturinCLOUD Limited</strong> – Azure Cloud Security Consulting</p>
  <p>AZ-500 Lab | February 2026</p>


</div>

## Project Summary

FuturinCLOUD Limited was tasked with implementing secure network segmentation for a client environment with public-facing web servers and restricted management/administrative servers.

**Business & Security Objectives Achieved**
- Allow HTTP/HTTPS traffic only to web servers  
- Restrict RDP access exclusively to management servers  
- Deny all other unsolicited inbound traffic  
- Use scalable, group-based rules (ASGs) instead of IP-based lists  
- Enforce least-privilege principle at the network layer

## Architecture Delivered

- **VNet**: FuturinCLOUD-VNet (10.0.0.0/16)  
- **Subnet**: default (10.0.0.0/24)  
- **ASGs**:  
  - futuricloud-web-asg → web tier  
  - futuricloud-mgmt-asg → management tier  
- **NSG**: futuricloud-nsg (associated to subnet)  
- **Inbound Rules**:
  - Priority 100: Allow HTTP/HTTPS → futuricloud-web-asg  
  - Priority 110: Allow RDP → futuricloud-mgmt-asg  
  - Implicit deny all other traffic

## Validation Summary

| Test Case                               | Method                          | Expected Outcome               | 
|-----------------------------------------|---------------------------------|--------------------------------|
| HTTP access to web VM public IP         | Browser → public IP             | IIS welcome page loads         | 
| HTTPS access to web VM public IP        | Browser → public IP             | Allowed (same rule)            | 
| RDP attempt to web VM public IP         | Remote Desktop client           | Connection refused / timeout   | 
| RDP to management VM public IP          | Remote Desktop client           | Successful login               | 

## Full Documentation

 **Complete Lab Documentation Report and Screenshots (PDF)**  
[Open / View Full Report](https://github.com/cybervee-tech/Azure-Network-Security/blob/main/docs/Azure%20Network%20Segmentation%20with%20NSGs%20%26%20ASGs%20%20.pdf)


## Challenges & Resolutions

- **ASG attachment delay** → Waited 1–2 minutes after attaching, refreshed NIC page, checked effective security rules  
- **IIS default page not appearing** → Used VM Run command: `Install-WindowsFeature -Name Web-Server -IncludeManagementTools`  
- **Rules not applying instantly** → Verified effective security rules on VM NIC, waited for propagation  
- **Public IP assignment delay** → Verified NSG association and waited for provisioning

## Conclusion

Lab 2 successfully delivered a production-ready network security baseline using Azure-native constructs:

- Demonstrated **least-privilege access control** at scale  
- Proved **logical grouping with ASGs** enables maintainable, intent-based rules  
- Validated **defense-in-depth** by denying all traffic not explicitly permitted  
- Confirmed correct segmentation through practical testing  

This design pattern is directly applicable to enterprise environments and forms the foundation for advanced controls (Azure Firewall, DDoS Protection, Network Watcher) in subsequent labs.

**FuturinCLOUD Limited** – Securing cloud environments across Africa  
Lagos, Nigeria
