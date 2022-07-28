You must have the internet toolkit installed and configured for this package to function properly.

1) Make sure that the RemotePanels.llb has been installed in <LabVIEW>/www/cgi-bin/test/.	

2) Start LabVIEW. Go to Tools=>Options=>Web Server: Configuration page, and enable the LabVIEW
built-in web server, RUNNING ON PORT 8080.

3) You will need more than one (default) remote panel license enabled in order to open several remote pages.

4) Go to Tools=>Internet Toolkit=>G Web Server Configuration. 
On the Operation page, select the Independent G Web Server option and set the port to 80. 
Make sure the server's root directory is set to <LabVIEW dir>/www. 
Click on the Advanced tag, and click on the Start G Web Server button. 
When the server is running, click on the Connect Browser button.

5) In your web browser, go to http://localhost/cgi-bin/test/default.html.  A configuration form should appear.
Hit "submit" on the form. This should cause the VI "redirect.vi" to run, which will clone a new handler 
from the handler template (handler.vit), create an HTML document in <LabVIEW dir>/www that contains an embedded 
link to the handler VI, and return HTML code to the web browser that redirects the browser to the HTML document 
just created.  

6) The created HTML document allows you to use the handler VI for 5 minutes. After that time (or if you select
the Finish button on the page) it will redirect you back to the default.html page.

7) Since the VI is opened as a template VI, each run of the CGI (default.html page) will result in a new
instance of the VI, with a new number in its name. Each client can gain control of its instance.
The numbers in the VIs names are 32 bit integers, so the highest number will be 4,294,967,295.

8) These instance numbers in the handler VIs names, start from 0 and increment by 1, until the 
CGI application is closed. Therefore, the application is not aware of what previous numbers are 
still in use.
If you would prefer to not iterate indefinitely, then you must to keep track of instance 
numbers currently in use. Then each time a new instance is created, the code will look for the 
first open spot in this list or just add one to the largest number.
