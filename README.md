#System Preparation#

1) Download and install [WAMPSERVER][1] to install Apache and PHP(32 bit for example). if you met install exception on missing "MSVCR110.dll is missing", you can fix this by refering to http://forum.wampserver.com/read.php?2,123608

2) Add following modules in Apache with WAMPSERVER:  

 - expires_module
 - headers_module
 - rewrite_module

3) Add following modules in PHP with WAMPSERVER:  

 - php_gd2
 - php_zip(no need)
 - php_curl
 - zlib output compression (in settings)

4) Restart WAMPSERVER. Link to [localhost:80][2] to check if it works.

5) Download following tools and **make them available in the path** for video and jpeg analysis:  

 - [ffmpeg][3]
 - [jpegtran][4]
 - [exiftool][5]


#Web Server Configuration#

 1) Download and unzip [WebPagetest Private Instances archive][6]. Two
    folders will be used: **www** and **agent**.

 2) Configure Apache in **httpd.conf**, add following configuration (you can define the path */var/www/webpagetest* by yourself).

```
<Directory "/var/www/webpagetest">  
    AllowOverride all
    Order allow,deny
    Allow from all 
</Directory>
<VirtualHost *:80>
    DocumentRoot /var/www/webpagetest 
</VirtualHost>
```
3) Set **upload_max_filesize** and **post_max_size** to large values(10M should be enough) in **php.ini**. 
  
4) Restart WAMPSERVER.

5) Copy the files under the **www** folder in the archive to the DocumentRoot location (e.g. */var/www/webpagetest*).

6) Make a copy of all of the **.sample** files (removing the .sample extension) under the **settings** folder.

7) Define agent locations by editing **locations.ini** under the **setting** folder. Note that the first browser of the default location will be used in Visual Comparison.


#Test Machine Configuration#

1) Copy the files under the **agent** folder to your agent path (e.g. "*C:\WPTAgent*").

2) Install **AVISynth** from the installer in the **agent** folder, which is necessary for creating videos.

3) Install the **DUMMYNET** ipfw driver  

   1. (**only for** those installing on **64-bit** Windows) Right-click on "*testmode.cmd*" in the *C:\WPTAgent\dummynet\64bit* folder and "Run as Administrator". **Reboot the system to enable testmode.**  

   2. (depending on your OS) Copy the files from either the *C:\WPTAgent\dummynet\32bit* or *C:\WPTAgent\dummynet\64bit* directory into the *C:\WPTAgent\dummynet* directory

   3. Open the properties for the Network Adapter that is used to access the Internet. Normally it is **Local Area Connection** in the path *Control Panel\Network and Internet\Network and Sharing Center\*

   4. Click "Install"

   5. Select "Service" and click "Add"

   6. Click "Have Disk" and navigate to *C:\WPTAgent\dummynet*

   7. Select the ipfw+dummynet service (and click through any warnings about the driver being unsigned)


#WPTDriver Configuration#
**(for running test on Chrome and Firefox)**

1) Create a shortcut to **C:\WPTAgent\wptdriver.exe** on the Desktop.

2) Make a copy of **wptdriver.init.sample** and removing the .sample extension.

3) Configure WPTDriver by editing **wptdriver.ini**.

   1. After manually installing Chrome and Firefox, make sure the path to the **browser executables** are correct

   2. Remove or comment **installer=...** entry for each of the browsers you've manually installed

   3. (only if you've modified configurations in locations.ini when configuring Web Server) Configure the location and the location key to match those defined in locations.ini on the server

4) Reboot the system


#Install Chrome Frame (Deprecated)#

Download and install [Chrome Frame][7]. 


#How to upgrade the WPT private instance:#

Preparation: 

1) Download the lastest WPT zip file and extract to local Disk 

Config WPT Agent: 

2-1) Copy C:\WPT\webpagetest_2.15\agent and paste to C:\WPTAgent\ 

2-2) Edit or Paste original version of wptdriver.ini 

2-3) Copy all files from C:\WPTAgent\dummynet\64bit to C:\WPTAgent\dummynet\ (For example, Based on 64bit OS) 

Config WPT Server: 

3-1) Copy all files from C:\WPT\webpagetest_2.15\www\ and paste them to C:\WPTServer\www\webpagetest\ 

3-2) Go to "settings" folder and Edit/paste original version of all *.sample files 

3-3) Copy and paste C:\WPTServer\exiftool , C:\WPTServer\ffmpeg, C:\WPTServer\jpegtran 

3-4) Reboot the system and run the WPTdriver shotcut to start your test! 


#[How to make RDP window session never expired(fix black video captured)][8]#
#[How to fix the black screen when you minimize your RDP][9]#

  [1]: http://www.wampserver.com/en/
  [2]: http://localhost:80
  [3]: http://www.ffmpeg.org/download.html
  [4]: http://jpegclub.org/jpegtran/
  [5]: http://www.sno.phy.queensu.ca/~phil/exiftool/
  [6]: https://sites.google.com/a/webpagetest.org/docs/private-instances/releases
  [7]: http://www.google.com/chromeframe/eula.html?prefersystemlevel=true
  [8]: http://technet.microsoft.com/en-us/library/cc754272.aspx
  [9]: http://serverfault.com/questions/48650/remote-desktop-session-black-after-minimize
