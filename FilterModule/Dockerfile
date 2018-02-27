FROM microsoft/dotnet:2.0-sdk AS build
RUN ls

WORKDIR /app
RUN ls

# copy csproj and restore as distinct layers
COPY /FilterModule/FilterModule.csproj ./FilterModule/
RUN ls
RUN dotnet restore

# copy and build everything else
COPY /FilterModule/. ./FilterModule/
RUN ls
RUN dotnet build

WORKDIR /app/FilterModule
RUN ls
RUN dotnet publish -o out

FROM microsoft/dotnet:2.0-runtime AS runtime
WORKDIR /app
COPY --from=publish /app/FilterModule/out ./
ENTRYPOINT ["dotnet", "FilterModule.dll"]