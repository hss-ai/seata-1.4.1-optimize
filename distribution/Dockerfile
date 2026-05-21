# https://hub.docker.com/orgs/seataio
FROM openjdk:8u232-jdk-stretch

# set label
LABEL maintainer="Seata <seata.io>"

WORKDIR /$BASE_DIR

# ADD arthas
COPY --from=hengyunabc/arthas:latest /opt/arthas /opt/arthas

# ADD FORM distribution
ADD bin/ /seata-server/bin
ADD lib/ /seata-server/lib
ADD conf/ /seata-server/conf
ADD LICENSE-BIN /seata-server/LICENSE

# set extra environment
ENV EXTRA_JVM_ARGUMENTS="-Djava.security.egd=file:/dev/./urandom -server -Xms512m -Xmx2048m -Xss512k -XX:+UnlockExperimentalVMOptions -XX:+UseContainerSupport XX:SurvivorRatio=10 -XX:MetaspaceSize=256m -XX:MaxMetaspaceSize=512m -XX:MaxDirectMemorySize=1024m -XX:-OmitStackTraceInFastThrow -XX:-UseAdaptiveSizePolicy -XX:+HeapDumpOnOutOfMemoryError -XX:+DisableExplicitGC -XX:+CMSParallelRemarkEnabled -XX:+UseCMSInitiatingOccupancyOnly -XX:CMSInitiatingOccupancyFraction=75 -Xloggc:/var/log/seata_gc.log -verbose:gc -Dio.netty.leakDetectionLevel=advanced"

CMD ["sh","/seata-server/bin/seata-server.sh"]
