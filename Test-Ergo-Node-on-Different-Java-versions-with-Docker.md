1. Compile your Ergo node (install JRE and SBT first if you have not):

        git clone https://github.com/ergoplatform/ergo
        cd ergo
        sbt sbt reload clean assembly

2. Then, copy your Ergo jar and application.conf to some location, for example `/tmp/ergo`:

        cp `find . -name ergo-assembly*.jar` /tmp/ergo/ergo.jar
        cp ./src/main/resources/application.conf /tmp/ergo/application.conf

3. Adjust your node settings: `nano /tmp/ergo/application.conf`

4. Test your node`s .jar file in different environments:

        sudo docker run --rm -p 9002:9002 -p 9052:9052 \
          -v /tmp/ergo/ergo.jar:/ergo.jar:ro \
          -v /tmp/ergo/application.conf:/application.conf \
          openjdk:8-jre-alpine /usr/bin/java -jar /ergo.jar /application.conf

    Command above will run your locally compiled Ergo node in docker container. All logs and errors would be printed directly to stdout, you can press Ctrl+C to stop it. When you stop the node, all the blockchain data would be cleaned up automatically (`--rm` flag).

    Then, replace tag `8-jre-alpine` with [tags](https://hub.docker.com/_/openjdk/) you like. For example, try:

    - 8-jre-alpine
    - 8-jre-slim
    - 9-jre-slim
    - 10-jre-slim
    - 11-jre-slim
