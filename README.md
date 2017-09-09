# <p align="center">File storage
 
<p align="center">A simple, but extensible Python 
implementation for the File storage.

<p align="center">This project shows how you can use this API on the
example of File storage.

  * [Description.](#description)
  * [Getting started.](#getting-started)
  * [Class Register.](#class-register)
  * [Class LogIn.](#class-login)
  * [Class UsersData.](#class-usersdata)
  
## Description.

Api consists of three classes: Register, LogIn and UsersData:

- [Register class](#class-register) is responsible for user registration;
- [LogIn class](#class-login) is responsible for identifying the user in the database's database system;
- [UsersData class](#class-usersdata) is responsible for all the work with files and user directories.

## Getting started.

This API works with Python 2.7

In order to start using the API, you need to download it to your project.

```
$ git clone https://github.com/ihgorek/File-Storage-API.git
$ cd File-Storage-API
$ pip install -r requirements.txt 
```
All the necessary libraries for the API are installed.

Api works with the MongoDB database on the local computer.
You need to [install MongoDB](https://docs.mongodb.com/manual/installation/)
to your computer.
After installing the database on your computer and launching it, 
API is ready to work.

## Class Register.

Register Class is responsible for adding the user to the database and obtaining 
the necessary information about the user at the time of registration, for further 
work. In this class 4 auxiliary methods and 2 basic methods.

### Methods.
The two main methods are `add_user` and `get_user_id`.

#### Add user
The `add user` method adds a new user to the database, assigning it a unique user ID. 
If a user with this name and email exists, then this method will display an error message.

Use this method to add new user. On success, the ok is returned.

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |
| email | String | Yes | Unique email |
| password | crypt String | Yes |  crypt password |
| tracking | String | Yes | path user |

#### Get user id
The `get user id` method gives a unique user number stored in the database.
Use this method to obtain a unique user number. If such a user does not exist, the method will report this: This user does not exist.

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |


## Class LogIn.

Login class is needed to identify the user on the system and update his data. 
The class contains 6 basic methods for dabot with the user.


### Methods.
#### Login user
Use this method to verify the user in the database.

The method produces two messages:
- "ok" - if this user exists in the database
- "bad" - if this user does not exist in the database

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |

#### Get pwd
Use this method to retrieve a user password.

The method gives the user's password if such a user exists, otherwise, the error message is printed - 'bad'

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |

#### Change password
Use this method to change the user's password in the database.

The method changes the password for this user. If this user does not exist, the method will display an error message.

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |
| user_id | Integer | Yes | Unique user id |
| password | crypt String | Yes | New password user |

#### Del user
Use this method to remove a user from the database.

The method deletes the user from the database. If this user does not exist, the error message will not be displayed. The program will work as usual.

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |
| user_id | Integer | Yes | Unique user id |

#### Change Email
Use this method to change email address from the database.

The method modifies the user's email address in the database. The method requires that in the email there are such symbols as '@' and '.'

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |
| user_id | Integer | Yes | Unique user id |
| new_email | String | Yes | New user email |


## Class UsersData.

UsersData class is the main class. He does all the work with the user's files. 
Creates the necessary folders for storing files and updating them. All user files 
are stored in the directory that is in the directory variable, in the `usersdata.py` file. 
All folders for storing files are created in this directory. 
To change the directory for saving files, you need to change this variable in the `usersdata.py` file.

### Methods.
The main methods of this class are `create_dir_for_user`, `add_file`, `rename_file`, `del_file`, `find_files_in_dirs`, `create_folder`, `get_folder`, `get_dir`, `change_dir_name`, `delete_dir`, `delete_user`

#### Craete dir for user
Use this method to create a user by creating the user's root folder and adding the user to the database.

The method adds a user to the database and creates a user's root folder in the system, preparing for the user's further work with it. If successful, the motor returns `None`, otherwise it writes an exception to the console.

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |
| user_id | Integer | Yes | Unique user id |

#### Add file
Adding a file to the database and creating a directory to write it to the server.

This method implements adding a file to the database and creating directories on the server and directories for the user to store this file. Before adding the file to the database and saving it to the server, the method checks the file extension.

At the moment, you can save almost all files such as TEXT (`txt`, `doc`, `docx`, `docm`, `dotm`, `dotx`, `pdf`, `xls`, `xlsx`, `xlsm`, `xltx`, `xlt`, `xltm`, `pptx`, `ppt`, `ppsx`, `pps`, `potx`, `pot`, `ppa`, `ppam`), PICTURE (`jpg`, `jpeg`, `tif`, `tiff`, `png`, `gif`, `bmp`), SONG (`wav`, `mp3`, `wma`, `ogg`, `aac`, `flac`) and VIDEO (`avi`, `mkv`, `mp4`, `mpeg`). If a file exists for a given user path, the method overwrites the file by changing its name.

Example:
        
            words.txt
            words(1).txt
            words(2).txt
            
On the server, the file is saved in folders created using the md5 algorithm.

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |
| user_id | Integer | Yes | Unique user id |
| filename | String | Yes | User file name |
| user_dir | String | Optional | If None - > saves the file to the root folder of the user |
