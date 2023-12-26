## **Install**

### Windows
# If you installed PostgreSQL on Windows but are unable to run `psql` in the command line, it may be because the PostgreSQL binaries directory is not in your system's PATH environment variable. To fix this, you can add the PostgreSQL binaries directory to your system's PATH environment
# variable by following these steps:

# 1. Open the Start menu and search for `Environment Variables` and select `Edit the system environment variables`.
# 2. Click on the `Environment Variables` button at the bottom of the `System Properties` window.
# 3. In the `System Variables` section, scroll down and select the `Path` variable, then click the `Edit` button.
# 4. Click the `New` button and add the path to the PostgreSQL binaries directory, which is typically:
"C:\\Program Files\\PostgreSQL\\<version>\\bin"
# (replace `<version>` with the version of PostgreSQL you installed).
# 5. Click `OK` to close all the windows, then open a new command prompt window and try running `psql` again.

Change `os_user` `role` & `password`
```shell
cd "C:\\Program Files\\PostgreSQL\\15\\data"
psql -U postgres
CREATE DATABASE <username>;
CREATE ROLE <username> WITH LOGIN PASSWORD '<password>' SUPERUSER;
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO <username>;
```

# Start
pg_ctl start -D "C:\\Program Files\\PostgreSQL\\15\\data"

# Enable
pg_ctl register -N "PostgreSQL" -D "C:\\Program Files\\PostgreSQL\\15\\data" -o "-p 5432"

# Change os_user role & password
psql -d template1
CREATE DATABASE <username>;
CREATE ROLE <username> WITH LOGIN PASSWORD '<password>' SUPERUSER;
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO <username>;

# MacOS
brew install postgresql@14
PATH=$(brew --prefix postgresql@14)/bin:$PATH

# Superuser
psql -U postgres -d postgres
CREATE ROLE $(whoami) WITH LOGIN PASSWORD 'y|re^M|=?h£UD^Og<668/£I^*;w`"E)]0_!{eX1lqE0}!0|:#e' SUPERUSER;
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO ale;

# Specific database
psql -d ale -c "CREATE DATABASE indulge_local;"
psql -d ale -c "CREATE ROLE postgres WITH LOGIN PASSWORD 'Hellohello2022';"
psql -d ale -c "GRANT ALL PRIVILEGES ON DATABASE indulge_local TO postgres;"

# Postgis
brew install postgis
psql -d ale -c "CREATE EXTENSION postgis;"
brew services restart postgresql@14
