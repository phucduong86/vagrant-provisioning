Instruction to create a new Tomcat Instance

- Copy tc-hello-world folder to 'tc-app-name' folder
- Copy app-name.war file to /templates
- Edit default/main.yml with new ports numbers and app-name
- Edit task/main.yml
    Under Check if tomcat service has been created
    Change tc-hello-world to tc-app-name

    Under Create tomcat service
    CHange tc-hello-world to tc-app-name

- Rename tc-hello-world to tc-appname (init script)
- Rename tc-hello-wolrd-vhost.conf to tc-app-name.conf
- Edit specific parameters under Deploy Application
- Add worker information to workers.properties (apache/templates)
- Run vagrant reload