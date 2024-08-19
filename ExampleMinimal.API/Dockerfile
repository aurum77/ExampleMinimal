# FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
# USER app
# WORKDIR /app
# EXPOSE 8080
# EXPOSE 8081
# 
# FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
# ARG BUILD_CONFIGURATION=Release
# WORKDIR /src
# COPY ["Adisyon.WebAPI/Adisyon.WebAPI.csproj", "Adisyon.WebAPI/"]
# COPY ["Adisyon.Infrastructure/Adisyon.Infrastructure.csproj", "Adisyon.Infrastructure/"]
# COPY ["Adisyon.Application/Adisyon.Application.csproj", "Adisyon.Application/"]
# COPY ["Adisyon.Domain/Adisyon.Domain.csproj", "Adisyon.Domain/"]
# COPY ["Adisyon.Persistence/Adisyon.Persistence.csproj", "Adisyon.Persistence/"]
# RUN dotnet restore "./Adisyon.WebAPI/Adisyon.WebAPI.csproj"
# COPY . .
# WORKDIR "/src/Adisyon.WebAPI"
# RUN dotnet build "./Adisyon.WebAPI.csproj" -c $BUILD_CONFIGURATION -o /app/build
# 
# FROM build AS publish
# ARG BUILD_CONFIGURATION=Release
# RUN dotnet publish "./Adisyon.WebAPI.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false
# 
# FROM base AS final
# WORKDIR /app
# COPY --from=publish /app/publish .
# ENTRYPOINT ["dotnet", "Adisyon.WebAPI.dll"]

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER app
WORKDIR /app
 EXPOSE 8080
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["./ExampleMinimal.API.csproj", "ExampleMinimal.API/"]
RUN dotnet restore "./ExampleMinimal.API/ExampleMinimal.API.csproj"
COPY . ./ExampleMinimal.API
WORKDIR "/src/ExampleMinimal.API"
RUN dotnet build "./ExampleMinimal.API.csproj" -c $BUILD_CONFIGURATION -o /app/build
FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "./ExampleMinimal.API.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ExampleMinimal.API.dll"]
