FROM python:3.9-slim-bullseye
LABEL maintainer="OneQA"
LABEL repository="oneqa"

# Pyserini needs Java
ENV JAVA_HOME=/usr/local/openjdk-11
ENV PATH=${PATH}:${JAVA_HOME}/bin
COPY --from=openjdk:11.0-jdk-slim-bullseye ${JAVA_HOME} ${JAVA_HOME}
RUN update-alternatives --install /usr/bin/java java ${JAVA_HOME}/bin/java 1
RUN update-alternatives --install /usr/bin/javac javac ${JAVA_HOME}/bin/javac 1

RUN apt update && \
    apt install -y bash \
                   build-essential \
                   git \
                   curl \
                   ca-certificates \
                   python3 \
                   python3-pip && \
    rm -rf /var/lib/apt/lists

RUN python3 -m pip install --no-cache-dir --upgrade pip

WORKDIR /workspace
COPY dev oneqa/
RUN cd oneqa/ && \
    python3 -m pip install --no-cache-dir .[all]

CMD ["/bin/bash"]