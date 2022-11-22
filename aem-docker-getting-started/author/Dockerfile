FROM aem-base

WORKDIR /opt/aem

#COPY ./author/packages/* /opt/aem/packages/

#RUN python aem_installer.py -i AEM_6.x_Quickstart.jar -r author,nosamplecontent,local -p 4502

EXPOSE 4502
CMD java -Djava.awt.headless=true -Xms1024m -Xmx2048m -Xdebug -Xnoagent -agentlib:jdwp=transport=dt_socket,address=30303,server=y,suspend=n -jar AEM_Quickstart.jar -p 4502 -r author,local -v -nofork