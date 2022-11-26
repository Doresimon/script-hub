# Quick Commands to create Server on Azure

## Scripts

```bash
#############################
#### Step 1 (Azure Bash) ####

### parameters ###
export today=$(date +%Y%m%d)
export lucky_number=$RANDOM
export group=v2ray_${today}_$lucky_number
export reource_group_name=rg_$group
export reource_group_location=eastasia
export vm_name=vm_$group
export vm_admin_username=halo
export vm_admin_password=@Pa55W0rD$RANDOM # The password length must be between 12 and 72. Password must have the 3 of the following: 1 lower case character, 1 upper case character, 1 number and 1 special character.
export vm_authentication_type=all # [all, password, ssh]
export vm_image_type=Canonical:0001-com-ubuntu-server-jammy:22_04-lts-gen2:latest # [UbuntuLTS, Canonical:0001-com-ubuntu-server-jammy:22_04-lts-gen2:latest]
export vm_size=Standard_D2s_v3 # HK$550/month ## az vm list-sizes
export vm_ports_to_open=10086-10096 #

### create resource group ###
az group create \
--name $reource_group_name \
--location $reource_group_location

### create vm ###
az vm create \
--name $vm_name \
--resource-group $reource_group_name \
--admin-username $vm_admin_username \
--admin-password $vm_admin_password \
--authentication-type  $vm_authentication_type \
--image $vm_image_type \
--size $vm_size \
--public-ip-sku Standard \
--zone 2 \
--generate-ssh-keys

### open port ###
az vm open-port --resource-group $reource_group_name --name $vm_name --port $vm_ports_to_open --priority 1024

### login ###
export vm_public_ip=$(az vm show -d --resource-group $reource_group_name --name $vm_name --query publicIps -o tsv)
ssh -i ~/.ssh/id_rsa $vm_admin_username@$vm_public_ip -o StrictHostKeyChecking=no

#### Step 1 (Done) ####
#######################



##########################
#### Step 2 (VM Bash) ####

### in vm~ ###
export workdir=work
export PORT_10086=10086
export USER_GUID_10086=$(uuidgen)
export PORT_10087=10087
export USER_GUID_10087=$(uuidgen)
export PORT_10088=10088
export USER_GUID_10088=$(uuidgen)
export PORT_10089=10089
export USER_GUID_10089=$(uuidgen)
export JSON_PATH="/usr/local/etc/v2ray"
export CONFIG_CURRENT_JSON_FILE="config.current.json"
export CONFIG_JSON_FILE="$JSON_PATH/config.json"
sudo apt update -y && sudo apt install curl -y
mkdir $workdir && cd $workdir
curl -O https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh && sudo bash install-release.sh
curl -O https://raw.githubusercontent.com/Doresimon/script-hub/main/network/v2ray/config.template.json && sudo cp config.template.json $CONFIG_CURRENT_JSON_FILE 
sudo sed -i "s/%PORT_10086%/$PORT_10086/" $CONFIG_CURRENT_JSON_FILE 
sudo sed -i "s/%USER_GUID_10086%/$USER_GUID_10086/" $CONFIG_CURRENT_JSON_FILE 
sudo sed -i "s/%PORT_10087%/$PORT_10087/" $CONFIG_CURRENT_JSON_FILE 
sudo sed -i "s/%USER_GUID_10087%/$USER_GUID_10087/" $CONFIG_CURRENT_JSON_FILE 
sudo sed -i "s/%PORT_10088%/$PORT_10088/" $CONFIG_CURRENT_JSON_FILE 
sudo sed -i "s/%USER_GUID_10088%/$USER_GUID_10088/" $CONFIG_CURRENT_JSON_FILE 
sudo sed -i "s/%PORT_10089%/$PORT_10089/" $CONFIG_CURRENT_JSON_FILE 
sudo sed -i "s/%USER_GUID_10089%/$USER_GUID_10089/" $CONFIG_CURRENT_JSON_FILE 
sudo cp $CONFIG_CURRENT_JSON_FILE $CONFIG_JSON_FILE
sudo systemctl restart v2ray
systemctl status v2ray

#### Step 2 (Done) ####
#######################



#####################################
#### Step 3 (Get All Parameters) ####

# in VM
echo -e "\n################################################\n####            User Parameter ~            ####\n################################################\nUser 10086:\nPort = $PORT_10086\nGuid = $USER_GUID_10086\nLevel = 1\nAlterId = 64\n################################################\nUser 10087:\nPort = $PORT_10087\nGuid = $USER_GUID_10087\nLevel = 1\nAlterId = 64\n################################################\nUser 10088:\nPort = $PORT_10088\nGuid = $USER_GUID_10088\nLevel = 1\nAlterId = 64\n################################################\nUser 10089:\nPort = $PORT_10089\nGuid = $USER_GUID_10089\nLevel = 1\nAlterId = 64\n################################################" && exit
# in Azure Bash
echo -e "\n################################################\n####             VM Parameter ~             ####\n################################################\nVM:\nPublic IP = $vm_public_ip\nName = $vm_name\nResource Group = $reource_group_name\n################################################"

#### Step 3 (Done) ####
#######################
```

## Clients

- [v2rayN](https://github.com/2dust/v2rayN)
  - `Windows`
- [V2rayU](https://github.com/yanue/V2rayU)
  - `MacOS`
- [v2rayNG](https://github.com/2dust/v2rayNG)
  - `Andriod`
- [v2rayA](https://github.com/v2rayA/v2rayA)
  - `Linux`
- ???
  - `IOS`
