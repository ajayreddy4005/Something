#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Capstone_Project/Capstone_Project.csproj", "Capstone_Project/"]
COPY ["Business_Logic/Business_Logic.csproj", "Business_Logic/"]
COPY ["EntityApi/EntityApi.csproj", "EntityApi/"]
COPY ["Models/Models.csproj", "Models/"]
RUN dotnet restore "Capstone_Project/Capstone_Project.csproj"
COPY . .
WORKDIR "/src/Capstone_Project"
RUN dotnet build "Capstone_Project.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Capstone_Project.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Capstone_Project.dll"]