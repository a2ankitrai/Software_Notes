Installing Mongo DB
---

# Install MongoDB Community Edition with Homebrew

- Update Homebrew’s package database.
	In a system shell, issue the following command:

	```brew update```

- Install MongoDB	

	To install the MongoDB binaries, issue the following command in a system shell:

	```brew install mongodb ```

	Install the Latest Development Release of MongoDB

	```brew install mongodb --devel```


# Run MongoDB

- Create the data directory

	Before you start MongoDB for the first time, create the directory to which the mongod process will write data. By default, the mongod process uses the /data/db directory. If you create a directory other than this one, you must specify that directory in the dbpath option when starting the mongod process later in this procedure.

	The following example command creates the default /data/db directory:

	```
	mkdir -p /data/db
	```

- Set permissions for the data directory.

	Before running `mongod` for the first time, ensure that the user account running `mongod` has read and write permissions for the directory.

- Run MongoDB

	To run MongoDB, run the `mongod` process at the system prompt. If necessary, specify the path of the `mongod` or the data directory.

	- Run without specifying paths

		If your system PATH variable includes the location of the mongod binary and if you use the default data directory (i.e., /data/db), simply enter mongod at the system prompt:

		```
		mongod
		```

	- Specify the path of the mongod

		If your PATH does not include the location of the mongod binary, enter the full path to the mongod binary at the system prompt:

		```
		<path to binary>/mongod
		```

	- Specify the path of the data directory

		If you do not use the default data directory (i.e., /data/db), specify the path to the data directory using the --dbpath option:

		```
		mongod --dbpath <path to data directory>	
		```

- Verify that MongoDB has started successfully		

	Verify that MongoDB has started successfully by checking the process output for the following line:

	```
	[initandlisten] waiting for connections on port 27017
	```

- Begin using MongoDB

	Start a `mongo` shell on the same host machine as the `mongod`. Use the `--host` command line option to specify the localhost address and port that the mongod listens on:

	```
	mongo --host 127.0.0.1:27017
	```

	Later, to stop MongoDB, press Control+C in the terminal where the mongod instance is running.

