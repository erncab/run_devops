#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

###############################################################
### Build. "CTRL + /" to comment/uncomment block.
###############################################################
#FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
#WORKDIR /app
#EXPOSE 80
#
#FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
#WORKDIR /src
#COPY ["Shopping.Client.csproj", "Shopping.Client/"]
#RUN dotnet restore "Shopping.Client/Shopping.Client.csproj"
#COPY . .
#WORKDIR "/src/Shopping.Client"
#RUN dotnet build "Shopping.Client.csproj" -c Release -o /app/build
#
#FROM build AS publish
#RUN dotnet publish "Shopping.Client.csproj" -c Release -o /app/publish
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "Shopping.Client.dll"]

###############################################################
### Pushing to GitHub repo to trigger build in Docker Hub repo.
### "CTRL + /" to comment/uncomment block.
###############################################################
FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["./Shopping/Shopping.Client/Shopping.Client.csproj", "Shopping.Client/"]
RUN dotnet restore "Shopping.Client/Shopping.Client.csproj"

COPY ["./Shopping/Shopping.Client/", "./Shopping.Client/"]
WORKDIR "/src/Shopping.Client"
RUN dotnet build "Shopping.Client.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Shopping.Client.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Shopping.Client.dll"]