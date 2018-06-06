FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY Shoppee/Shoppee.csproj Shoppee/
RUN dotnet restore Shoppee/Shoppee.csproj
COPY . .
WORKDIR /src/Shoppee
RUN dotnet build Shoppee.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Shoppee.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Shoppee.dll"]
