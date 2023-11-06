FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["WilpSocialMedia.ApiGateway/WilpSocialMedia.ApiGateway.csproj", "WilpSocialMedia.ApiGateway/"]
COPY ["WilpSocialMedia.Common/WilpSocialMedia.Common.csproj", "WilpSocialMedia.Common/"]
RUN dotnet restore "WilpSocialMedia.ApiGateway/WilpSocialMedia.ApiGateway.csproj"
COPY . .
WORKDIR "/src/WilpSocialMedia.ApiGateway"
RUN dotnet build "WilpSocialMedia.ApiGateway.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WilpSocialMedia.ApiGateway.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WilpSocialMedia.ApiGateway.dll"]
