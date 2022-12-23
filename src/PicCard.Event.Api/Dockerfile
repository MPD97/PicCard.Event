FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/PicCard.Event.Api/PicCard.Event.Api.csproj", "src/PicCard.Event.Api/"]
RUN dotnet restore "src/PicCard.Event.Api/PicCard.Event.Api.csproj"
COPY . .
WORKDIR "/src/src/PicCard.Event.Api"
RUN dotnet build "PicCard.Event.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PicCard.Event.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PicCard.Event.Api.dll"]