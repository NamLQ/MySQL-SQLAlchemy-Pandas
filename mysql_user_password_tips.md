# create user
	# https://stackoverflow.com/a/10236195/2757266
	# account can be used only when connecting from the local host
		CREATE USER 'namlq'@'localhost' IDENTIFIED BY 'abc123';
	# superuser account with full privileges to do anything
		GRANT ALL PRIVILEGES ON *.* TO 'namlq'@'localhost' WITH GRANT OPTION;
		
	# uses the '%' wildcard for the host part, so it can be used to connect from any host.
		CREATE USER 'namlq'@'%' IDENTIFIED BY 'abc123';
	# superuser account with full privileges to do anything
		GRANT ALL PRIVILEGES ON *.* TO 'namlq'@'%' WITH GRANT OPTION;
		CREATE USER 'admin'@'localhost';
		GRANT RELOAD,PROCESS ON *.* TO 'admin'@'localhost';
		CREATE USER 'dummy'@'localhost';


# show user
		use mysql
		SELECT user, host, account_locked, password_expired FROM mysql.user;
		
	+------------------+-----------+----------------+------------------+
	| user             | host      | account_locked | password_expired |
	+------------------+-----------+----------------+------------------+
	| namlq            | %         | N              | N                |
	| admin            | localhost | N              | N                |
	| dummy            | localhost | N              | N                |
	| mysql.infoschema | localhost | Y              | N                |
	| mysql.session    | localhost | Y              | N                |
	| mysql.sys        | localhost | Y              | N                |
	| namlq            | localhost | N              | N                |
	| root             | localhost | N              | N                |
	+------------------+-----------+----------------+------------------+
	8 rows in set (0.00 sec)

# password policy
		SHOW VARIABLES LIKE 'validate_password%';
	+--------------------------------------+-------+
	| Variable_name                        | Value |
	+--------------------------------------+-------+
	| validate_password.check_user_name    | ON    |
	| validate_password.dictionary_file    |       |
	| validate_password.length             | 8     |
	| validate_password.mixed_case_count   | 1     |
	| validate_password.number_count       | 1     |
	| validate_password.policy             | LOW   |
	| validate_password.special_char_count | 1     |
	+--------------------------------------+-------+
		SET GLOBAL validate_password.policy = LOW;
		SET GLOBAL validate_password.length = 6;
		SET GLOBAL validate_password.number_count = 0;
		SET GLOBAL validate_password.mixed_case_count = 0;
		SET GLOBAL validate_password.special_char_count = 0;

# load databases:
		source mysqlsampledatabase.sql;

