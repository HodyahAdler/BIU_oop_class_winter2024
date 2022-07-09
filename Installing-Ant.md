# Installing Apache Ant

Apache Ant is a software, thus it requires installation wherever you want to use it.
We will install the 1.10.12 version.

### Pre-requisite

It is assumed that you have already downloaded and installed Java Development Kit (JDK) 
on your computer. 

### Download  

For Mac users who use brew to install packages (highly recommended in general), you can simply install ant using `brew install ant` and move to Verify Installation. 

For Windows and Linux, proceed as follows:

* Download [Apache-Ant-1.10.12 binaries](http://apache.spd.co.il/ant/binaries/apache-ant-1.10.12-bin.zip). 
 It is a zip file.

* Unzip the zip file to a convenient location (e.g. `C:\Users\User`). 
To unzip on Windows, you can use [7-zip](https://www.7-zip.org/) or similar programs. 

### Set environment variables (Windows and Linux)

* Create a new environment variable called ANT_HOME that points to the 
Ant installation folder, in our example, the `C:\User\User\apache-ant-1.10.12-bin` folder.

* Append the path to the Apache Ant batch file to the PATH environment variable. 
In our example this would be the `C:\User\User\apache-ant-1.10.12-bin\bin` folder.
You can now run `ant` commands from anywhere on your system.

If you are not sure how to create or modify an environment variable, 
here are simple guides for [Windows](https://www.architectryan.com/2018/08/31/how-to-change-environment-variables-on-windows-10/),
 [Linux](https://www.serverlab.ca/tutorials/linux/administration-linux/how-to-set-environment-variables-in-linux/),
 and [Mac](https://medium.com/@youngstone89/setting-up-environment-variables-in-mac-os-28e5941c771c)
 (note you should make it a persistent setting).  
 
 ### Verify Installation
 
 To verify the successful installation of Apache Ant on your computer, type `ant -version` on your command prompt.
 
 You should see an output similar to −
 ```$xslt
Apache Ant(TM) version 1.10.12 compiled on October 13 2021
```

## Integration with IDEs

Common Java IDEs, such as IntelliJ and Eclipse, support the usage of Ant.
You can copy the `build.xml` (that we will provide you) into your project directory 
and then edit your build configuration so that it uses Ant targets specified there.

For integration with IntelliJ, see Ayal Klein's [video](https://www.youtube.com/watch?v=WNHGXAygwZw&feature=youtu.be) 
in hebrew.