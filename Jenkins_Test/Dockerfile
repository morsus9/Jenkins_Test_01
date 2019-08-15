FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Jenkins_Test/Jenkins_Test.csproj", "Jenkins_Test/"]
RUN dotnet restore "Jenkins_Test/Jenkins_Test.csproj"
COPY . .
WORKDIR "/src/Jenkins_Test"
RUN dotnet build "Jenkins_Test.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Jenkins_Test.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Jenkins_Test.dll"]
