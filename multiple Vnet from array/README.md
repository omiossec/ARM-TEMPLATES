# Deploy Multiple Azure Virtual Network with multiple Sub Net

This themplate deploy multiple Azure Virtual Network in on resource group (it can be change to deploy vnet accross multiple resources groups and multiple subscriptions).

Network configuration is stored in the parameter file inside a array or array. 

````Json
"NetConf": {
            "value": [
                {
                    "VirtualNetworkName": "Production",
                    "CIDR": "172.24.0.0/24",
                    "Subnet": [
                        {
                            "SubnetName": "Prod",
                            "Prefix": "172.24.0.0/24"
                        }
                    ]
                },
                {
                    "VirtualNetworkName": "Dev",
                    "CIDR": "172.25.0.0/24",
                    "Subnet": [
                        {
                            "SubnetName": "Dev",
                            "Prefix": "172.25.0.0/25"
                        },
                        {
                            "SubnetName": "bacasable",
                            "Prefix": "172.25.0.128/25"
                        }
                    ]
                }
            ]
        }
````

You can add any Virtual Network with any number of subnet. The only rule is that you need to make sur your prefix are correct and that there is no overlap betwen network ID. 

To deploy 

````PowerShell
new-AzResourceGroupDeployment -ResourceGroupName <ResourceGroup> -TemplateParameterFile .\azuredeploy.paramters.json -TemplateFile .\azuredeploy.json -Verbose
````

