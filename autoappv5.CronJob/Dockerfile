FROM mcr.microsoft.com/dotnet/runtime:8.0 AS base
WORKDIR /app
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["autoappv5.CronJob/autoappv5.CronJob.csproj", "autoappv5.CronJob/"]
RUN dotnet restore "autoappv5.CronJob/autoappv5.CronJob.csproj"
COPY . .
WORKDIR "/src/autoappv5.CronJob"
RUN dotnet publish "autoappv5.CronJob.csproj" -c Release -o /app/publish
FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "autoappv5.CronJob.dll"]