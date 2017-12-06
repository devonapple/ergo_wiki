# Install the JRE 1.8

Windows users can install the Oracle JRE 8 from [the official site](http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html).

You must add a line `;JAVA_HOME/bin` to your existing PATH environment variable to access the JRE from the command line. 
You can find detailed instructions on this step [here](https://docs.oracle.com/javase/tutorial/essential/environment/paths.html).

Now you can check your JRE installation. Run start Windows Command line app `cmd.exe` and execute command `java -version`. If you see

```
java version "1.8.0_74"
Java(TM) SE Runtime Environment (build 1.8.0_74-b02)
Java HotSpot(TM) 64-Bit Server VM (build 25.74-b02, mixed mode)
```

then all is ok, and you can move on to the next step!

If you get an error check your installation and try find a solution or a better tutorial online.

# Download Ergo package and configure the application

Download the latest version of ergo.jar and create the configuration file to any folder, for example `C:/ergo`.

Just open it with your favorite text editor, pour a cup of tea and read [the documentation of the configuration file](https://github.com/ergoplatform/ergo/wiki/Node-Configuration-File).

Then start Windows Command line app `cmd.exe`, navigate to the folder with the jar file with the command `cd C:/ergo` and start ergo node with command `java -jar ergo.jar ergo.conf`.