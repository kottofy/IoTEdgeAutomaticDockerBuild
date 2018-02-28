FROM microsoft/dotnet:2.0-sdk AS build-env
RUN ls
RUN pwd
WORKDIR /app
RUN ls
RUN pwd

# copy csproj and restore as distinct layers
COPY *.csproj ./
RUN ls
RUN pwd
RUN dotnet restore
RUN ls
RUN pwd

# copy everything else and build
COPY . ./
RUN ls
RUN pwd
RUN dotnet publish -c Release -o out
RUN ls
RUN pwd

# build runtime image
FROM microsoft/dotnet:2.0-runtime 
RUN ls
RUN pwd
WORKDIR /app
RUN ls
RUN pwd
COPY --from=build-env /app/out ./
RUN ls
RUN pwd
ENTRYPOINT ["dotnet", "dotnetapp.dll"]