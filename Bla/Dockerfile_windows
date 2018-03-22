FROM microsoft/dotnet:2.0-runtime-nanoserver-sac2016 AS base
WORKDIR /app

FROM microsoft/dotnet:2.0-sdk-nanoserver-sac2016 AS build
WORKDIR /src
COPY Bla.sln ./
COPY Bla/Bla.csproj Bla/
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/Bla
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Bla.dll"]
