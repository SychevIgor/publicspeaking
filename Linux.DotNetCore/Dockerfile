FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Linux.DotNetCore/Linux.DotNetCore.csproj", "Linux.DotNetCore/"]
RUN dotnet restore "Linux.DotNetCore/Linux.DotNetCore.csproj"
COPY . .
WORKDIR "/src/Linux.DotNetCore"
RUN dotnet build "Linux.DotNetCore.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Linux.DotNetCore.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Linux.DotNetCore.dll"]