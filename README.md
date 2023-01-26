# Livraria.

## Padronização de código:

- Linguagem no código (nome de varíaveis, funções, etc...): inglês
- Variáveis: CamelCase
- Funções: CamelCase & Arrow Function
- Pastas: CamelCase
- Interfaces: Começa com I, exemplo (IUser)

## Pastas e configurações globais:

- routes: Pasta para organização das rotas globais.
- \_tests\_\_: Pasta para organização dos testes de funcionamento da API.
- controllers: Pasta para organização dos controllers.
- [entities](https://miro.com/app/board/uXjVP0RfmY4=/): Modelos para criação das entidades.
- errors: Fará o retorno dos erros da API.
- interfaces: Local onde ficarão as interfaces.
- middlewares: Pasta dos middlewares.
- schemas: Onde ficarão os schemas do yup.
- services: Paste de armazenamento dos services.

## Bibliotecas Utilizadas:

- bcryptjs
- jsonwebtoken
- cross-env
- dotenv
- express
- express-async-errors
- pg
- reflect-metadata
- typeorm
- supertest
- yup
- jest
- sqlite3
- ts-jest
- ts-node-dev
- typescrip

## Ao clonar o repositório:

- Abra o seu terminal e digite $yarn para instalar as dependencias
- Configure as variáveis de ambiente no arquivo .env
- E para rodar a aplicação $yarn dev


Library API

This is an API made by Kenzie Academy students. The API works as a backend for an online bookstore.

## Link To Use The API
- https://m4-e-library-api.onrender.com



# Existing endpoints:

- /users - Create, Update, List Delete and SoftDelete
- /login - Login user
- /profile - Get current user profile
- /books - Create, Update, List Delete and SoftDelete
- /categories - Create, Update, List and SoftDelete
- /orders - Create, Update, List and SoftDelete
- /carts - Create, Update, List and Delete
- /stocks - Get the number of selected book in stock


# - Creating Users (POST)
/users

## Create user - status 201


Request example:
```
{
	"name": "Normal User",
	"email": "normal@mail.com",
	"isEmployee": false,
	"password": "password123$"
}
```

Expected return:
```
{
	"updatedAt": "2023-01-18T17:58:35.054Z",
	"createdAt": "2023-01-18T17:58:35.054Z",
	"isActive": true,
	"id": "54c07e45-60c1-4a4d-b0f7-029f3983ee9a",
	"isEmployee": false,
	"email": "normal@mail.com",
	"name": "Normal User"
}
```

### Create employee - status 201

Request example:
```
{
	"name": "employee User",
	"email": "employee@mail.com",
	"isEmployee":true,
	"password": "password123$"
}
```

the only difference from the request above is that the employee has a true value instead of false


Expected return:
```
{
	"updatedAt": "2023-01-18T17:58:35.054Z",
	"createdAt": "2023-01-18T17:58:35.054Z",
	"isActive": true,
	"id": "54c07e45-60c1-4a4d-b0f7-029f3983ee9a",
	"isEmployee": true,
	"email": "employee@mail.com",
	"name": "Employee  User"
}
```


### Create bad request user - status 400

Request example:
```
{
	"name": "Normal User",
	"email": "normal@mail.com",
	"isEmployee": false
}
```

Expected return:
```
{
	"message": "password is a required field"
}
```



### Create duplicate user - status 409

Request example:
```
{
	"name": "Normal User",
	"email": "normal@mail.com",
	"isEmployee": false,
	"password": "password123$"
}
```

Expected return:
```
{
    "message": "User already exists"
}
```


## - Updating Users (PATCH)
/users/:id

*Needs Headers with token.

### Update your own user - status 200

Request example:
```
{
	"name": "Normal User7 Green",
	"email": "normal78@mail.com"
}
```
Expected return:
```
{
	"updatedAt": "2023-01-18T21:39:11.033Z",
	"createdAt": "2023-01-18T21:13:58.612Z",
	"isActive": true,
	"id": "a5d26115-1d6a-4784-81b5-aff36754d2a9",
	"isEmployee": false,
	"email": "normal78@mail.com",
	"name": "Normal User7"
}
```


### Update user (isEmployee=true) - status 200

Request example:
```
{
	"name": "Normal User Green",
	"email": "normal@mail.com"
}
```
Expected return:
```
{
	"updatedAt": "2023-01-18T19:10:06.798Z",
	"createdAt": "2023-01-18T17:58:35.054Z",
	"isActive": true,
	"id": "54c07e45-60c1-4a4d-b0f7-029f3983ee9a",
	"isEmployee": true,
	"email": "normal@mail.com",
	"name": "Normal User Green",
}
```


### Update user(not auth) - status 401

Expected return:
```
{
	"message”: “Not authorized”
}
```

### Update user(invalid id) - status 404


Expected return:
```
{
	"message": "invalid id"
}
```


### Update user(invalid credential) - status 403

Expected return:
```
{
	"message": "invalid signature"
}
```


### Update user(inactive user) - status 400

Expected return:
```
{
	"message”: “You don’t have permission”
}
```


## - Listing Users (GET)
/users

*No body required.

*Needs Headers with token(with credential).


### List users - status 200- Private employee route


Request example:
```
{
	Bearer: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOiIxYjdkNzQ5MC0wNzUxLTQwMjUtOGYzOC1mNmJjOTY3MmVjMWMiLCJpc0FkbSI6dHJ1ZSwiaWF0IjoxNjcyNzc4NDk0LCJleHAiOjE2NzI4NjQ4OTR9.DCT3Xa2Jv8I0lOUF6i-w6zaFkGR5_6w1OPqQoNm9D0o"
}
```

Expected return:
```
[
	{
		"updatedAt": "2023-01-12T15:25:04.932Z",
		"createdAt": "2023-01-12T15:10:18.390Z",
		"isActive": false,
		"id": "04138b42-cd9e-4207-b690-bf09152a8d04",
		"isEmployee": false,
		"email": "josue@mail.com",
		"name": "josue"
	},
	{
		"updatedAt": "2023-01-17T20:01:24.782Z",
		"createdAt": "2023-01-17T20:01:24.782Z",
		"isActive": true,
		"id": "f5e1f672-c9d1-4888-9cd4-0519d1ce0fcd",
		"isEmployee": false,
		"email": "usuarioCliente@mail.com",
		"name": "Usuario Não Empregado"
	},
	{
		"updatedAt": "2023-01-17T23:44:42.122Z",
		"createdAt": "2023-01-17T23:42:24.157Z",
		"isActive": true,
		"id": "0b55e860-38a8-40ec-afac-153793f0f346",
		"isEmployee": true,
		"email": "lucasssdffs@mail.com",
		"name": "Lucas"
	}
]
```


### List users with unauthorized token - status 401


Expected return:
```
{
	"message": "Unauthorized"
}
```

### List users without credentials - status 403


Expected return:
```
{
	"message": "User is not authorized"
}
```

##- Deleting Users (DELETE)
/users/delete/:id

*No body required.

*Needs Headers with token.

*Must have the isEmployee credential or delete the user's own

### Delete user - status 204

Expected return:

No body returned for response


### Delete users with invalid id - status 404

Expected return:
```
{
	"message": "User not found"
}
```

### Delete user without having credentials - status 403

Expected return:
```
{
	"message": "Unauthorized"
}
```


## - Soft Deleting Users (DELETE)
/users/:id

*No body required.

*Needs Headers with token.

### Soft delete your own user - status 204

Expected return:
No body returned for response


### Soft delete users with invalid id - status 404

Expected return:
```
{
	"message": "User not found"
}
```

### Soft delete users without user login  - status 401

Expected return:
```
{
     "message": "Not authorized! You can just delete your own user."
}
```

### Soft delete user without credential - status 403

Expected return:
```
{
	"message": "Unauthorized"
}
```


### Soft delete user not active - status 400

Expected return:
```
{
	"message": "User is already inactive"
}
```

## - Creating user address (POST)
/address/:id

*Needs Headers with jwt token.

### Create user address - status 201


Request example:
```
{
	Bearer: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOiIxYjdkNzQ5MC0wNzUxLTQwMjUtOGYzOC1mNmJjOTY3MmVjMWMiLCJpc0FkbSI6dHJ1ZSwiaWF0IjoxNjcyNzc4NDk0LCJleHAiOjE2NzI4NjQ4OTR9.DCT3Xa2Jv8I0lOUF6i-w6zaFkGR5_6w1OPqQoNm9D0o"
}
```
```
{
	“zipCode”: 12234-222,
	“street”: “Down street”,
	“number”: 123,
	“neighborhood”: “next to plaza”,
	“city”:	“New York”,
	“state”: “New York”,
}
```

Expected return:
```
{
	“message”: “Address created”
}
```

### Create user address with no authorization - status 401

Expected return:
```
{
	"message": "Unauthorized"
}
```
 
### Create user address for another user - status 403

Expected return:
```
{
	"message": "Forbidden"
}
```

### Create user address bad data - status 400

Expected return:
```
{
	"message": "Bad request"
}
```

## - Listing addresses (GET)
/address

*Needs Headers with jwt token(with credential).


### List addresses - status 200

Expected return:
```
[
	{
“id”: "dd2f4148-65b2-4202-adfd-863638bd3b62",
	“zipCode”: 12234-222,
	“street”: “Down street”,
	“number: 123,
	“neighborhood”: “next to plaza”,
	“city”:	“New York”,
	“state”: “New York”,
},
{
“id”: "dd2f4148-65b2-4202-adfd-863638bd3b62",
	“zipCode”: 12234-222,
	“street”: “Down street”,
	“number: 123,
	“neighborhood”: “next to plaza”,
	“city”:	“New York”,
	“state”: “New York”,
}
]
```

### List address with no authorization - status 401

Expected return:
```
{
	"message": "Unauthorized"
}
```
 
### List address with no credential - status 403

Expected return:
```
{
	"message": "Unauthorized"
}
```


## - Get address (GET)
/address/:id

*Needs Headers with jwt token.



### Get address - status 200

Expected return:
```
{
“id”: "dd2f4148-65b2-4202-adfd-863638bd3b62",
	“zipCode”: 12234-222,
	“street”: “Down street”,
	“number: 123,
	“neighborhood”: “next to plaza”,
	“city”:	“New York”,
	“state”: “New York”,
}
```

### Get user address without auth - status 401

Expected return:
```
{
	“message”: “Unauthorized”
}
```

### Get another user address without credential - status 403

Expected return:
```
{
	“message”: “Unauthorized”
}
```
### Get user address with invalid data - status 404

Expected return:
```
{
	“message”: “Not found”
}
```
### Get user address with bad data - status 400

Expected return:
```
{
	“message”: “Bad data”
}
```

## - Updating user address (PATCH)
/address/:id

*Needs Headers with jwt token.


### Update user address - status 200


Request example:
```
{
	Bearer: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOiIxYjdkNzQ5MC0wNzUxLTQwMjUtOGYzOC1mNmJjOTY3MmVjMWMiLCJpc0FkbSI6dHJ1ZSwiaWF0IjoxNjcyNzc4NDk0LCJleHAiOjE2NzI4NjQ4OTR9.DCT3Xa2Jv8I0lOUF6i-w6zaFkGR5_6w1OPqQoNm9D0o"
}
```
```
{
	“id”: "dd2f4148-65b2-4202-adfd-863638bd3b62",
	“zipCode”: 15144-200,
	“street”: “Down street”,
	“number: 123,
	“neighborhood”: “next to Chile”,
	“city”:	“Rio de Janeiro”,
	“state”: “Rio de Janeiro”,
}
```
Expected return:
```
{
	“message”: “Address updated”
}
```

### Update user without auth - status 401

Expected return:
```
{
	“message”: “Unauthorized”
}
```
### Update user address - status 403


Expected return:
```
{
	"message": "Unauthorized"
}
```
### Update user address - status 200


Expected return:
```
{
	“message”: “Address updated”
}
```


## - Delete address (DELETE)
/address/delete/:id

*Needs Headers with jwt token.


### Delete address - status 200

Expected return:
```
{
	“message”: “Address deleted”
}
```

### Delete address - status 200

Expected return:
```
{
	“message”: “Address deleted”
}
```

### Delete user address with bad data - status 400

Expected return:
```
{
	“message”: “Bad data”
}
```

### Delete user address without auth - status 401

Expected return:
```
{
	“message”: “Unauthorized”
}
```

## - Login User (POST)
/login

### Login user - status 200


Request example:
```
{
	"email": "normal@mail.com",
	"password": "password123$"
}
```
Expected return:
```
{
	token: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOiIxYjdkNzQ5MC0wNzUxLTQwMjUtOGYzOC1mNmJjOTY3MmVjMWMiLCJpc0FkbSI6dHJ1ZSwiaWF0IjoxNjcyNzc4NDk0LCJleHAiOjE2NzI4NjQ4OTR9.DCT3Xa2Jv8I0lOUF6i-w6zaFkGR5_6w1OPqQoNm9D0o"
}
```

### Login admin - status 200


Request example:
```
{
	"email": "normal@mail.com",
	"password": "password123$"
}
```
Expected return:
```
{
	token: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOiIxYjdkNzQ5MC0wNzUxLTQwMjUtOGYzOC1mNmJjOTY3MmVjMWMiLCJpc0FkbSI6dHJ1ZSwiaWF0IjoxNjcyNzc4NDk0LCJleHAiOjE2NzI4NjQ4OTR9.DCT3Xa2Jv8I0lOUF6i-w6zaFkGR5_6w1OPqQoNm9D0o"
}
```

### Login user - status 403


Request example:
```
{
	"email": "normal@mail.com",
	"password": "password1zzzz$"
}
```
Expected return:
```
{
	“message”: “Wrong email or password”
}
```


## - User profile (GET)
/profile

*Needs Headers with jwt token.


### Get user profile - status 200

Expected return:
```
{
"id": "7bb2a285-0735-4b03-a9b1-27e595e26f86",
	"name": "Normal User",
	"email": "normal@mail.com",,
	"isEmployee": false,
	"isActive": true,
	"id": "dd2f4148-65b2-4202-adfd-863638bd3b62",
	"createdAt": "2022-09-17T20:11:22.646Z",
	"updatedAt": "2022-09-17T20:11:22.646Z"
}
```

### Get user profile with bad data - status 400

Expected return:
```
{
	“message”: “Bad data”
}
```

### Get user profile without auth - status 401

Expected return:
```
{
	“message”: “Unauthorized”
}
```

### Get another user profile without credential - status 403

Expected return:
```
{
	“message”: “Unauthorized”
}
```

### Get invalid user profile - status 404

Expected return:
```
{
	“message”: “Not found”
}
```


## - Creating Books (POST)
/books

*Needs Headers token with credential.


### Create book - status 201

Request example:
```
{
	"name": "How to be a billionaire",
	"price": 99.344,
	"author": “The author”,
	"synopsis": "Synopsis ponysos soysinp synopsis ponysos soysinp synopsis ponysos soysinp synopsisponysos soysinp synopsis ponysos soysinp synopsis",
	“category”: “Romance”
}
```
Expected return:
```
{
	“id”: "dd2f4148-65b2-4202-adfd-863638bd3b62",
	"name": "How to be a billionaire",
	"price": 99.344,
	"author": “The author”,
	"synopsis": "Synopsis ponysos soysinp synopsis ponysos soysinp synopsis ponysos soysinp synopsisponysos soysinp synopsis ponysos soysinp synopsis",
	“category”: “Romance”
}
```

### Create book, bad data - status 400

Request example:
```
{
	"price": 99.344,
	"author": “The author”,
	"synopsis": "Synopsis ponysos soysinp synopsis ponysos soysinp synopsis",
	“category”: “Romance”
}
```
Expected return:
```
{
	“message”: “Missing data”
}
```

### Create duplicate book - status 409

Request example:
```
{
"name": "How to be a billionaire",
	"price": 99.344,
	"author": “The author”,
	"synopsis": "Synopsis ponysos soysinp synopsis ponysos soysinp synopsis synopsis",
	“category”: “Romance”
}
```
Expected return:
```
{
	“message”: “Book name is already have been used”
}
```

### Create book without user login - status 401


Request example:
```
{
"name": "How to be a billionaire",
	"price": 99.344,
	"author": “The author”,
	"synopsis": "Synopsis ponysos soysinp synopsis ponysos soysinp",
	“category”: “Romance”
}
```
Expected return:
```
{
	“message”: “Unauthorized”
}
```

### Create book without credential - status 403


Request example:
```
{
"name": "How to be a billionaire",
	"price": 99.344,
	"author": “The author”,
	"synopsis": "Synopsis ponysos soysinp synopsis synopsis",
	“category”: “Romance”
}
```
Expected return:
```
{
	“message”: “Unauthorized”
}
```


## - Listing books (GET)
/books

*Don't need Headers token.


### List books - status 200

Expected return:
```
[
	{
		"id": "e035e3da-0f7f-43e6-a1e3-867f1fe138cc",
		"name": "How to be a billionaire",
		"price": "99.34",
		"author": "The author",
		"synopsis": "Synopsis ponysos soysinp synops",
		"booksCategories": [
			{
				"id": "8d274bc0-cf22-478a-ae3c-08fd42deabcf",
				"category": {
					"id": "1ce19407-5e4c-4f71-9160-133d2829439f",
					"category_name": "Romance",
					"description": "Leitura sobre historias de amor e paixao"
				}
			}
		]
	},
	{
		"id": "b7f72ce0-0f75-4dae-9fd6-1c7bc57a4e5d",
		"name": "HSSSSSSSSSSSSaaaaaaaaaaa",
		"price": "99.34",
		"author": "The author",
		"synopsis": "Synopsis ponysos soysinp synops",
		"booksCategories": [
			{
				"id": "982d3e6b-5f7e-45af-8293-70ece4a8e613",
				"category": {
					"id": "1ce19407-5e4c-4f71-9160-133d2829439f",
					"category_name": "Romance",
					"description": "Leitura sobre historias de amor e paixao"
				}
			}
		]
	}
]
```


## - Getting books by id(GET)
/books/:id

*Don't need Headers token.


### Getting a book by id - status 200

Expected return:
```
{
	"id": "1118378e-e29b-4f50-b73a-8afe84d5dcaa",
	"name": "Harry Potter d a Pedra Filosofal-123",
	"price": "39.90",
	"author": "jk rowling",
	"synopsis": "Harry Potter é um garoto órfão de 10 anos que vive infeliz com seus tios.",
	"booksCategories": [
		{
			"id": "b71fb962-c42b-49e4-a084-aa69fb8cd9c1",
			"category": {
				"id": "0dec7934-928b-4a23-afa1-8f5b0ea9ac9a",
				"category_name": "Ficcao",
				"description": "Criacao de caracter artistico, baseada na imaginacao"
			}
		}
	]
}
```


### Getting book not found - status 404

Expected return:
```
{
	“message”: “Book not found”
}
```

### Getting book bad data - status 400

Expected return:
```
{
	“message”: “Book not exists”
}
```

## - Deleting book (DELETE)
/books/:id

*Need Headers token.

Deleting a book - status 204

No expected return


### Deleting a book without auth - status 401

Expected return:
```
{
“message”: “Invalid signature”
}
```


### Deleting a book without credential - status 403

Expected return:
```
{
“message”: “Not authorization”
}
```


### Deleting a book with bad data - status 400

Expected return:
```
{
“message”: “Bad data”
}
```


## - Updating book (PATCH)
/books/:id

*Need Headers token.


### Updating a book - status 200

Expected return:
```
{
	"id": "0445a43f-b305-4c0f-8c3a-d1adafe97853",
	"name": "Harry Potter e o Prisioneiro de Azkaban",
	"price": 39.5,
	"author": "jk rowling",
	"synopsis": "Harry Potter é um garoto órfão de 10 anos que vive infeliz com seus tios.",
	"booksCategories": [
		{
			"id": "df597f6a-f6a3-48d5-a2b0-e418efb98b83",
			"category": {
				"id": "0dec7934-928b-4a23-afa1-8f5b0ea9ac9a",
				"category_name": "Ficcao",
				"description": "Criacao de caracter artistico, baseada na imaginacao."
			}
		}
	]
}
```

### Updating book without auth - status 401

Expected return:
```
{
“message”: “Invalid signature”
}
```

### Updating book without credential - status 403

Expected return:
```
{
“message”: “Not authorization”
}
```

## - Listing Categories (GET)
/categories

*Don't need Headers token.

### List category - status 200

Expected return:
```
[
	{
		"id": "af199e32-f0c4-4a9a-93ac-2c5fbd9ffb12",
		"category_name": "Direito",
		"description": "Livros sobre doutrinas brasileiras"
	},
	{
		"id": "9c0d858f-cfe3-4cfb-894c-a4db4e9ae2ef",
		"category_name": "Acao",
		"description": "Livros genero acao"
	},
	{
		"id": "0dec7934-928b-4a23-afa1-8f5b0ea9ac9a",
		"category_name": "Ficcao",
		"description": "Criacao de caracter artistico, baseada na imaginacao, mesmo se idealizada a partir de dados reais"
	}
]
```

## - Select Category (GET)
/categories/:id

*Don't need Headers token.


### Select category - status 200

Expected return:
```
{
	"id": "af199e32-f0c4-4a9a-93ac-2c5fbd9ffb12",
	"category_name": "Direito",
	"description": "Livros sobre doutrinas brasileiras"
}
```


### Select category with bad data - status 400

Expected return:
```
{
	"message": "invalid input syntax for type uuid: \"545\""
}
```


### Select category with invalid id - status 404

Expected return:
```
{
	“message”: “Category not found”
}
```


## - Adding items on a cart (POST)
/carts/:id

*Need Headers token.


### Adding item - status 201

Expected return:
```
{
	"isActive": true,
	"cart": {
		"id": "7afec6c7-75e9-41fc-995b-69ea8c92cc3c",
		"status": "open"
	},
	"book": {
		"id": "1118378e-e29b-4f50-b73a-8afe84d5dcaa",
		"name": "Harry Potter d a Pedra Filosofal-123",
		"price": "39.90",
		"author": "jk rowling",
		"synopsis": "Harry Potter é um garoto órfão de 10 anos que vive infeliz.",
		"booksCategories": [
			{
				"id": "b71fb962-c42b-49e4-a084-aa69fb8cd9c1",
				"category": {
					"id": "0dec7934-928b-4a23-afa1-8f5b0ea9ac9a",
					"category_name": "Ficcao",
					"description": "Criacao de caracter artistico."
				}
			}
		]
	},
	"id": "a21e6239-00e4-4ad7-9c92-8de4c0ad429c"
}
```


### Adding item with bad data - status 400

Expected return:
```
{
	“message”: “Bad data”
}
```

### Adding item without auth - status 401

Expected return:
```
{
	“message”: “Invalid signature”
}
```

### Adding item in another cart without credential - status 403

Expected return:
```
{
“message”: “Not authorization”
}
```

## - Finding a cart (GET)
/cart/:id

*Need Headers token.


### Finding a cart - status 200

Expected return:
```
{
	“id”: "dd2f4148-65b2-4202-adfd-863638bd3b62"
	“status”: “closed”
	“userId”: "dd2f4148-65b2-4202-adfd-863638bd3b62"
	“books”:
[
			{
		“id”: "dd2f4148-65b2-4202-adfd-863638bd3b62",
		"name": "How to be a billionaire",
		"price": 99.344,
		"author": “The author”,
		"synopsis": "Synopsis ponysos soysinp synopsis ponysos soysinp synopsis",
},
{
		“id”: "dd2f4148-65b2-4202-adfd-863638bd3b62",
		"name": "There are many products in your cart",
		"price": 31.44,
		"author": “The author”,
		"synopsis": "Synopsis ponysos soysinp synopsis ponysos soysinp synopsis",
},
		]
}
```

### Finding a cart with bad data - status 400

Expected return:
```
{
	“message”: “Bad data”
}
```

### Finding a cart without auth - status 401

Expected return:
```
{
	“message”: “Invalid signature”
}
```

### Finding a cart of another user without credential - status 403

Expected return:
```
{
	“message”: “Not authorization”
}
```

### Finding invalid cart - status 404

Expected return:
```
{
	“message”: “Not found”
}
```

## - Soft delete cart book (GET)
/cart/books/:id

*Need Headers token.


### Soft delete a cart book - status 200

Expected return:
```
{
	“message”: “Cart item soft deleted”
}
```

### Soft delete a cart with bad data - status 400

Expected return:
```
{
	“message”: “Bad data”
}
```

### Soft delete a cart without auth - status 401

Expected return:
```
{
	“message”: “Invalid signature”
}
```

### Soft delete another cart without credential - status 403

Expected return:
```
{
	“message”: “Not authorization”
}
```

### Soft delete on invalid cart - status 404

Expected return:
```
{
	“message”: “Not found”
}
```


## - Delete cart book (GET)
/cart/book/:id

*Need Headers token.


Delete a cart book - status 200

No expected return


### Delete a cart with bad data - status 400

Expected return:
```
{
	“message”: “Bad data”
}
```

### Delete a cart without auth - status 401

Expected return:
```
{
	“message”: “Invalid signature”
}
```

### Delete another cart without credential - status 403

Expected return:
```
{
	“message”: “Not authorization”
}
```

### Soft delete on invalid cart - status 404

Expected return:
```
{
	“message”: “Not found”
}
```


## - Create book stock (POST)
/stock/:id

*Need Headers token with credential.


### Create a book stock - status 201

Expected return:
```
{
	"book_qntd": 600,
	"book": "0445a43f-b305-4c0f-8c3a-d1adafe97853",
	"id": "aee11f9f-6c85-40fa-8199-2bdc71cc2155"
}
```

### Create a book stock that already exists - status 409

Expected return:
```
{
	“message”:  “Book already have stock”
}
```
### Create a negative book stock - status 404

Expected return:
```
{
	“message”:  “Not possible.”
}
```
### Create a book stock with the book that does not exist - status 404

Expected return:
```
{
	“message”:  “Not possible.”
}
```


## - Select all books stock (GET)
/stock

*Need Headers token with credential.


### Select all books stock - status 200

Expected return:
```
[
	{
		"id": "aee11f9f-6c85-40fa-8199-2bdc71cc2155",
		"book_qntd": 600,
		"book": {
			"id": "0445a43f-b305-4c0f-8c3a-d1adafe97853",
			"name": "Harry Potter e o Prisioneiro do Clube do Bolinha",
			"price": "39.50",
			"author": "jk rowling",
			"synopsis": "Harry Potter é um garoto órfão de 10 anos que vive infeliz.",
			"booksCategories": [
				{
					"id": "df597f6a-f6a3-48d5-a2b0-e418efb98b83"
				}
			]
		}
	},
	{
		"id": "e8354dfb-8555-4d29-9978-628625a5bebf",
		"book_qntd": 344,
		"book": {
			"id": "8aa57019-bd42-4231-bbd7-9d3dc314b626",
			"name": "Harry Potter e a Grande Pedra",
			"price": "39.90",
			"author": "jk rowling",
			"synopsis": "Harry Potter é um garoto órfão de 10 anos que vive infeliz.",
			"booksCategories": [
				{
					"id": "d88a5ece-467a-4b70-b302-bdb57dd591d6"
				}
			]
		}
	}
]
```

### Select all books stock without credential - status 403

Expected return:
```
{
	“message”: “Not authorization”
}
```

### Select all books stock without valid token - status 401

Expected return:
```
{
	“message”: “Invalid signature”
}
```


## - Update a book stock (PATCH)
/stock/:id

*Need Headers token with credential.


### Update a book stock - status 200

Expected return:
```
{
	"id": "e8354dfb-8555-4d29-9978-628625a5bebf",
	"book_qntd": 80
}
```

### Update with a negative book stock - status 404

Expected return:
```
{
	“message”:  “Not possible.”
}
```

### Update stock without credential - status 403

Expected return:
```
{
	“message”: “Not authorization”
}
```

### Update stock without valid token - status 401

Expected return:
```
{
	“message”: “Invalid signature”
}
```

### Update with non-existent stock id - status 404

Expected return:
```
{
	“message”:  “Stock not exists.”
}
```
