# STEP 1: Build the application
FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/sdk:10.0 AS build
ARG TARGETARCH

WORKDIR /source

COPY WebsiteInterface.csproj .
RUN dotnet restore -a $TARGETARCH

COPY . .
RUN dotnet publish WebsiteInterface.csproj -a $TARGETARCH -c Release -o /app

# STEP 2: Build the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:10.0
WORKDIR /app
COPY --from=build /app .

ENV ASPNETCORE_URLS=http://+:8080
ENV ASPNETCORE_ENVIRONMENT=Production
EXPOSE 8080
USER $APP_UID
ENTRYPOINT ["dotnet", "WebsiteInterface.dll"]