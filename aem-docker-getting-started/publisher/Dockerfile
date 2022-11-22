FROM aem-base

WORKDIR /opt/aem

#COPY ./publish/packages/* /opt/aem/crx-quickstart/install

EXPOSE 4503
CMD java -Djava.awt.headless=true -Xms1024m -Xmx2048m -Xdebug -Xnoagent -agentlib:jdwp=transport=dt_socket,address=30304,server=y,suspend=n -jar AEM_Quickstart.jar -p 4503 -r publish,local -v -nofork