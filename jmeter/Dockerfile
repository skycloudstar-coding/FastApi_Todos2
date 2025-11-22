# JMeter용 Dockerfile (멀티 아키텍처: amd64/arm64 모두 지원)
# 기존: FROM openjdk:11-jre-slim  ← 이게 지금 Docker Hub에 없음
FROM eclipse-temurin:11-jre-jammy

# Set JMeter version and environment variables
ENV JMETER_VERSION=5.4.1
ENV JMETER_HOME=/opt/apache-jmeter-${JMETER_VERSION}
ENV PATH=${JMETER_HOME}/bin:$PATH

# Install required packages (wget, unzip, ca-certificates)
RUN apt-get update && \
    apt-get install -y --no-install-recommends wget unzip ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# Download and extract Apache JMeter
RUN wget https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-${JMETER_VERSION}.tgz && \
    tar -xzf apache-jmeter-${JMETER_VERSION}.tgz -C /opt/ && \
    rm apache-jmeter-${JMETER_VERSION}.tgz

# Create default work dir for mounted test plans / reports
RUN mkdir -p /jmeter

# Set the working directory (JMeter home; tests는 /jmeter로 볼륨 마운트)
WORKDIR ${JMETER_HOME}

# Default command: JMeter in non-GUI mode
CMD ["jmeter", "-n"]