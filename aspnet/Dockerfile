FROM mcr.microsoft.com/dotnet/sdk:6.0 as deps
WORKDIR /app
COPY aspnet.csproj .
RUN dotnet restore

FROM mcr.microsoft.com/dotnet/sdk:6.0 as builder
WORKDIR /app

COPY --from=deps /app/obj ./obj
COPY . .

RUN dotnet publish -c release -o /app/out

FROM mcr.microsoft.com/dotnet/aspnet:6.0 as runner
ENV ASPNETCORE_ENVIRONMENT=Production
WORKDIR /app
COPY --from=builder /app/out ./

CMD ["dotnet", "aspnet.dll"]