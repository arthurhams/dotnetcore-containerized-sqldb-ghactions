FROM mcr.microsoft.com/dotnet/aspnet:6.0 as base
WORKDIR /app
EXPOSE 5000
ENV ASPNETCORE_URLS="http://*:5000"

FROM mcr.microsoft.com/dotnet/sdk:6.0 as build
WORKDIR /src
COPY ["DotNetCoreSqlDb.csproj", "./"]
RUN dotnet restore "./DotNetCoreSqlDb.csproj"
COPY . .
WORKDIR /src/.
RUN dotnet build "DotNetCoreSqlDb.csproj" -c Release -o /app/build

FROM build as publish
RUN dotnet publish "DotNetCoreSqlDb.csproj" -c Release -o /app/publish

FROM base as final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DotNetCoreSqlDb.dll"]
