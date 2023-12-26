# Setup Development environment (Nest.js)

1. Package manager: `homebew` Windows: `scoop`

2. NVM

    - macos

        ```shell
        type nvm
        ```

        ```shell
        brew install nvm && brew info nvm
        ```

        Create NVM's Working Directory

        ```shell
        mkdir -p ~/.nvm
        ```

        Add NVM Configurations to Shell Configuration File

        ```shell
        echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.zshrc echo '. "/usr/local/opt/nvm/nvm.sh"' >> ~/.zshrc && source ~/.zshrc
        ```

        ```shell
        nvm install latest && nvm use latest
        ```

    - Windows:
        ```shell
        scoop install nvm && nvm install latest && nvm use latest
        ```

3. Yarn
    ```shell
    npm install --global yarn
    ```
4. Nest

    ```shell
    yarn global add @nestjs/cli
    ```

## Software

-   VSCode
-   SSH KEYS
-   Docker Desktop
-   Postman
