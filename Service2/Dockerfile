FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Service2/Service2.csproj", "Service2/"]
RUN dotnet restore "Service2/Service2.csproj"
COPY . .
WORKDIR "/src/Service2"
RUN dotnet build "Service2.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Service2.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Service2.dll"]