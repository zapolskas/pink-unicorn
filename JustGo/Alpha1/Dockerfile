FROM ubuntu:bionic AS build
RUN apt-get update && \
	apt-get install -y build-essential git cmake autoconf libtool pkg-config
WORKDIR /src
COPY CMakeLists.txt main.cpp ./
RUN cmake . && make
FROM ubuntu:bionic
WORKDIR /opt/alpha1
COPY --from=build /src/alpha1 ./
CMD [ "./alpha1" ]