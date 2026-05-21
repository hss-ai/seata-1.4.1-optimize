# https://hub.docker.com/orgs/seataio
FROM eclipse-temurin:8u492-b09-jdk-jammy

# set label
LABEL maintainer="Seata <seata.io>"

WORKDIR /$BASE_DIR

ENV TZ=Asia/Shanghai

# ADD arthas
COPY --from=hengyunabc/arthas:latest /opt/arthas /opt/arthas

# ADD FORM distribution
ADD bin/ /seata-server/bin
ADD lib/ /seata-server/lib
ADD conf/ /seata-server/conf
ADD LICENSE-BIN /seata-server/LICENSE

RUN mkdir -p /seata-server/logs

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        tzdata \
        libxcb1 \
        libxau6 \
        libasound2 \
        curl \
        wget \
        iputils-ping \
        telnet \
        dnsutils \
        iproute2 \
        net-tools \
        netcat \
        procps \
        lsof \
        htop \
        strace \
        vim \
        unzip \
        zip \
        jq \
        less \
        ca-certificates \
        fontconfig \
        fonts-wqy-zenhei \
        fonts-wqy-microhei \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone \
    && fc-cache -fv \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# set extra environment
ENV EXTRA_JVM_ARGUMENTS="-Djava.security.egd=file:/dev/./urandom -server -Xms512m -Xmx2048m -Xss512k -XX:+UnlockExperimentalVMOptions -XX:+UseContainerSupport -XX:SurvivorRatio=10 -XX:MetaspaceSize=256m -XX:MaxMetaspaceSize=512m -XX:MaxDirectMemorySize=1024m -XX:-OmitStackTraceInFastThrow -XX:-UseAdaptiveSizePolicy -XX:+HeapDumpOnOutOfMemoryError -XX:+DisableExplicitGC -XX:+CMSParallelRemarkEnabled -XX:+UseCMSInitiatingOccupancyOnly -XX:CMSInitiatingOccupancyFraction=75 -Xloggc:/var/log/seata_gc.log -verbose:gc -Dio.netty.leakDetectionLevel=advanced"

CMD ["sh","/seata-server/bin/seata-server.sh"]
