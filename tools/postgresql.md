# PostgreSQL Installation and Configuration Guide

## 📥 Install

### Windows

To run `psql` in the command line after installing PostgreSQL on Windows, ensure the PostgreSQL binaries directory is included in your system's PATH environment variable. Follow these steps to update the PATH:

1. Open the Start menu, search for `Environment Variables`, and select `Edit the system environment variables`.
2. Click on the `Environment Variables` button at the bottom of the `System Properties` window.
3. In the `System Variables` section, find and select the `Path` variable, then click `Edit`.
4. Click `New` and add the PostgreSQL binaries directory path:

    ```powershell
    "C:\\Program Files\\PostgreSQL\\<version>\\bin"
    ```
   (Replace `<version>` with the version number of PostgreSQL you installed).

5. Confirm changes with `OK`, open a new command prompt window, and attempt running `psql` again.

To start and enable PostgreSQL:

   ```shell
   pg_ctl start -D "C:\\Program Files\\PostgreSQL\\<version>\\data"
   ```

To register PostgreSQL as a service:

   ```shell
   pg_ctl register -N "PostgreSQL" -D "C:\\Program Files\\PostgreSQL\\<version>\\data" -o "-p 5432"
   ```

### MacOS

Install PostgreSQL using Homebrew and update your PATH:

```shell
brew install postgresql@14
PATH=$(brew --prefix postgresql@14)/bin:$PATH
```

## 🔩 Configuration

### Change os_user Role & Password

- Connect to the default template database:

    ```shell
    psql -d template1
    ```

- Create a new database and role with superuser privileges:

    ```sql
    CREATE DATABASE <username>;
    CREATE ROLE <username> WITH LOGIN PASSWORD '<password>' SUPERUSER;
    GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO <username>;
    ```

- For superuser access:

    ```shell
    psql -U postgres -d postgres
    ```

- Create a superuser role:

    ```sql
    CREATE ROLE $(whoami) WITH LOGIN PASSWORD '<your_super_secure_password>' SUPERUSER;
    ```

- Assign privileges to a user:

    ```sql
    GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO <username>;
    ```

### Specific Database Operations

- Create and configure a specific database and user:

    ```shell
    psql -d <db_name> -c "CREATE DATABASE <new_db_name>;"
    psql -d <db_name> -c "CREATE ROLE <new_role> WITH LOGIN PASSWORD '<password>';"
    psql -d <db_name> -c "GRANT ALL PRIVILEGES ON DATABASE <new_db_name> TO <new_role>;"
    ```

### PostGIS Installation

For MacOS users needing to use PostGIS:

- Install PostGIS using Homebrew:

    ```shell
    brew install postgis
    ```

- Activate PostGIS on your database:

    ```shell
    psql -d <db_name> -c "CREATE EXTENSION postgis;"
    ```

- Restart PostgreSQL service:

    ```shell
    brew services restart postgresql@14
    ```

Replace placeholders like `<username>`, `<password>`, `<db_name>`, `<new_db_name>`, `<new_role>`, and `<version>` with the actual values relevant to your setup.
