# Stage 1 - Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS builder
WORKDIR /app1
COPY *.csproj ./
RUN dotnet restore
COPY . .
RUN dotnet publish -c Release -o out

# Stage 2 - Runtime only (much smaller than SDK image)
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app1
COPY --from=builder /app/out .
EXPOSE 5000
ENV ASPNETCORE_URLS=http://+:5000
CMD ["dotnet", "sample-app-dotnet.dll"]
