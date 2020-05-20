FROM ubuntu:18.04

RUN apt update && apt install -y build-essential libssh-dev openssl wget apt-utils kmod gcc libcap2-bin

RUN wget https://nmap.org/dist/nmap-7.70.tar.bz2 && tar -xjvf nmap-7.70.tar.bz2

WORKDIR /nmap-7.70

RUN ./configure && make && make install

FROM ubuntu:18.04

RUN apt update && apt install -y git libcap2-bin libssh-dev openssl build-essential wget apt-utils kmod gcc libcap2-bin python3 zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libelf-dev elfutils && rm -rf /var/cache/apt/* && rm -rf /var/lib/apt/lists/* && update-alternatives --install /usr/bin/python python /usr/bin/python3.6 1

RUN mkdir /usr/local/share/nmap/
COPY --from=0 /usr/local/share/nmap/ /usr/local/share/nmap/
COPY --from=0 /usr/local/bin/* /usr/local/bin/

ENTRYPOINT ["/usr/local/bin/ncat"]
