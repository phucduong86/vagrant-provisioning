Instruction to prepare a Role for a new Tomcat Instance

1. Copy tc-hello-world folder to 'tc-app-name' folder

  cp -R tc-hello-world tc-app-name
2. Copy app-name.war file to /templates

  cp app-name.war /provisioning/roles/tc-app-name/template/

3. Edit default/main.yml with new ports numbers and app-name

  app_name: sample
  tomcat_inst_port: 8280
  tomcat_inst_ajp_port: 8209
  tomcat_inst_shutdown_port: 8205

4. Edit task/main.yml
  
  Under Check if tomcat service has been created
  Change tc-hello-world to tc-app-name

  Under Create tomcat service
  CHange tc-hello-world to tc-app-name

- Rename tc-hello-world to tc-appname (init script)
- Rename tc-hello-wolrd-vhost.conf to tc-app-name.conf

5. Edit war file name under Deploy Application

  src: '/vagrant/provisioning/roles/{{ tomcat_inst_name }}/templates/sample.war'

6. Add worker information to workers.properties (apache/templates) make sure the name is in the worker.list
 
  worker.tc-sample.type=ajp13
  worker.tc-sample.host=localhost
  worker.tc-sample.port=8209

7. Update /roles/apache/templates/httpd-vhost.conf
  
  Add the following line:
  JkMount /app-name* tc-app-name

8. Run vagrant reload