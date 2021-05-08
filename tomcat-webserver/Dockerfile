FROM tomcat:8.5.50

# as a part of security folder in webapps are moved to
# webapps.dist, copying back the same into webapps folder 
RUN cp -r webapps.dist/* webapps && \
        rm conf/tomcat-users.xml \
            webapps/manager/META-INF/context.xml \
            webapps/host-manager/META-INF/context.xml 

# copying the configuration files

COPY tomcat-conf/tomcat-users.xml conf/tomcat-users.xml

COPY tomcat-conf/context.xml webapps/manager/META-INF/context.xml

COPY tomcat-conf/context.xml webapps/host-manager/META-INF/context.xml

# copy the war into webapps directory
COPY ./*.war /usr/local/tomcat/webapps/

# redirecting from home page to the web_app
RUN cp webapps/ROOT/index.jsp webapps/ROOT/index.jsp.bak && \
    echo '<% response.sendRedirect("/<web_app_path>"); %>' > webapps/ROOT/index.jsp
