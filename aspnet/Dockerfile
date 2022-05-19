FROM mcr.microsoft.com/dotnet/sdk:6.0 as build-env

WORKDIR /app

COPY aspnet.csproj ./

RUN dotnet restore

COPY . .

RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/aspnet:6.0 as runtime

WORKDIR /app

COPY --from=build-env /app/out ./

CMD dotnet aspnet.dll