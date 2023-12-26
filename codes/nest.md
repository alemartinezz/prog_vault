# NestJS

## Run Nest.js Project Using Docker

```bash
docker-compose build --no-cache && docker-compose up --remove-orphans
```

## Steps to Initialize a Nest.js Project

1. **Start Project**

    ```bash
    npx nest new <project_name> && cd <project_name>
    ```

2. **Auto Format Code** - Configure `.prettierrc`.

3. **Environment Variables** - Create `.env` and update `.gitignore`.

    ```bash
    touch .env && echo -e "\n\n# ENVIRONMENT\n.env" >> .gitignore
    ```

4. **Base Dependencies** - Install required libraries.

    ```bash
    yarn add @nestjs/config @nestjs/typeorm bcrypt typeorm class-validator class-transformer
    ```

5. **Docker Configuration** - Create `Dockerfile` & `docker-compose.yml`.

6. **Organize App Files** - Move application files to the appropriate folder.

    ```plaintext
    |-- src
    |   |-- app
    |   |-- common
    |   |-- database
    |   |-- main.ts
    |   `-- usuario
    ```

7. **Set Global Prefix and Middleware** - Configure the global prefix and validation pipes.

    ```typescript
    // ...import statements...

    async function bootstrap() {
    	const app = await NestFactory.create(AppModule);
    	app.useGlobalPipes(new ValidationPipe());
    	const configService = app.get(ConfigService);
    	app.setGlobalPrefix(configService.get<string>('API_PREFIX'));
    	await app.listen(configService.get<number>('API_PORT', 3000));
    }

    bootstrap();
    ```

## User Module

1. **Create Module**

    ```bash
    npx nest g resource users
    ```

2. **Define TypeORM User Model**

    ```typescript
    import { Entity, PrimaryGeneratedColumn, Column, CreateDateColumn, UpdateDateColumn } from 'typeorm';

    @Entity()
    export class Usuario {
    	@PrimaryGeneratedColumn('uuid')
    	id: string;

    	@Column({ unique: true })
    	username: string;

    	@Column({ unique: true })
    	email: string;

    	@Column()
    	password: string;

    	@CreateDateColumn()
    	createdAt: Date;

    	@UpdateDateColumn()
    	updatedAt: Date;
    }
    ```

## Database connection

```jsx
mkdir src/database && touch src/database/database.module.ts
```

```jsx
import { Module, Logger } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { ConfigModule, ConfigService } from '@nestjs/config';

@Module({
	imports: [
		TypeOrmModule.forRootAsync({
			imports: [ConfigModule],
			useFactory: async (configService: ConfigService) => {
				const logger = new Logger('DatabaseConnection');
				const connectionOptions: object = {
					type: 'postgres',
					host: configService.get('DB_HOST'),
					port: +configService.get('DB_PORT') || 5432,
					username: configService.get('DB_USER'),
					password: configService.get('DB_PASSWORD'),
					database: configService.get('DB_NAME'),
					entities: [__dirname + '/../**/*.entity{.ts,.js}'],
					synchronize: true
				};

				try {
					await TypeOrmModule.forRoot(connectionOptions);
					logger.log('Database connection successful');
				} catch (error) {
					logger.error('Database connection failed', error);
				}

				return connectionOptions;
			},
			inject: [ConfigService]
		})
		// TypeOrmModule.forFeature([Usuario]) // Omitido ya que no tienes el módulo Usuario
	]
	// providers: [DataLoadService, UsuarioService] // Actualiza según tus servicios actuales
})
export class AppModule {}
```