Zend Studio 5.5 on Windows 7  
==========

> If you are reading this, then you have Windows 7 installed and gave Zend Studio 7.x the old college try, and found it to be quite cumbersome and annoying. After trying to adapt to Zend with Eclipse you opted to go back to Zend Studio 5.5 but found that it doesn’t work ‘out of the box’ on Windows - If you googled ‘Zend 5.5 Windows 7′ you probably found a response on Zend’s Forums where a savior post is located. At first read it is a bit confusing so I am going to attempt to make it a bit more clear here. Make no mistake, save for a few minor changes, the original author djvirgen (appended to by phliplip), are the true geniuses behind the work. You can find the original post @ <http://www.zend.com/forums/index.php?t=msg&th=7855#21175>

- Download and install the latest JRE for Windows 7: http://java.com/en/download/manual.jsp
- Download and install WinRAR (ensure you install with Explorer shell extension checked): http://rarlabs.com
- Download Zend Studio 5.5.1 (you will need Zend account): http://www.zend.com/products/studio/downloads-prev
- Extract Zend Studio 5.5.1
- Click into ZendStudio-5_5_1 directory after extraction
- Right mouse click on ZendStudio-5_5_1 executable, you will then see an option to ‘extract to (thanks to winrar shell extension), click it.
- After Zend Studio 5.5.1 has been extracted click into ZendStudio-5_5_1/Windows/resource
- You should see a dir named ‘jre’, rename this to ‘jre_came_with_zend’
- Copy ‘jre6′ from your Java install directory (typically C:\Program Files (x86)\Java) into the Zend Studio extracted directory (ZendStudio-5_5_1\Windows\resource)
- Rename ‘jre6′ to ‘jre’
- Click up one dir so you are in ZendStudio-5_5_1/ and click on ZendStudio-5_5_1.exe
- You will instantly know if you did not do the above steps correctly was windows 7 will inform you that you are attempting to run an app incompatible with Aero (this is because the jre packaged with zend is old, if so re-read above steps and try again)
- If everything went fine, you should now be faced with a message “Java Runtime Environment Not Found.” Don’t worry about it, install zend as you normally would.
- Zend Studio install should be finished, do not launch zend yet, we aren’t quite done.
- Copy the ‘jre_came_with_zend’ directory from the original extraction folder and paste it into your Zend install directory (the one you selected during install, default is: c:\Program Files (x86)\Zend\ZendStudio-5.5.1
- Rename the current ‘jre’ directory found in the Zend install directory to ‘jre_installed_with_zend’
- Rename the ‘jre_came_with_zend’ to ‘jre’
- Click into bin directory
- Right mouse click ZDE.exe
- Click properties
- Click the compatibility tab
- Click checkmark for ‘Compatibility Mode’ and select ‘Windows Vista’ from the dropdown menu
- Click apply
- Click ok
- Now, with any luck you can double click on the ZDE.exe file and Zend should start normally.

> Took a few hours to get all this down, hope this helps anyone else out there wanting to use Zend Studio 5.5.x vs the new Zend /w Eclipse crap. Good luck!