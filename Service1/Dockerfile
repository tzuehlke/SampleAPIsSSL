FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Service1/Service1.csproj", "Service1/"]
RUN dotnet restore "Service1/Service1.csproj"
COPY . .
WORKDIR "/src/Service1"
RUN dotnet build "Service1.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Service1.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Service1.dll"]