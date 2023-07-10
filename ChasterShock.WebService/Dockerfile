FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["ChasterShock.WebService/ChasterShock.WebService.csproj", "ChasterShock.WebService/"]
RUN dotnet restore "ChasterShock.WebService/ChasterShock.WebService.csproj"
COPY . .
WORKDIR "/src/ChasterShock.WebService"
RUN dotnet build "ChasterShock.WebService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ChasterShock.WebService.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ChasterShock.WebService.dll"]
