# Install the JRE 1.8

Windows users can install the Oracle JRE 8 from [the official site](http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html).

You must add a line `;JAVA_HOME/bin` to your existing `Environment Variables / System Variable Path` to access JRE from the Command Prompt. For detailed instructions to complete this step please follow the link here.

Proceed to check JRE version. Open Run Prompt and execute `cmd.exe` command. Now execute `java -version`. If you see

```
java version "1.8.0_74"
Java(TM) SE Runtime Environment (build 1.8.0_74-b02)
Java HotSpot(TM) 64-Bit Server VM (build 25.74-b02, mixed mode)
```

then all is ok, and you can move on to the next step!

then installation was successful. Please proceed to the next step!

If you get an error check your installation or search online for a solution to the particular error prompted.

# Download Ergo package and configure the application

Download the latest version of (ergo.jar)[https://github.com/ergoplatform/ergo/releases] and create ergo.conf file to any folder, for example `C:/ergo` .

Lastly, Open Run Prompt and execute cmd.exe command, navigate to the folder with the jar file by executing the command `cd C:/ergo` . Your Ergo node can now be booted up by executing the command `java -jar ergo.jar ergo.conf` .

Download the latest version of ergo.jar and create the configuration file to any folder, for example `C:/ergo`.

Just open it with your favorite text editor, pour a cup of tea and read [the documentation of the configuration file](https://github.com/ergoplatform/ergo/wiki/Node-Configuration-File).

Lastly, Open Run Prompt and execute `cmd.exe` command, navigate to the folder with the jar file by executing the command `cd C:/ergo` . Your Ergo node can now be booted up by executing the command `java -jar ergo.jar ergo.conf` .