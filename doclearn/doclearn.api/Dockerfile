#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["doclearn.api/doclearn.api.csproj", "doclearn.api/"]
RUN dotnet restore "doclearn.api/doclearn.api.csproj"
COPY . .
WORKDIR "/src/doclearn.api"
RUN dotnet build "doclearn.api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "doclearn.api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "doclearn.api.dll"]