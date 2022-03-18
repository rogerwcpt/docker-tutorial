FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WeissDigital.DockerTutorial.WebApp/WeissDigital.DockerTutorial.WebApp.csproj", "WeissDigital.DockerTutorial.WebApp/"]
RUN dotnet restore "WeissDigital.DockerTutorial.WebApp/WeissDigital.DockerTutorial.WebApp.csproj"
COPY . .
WORKDIR "/src/WeissDigital.DockerTutorial.WebApp"
RUN dotnet build "WeissDigital.DockerTutorial.WebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WeissDigital.DockerTutorial.WebApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WeissDigital.DockerTutorial.WebApp.dll"]
