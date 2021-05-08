FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["HelloBlazor/HelloBlazor.csproj", "HelloBlazor/"]
RUN dotnet restore "HelloBlazor/HelloBlazor.csproj"
COPY . .
WORKDIR "/src/HelloBlazor"
RUN dotnet build "HelloBlazor.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HelloBlazor.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HelloBlazor.dll"]
