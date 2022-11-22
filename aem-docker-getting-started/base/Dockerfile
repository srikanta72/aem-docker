FROM centos:7

# Install packages
# ld-linux.so.2, glibc.i686 and libuuid.i686 are added to enable XMP extraction and write-back on 64-bit RedHat Linux
# See https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html.
RUN yum -y update
RUN yum -y install java-11-openjdk

# Copy required build media
ADD aem_instance/aem-quickstart.jar /opt/aem/aem-quickstart.jar
ADD aem_instance/license.properties /opt/aem/license.properties

# Extract AEM
WORKDIR /opt/aem
RUN java -Djava.awt.headless=true -Xms1024m -Xmx4096m -jar aem-quickstart.jar -unpack

COPY ./base/packages/aem-service-pkg-6.5.13-SITES-3574-B0001.zip /opt/aem/crx-quickstart/install/aem-service-pkg-6.5.13-SITES-3574-B0001.zip