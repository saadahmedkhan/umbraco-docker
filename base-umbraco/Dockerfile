FROM mcr.microsoft.com/dotnet/framework/aspnet:4.7.2-windowsservercore-ltsc2019

# Can be changed without editing the docker file by running: "docker build --build-arg version=8.1.5 ."
ARG VERSION=7.1.7

# Delete all files in the default IIS folders
RUN powershell -NoProfile -Command Remove-Item -Recurse C:\inetpub\wwwroot\*

# Install of the site to C:/Umbraco
WORKDIR C:/Umbraco

# Copy all local files
COPY . .

# Configure IIS with the website
RUN powershell -NoProfile -Command \
    Import-Module IISAdministration; \
    New-IISSite -Name "Site" -PhysicalPath C:\Umbraco -BindingInformation "*:8080:"

# Release from this page: https://github.com/umbraco/Umbraco-CMS/releases update to the latest version required
#ADD https://umbracoreleases.blob.core.windows.net/download/UmbracoCms.${VERSION}.zip .

# Expand the archive with powershell
#RUN $file = ls; \
    #$fileName = $file[0].Name; \
    #$filePath = 'C:/Umbraco/' + "$fileName"; \
    #powershell -NoProfile -Command Expand-Archive $filePath .; \
    #Remove-Item $filePath

EXPOSE 8080
EXPOSE 80