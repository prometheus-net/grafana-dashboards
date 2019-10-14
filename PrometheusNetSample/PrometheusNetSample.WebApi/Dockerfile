FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["PrometheusNetSample.WebApi/PrometheusNetSample.WebApi.csproj", "PrometheusNetSample.WebApi/"]
RUN dotnet restore "PrometheusNetSample.WebApi/PrometheusNetSample.WebApi.csproj"
COPY . .
WORKDIR "/src/PrometheusNetSample.WebApi"
RUN dotnet build "PrometheusNetSample.WebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PrometheusNetSample.WebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PrometheusNetSample.WebApi.dll"]