
FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY NewSaturn/NewSaturn.fsproj NewSaturn/
RUN dotnet restore NewSaturn/NewSaturn.fsproj
COPY . .
WORKDIR /src/NewSaturn

RUN dotnet build "NewSaturn.fsproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "NewSaturn.fsproj" -c Release -o /app

FROM microsoft/dotnet:2.1-aspnetcore-runtime
WORKDIR /app

COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NewSaturn.dll"]
ENV ASPNETCORE_URLS="http://0.0.0.0:5000"