FusePoC
=======

- Clone this repository
- Download jboss-fuse-full-6.0.0.redhat-024.zip from access.redhat.com and save in the dist directory of this repository. Don't worry about unzipping it.
- Install Vagrant - http://www.vagrantup.com/
- At the command line go to the main directory of this repository and then type:

> vagrant up

- Wait a bit, You will now have a fully configured vm image running locally. To connect to it type:

> vagrant ssh

- You will now be ssh'ed into your vm
- Change to the Fuse bin directory

> cd /vagrant/runtime/jboss-fuse-6.0.0.redhat-024/bin

- Start Fuse

> ./start

- After 20-30 seconds start a Fuse client

> ./client -u admin -p admin

- Create a Fuse fabric

> fabric:create --clean

- Wait for 30 seconds and then modify the fabric profile

> fabric:profile-edit --pid org.fusesource.fabric.agent/org.ops4j.pax.url.mvn.repositories='file:///vagrant/fuse-poc-offline-repo/target/features-repo@snapshots@id=poc' default

- Run the Karaf script to deploy the PoC

> source mvn:com.mycompany/fuse-poc-features/1.0.0-SNAPSHOT/karaf/create

- Check the new container has started up successfully. Run the following command and check container1 status is success

> container-list

- You will have to wait a bit for everything to get up and running then test the camel route. Browse to http://localhost:9090/route/accountservice/account/1234 and you should get a JSON response


Not using Vagrant
=================

- Uncomment the admin user in user.properties under $FUSE_HOME/etc

- Ensure running from a fresh Fuse install by deleting 

>	$FUSE_HOME/data
>	$FUSE_HOME/instances
	
- Launch Fuse $FUSE_HOME/bin/fuse

- To create from scratch run the following

>	source mvn:com.mycompany/fuse-poc-features/1.0.0-SNAPSHOT/karaf/create
	
- To recreate the container and profile run

>	source mvn:com.mycompany/fuse-poc-features/1.0.0-SNAPSHOT/karaf/recreate




 
