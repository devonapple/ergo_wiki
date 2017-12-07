# Install the JRE 1.8

Ubuntu users can use the following commands to install JRE.

```
sudo add-apt-repository -y ppa:webupd8team/java
sudo apt-get update
sudo apt-get -y install oracle-java8-installer
```

Proceed to check JRE version. Start Console and execute command `java -version`. If you see

```
java version "1.8.0_74"
Java(TM) SE Runtime Environment (build 1.8.0_74-b02)
Java HotSpot(TM) 64-Bit Server VM (build 25.74-b02, mixed mode)
```

then installation was successful. Please proceed to the next step!

If you get an error check your installation or search online for a solution to the particular error prompted.

# Installation of jar package

Download latest version of [ergo.jar](https://github.com/ergoplatform/ergo/releases) to any folder, for example `/opt/ergo`.

Now your configuration file can be created, for example `/opt/ergo/ergo.conf` .

Just open it via your favorite text editor, pour a cup of tea and read [the documentation of the configuration file](https://github.com/ergoplatform/ergo/wiki/Node-Configuration-File).

Start Console and execute cmd.exe command, navigate to the folder with the jar file by executing the command `cd /opt/ergo` . Your Ergo node can now be booted up by executing the command `java -jar ergo.jar ergo.conf` .

Lastly proceed to write a script (with bash, zsh or smtn; whichever is your favorite) to customize your node's operation! :)