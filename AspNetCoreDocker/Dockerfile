
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["AspNetCoreDocker.csproj", "./"]
RUN dotnet restore "AspNetCoreDocker.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "AspNetCoreDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AspNetCoreDocker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AspNetCoreDocker.dll"]