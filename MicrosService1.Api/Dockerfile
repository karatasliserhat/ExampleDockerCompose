#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["MicrosService1.Api/MicrosService1.Api.csproj", "MicrosService1.Api/"]
RUN dotnet restore "MicrosService1.Api/MicrosService1.Api.csproj"
COPY . .
WORKDIR "/src/MicrosService1.Api"
RUN dotnet build "MicrosService1.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MicrosService1.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MicrosService1.Api.dll"]