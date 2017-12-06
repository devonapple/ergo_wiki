# Install the JRE 1.8

Ubuntu users can use the following commands to install JRE.

```
sudo add-apt-repository -y ppa:webupd8team/java
sudo apt-get update
sudo apt-get -y install oracle-java8-installer
```

Now you can check your JRE installation. Run start console and execute command `java -version`. If you see

```
java version "1.8.0_74"
Java(TM) SE Runtime Environment (build 1.8.0_74-b02)
Java HotSpot(TM) 64-Bit Server VM (build 25.74-b02, mixed mode)
```

then it good, you can move to the next step!

But if you get a error, then check your installation and try find some better tutorials in google.

# Installation of jar package

Download latest version of ergo.jar to any folder, for example `/opt/ergo`.

Then create the configuration file, for example `/opt/ergo/ergo.conf`.

Just open it via your favorite text editor, pour a cup of tea and read [the documentation of the configuration file](https://github.com/ergoplatform/ergo/wiki/Node-Configuration-File).

Then start console, navigate to the folder with the jar file with the command `cd /opt/ergo` and start ergo node with command `java -jar ergo.jar ergo.conf`.

Now you can write a script (bash, zsh or smtn) to run the node, which you like and use it! :)