#

<https://docs.docker.com/engine/examples/dotnetcore/>

docker build . -t cpp-build-base:0.1.0

PS C:\Users\Vytautas\OneDrive\CV\LAZERIAI\Linux> docker images
REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
cpp-build-base      0.1.0               143873876730        About a minute ago   423MB
ubuntu              bionic              4e5021d210f6        15 hours ago         64.2MB

docker build . -t alpha1:1.0.14
docker run -d alpha1:1.0.14

choco install dotnetcore-sdk -Y

docker build -t alpha2:1.0.0 .
docker run -d -p 5000:80 --name alpha2 alpha2:1.0.12

RUN git clone https://github.com/example/example.git && cd example && git checkout 0123abcdef
