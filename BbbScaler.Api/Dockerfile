#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["BbbScaler.Api/BbbScaler.Api.csproj", "BbbScaler.Api/"]
RUN dotnet restore "BbbScaler.Api/BbbScaler.Api.csproj"
COPY . .
WORKDIR "/src/BbbScaler.Api"
RUN dotnet build "BbbScaler.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BbbScaler.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BbbScaler.Api.dll"]