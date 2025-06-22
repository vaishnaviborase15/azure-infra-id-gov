#  Azure Virtual Machine Creation using PowerShell

##  Prepared By: *Vaishnavi Borase*

##  Objective

To create a Virtual Machine (VM) in Azure using **PowerShell**, including:
- Creating a resource group
- Creating a virtual network and subnet
- Creating a public IP and NIC
- Creating a VM with username and password login

---

##  Prerequisites

- Active Azure Subscription
- Azure PowerShell installed (`Az` module)
- Logged in via PowerShell:

```powershell
Connect-AzAccount
```

---

##  Step-by-Step Procedure

###  Step 1: Set Variables (Change as needed)

```powershell
# Custom Variables
$resourceGroup = "VaishnaviResourceGroup"
$location = "EastUS"
$vmName = "VaishnaviVM"
$vnetName = "VaishnaviVNet"
$subnetName = "VaishnaviSubnet"
$ipName = "VaishnaviPublicIP"
$nicName = "VaishnaviNIC"
$username = "vaishnaviadm"
$password = ConvertTo-SecureString "Vaishnavi@123" -AsPlainText -Force
```

---

###  Step 2: Create Resource Group

```powershell
New-AzResourceGroup -Name $resourceGroup -Location $location
```

---

###  Step 3: Create Virtual Network and Subnet

```powershell
$vnet = New-AzVirtualNetwork `
  -ResourceGroupName $resourceGroup `
  -Location $location `
  -Name $vnetName `
  -AddressPrefix "10.0.0.0/16"

Add-AzVirtualNetworkSubnetConfig `
  -Name $subnetName `
  -AddressPrefix "10.0.0.0/24" `
  -VirtualNetwork $vnet

$vnet | Set-AzVirtualNetwork
```

---

###  Step 4: Create Public IP and Network Interface

```powershell
$pip = New-AzPublicIpAddress `
  -Name $ipName `
  -ResourceGroupName $resourceGroup `
  -Location $location `
  -AllocationMethod Dynamic

$subnet = Get-AzVirtualNetworkSubnetConfig `
  -Name $subnetName `
  -VirtualNetwork $vnet

$nic = New-AzNetworkInterface `
  -Name $nicName `
  -ResourceGroupName $resourceGroup `
  -Location $location `
  -SubnetId $subnet.Id `
  -PublicIpAddressId $pip.Id
```

---

###  Step 5: Create Virtual Machine Configuration

```powershell
$vmConfig = New-AzVMConfig -VMName $vmName -VMSize "Standard_B1s"

$vmConfig = Set-AzVMOperatingSystem `
  -VM $vmConfig `
  -ComputerName $vmName `
  -Credential (New-Object System.Management.Automation.PSCredential($username, $password)) `
  -Windows

$vmConfig = Add-AzVMNetworkInterface -VM $vmConfig -Id $nic.Id

$vmConfig = Set-AzVMSourceImage `
  -VM $vmConfig `
  -PublisherName "MicrosoftWindowsServer" `
  -Offer "WindowsServer" `
  -Skus "2019-Datacenter" `
  -Version "latest"
```

---

###  Step 6: Create the Virtual Machine

```powershell
New-AzVM `
  -ResourceGroupName $resourceGroup `
  -Location $location `
  -VM $vmConfig
```

---

##  Summary

| Step                        | Command Used                             |
|-----------------------------|------------------------------------------|
| Connect to Azure            | `Connect-AzAccount`                      |
| Create Resource Group       | `New-AzResourceGroup`                    |
| Create VNet/Subnet          | `New-AzVirtualNetwork`, `Add-AzSubnet`  |
| Create Public IP & NIC      | `New-AzPublicIpAddress`, `New-AzNIC`    |
| Configure VM Settings       | `New-AzVMConfig`, `Set-AzVMOperatingSystem` |
| Create VM                   | `New-AzVM`                               |

---

## Prepared By

**Vaishnavi Borase**  
Azure Account: `221106014@rcpit.ac.in`  
Directory: `vaishnavidirectory.onmicrosoft.com`

---
