FROM centos
WORKDIR /opswat

EXPOSE 8008/tcp
EXPOSE 8007/tcp

COPY src/* ./


#RUN /usr/bin/yum -q -y *.rpm
#RUN Start-Process msiexec.exe -Wait -ArgumentList "/i", "C:\\OPSWAT\\$env:ometascan_install_file", "/qn", "/norestart" ;

# Define entrypoint
#ENTRYPOINT ["sh", "-c", "start.sh"]
ENTRYPOINT ["echo", "hello world"]

