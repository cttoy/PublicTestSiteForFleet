FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["PublicTestSiteForFleet/PublicTestSiteForFleet.csproj", "PublicTestSiteForFleet/"]

RUN dotnet restore "PublicTestSiteForFleet/PublicTestSiteForFleet.csproj"
COPY . .
WORKDIR "/src/PublicTestSiteForFleet"
RUN dotnet build "PublicTestSiteForFleet.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PublicTestSiteForFleet.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PublicTestSiteForFleet.dll"]