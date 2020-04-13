## Requirements
- A Valid Cq5 or AEM quick start jar.
- A Valid license key(license.properties).
- The Java Development Kit JDK version 1.5 and above.
- The Java Runtime Environment (JRE). Version 1.7 is preferred.
- 3 GB free hard disk drive space.
- At least 1.5 GB of RAM.

## Install
### Rename the AEM or CQ jar to cq-author-4502.jar:-
- cq refers to the adobe communique application name(you can use any name over here)
- author refers to the WCM mode we want to use (eg. author or publish)
- 4502 refers to the port that we want to use for running cq.

**Note**:- If no port number is provided in the file name, AEM6.0 will select the first available port from
the following list: 1) 4502, 2) 8080, 3) 8081, 4) 8082, 5) 8083, 6) 8084, 7) 8085, 8) 8888, 9)
9362, 10) random.

### Running
- If you are using 32 bit VM: java -Xmx1024M -jar cq5-author-4502.jar
- If you are using 64 bit VM: java -XX:MaxPermSize=256m -Xmx1024M -jar cq5-author-4502.jar

### Configuration user and service
Create these ones files
#### AEM
```
        #!/bin/bash
        #
        # /etc/rc.d/init.d/aem6
        #
        #
        # # of the file to the end of the tags section must begin with a #
        # character. After the tags section, there should be a blank line.
        # This keeps normal comments in the rest of the file from being
        # mistaken for tags, should they happen to fit the pattern.>
        #
        # chkconfig: 35 85 15
        # description: This service manages the Adobe Experience Manager java process.
        # processname: aem6
        # pidfile: /crx-quickstart/conf/cq.pid
         
        # Source function library.
        . /etc/rc.d/init.d/functions
         
        SCRIPT_NAME=`basename $0`
        AEM_ROOT=/opt/aem6
        AEM_USER=aem
         
        ########
        BIN=${AEM_ROOT}/crx-quickstart/bin
        START=${BIN}/start
        STOP=${BIN}/stop
        STATUS="${BIN}/status"
         
        case "$1" in
        start)
        echo -n "Starting AEM services: "
        su - ${AEM_USER} ${START}
        touch /var/lock/subsys/$SCRIPT_NAME
        ;;
        stop)
        echo -n "Shutting down AEM services: "
        su - ${AEM_USER} ${STOP}
        rm -f /var/lock/subsys/$SCRIPT_NAME
        ;;
        status)
        su - ${AEM_USER} ${STATUS}
        ;;
        restart)
        su - ${AEM_USER} ${STOP}
        su - ${AEM_USER} ${START}
        ;;
        reload)
        ;;
        *)
        echo "Usage: $SCRIPT_NAME {start|stop|status|reload}"
        exit 1
        ;;
        esac
```
#### aem.service
```
    [Unit]
    Description=Adobe Experience Manager
    
    [Service]
    Type=simple
    ExecStart=/usr/bin/aem start
    ExecStop=/usr/bin/aem stop
    ExecReload=/usr/bin/aem restart
    RemainAfterExit=yes
    
    [Install]
    WantedBy=multi-user.target
```
- Apri il file di script di aem e aggiorna quanto segue
  AEM_ROOT (es: /mnt/crx è la radice, dove /mnt/crx/crx-quickstart è il percorso completo)
  AEM_USER (es .: aem )
- SCP questi file sul server
  Copia aem in /usr/bin/aem
    Esempio: dal terminale sul desktop $ scp <filename> user@1.1.1.1:/usr/bin/aem
  Copia aem.service su /etc/system.d/system/aem.system
    Esempio: dal terminale sul desktop $ scp <filename> user@1.1.1.1:/etc/system.d/system/aem.system
- On server: To give authorization on files
  sudo chmod u+rwx /usr/bin/aem
  sudo chmod u+rwx /etc/system.d/system/aem.system
- Updating 
    cd /etc/system.d/system
    systemctl enable aem.system

<cite>Rif. [Riptutorial](https://riptutorial.com/it/aem/example/30703/impostazione-di-aem-6-x-su-centos-7)</cite>
