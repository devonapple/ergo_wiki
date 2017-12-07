# Install the JRE 1.8

Mac OS X users can install the latest Oracle JRE from [Homebrew](http://brew.sh/) through [Cask](https://caskroom.github.io/).

Now simply run `brew cask install Caskroom/cask/java` to install latest Java version.

Proceed to check JRE version. Run Terminal.app and execute command `java -version`. If you see

```
java version "1.8.0_74"
Java(TM) SE Runtime Environment (build 1.8.0_74-b02)
Java HotSpot(TM) 64-Bit Server VM (build 25.74-b02, mixed mode)
```

then installation was successful. Please proceed to the next step!

If you get an error check your installation or search online for a solution to the particular error prompted.

# Download Ergo package and configure the application

Download the latest version of [ergo.jar](https://github.com/ergoplatform/ergo/releases) and create ergo.conf file to any folder, for example `~/ergo` .

Lastly, open Terminal.app, navigate to the folder with the jar file by executing the command `cd ~/ergo` . Your Ergo node can now be booted up by executing the command `java -jar ergo.jar ergo.conf`.

Just open it with your favorite text editor, pour a cup of tea and read [the documentation of the configuration file](https://github.com/ergoplatform/ergo/wiki/Node-Configuration-File).

Then start Terminal app `Terminal.app`, navigate to the folder with the jar file with the command `cd ~/ergo` and start ergo node with command `java -jar ergo.jar ergo.conf`.