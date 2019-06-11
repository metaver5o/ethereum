FROM ubuntu
LABEL maintainer="M Matos <marco@mmatos.com>"

    ENV DEBIAN_FRONTEND=noninteractive
    RUN apt-get update && \ 
        apt-get install --yes software-properties-common

    RUN add-apt-repository ppa:ethereum/ethereum
    RUN apt-get update && apt-get install --yes geth

    RUN adduser --disabled-login --gecos "" eth_user

    USER eth_user
    WORKDIR /home/eth_user

    ENTRYPOINT bash