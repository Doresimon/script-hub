# create vm

## base

```bash
#############################
#### Step 1 (Azure Bash) ####
### parameters ###
export lucky_numer=$RANDOM
export group=v2ray_$lucky_numer
# resource group
export reource_group_name=rg_$group
export reource_group_location=eastasia
# vm
export vm_name=vm_$group
export vm_admin_username=user_$group
export vm_admin_password=@Pa55W0rD$RANDOM # The password length must be between 12 and 72. Password must have the 3 of the following: 1 lower case character, 1 upper case character, 1 number and 1 special character.
export vm_authentication_type=ssh # [all, password, ssh]
export vm_os_type=linux # [linux, windows]
export vm_image_type=UbuntuLTS # [UbuntuLTS]
export vm_max_price_in_us_dollar=120
export vm_size=Standard_DS1_v2 # $78.11/month
export vm_host=$vm_name$vm_image_type #
# port
export vm_ports_to_open=443,10086 #


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
--generate-ssh-keys
# --host $vm_host \
# --max-price $vm_max_price_in_us_dollar \
# --location $reource_group_location \
# --os-type $vm_os_type \

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
export PORT_X=10086
export USER_GUID_X=$(uuidgen)
export PORT_Y=10087
export USER_GUID_Y=$(uuidgen)
export JSON_PATH="/usr/local/etc/v2ray"
export CONFIG_JSON_FILE="$JSON_PATH/config.json"
sudo apt update && sudo apt install curl
mkdir $workdir && cd $workdir
curl -O https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh && sudo bash install-release.sh
curl -O https://raw.githubusercontent.com/Doresimon/script-hub/v2ray-config-template/network/v2ray/config.template.json && sudo cp config.template.json $CONFIG_JSON_FILE
sudo sed -i "s/%PORT_X%/$PORT_X/" $CONFIG_JSON_FILE
sudo sed -i "s/%USER_GUID_X%/$USER_GUID_X/" $CONFIG_JSON_FILE
sudo sed -i "s/%PORT_Y%/$PORT_Y/" $CONFIG_JSON_FILE
sudo sed -i "s/%USER_GUID_Y%/$USER_GUID_Y/" $CONFIG_JSON_FILE
sudo systemctl restart v2ray
systemctl status v2ray

#### Step 2 (Done) ####
#######################



#####################################
#### Step 3 (Get All Parameters) ####

# in VM
echo -e "\n################################################\n####            User Parameter ~            ####\n################################################\nUser X:\nPort = $PORT_X\nGuid = $USER_GUID_X\nLevel = 1\nAlterId = 64\n################################################\nUser Y:\nPort = $PORT_Y\nGuid = $USER_GUID_Y\nLevel = 1\nAlterId = 64\n################################################" && exit
# in Azure Bash
echo -e "\n################################################\n####             VM Parameter ~             ####\n################################################\nVM:\nPublic IP = $vm_public_ip\nName = $vm_name\nResource Group = $reource_group_name\n################################################"

#### Step 3 (Done) ####
#######################
```
