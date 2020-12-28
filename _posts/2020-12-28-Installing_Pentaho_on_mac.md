## How to install Pentaho on macOs Catalina:



1. Check if JDK is installed on your machine? 
   
   You can check using this command on your terminal. 
   
   * java -version
   
   The output should look something like this: 
   
   **java version "1.8.0_92"
   Java(TM) SE Runtime Environment (build 1.8.0_92-b14)
   Java HotSpot(TM) 64-Bit Server VM (build 25.92-b14, mixed mode)**

   If not- download jdk version 8 available on oracle site: https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html

2. Download the latest jar file from : https://mvnrepository.com/artifact/org.eclipse.platform/org.eclipse.swt.cocoa.macosx.x86_64

   Replace the original 'swt.jar' file with the jar file you just downloaded. The swt.jar file is located in **libswt/osx64** folder.

3. Download Community edition of Pentaho : https://sourceforge.net/projects/pentaho/files/latest/download

   Extract the file after which you will have data-intergration folder.
   Move this folder to /Applications and paste it.
 
4. Finally, navigate to data-integration folder and execute spoon.sh
  
   * cd /Applications/data-integration
  
   * ./spoon.sh
 
