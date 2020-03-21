FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
WORKDIR /app

# Pull code from GIT

RUN git init && git remote add origin https://github.com/zapolskas/pink-unicorn.git && git fetch origin && git checkout origin/master -- JustGo/Gamma1/src

# Build an APP and publish it

RUN cd /app/JustGo/Gamma1/src && dotnet restore
RUN cd /app/JustGo/Gamma1/src && dotnet publish -c Release -o /app/JustGo/Gamma1/out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
COPY --from=build-env /app/JustGo/Gamma1/out .
ENTRYPOINT ["dotnet", "Gamma1.dll"]