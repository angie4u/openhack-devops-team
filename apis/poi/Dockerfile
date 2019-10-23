FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.sln .
COPY web/*.csproj ./web/
COPY tests/IntegrationTests/*.csproj ./tests/IntegrationTests/
COPY tests/UnitTests/*.csproj ./tests/UnitTests/
RUN dotnet restore

# copy everything else and build app
COPY web/. ./web/
COPY tests/. ./tests/
WORKDIR /app
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS runtime
WORKDIR /app
COPY --from=build /app/web/out ./
ENTRYPOINT ["dotnet", "poi.dll"]