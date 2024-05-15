FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["ABV-Converter/ABV-Converter.csproj", "ABV-Converter/"]
RUN dotnet restore "ABV-Converter/ABV-Converter.csproj"
COPY . .
WORKDIR "/src/ABV-Converter"
RUN dotnet build "ABV-Converter.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ABV-Converter.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ABV-Converter.dll"]
