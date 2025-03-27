# =======================
# 1️⃣ Base Image để Build
# =======================
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /app

# Copy file project
COPY ["Test2/Test2.csproj", "Test2/"]
RUN dotnet restore "Test2/Test2.csproj"

# Copy toàn bộ mã nguồn vào container
COPY . . 
WORKDIR "/app/Test2"

# Build project
RUN dotnet build "Test2.csproj" -c Release -o /build
RUN dotnet publish "Test2.csproj" -c Release -o /publish /p:UseAppHost=false

# =========================
# 2️⃣ Base Image để Runtime
# =========================
FROM mcr.microsoft.com/dotnet/aspnet:9.0

# Chạy với quyền root (Linux mode)
USER root

# Cài đặt Google Chrome & ChromeDriver
RUN apt-get update && apt-get install -y wget unzip curl && \
    wget -q https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && \
    apt-get install -y ./google-chrome-stable_current_amd64.deb && \
    rm google-chrome-stable_current_amd64.deb && \
    rm -rf /var/lib/apt/lists/*

RUN wget -q -O /tmp/chromedriver.zip "https://storage.googleapis.com/chrome-for-testing-public/134.0.6998.35/linux64/chrome-linux64.zip" && \
    unzip /tmp/chromedriver.zip -d /usr/local/bin/ && \
    rm /tmp/chromedriver.zip


WORKDIR /app
COPY --from=build /publish .

# Mở cổng ứng dụng
EXPOSE 8080
EXPOSE 8081

# Chạy ứng dụng
ENTRYPOINT ["dotnet", "Test2.dll"]
