FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DockerDebugging101/DockerDebugging101.csproj", "DockerDebugging101/"]
RUN dotnet restore "DockerDebugging101/DockerDebugging101.csproj"
COPY . .
WORKDIR "/src/DockerDebugging101"
RUN dotnet build "DockerDebugging101.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DockerDebugging101.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerDebugging101.dll"]
