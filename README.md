
>START HERE

> IF USER APP EXISTS

    userdel -r app
    sudo userdel app
    sudo rm -r /home/app

ERROR: No home directory, logging in with HOME=/ [closed] (REPLACE dummy with app)
    $ ls -ld /home dummy
    drwx------ dummy dummy ........... dummy
    chown dummy:dummy /home/dummy
    chmod 700 /home/dummy
    sudo su -

    apt install -y git redis-server build-essential python3 python3-pip libmagic-dev mysql-server mysql-client libmysqlclient-dev libexiv2-dev libssl1.0-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget libffi-dev libboost-python-dev arcanist curl

    adduser --disabled-password --gecos "" app
    su - app
    git clone https://phab.phuks.co/source/throat.git

OR

    git clone https://github.com/Polsaker/throat <Defunct now

OR

    git clone https://github.com/jsailo/lawrkhawm.git

> AT THIS POINT YOU CAN CORRECT PEEWEE TO THE LATEST VERSION 3.10.0

    cd throat
    nano requirements.txt
    curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash
    echo 'export PATH="/home/app/.pyenv/bin:PATH"' >> ~/.bashrc
    echo 'eval "(pyenv init -)"' >> ~/.bashrc
    echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
    script

>The following command takes the longest time to execute

    pyenv install 3.5.2
    pyenv virtualenv 3.5.2 app
    exit
    exit

>BLANK SCREEN

     apt install -y npm  

 >INSTALL above AS ROOT

    su - app
    script
    cd throat
    npm install  
OR

    npm install -g npm (AVOID using this global option)
    npm run build
    pyenv local app
    pip install --upgrade pip

 > ALL FINE TILL HERE NO ERRORS

     pip install -r requirements.txt

>OPTIONAL FOR PY2EXIV
  
    pip install py3exiv2==0.1.0
    sudo apt-get install build-essential python-all-dev libexiv2-dev libboost-python-dev
    pip3 install py3exiv2
    pip install py3exiv2
    exit
    exit
    nano /etc/mysql/debian.cnf
    
>Note contents of debian.cnf file: 

    [client]
    host     = localhost
    user     = debian-sys-maint
    password = 5oCNi3MRmSXRxJFI
    socket   = /var/run/mysqld/mysqld.sock
    [mysql_upgrade]
    host     = localhost
    user     = debian-sys-maint
    password = 5oCNi3MRmSXRxJFI
    socket   = /var/run/mysqld/mysqld.sock
>USE THIS TO TEST YOUR MYSQL CONNECTION

    mysql -u debian-sys-maint -p

> If you get ERROR 2002 (HY000): Can’t connect to local MySQL server through socket ’/var/run/mysqld/mysqld.sock’ (2) ENSURE database server is started, start it using

    services mysql start
OR
    /etc/init.d/mysql start


>Export your Phuks database
  
    $ mysqldump throat > /home/app/throat_latest.sql

    $ mysql

    mysql> drop database throat;
    mysql> CREATE DATABASE throat;
    exit

> Your Sample database entry
  
    GNU nano 2.9.3
    /etc/mysql/debian.cnf                                           

>Automatically generated for Debian scripts. DO NOT TOUCH!

    [client]
    host     = localhost
    user     = debian-sys-maint
    password = 0L6hYNDw4QwpmsQ4 //sample
    socket   = /var/run/mysqld/mysqld.sock
    [mysql_upgrade]
    host     = localhost
    user     = debian-sys-maint
    password = 0L6hYNDw4QwpmsQ4 //sample

    socket   = /var/run/mysqld/mysqld.sock

>IMPORTANT: IMPORT THE EXPORTED DB BACK TO THROAT

>EXAMPLE
    $ mysql -u root -p throat < ../home/app/13082019.sql
    Enter password:
    su - app
    script
    cd throat
    cp example.config.py config.py
    nano config.py
                                                    
>This is where you enter the database connection strings (NOTE without CRLF. In notepad++ use paste special > paste binary content)

>Database connection information format in config.py

    set DB_USER to debian-sys-maint
    set DB_PASSWD to password from /etc/mysql/debian.cnf
    set DB_NAME to throat (or whatever was created, default is phuks)
    cd scripts
    ./install.py
    cd ..
    nano wsgi.py   //<NEVER RUN THIS COMMAND ON PRODUCTION

    socketio.run(app, debug=True, host='0.0.0.0')

>to run

    ./wsgi.py   < IF REDIS ERROR< START REDIS > sudo service redis-server start 

>To find the IP of your machine, visit http://<ip address>:5000
    username: admin
    
    password: adminadmin
    

>To host in production
    
    chmod 0777 /home/app/throat/start.sh
    supervisorctl start throat
