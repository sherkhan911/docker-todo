FROM mcr.microsoft.com/dotnet/aspnet:5.0-focal AS base
WORKDIR /app
EXPOSE 8080

ENV ASPNETCORE_URLS=http://+:8080

FROM mcr.microsoft.com/dotnet/sdk:5.0-focal AS build
WORKDIR /src
COPY ["todoApp.csproj", "./"]
RUN dotnet restore "todoApp.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "todoApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "todoApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "todoApp.dll"]
