# V2.0-phpShop
This is a source file of phpShop.
Shop version V2.0
For additional instructions see the WEB-INF/docs/ directory.

Visit http://www.shikto.me for additional assistance.

!!!phpShop ToDo List!!!

* Need to add VAT tax capabilities
* Need to make product attributes easier to manage
* Need to fix formatting of overall admin screens
* Create an alternative shipping module for international shipping.
* Allow items to be place in more than one category.



*************
INSTALLATION
*************
!!Step 1. 
Make sure you have PHP 4.3.4 or higher
a.  Make sure that magic_quotes_gpc is ENABLED.  This can be done by editing the php.ini file. For more information on how to do this, please refer to the PHP manual.

!!Step 2.
Make sure you are running MySQL 3.23 or higher.

!!Step 3.
Uncompress the phpshop distribution anywhere inside your web tree.

!!Step 4. 
Now we have to create the phpShop database. You will need a MySQL user with sufficient permissions to do this. If you use a HOSTING server, you might have to use the tools they provide (ie. phpMyAdmin). You might also need to add the user and password options to the commands (-u <user> -p<password>) in the following examples, which use the command line programs usually provided in MySQL distributions.

   a. Create a database on MySQL:

   EXAMPLE:
   mysqladmin create phpshop

   b. We need to make sure we have a user with SELECT, INSERT
   UPDATE, DELETE, CREATE, ALTER, and DROP privileges:

   EXAMPLE:

   $ mysql -e "GRANT select, insert, update, create, alter, delete, drop
   ON phpshop TO dbuser@localhost IDENTIFIED BY 'dbpass'" phpshop
   $ mysqladmin reload

   where you replace the relevant information (i.e. phpshop (db name),
   dbuser, and dbpass).


   c. We then import the tables and data from the phpShop distribution. This
   includes the demo data. The file is found at ./db/phpshop.sql

   EXAMPLE:
   mysql -u dbuser -p dbpass -h localhost phpshop < ./db/phpshop.sql

If you use a hosting service, they may provide tools that automate much of the process described above.  Simply create the phpshop database and import the SQL file.

!!Step 5. 
Next we need to setup the WEB-INF/etc/config.php.  This is the main configuration file for the phpShop system. First off, we need to rename the etc/config-dist.php to etc/config.php.

Then edit etc/config.php.  You will need to edit the following entries: URL, SECUREURL, DB_HOST, DB_NAME, DB_USER, DB_PWD

   EXAMPLE:
     define("URL","http://your.site.org/demo/");
     define("SECUREURL","http://your.site.org/demo/");
     define("DB_HOST","localhost");
     define("DB_NAME","phpshop");
     define("DB_USER","dbuser");
     define("DB_PWD","dbpass");

    ** NOTE: If you do not have a secure server, you still must set the
       SECUREURL variable.  You can simply set it to be the same
       as the URL variable.  If you have a secure server then use the
       url to your secure sever (i.e. https://your.site.org/demo/).

You'll see a bunch of other stuff, but this will get you going for now. You can play with the rest later.  Beware of the beginning and ending slashes on the directory names.

!!Step 6. 
Open your web browser and go to the directory where you installed the index.php file:

   EXAMPLE:
     http://your.site.org/demo

You should see the demo store.

To get into the administration area, login as:

   username:  admin
   password:  test

In the administrative area, go the the phpShop Administrator and immediately change the admin's password to something else.

NOTE:  The following users are preinstalled in the phpShop distribution:

      UID            PWD       PERMS
      -------------- --------- ----------
      test           test      shopper
      storeadmin     test      storeadmin
      demo           demo      demo
      admin          test      admin

You should remove these users or reset their passwords before going live.

Study the demo store. Study both the shop and the way it is set up in the administrative area and you should be off to a good start!

Create your own store by editing "Washupito's Tiendita".

Let us know if anything goes wrong.  phpShop has quite a few lines of code which makes debugging a real... pleasant experience.  But we would not be able to enjoy the peace and tranquility of a soothing summer afternoon sitting - debugging, without your help.






##Authorize.Net

Shikto Release V2.0 of PHPShop

Using Authorize.net with phpShop

Authorize.net integration was added in version 0.7.0 of phpshop
using Authorize.Net's Advanced Integration Method (AIM) using 
OpenSSL and sockets to send and receive information securely.
Read Authorize.Net implementation guides to better understand 
how to implement it.

Requirements:
- PHP 4.3.0 or later, compiled with OpenSSL support.

  NOTE: There was a bug in Windows PHP with using fsockopen() in 
        SSL mode. A patch is offered at:
        http://ftp.proventum.net/pub/php/win32/misc/openssl/
        (use at your own risk)

Installation:
1. In the phpshop.cfg file you need to set 4 variables:
   AN_ENABLE, AN_LOGIN, AN_TRAN_KEY, AN_TYPE, AN_TEST_REQUEST

   - AN explanation and an example of each is provided in the 
     phpshop.cfg file.

2. You must also enable each "Payment Method" to be used with authorization
   methods (ie. Authorize.net). This is done in the Administration area of
   phpshop:
     - In "Store", choose "List Payment Methods"
     - Make sure that the desired Payment Methods have a "Y" for "Authorize".

This should enable Authorize.Net

Advanced Settings:
------------------
Authorize.Net has many configurations. You can set all these in:
./modules/checkout/lib/ps_checkout.inc
on the authnet_process() function.
(Careful editing this file. Make sure you understand what you are
doing)

csv product upload script for phpShop
Created by John Syben (webme.co.nz)
Version 0.3 13 Sept 2002
Comments/Questions: john@webme.co.nz

OVERVIEW
This script allows for the bulk addition of products to the phpShop database.
It will create categories as required and will update product if it's sku alreay exists.

HOW TO USE IT
First you need a csv file with the required product information.
See test.csv for an example.

The following product information can be included:
  product_sku
  product_s_desc
  product_desc
  product_thumb_image
  product_full_image
  product_weight
  product_weight_uom
  product_length
  product_width
  product_height
  product_lwh_uom
  product_in_stock
  product_available_date
  product_special
  product_discount_id
  product_name
  product_price
  category_path

Minimum required information is
  product_sku
  product_name
  product_price
  category_path

category_path is a slash delimited string which begins
with a top-level category and follows with sub-categories,
e.g. category/sub-category_1/sub_category_2

product_thumb_image and product_full_image
are the names of the respective image files. You will
need to FTP the image directly to the image folder.

In the csv table, each of the above product fields
is assigned a number which represents it's position
in the delimited line. You can change these to suit the
positions in your own lines. The positions set in the
mycsv.sql file relate to the included test.csv so you
can test your installation.

No just go to products/csv_upload.ihtml,
browse to the csv file and hit submit.
##############################################
ADDITIONAL FILE
confirm_images.ihtml

This is a companion to the csv_upload script

After you use the csv_upload script you need to
FTP your images to the shop_image/product directory
to match the image names from the csv file.
This script will get all the image names from the product
table and check if the images are in the shop_image/product
folder and report which files are missing.

Simply put this file in the product/html folder
and make a link to it in the menu.

##CYBERCASH and phpShop##

* We are deprecating support for Cybercash as the payment gateway is no 
longer used by Verisign.

phpShop offers integration with the Cybercash CashRegister software.
In order to use Cybercash with phpShop (or with PHP for that matter) you
need to recompile your PHP intepreter with the cybercash extensions
provided by the PHP team.  The extensions are in the ext/cyberlib directory 
under your source distribution of PHP.   
                
In order to set up PHP for this, do the following:

1.  Setup a cybercash account or get a demo account where they
    will provide you with a Merchant ID.  

2.  Download the Cybercask MCK for your OS type.  Install the C API by 
    following the MCK installation instructions.

3.  Setup your PHP source by running the configure script with your
    regular setup options and add:
  
                      --with-cybercash=[DIR]
    
    if using PHP 3.x it will be

		      --with-mck=[DIR]

    where [DIR] is the path to the MCK C API files.    

4.  In the phpshop.cfg file you need to set 4 variables.  They are:

    CC_MERCHANT            => This is your Cybercash ID.
    CC_MERCHANT_KEY"       => Your Cybercash Secret Merchant Key
    CC_PAYMENT_URL"        => The Cybercash Payment URL
    CC_AUTH_TYPE"          => The authentication type preceded by the 
			      letter 'm' (e.g. mauthonly)

    These fields are given to you immediately by Cybercash.  It's actually quite 
    simple

5.  The payment methods listed in the Store Administrator allow you to select which 
    payment methods Cybercash is setup to handle. Select the cards you want to support
    and enable the Cybercash processing by selecting it and saving the changes.

You are now setup to handle Cybercash!


The Cybercash transaction log is appended to each Order in the Order Administrator.


