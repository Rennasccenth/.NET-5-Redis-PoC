FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Redis-PoC/Redis-PoC.csproj", "Redis-PoC/"]
RUN dotnet restore "Redis-PoC/Redis-PoC.csproj"
COPY . .
WORKDIR "/src/Redis-PoC"
RUN dotnet build "Redis-PoC.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Redis-PoC.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Redis-PoC.dll"]
