# Install the JRE 1.8

Mac OS X users can install the Oracle JRE 8 from the [Homebrew](http://brew.sh/) throw [Cask](https://caskroom.github.io/). It is enough to run `brew cask install Caskroom/cask/java`.

Now you can check your JRE installation. Run terminal and execute command `java -version`. If you see

```
java version "1.8.0_74"
Java(TM) SE Runtime Environment (build 1.8.0_74-b02)
Java HotSpot(TM) 64-Bit Server VM (build 25.74-b02, mixed mode)
```

then all is ok, and you can move on to the next step!

If you get an error check your installation and try find a solution or a better tutorial online.

# Download Ergo package and configure the application

Download the latest version of ergo.jar and create the ergo.conf configuration to any folder, for example `~/ergo`.

Just open it with your favorite text editor, pour a cup of tea and read [the documentation of the configuration file](https://github.com/ergoplatform/ergo/wiki/Node-Configuration-File).

Then start Terminal app `Terminal.app`, navigate to the folder with the jar file with the command `cd ~/waves` and start waves node with command `java -jar waves.jar waves.conf`.