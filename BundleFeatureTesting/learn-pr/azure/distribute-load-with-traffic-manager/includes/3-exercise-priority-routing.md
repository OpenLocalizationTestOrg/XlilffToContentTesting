---
ms.openlocfilehash: efc18a3148293f7ee0e31981b6e919c5def49859
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
Let's assume that your music streaming application has an equal distribution of users in the western United States and eastern Asia. You'd like to have a failover version of the app, in one of the regions.

The sample application we'll use for this exercise will display the region it's running in on the page. One of the two instances will have higher priority and will be the primary endpoint. The other instance will have lower priority and will be the failover endpoint. Taking the primary endpoint offline will automatically route all traffic to failover endpoint.

You'll set up Traffic Manager to use the US endpoint as the primary, failing over to the Asian endpoint if any errors occur.

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-new-traffic-manager-profile"></a>Create a new Traffic Manager profile

1. In the Cloud Shell, run this command to create a Traffic Manager profile.

    ```azurecli
    az network traffic-manager profile create \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name TM-MusicStream-Priority \
        --routing-method Priority \
        --unique-dns-name TM-MusicStream-Priority-$RANDOM
    ```

    There are a couple parameters of note in this command:

    - **--routing-method Priority** - Create the Traffic Manager profile using the priority routing method.
    - **--unique-dns-name** - Creates a globally unique domain name `<unique-dns-name>.trafficmanager.net`. We use the `$RANDOM` Bash function to return a random whole number to ensure the name is unique.

## <a name="deploy-the-web-apps-to-the-regions"></a>Deploy the web apps to the regions

1. Deploy the East Asia web app.

    ```azurecli
    EASTAPP="MusicStore-EastAsia-$RANDOM"

    az appservice plan create \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name MusicStore-EastAsia-Plan \
        --location eastasia \
        --sku S1

    az webapp create \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name $EASTAPP \
        --plan MusicStore-EastAsia-Plan \
        --runtime "node|10.6" \
        --deployment-source-url https://github.com/MicrosoftDocs/mslearn-distribute-load-with-traffic-manager
    ```

    Note the `--sku S1` parameter when you created the app service plan. Traffic Manager is a premium feature that requires web apps to be running on at least a S1 pricing tier plan.

1. Deploy the West US 2 web app.

    ```azurecli
    WESTAPP="MusicStore-WestUS-$RANDOM"

    az appservice plan create \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name MusicStore-WestUS-Plan \
        --location westus2 \
        --sku S1

    az webapp create \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name $WESTAPP \
        --plan MusicStore-WestUS-Plan \
        --runtime "node|10.6" \
        --deployment-source-url https://github.com/MicrosoftDocs/mslearn-distribute-load-with-traffic-manager
    ```

## <a name="add-the-endpoints-to-the-traffic-manager"></a>Add the endpoints to the Traffic Manager

1. With both the web apps created, add them as endpoints to the Traffic Manager profile.

    ```azurecli
    WestId=$(az webapp show \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name $WESTAPP \
        --query id \
        --out tsv)

    az network traffic-manager endpoint create \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --profile-name TM-MusicStream-Priority \
        --name "Primary-WestUS" \
        --type azureEndpoints \
        --priority 1 \
        --target-resource-id $WestId

    EastId=$(az webapp show \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name $EASTAPP \
        --query id \
        --out tsv)

    az network traffic-manager endpoint create \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --profile-name TM-MusicStream-Priority \
        --name "Failover-EastAsia" \
        --type azureEndpoints \
        --priority 2 \
        --target-resource-id $EastId
    ```

    The above commands get the unique IDs from both of the web apps, then uses those IDs to add them as endpoints to the Traffic Manager profile. Using the `--priority` flag to set the West US app to the highest priority.

1. Let's take a quick look at the endpoints we configured.

    ```azurecli
    az network traffic-manager endpoint list \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --profile-name TM-MusicStream-Priority \
        --output table
    ```

## <a name="test-the-app"></a>Test the app

1. Let's take a look at what DNS shows for the web apps and for our Traffic Manager profile. The following command will output the IP addresses for each of the resources we've created.

    ```bash
    # Retrieve the address for the West US 2 web app
    nslookup $WESTAPP.azurewebsites.net
    # Retrieve the address for the East Asia web app
    nslookup $EASTAPP.azurewebsites.net
    # Retrieve the address for the Traffic Manager profile
    nslookup $(az network traffic-manager profile show \
                --resource-group <rgn>[sandbox resource group name]</rgn> \
                --name TM-MusicStream-Priority \
                --query dnsConfig.fqdn \
                --out tsv)
    ```

    The address for the Traffic Manager profile should match the West US 2 web app.

1. Navigate to the Traffic Manager profiles Fully Qualified Domain Name (FQDN), your request will be routed to the endpoint that responds with the highest priority.

    ```bash
    echo http://$(az network traffic-manager profile show \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name TM-MusicStream-Priority \
        --query dnsConfig.fqdn \
        --out tsv)
    ```

    The above prints out the FQDN in the Cloud Shell to allow you to click on it to open a new browser window or tab.

1. Verify that the application is working and the location shown at the bottom of the page is "West US 2".

    ![Screenshot of the running West US web app](../media/3-west-us-app.png)

1. Disable the primary endpoint.

    ```bash
    az network traffic-manager endpoint update \
        --resource-group <rgn>[sandbox resource group name]</rgn>  \
        --name "Primary-WestUS" \
        --profile-name TM-MusicStream-Priority \
        --type azureEndpoints \
        --endpoint-status Disabled
    ```

1. Let's again look at what DNS shows for the web apps and for our Traffic Manager profile.

    ```bash
    # Retrieve the address for the West US 2 web app
    nslookup $WESTAPP.azurewebsites.net
    # Retrieve the address for the East Asia web app
    nslookup $EASTAPP.azurewebsites.net
    # Retrieve the address for the Traffic Manager profile
    nslookup $(az network traffic-manager profile show \
                --resource-group <rgn>[sandbox resource group name]</rgn> \
                --name TM-MusicStream-Priority \
                --query dnsConfig.fqdn \
                --out tsv)
    ```

    The address for the Traffic Manager profile should now match the East Asia web app.

1. Test the application again from your browser by refreshing the web page. Traffic Manager should automatically redirect the traffic to the East Asia endpoint. Depending on your browser, this might take a few minutes for the cached address to expire. Opening the site in a private window should bypass this cache, allowing you to see the change immediately.

    ![Screenshot of the running East Asia web app](../media/3-east-asia-app.png)
