FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["TransImage/TransImage.csproj", "TransImage/"]
RUN dotnet restore "TransImage/TransImage.csproj"
COPY . .
WORKDIR "/src/TransImage"
RUN dotnet build "TransImage.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TransImage.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TransImage.dll"]