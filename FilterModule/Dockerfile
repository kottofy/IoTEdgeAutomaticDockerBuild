FROM microsoft/dotnet:2.0.0-runtime-stretch AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY /FilterModule/*.csproj ./FilterModule/
RUN dotnet restore

# copy and build everything else
COPY FilterModule/. ./FilterModule/
RUN dotnet build
WORKDIR /app/FilterModule
RUN dotnet publish -o out

FROM microsoft/dotnet:2.0-runtime AS runtime
WORKDIR /app
COPY --from=publish /app/FilterModule/out ./
ENTRYPOINT ["dotnet", "FilterModule.dll"]