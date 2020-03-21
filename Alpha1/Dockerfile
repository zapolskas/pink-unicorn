FROM cpp-build-base:0.1.0 AS build
WORKDIR /src
COPY CMakeLists.txt main.cpp ./
RUN cmake . && make
FROM ubuntu:bionic
WORKDIR /opt/alpha1
COPY --from=build /src/alpha1 ./
CMD [ "./alpha1" ]