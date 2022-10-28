# AWS Lightsail

## Background

Before you use lightsail, here is the pros and cons.

You can choose one of their pricing plans (starting at $3.50 USD per month) and have full control over your WordPress installation, including plugins.

Creating a Lightsail WordPress instance only takes a few minutes and self-maintained by AWS. No infrastructure knowledge is required. You only need to take care the wordpress content (your portfolio :clap: ) and the domain management.

Combining with AWS Lightsail and Cloudflare (Domain Management), you can have full access of everything. 

No need to depend on anyone and no need to maintain a physical server, suit for you :joy:

> Of course, you can choose to start a AWS EC2 instance for hosting a wordpress server. But it requires advanced knowledge on setting up the server,  network routing and domain management. With the advanced knowledge, you can keep the cost as low as possible.

But I would say *3.5 USD* per month is such a low price and you can skip everything and let AWS to take care of them.

Moreover, Cloudflare is free of charge for this kind of personal use.


## 3.5 USD Config and Cost illustration
___

| Item | Config |
| - | - |
| Memory | 512 MB |
| CPU | 1 Core Processor |
| Harddisk | 20 GB SSD |
| Data Transfer | 1 GB |


The website uses a CDN distribution to serve content around the world with a year free up to 50 GB, and hosts its static content in a Lightsail object storage bucket with 5 GB storage and 25 GB transfer. CDN helps you distribute your portfolio with cache, boots up your website performance, you are so international la.

Lightsail charges:

WordPress instance = $3.5 USD / month
CDN distribution = Free first year
Object Storage bucket = Free for first year, $1 USD / month
Total charges: $3.5 to get your WordPress site delivered around the world

![Steps to migrate](https://github.com/dannyyuen/awsWordPress/blob/main/00.png?raw=true)

# Prerequisites
1. [X] AWS account with credit card payment - [AWS Sign-up page](https://console.aws.amazon.com/console/home)
2. [X] Cloudflare account - [Cloudflare Sign-up page](https://developers.cloudflare.com/fundamentals/account-and-billing/account-setup/create-account/)
3. [X] GoDaddy Login ready

### Step 1: Back up your existing WordPress blog
___
You can use WordPress to back up your existing blog.

Navigate to your blog, and then choose Manage.

1. Enter your user name and password to log into the WordPress admin console.
2. On the WordPress Dashboard, choose Tools, and then choose Export.
3. On the Export page, choose All content to export everything as an XML file.

![Export XML](https://github.com/dannyyuen/awsWordPress/blob/main/01.png?raw=true)

4. Choose Download export file to download your old blog as an XML file.
5. Save the XML file in a location that's easy to find. You'll need it in the later part of Step 4.

### Step 2: Create a new WordPress instance in Lightsail
___

![Search Lightsail in aws](https://github.com/dannyyuen/awsWordPress/blob/main/08.png?raw=true)

1. Go to the Lightsail home page and log in.
2. Choose Create instance.
3. Select the AWS Region HK / Tokyo.
4. You can choose the default Availability Zone or change that once you select an AWS Region. WordPress is the default application on this page. Double-check that WordPress is selected. (App + OS)

![Select Instance](https://github.com/dannyyuen/awsWordPress/blob/main/02.png?raw=true)

5. Choose your $3.5 USD plan. (you can upgrade your Lightsail plan later if needed.)
6. Enter a name for your instance, 

> Resource name:
> Must contain 2 to 255 characters
> 
> Must start and end with an alphanumeric character or number.
> 
> Can include alphanumeric characters, numbers, periods, dashes, and underscores.

7. Choose Create instance.

### Step 3: Log into your new Lightsail WordPress blog
___
Now that you have a new blog in Lightsail, you'll need to access the WordPress Dashboard to import your old blog data.

1. Go to the Lightsail home page and find your WordPress blog.
2. Copy the Public IP address to the clipboard. You'll find this address listed on the Lightsail home page or on the instance details page.

![Find IP](https://github.com/dannyyuen/awsWordPress/blob/main/03.png?raw=true)

3. Paste the IP address into your browser, and add /wp-login.php at the end of the IP address. For example, 192.0.2.1/wp-login.php. You should see something like this:

![Login](https://github.com/dannyyuen/awsWordPress/blob/main/04.png?raw=true)

4. Use the default user name (user).

5. To get the login password, you'll need to connect to your instance. The simplest way to connect is to use the terminal icon next to your Lightsail instance.

## Type the following

```
cat bitnami_application_password
```

Note:
> 
> If you're in a directory other than the user home directory, then type cat $HOME/bitnami_application_password

You should see something like this:

![Find Password](https://github.com/dannyyuen/awsWordPress/blob/main/06.png?raw=true)

1. Highlight your password in the terminal screen, then choose the clipboard icon.
2. Highlight the text you want to copy in the clipboard text box, then press Ctrl+C or Cmd+C to copy the text to your local clipboard.
3. Paste your password into the WordPress login page, and then choose Log In.

If successful, you'll see the WordPress Dashboard.

### Step 4: Import your XML file into your new Lightsail blog
___
Once you have successfully logged into the WordPress Dashboard on your new Lightsail instance, follow these steps to import the XML file into your new Lightsail blog.

1. From the WordPress Dashboard on your new Lightsail instance, choose Tools.
2. Choose Import, and then choose Install Now to install the WordPress import tool.

![XML import](https://github.com/dannyyuen/awsWordPress/blob/main/07.png?raw=true)

3. Once the tool is done installing, choose Run Importer to run the import tool. On the Import WordPress page, choose Browse. Find the XML file you saved in Step 1: Back up your existing WordPress blog, and then choose Open.

4. Choose Upload file and import.

Accept the rest of the defaults, and then choose Submit.


# Another way to backup and migrate wordpress is using wordpress plugin

> *I have used All-in-one WP Migration before and it should be already installed in your wordpress admin panel for local hosting in your M800 computer.*

All-in-One WP Migration is probably the most popular WordPress moving plugin on the list. Unlike other plugins on this list that offer features like backup, staging, and security, All-in-One WP Migration focuses solely on the migration feature. The plugin exports your WordPress site which you can then drag and drop to another location.

## Highlights

Although you can bypass upload restrictions from your hosting provider, the migration plugin also has an upload restriction of only 512MB. Please check your exported files from the old admin panel.

> Ref: [All-in-one-wp-migration](https://wordpress.org/plugins/all-in-one-wp-migration/)

> Ref: [Other migration plugin](https://blogvault.net/wordpress-migration-plugins/)

# Cloudflare's domain name migration

## Step 1: Transfer out domain from GoDaddy
Transfer the domain from GoDaddy to Cloudflare

Can follow this [GoDaddy page](https://hk.godaddy.com/en/help/transfer-my-domain-away-from-godaddy-3560) to transfer away the domain from GoDaddy. After the process has been completed, you will get the authorization code and it is required to input in Cloudflare.

## Step 2: Accept domain in Cloudflare
Before moving GoDaddy domain to Cloudflare, ensure the aws lightsail is working as expected. Do UAT first ar.

1. Initiate your transfer to Cloudflare
Go to the Account Home > [Registrar](https://dash.cloudflare.com/?to=/:account/domains/transfer). Cloudflare will display the zones available for transfer.

You will be presented with the price for each transfer. When you transfer a domain, you are required by ICANN to pay to extend its registration by one year from the expiration date (One off fee to extend the valid date of domain). You can remove domains from your transfer by selecting x.

If you do not have a payment method on file, add one at this step before proceeding.

You will not be billed at this step. Cloudflare will only bill your card when you input the auth code and confirm the contact information at the conclusion of your transfer request.

2. Input your authorization code
In the next page, input the authorization code for each domain you are transferring. You also need to unlock each domain so that Cloudflare can process your request. For more information, refer to the instructions provided by your current registrar on how to transfer your domain.

3. Confirm or input your contact information
In the final stage of the transfer process, input the contact information for your registration. Cloudflare Registrar redacts this information by default but is required to collect the authentic contact information for this registration. It is important that you provide accurate WHOIS contact information. You may be required to verify the contact information. Failure to provide accurate information and/or failure to verify the information may result in suspension or deletion of your domain. After entering the contact information, agree to the domain registration terms of service by selecting Confirm transfer.

4. Approve the transfer
Once you have requested your transfer, Cloudflare will begin processing it, and send a Form of Authorization (FOA) email to the registrant, if the information is available in the public WHOIS database. The FOA is what authorizes the domain transfer.

After this step, your previous registrar will also email you to confirm your request to transfer. Most registrars will include a link to confirm the transfer request. If you select that link, you can accelerate the transfer operation. If you do not act on the email, the registrar can wait up to five days to process the transfer to Cloudflare. You may also be able to approve the transfer from within your current registrar dashboard.

​​Next steps
As mentioned in Review DNS records in Cloudflare, when moving your domain to Cloudflare Registrar, you might need to configure your DNS records to correctly point traffic to your web host. Cloudflare automatically scans for common records and adds them to your account’s DNS page, but the scan is not guaranteed to find all existing DNS records.

Refer to your web host’s documentation to learn what type of records you need to configure and where they should point, to avoid downtime.

For example, Netlify asks customers that host websites with them to add a CNAME record pointing <YOUR-DOMAIN> to apex-loadbalancer.netlify.com, and another CNAME record pointing www to <YOUR-DOMAIN>.netlify.app, depending on which one is the primary domain.

Remember to follow the below TLS setting for proxy the request to lightsail (CDN + CDN help to boot the routing)
![TLS Setting](https://github.com/dannyyuen/awsWordPress/blob/main/cloudflare1.png?raw=true)
Example of adding DNS records, cloudfront domain is provided by AWS lightsail
![DNS Record](https://github.com/dannyyuen/awsWordPress/blob/main/cloudflare2.png?raw=true)


# Conclusion
ALL THE BEST !!!
