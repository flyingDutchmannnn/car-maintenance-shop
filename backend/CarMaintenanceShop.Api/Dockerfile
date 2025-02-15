# Use the official .NET image as the base image
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

# Copy the project file and restore the dependencies
COPY *.csproj .
RUN dotnet restore

# Copy the rest of the application code
COPY . .

# Build the application
RUN dotnet publish -c Release -o /app

# Use the official ASP.NET runtime image
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS runtime
WORKDIR /app
COPY --from=build /app .

# Expose port 80 for the API
EXPOSE 80

# Start the application
ENTRYPOINT ["dotnet", "CarMaintenanceShop.Api.dll"]