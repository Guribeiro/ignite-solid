<p align="center">
  <img src="./assets/logo.png" alt="Cover Ignite Node">
</p>
<h2 align="center">Chapter II - Challenge</h2>
<h1 align="center">Users Management</h1>

<h1 align="center">
  <img alt="Last commit" src="https://img.shields.io/github/last-commit/nlnadialigia/dev.finances?color=91091e&style=flat-square"/>

  <img alt="Repo size" src="https://img.shields.io/github/repo-size/nlnadialigia/ignite-solid?color=91091e"/>
   
  <a href="./license.md">
  <img alt="License" src="https://img.shields.io/static/v1?label=license&message=MIT&color=91091e"/>
  </a>
</h1>
<br>

# ℹ️ Index

- [About the challenge](#-📔-about-the-challenge)
  - [API Routes](#-📚-API-Routes)
- [Tests Specification](#-✴️-tests-specification)
  - [Model Test](#-📚-Model-Test)
    - [Should be able to create an user with all props](#-📌-Should-be-able-to-create-an-user-with-all-props)
  - [Repository Tests](#-📚-Repository-Tests)
    - [Should be able to create new users](#-📌-Should-be-able-to-create-new-users)
    - [Should be able to list all users](#-📌-Should-be-able-to-list-all-users)
    - [Should be able to find user by ID](#-📌-Should-be-able-to-find-user-by-ID)
    - [Should be able to find user by e-mail address](#-📌-Should-be-able-to-find-user-by-e-mail-address)
    - [Should be able to turn an user as admin](#-📌-Should-be-able-to-turn-an-user-as-admin)
  - [UseCases Tests](#-📚-UseCases-Tests)
    - [Should be able to create new users](#-📌-Should-be-able-to-create-new-users)
    - [Should not be able to create new users when email is already taken](#-📌-Should-not-be-able-to-create-new-users-when-email-is-already-taken)
    - [Should be able to turn an user as admin](#-📌-Should-be-able-to-turn-an-user-as-admin)
    - [Should not be able to turn a non existing user as admin](#-📌-Should-not-be-able-to-turn-a-non-existing-user-as-admin)
    - [Should be able to get user profile by ID](#-📌-Should-be-able-to-get-user-profile-by-ID)
    - [Should not be able to show profile of a non existing user](#-📌-Should-not-be-able-to-show-profile-of-a-non-existing-user)
    - [Should be able to list all users](#-📌-Should-be-able-to-list-all-users)
    - [Should not be able to a non admin user get list of all users](#-📌-Should-not-be-able-to-a-non-admin-user-get-list-of-all-users)
    - [Should not be able to a non existing user get list of all users](#-📌-Should-not-be-able-to-a-non-existing-user-get-list-of-all-users)
  - [Routes Tests](#-📚-Routes-Tests)

<br>

# 📔 About the challenge

In this Challenge we create an Users Management API.

The user needs to be an admin to make the list users works.

## 📚 API Routes
<br>

### 📌 POST `/users`

The route must receive `name` and `email` inside the request body to be able to create an user.

<br>

### 📌 PATCH `/users/:user_id/admin`

The route must receive, in the request params, the user `id` and exchange this user to admin.

<br>

### 📌 GET `/users/:user_id`

The route must receive, in the request params, the user `id` and return the user's info found by the response body.

<br>

### 📌 GET `/users`

The route must receive, in the request header, a properties `user_id` with the user `id` and return a list with all users created.

The `id` must be used to validate if the user who is requesting the list is an admin. The list response only must be done if the user is an admin.

<br>

# ✴️ Tests Specification 

## 📚 Model Test

<br>

### 📌 Should be able to create an user with all props

For this test, you must create a model with the properties below:
```json
{
  "id": "string",
  "name": "string",
  "admin": "boolean",
  "email": "string",
  "created_at": "Date",
  "updated_at": "Date",
}
```
The `admin` property should be started with `false` and the `id` should be automatically generated as `uuid`.

<br>

## 📚 Repository Tests
<br>

### 📌 Should be able to create new users

For this test, the `create` method of UsersRepository file needs to receive the user's name and email to create an user from the model.

<br>

### 📌 Should be able to list all users

For this test, the `list` method of UsersRepository file return a list of all created users.

<br>

### 📌 Should be able to find user by ID

For this test, the `findById` method of UsersRepository file must recieve the user `id` and return an user who has the same `id`.

<br>

### 📌 Should be able to find user by e-mail address

For this test, the `findByEmail` method of UsersRepository file must recieve the user `email` and return the user who has the same `email`.

<br>

### 📌 Should be able to turn an user as admin

For this test, the `turnAdmin` method of UsersRepository must recieve the whole user object, change the `admin` property to `true`, update the `updated_at` propety and return the updated user.

<br>

## 📚 UseCases Tests

<br>

### 📌 Should be able to create new users

For this test, the `execute` method of CreateUserUseCase file must recieve the user `name` and `email` to be created, create an user through the repository's create method and return the created user.

<br>

### 📌 Should not be able to create new users when email is already taken

For this test, the `execute` method of CreateUserUseCase file must not allow an user to be created if exist an user with the same `email`.

If exist an user with the same email retun the error message:
```tsx
throw new Error("Mensagem do erro");
```

<br>

### 📌 Should be able to turn an user as admin

For this test, the `execute` method of TurnUserAdminUseCase file must recieve the user `id`, call the repository method wich change the user to `admin` and return the user after the change.

<br>

### 📌 Should not be able to turn a non existing user as admin

For this test, the `execute` method of TurnUserAdminUseCase file must not allow an `user` who does not exist to be changed in `admin`.

If the user does not exist return the error message:
```tsx
throw new Error("Mensagem do erro");
```
<br>

### 📌 Should be able to get user profile by ID

For this test, the `execute` method of ShowUserProfileUseCase file must recieve the user `id`, call the repository's method wich search an user by `id` and return the user found.

<br>

### 📌 Should not be able to show profile of a non existing user

For this test, the `execute` method of ShowUserProfileUseCase file must not allow a non-existing user to be return.

If the user does not exist return the error message:
```tsx
throw new Error("Mensagem do erro");
```
<br>

### 📌 Should be able to list all users

For this test, the `execute` method of ListAllUsersUseCase file must recieve the user `id`, call the repository's method which return all created users and return this info.

<br>

### 📌 Should not be able to a non admin user get list of all users

For this test, the `execute` method of ListAllUsersUseCase must not allow an user who is not a `admin` acess the created users.

If the user is not an `admin`, return a message error:
```tsx
throw new Error("Mensagem do erro");
```
<br>

### 📌 Should not be able to a non existing user get list of all users

For this test, the `execute` method of ListAllUsersUse Case file must not allow an user does not exist, acess the created users list.

If the user does not exist, return a message error:
```tsx
throw new Error("Mensagem do erro");
```
<br>

## 📚 Routes Tests

<br>

## 📝 Route - [POST] /users
<br>

### 📌 Should be able to create new users

For this test, using the proper useCase, the route must create an `user` and return a status `201` with the created user object.

<br>

### 📌 Should not be able to create new users when email is already taken

For this test, if an error has occurred in useCase, return a response with status `400` and a json with an object `{ error: "error message" }`, where the value of the `error` property should be the message thrown by the error in useCase.

To catch errors thrown by other files, you can wrap the contents of the controller in a `try/catch`.

<br>

## 📝 Rota - [PATCH] /users/:user_id/admin
<br>

### 📌 Should be able to turn an user as admin

For this test, using the proper useCase, the route must change an user to `admin` and return the user changed int the response body.

<br>

### 📌 Should not be able to turn a non existing user as admin

For this test, if an error has occurred in useCase, return a response with status `404` and a json with an object `{ error: "error message" }`, where the value of the `error` property should be the message thrown by the error in useCase.

<br>

## 📝 Rota - [GET] /users/:user_id
<br>

### 📌 Should be able to get user profile by ID

For this test, using the proper useCase, the route must recieve the user `id` by route params and return the founded user object in the response body.

<br>

### 📌 Should not be able to show profile of a non existing user

For this test, if an error has occurred in useCase, return a response with status `404` and a json with an object `{ error: "error message" }`, where the value of the `error` property should be the message thrown by the error in useCase.

<br>

## 📝 Rota - [GET] /users
<br>

### 📌 Should be able to list all users

For this test, using the proper useCase, the route must recieve the `admin` user `id` from `user_id` request header and return a user list created.

<br>

### 📌 Should not be able to a non admin user get list of all users and Should not be able to a non existing user get list of all users

For these tests, if an error has occurred in useCase, return a response with status `400` and a json with an object `{ error: "error message" }`, where the value of the `error` property should be the message thrown by the error in useCase.

<br>

## 👩‍💼 Author
<img style="border-radius: 50%" src="./assets/picture.jpg" width="100px;" alt="Picture"/>
<p><b>Nádia Ligia, budding back-end developer.</b></p>
<a href="https://www.linkedin.com/in/nlnadialigia/">
  <img alt="Linkedin" src="https://img.shields.io/badge/-Linkedin -91091e?style=flat&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/nlnadialigia/" />
</a>&nbsp;
<a href="mailto:nlnadialigia@gmail.com">
  <img alt="Email" src="https://img.shields.io/badge/-Email-91091e?style=flat&logo=Gmail&logoColor=white&link=mailto:nlnadialigia@gmail.com" />
</a>&nbsp;
<a href="https://www.nlnadialigia.com">
  <img alt="Homepage" src="https://img.shields.io/badge/-Homepage-91091e" />
</a>

<br><br>

## 📝 License

This project is under de MIT licence. Look at the file [LICENSE](./LICENSE) for more information.

