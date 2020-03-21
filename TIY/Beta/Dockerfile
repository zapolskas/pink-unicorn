FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
WORKDIR /app

# Pull code from GIT

RUN git init && git remote add origin https://github.com/zapolskas/pink-unicorn.git && git fetch origin && git checkout origin/master -- Beta/src

# Build an APP and publish it

RUN cd /app/Beta/src && dotnet restore
RUN cd /app/Beta/src && dotnet publish -c Release -o /app/Beta/out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
COPY --from=build-env /app/Beta/out .
ENTRYPOINT ["dotnet", "Beta.dll"]