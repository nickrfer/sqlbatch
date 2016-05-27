# sqlbatch
An application for executing batch SQL Statements from files stored in a directory. While reading these files, the program checks if the line starts with DML Commands (INSERT, DELETE, UPDATE, MERGE or CALL) and execute it, otherwise it is ignored.

For better optimization, the commit happens when 1000 batchs are added to the PreparedStatement, and at the final iteration.
Logs will be appended to sqlbatch.log where the generated JAR is executed.

The file sqlbatch.properties can be put in the same path as the generated JAR to configure the app form, if the user doesn't want to input the fields everytime. The properties are { db.name, server.name, db.port, db.user, db.password, import.path }.

So far the SQLBatch app supports the DB2, Oracle and SQL Server Databases. I am planning to add support for other Databases.

# configuration
Since the DB2 and Oracle drivers are not available at the mavenrepository.com, you need to run the following commands after downloading the drivers in order to add the dependencies to the local maven repository:

- ojdbc7
mvn install:install-file Dpackaging=jar -Dfile=<USER_HOME>/ojdbc7.jar -DgroupId=com.oracle -DartifactId=ojdbc7 -Dversion=12.1.0.1

- db2jcc:
mvn install:install-file Dpackaging=jar -Dfile=<USER_HOME>/db2jcc_license_cu.jar -DgroupId=com.ibm.db2.jcc -DartifactId=db2jcc_license_cu -Dversion=3.8.47

- db2jcc_lcense_cu:
mvn install:install-file -Dpackaging=jar -Dfile=<USER_HOME>/db2jcc_license_cu.jar -DgroupId=com.ibm.db2.jcc -DartifactId=db2jcc_license_cu -Dversion=3.8.47

Feel free to change the dependency versions to better suit your needs!
