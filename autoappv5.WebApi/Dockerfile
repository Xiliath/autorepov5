FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["autoappv5.WebApi/autoappv5.WebApi.csproj", "autoappv5.WebApi/"]
RUN dotnet restore "autoappv5.WebApi/autoappv5.WebApi.csproj"
COPY . .
WORKDIR "/src/autoappv5.WebApi"
RUN dotnet build "autoappv5.WebApi.csproj" -c Release -o /app/build
FROM build AS publish
RUN dotnet publish "autoappv5.WebApi.csproj" -c Release -o /app/publish
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "autoappv5.WebApi.dll"]