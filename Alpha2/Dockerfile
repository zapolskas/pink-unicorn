FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
WORKDIR /app

# Pull code from GIT

RUN git init && git remote add origin https://github.com/zapolskas/pink-unicorn.git && git fetch origin && git checkout origin/master -- Alpha2/src

# Build an APP and publish it

RUN cd /app/Alpha2/src && dotnet restore
RUN cd /app/Alpha2/src && dotnet publish -c Release -o /app/Alpha2/out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
COPY --from=build-env /app/Alpha2/out .
ENTRYPOINT ["dotnet", "Alpha2.dll"]