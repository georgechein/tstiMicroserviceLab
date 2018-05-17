FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY CoreWeb/CoreWeb.csproj CoreWeb/
RUN dotnet restore CoreWeb/CoreWeb.csproj
COPY . .
WORKDIR /src/CoreWeb
RUN dotnet build CoreWeb.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish CoreWeb.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CoreWeb.dll"]
