FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["server/Apis/Apis.csproj", "server/Apis/"]
COPY ["server/Application/Application.csproj", "server/Application/"]
COPY ["server/Core/Core.csproj", "server/Core/"]
COPY ["server/Infrastructure/Infrastructure.csproj", "server/Infrastructure/"]
COPY ["server/Hubs/Hubs.csproj", "server/Hubs/"]
RUN dotnet restore "server/Apis/Apis.csproj"
COPY server/ server/
WORKDIR "/src/server/Apis"
RUN dotnet publish "Apis.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=build /app/publish .
ENV ASPNETCORE_URLS=http://+:8080
EXPOSE 8080
ENTRYPOINT ["dotnet", "Apis.dll"]