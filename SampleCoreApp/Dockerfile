FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["SampleCoreApp/SampleCoreApp.csproj", "SampleCoreApp/"]
RUN dotnet restore "SampleCoreApp/SampleCoreApp.csproj"
COPY . .
WORKDIR "/src/SampleCoreApp"
RUN dotnet build "SampleCoreApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SampleCoreApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SampleCoreApp.dll"]