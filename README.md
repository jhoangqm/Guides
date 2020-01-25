# Guides
Guides

# NextCloud External Storage Openstack V3 with OVHcloud Object Storage

Here's a small guide on how to configure an External Storage with the OVHcloud Object Storage solution on Nextcloud.

 Here are the things you need to have:

- Openstack user
- OpenRC configuration file
- An Object Storage container
- Nextcloud installed on a server

Once you have everything noted above, you can start by configuring the external storage via Nextcloud

In the OpenRC file you will need to retrieve the following information:

export OS_AUTH_URL=https://auth.cloud.ovh.net/v3/
export OS_USER_DOMAIN_NAME=${OS_USER_DOMAIN_NAME:-"Default"}
export OS_USERNAME="xxxxxxxxxx"
export OS_PASSWORD=$OS_PASSWORD_INPUT
export OS_REGION_NAME="BHS"

For the password, you can generate the password via the Public Cloud Users & Management interface by clicking "Generate a password" on the user.

In the Nextcloud external storages configuration with Openstack v3 you will see the following information:

Service Name
Region
Bucket
Request timeout
Username
Domain
Password
Identity endpoint URL

You will need to fill each field with the appropriate value:

Here's an example:

Service Name: objectstoragetestv3
Region: BHS
Bucket: objectstoragetestv3 ( This is user-defined; think of it as a subdirectory of your total storage. The bucket will be created if it does not exist. )
Request timeout: 120 ( this is the default value )
Username: xxxxxxxxxx ( replace the X's by the username of your openstack account )
Domain: Default
Password: xxxxxxxxxx ( replace the X's by the password you generated from the control panel )
Identity endpoint URL: https://auth.cloud.ovh.net/v3/

Once that is done, it is important to note that by default Nextcloud does support Openstack v3 but the swiftfactory file needs to be configured.

server/lib/private/Files/ObjectStore/SwiftFactory.php 

Once you've found the location of the SwiftFactory.php file, you will need to comment out these line:

126 # if (!isset($this->params['scope'])) {
127 # throw new StorageAuthException('Scope has to be defined for V3 requests');
128 # }
129 #

After that is done, it should work.


