FROM microsoft/aspnetcore:2.0.0
MAINTAINER "Freeman Ke" guang810828@gmail.com
WORKDIR /root/
USER root
COPY ./bin/publish/ /root/
EXPOSE 45000/tcp
ENTRYPOINT ["dotnet", "Telemetry.Web.dll"]  
