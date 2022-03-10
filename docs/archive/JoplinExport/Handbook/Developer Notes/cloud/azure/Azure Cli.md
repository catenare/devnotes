---
title: Azure Cli
updated: 2021-06-24 02:14:45Z
created: 2021-06-24 02:12:24Z
latitude: -26.16670000
longitude: 27.86670000
altitude: 0.0000
---

Details
```
[
  {
    "cloudName": "AzureCloud",
    "homeTenantId": "d4f102d5-495c-4e63-b50e-e9b4123c4a29",
    "id": "8b07a6be-3d14-4943-8af8-36d59994587b",
    "isDefault": true,
    "managedByTenants": [],
    "name": "Free Trial",
    "state": "Enabled",
    "tenantId": "d4f102d5-495c-4e63-b50e-e9b4123c4a29",
    "user": {
      "name": "martin.johan@nziswano.co.za",
      "type": "user"
    }
  }
]
```
```
[
  {
    "additionalCapabilities": null,
    "availabilitySet": null,
    "billingProfile": null,
    "diagnosticsProfile": {
      "bootDiagnostics": {
        "enabled": true,
        "storageUri": null
      }
    },
    "evictionPolicy": null,
    "extendedLocation": null,
    "extensionsTimeBudget": null,
    "hardwareProfile": {
      "vmSize": "Standard_B1s"
    },
    "host": null,
    "hostGroup": null,
    "id": "/subscriptions/8b07a6be-3d14-4943-8af8-36d59994587b/resourceGroups/NZISWANODEV/providers/Microsoft.Compute/virtualMachines/DevWorkstation",
    "identity": null,
    "instanceView": null,
    "licenseType": null,
    "location": "southafricanorth",
    "name": "DevWorkstation",
    "networkProfile": {
      "networkApiVersion": null,
      "networkInterfaceConfigurations": null,
      "networkInterfaces": [
        {
          "deleteOption": null,
          "id": "/subscriptions/8b07a6be-3d14-4943-8af8-36d59994587b/resourceGroups/NziswanoDev/providers/Microsoft.Network/networkInterfaces/devworkstation413",
          "primary": null,
          "resourceGroup": "NziswanoDev"
        }
      ]
    },
    "osProfile": {
      "adminPassword": null,
      "adminUsername": "catenare",
      "allowExtensionOperations": true,
      "computerName": "DevWorkstation",
      "customData": null,
      "linuxConfiguration": {
        "disablePasswordAuthentication": true,
        "patchSettings": {
          "assessmentMode": "ImageDefault",
          "patchMode": "ImageDefault"
        },
        "provisionVmAgent": true,
        "ssh": {
          "publicKeys": [
            {
              "keyData": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDJ8BTI5lg7Lf5r706DUnKHBhR7\r\nS7m6sefWoVFAS3hjFE6SAM1mvOl3lZDY02gOLiOpmS3a/qAZObvFnSAojCkrtrDp\r\noto7acq+IxSx1if0S7pFc0+RhCXF8NyxzBCvB8xxxKZGsHOB52Bzkgs8InKts9yf\r\n0h0vZ99NfhJoV8mqTfzvtz0jUlJuX9IaBKP0euwz4634koAR31CtdhpasGDmeGmu\r\nSkNBr9OFe+Mf806xvpFr3+3hNv0FF6UX9eGcz66I9EuPxat+lbSNZTVgpkJZRWgl\r\nJK3PZNdd+GJ4X2oWW9otvzgT09SkQReVRz+O++rH5ok9lhGhJ8ojABX8nGprU/Dq\r\nZOxEvgppJHNTgrYRG8+8uYnz3NYaZNQBvE08Jwe30tqg5JhKJCQMP4EpDS0c2Vbz\r\nRcHii75zUmeAAG8yUUqpgif/J5j35VMX/5zxLmDIjjPeZ8xTir52HOWlvGumAMjE\r\nz9zHqaZAZK23ai+So6Lm8KeRnFJnndSdr0XqDeU= generated-by-azure\r\n",
              "path": "/home/catenare/.ssh/authorized_keys"
            }
          ]
        }
      },
      "requireGuestProvisionSignal": true,
      "secrets": [],
      "windowsConfiguration": null
    },
    "plan": null,
    "platformFaultDomain": null,
    "priority": null,
    "provisioningState": "Succeeded",
    "proximityPlacementGroup": null,
    "resourceGroup": "NZISWANODEV",
    "resources": [
      {
        "autoUpgradeMinorVersion": null,
        "enableAutomaticUpgrade": null,
        "forceUpdateTag": null,
        "id": "/subscriptions/8b07a6be-3d14-4943-8af8-36d59994587b/resourceGroups/NZISWANODEV/providers/Microsoft.Compute/virtualMachines/DevWorkstation/extensions/AzureNetworkWatcherExtension",
        "instanceView": null,
        "location": null,
        "name": null,
        "protectedSettings": null,
        "provisioningState": null,
        "publisher": null,
        "resourceGroup": "NZISWANODEV",
        "settings": null,
        "tags": null,
        "type": null,
        "typeHandlerVersion": null,
        "typePropertiesType": null
      }
    ],
    "scheduledEventsProfile": null,
    "securityProfile": null,
    "storageProfile": {
      "dataDisks": [],
      "imageReference": {
        "exactVersion": "20.04.202106140",
        "id": null,
        "offer": "0001-com-ubuntu-server-focal",
        "publisher": "canonical",
        "sku": "20_04-lts-gen2",
        "version": "latest"
      },
      "osDisk": {
        "caching": "ReadWrite",
        "createOption": "FromImage",
        "deleteOption": null,
        "diffDiskSettings": null,
        "diskSizeGb": null,
        "encryptionSettings": null,
        "image": null,
        "managedDisk": {
          "diskEncryptionSet": null,
          "id": "/subscriptions/8b07a6be-3d14-4943-8af8-36d59994587b/resourceGroups/NZISWANODEV/providers/Microsoft.Compute/disks/DevWorkstation_OsDisk_1_6ade046ccb0141c2a48d8c1b27df9547",
          "resourceGroup": "NZISWANODEV",
          "storageAccountType": null
        },
        "name": "DevWorkstation_OsDisk_1_6ade046ccb0141c2a48d8c1b27df9547",
        "osType": "Linux",
        "vhd": null,
        "writeAcceleratorEnabled": null
      }
    },
    "tags": {
      "Client": "Internal"
    },
    "type": "Microsoft.Compute/virtualMachines",
    "userData": null,
    "virtualMachineScaleSet": null,
    "vmId": "a60e1f74-f4fc-41a7-9e48-88e3b3b11242",
    "zones": null
  }
]
```