# <p align="center">File storage API

<p align="center">This project shows File storage API.

  * [Description.](#description)
  * [Getting started.](#getting-started)
  * [Class Register.](#class-register)
      * [Register Methods.](#register-methods)
          * [Add user](#add-user)
          * [Get User id](#get-user-id)
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

### Register Methods.
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

The method returns a dictionary of the form 
```
{
    filename: filename, 
    file_dir: file dir in system
}
```
Where *filename* is the file name in the database, and *file dir in system* is the directory where the file is located for further download.

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |
| user_id | Integer | Yes | Unique user id |
| filename | String | Yes | User file name |
| user_dir | String | Optional | If None - > saves the file to the root folder of the user |

 #### Reaname file
 
 Use this method to change the filename.
 
This method implements the renaming of the file in the database and in the system along the way from the database.

This method for successful execution returns `None`, otherwise the error message.    

 
| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |
| user_id | Integer | Yes | Unique user id |
| user_dir | String | Yes | User directory in which he will save the file |
| old_filename | String | Yes | The name of the old file |
| new_filename | String | Yes | New filename |

**Important.** In the method, the filename is supplied with an extension and, if the extensions do not coincide the file to be modified, and the proposed file, the method will return an error message: 

"You can not change the extension file * to an extension *"

#### Del file
Use this method to delete a file from the database and the system.
 
Delete a file from the database and the system. The path to the file is stored in the database.

On successful execution, the method returns None, if the method did not find the file in this directory, an error message will be displayed.

"There is no such file in this directory"

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |
| user_id | Integer | Yes | Unique user id |
| filename | String | Yes | Filename |
| user_dir | String | Yes | User directory in which he will save the file |

#### Find files in dirs
Search all files in this directory.

Search for a file by directory, checking whether it's the user with using two identifiers username and user_id displays a file and its location, for downloading.

The method returns a dictionary of the form
```
{ 
    filename: filename, 
    file_path : file path in system 
}
```
Where *filename* is the file name in the database, and *file dir in system* is the directory where the file is located for further download.

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |
| user_id | Integer | Yes | Unique user id |
| user_dir | String | Yes | The user directory in which he wants to see the files |

#### Create folder
This method is used to create a new folder for the user.

Creates a folder for the user in which you can store data. This method is also creates dependencies between the rest of the folders, creating a "tree".

If it works correctly, the method returns None, if such a folder already exists in this directory, then the method returns an error message:

"This folder exist exist"

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |
| user_id | Integer | Yes | Unique user id |
| new_folred | String | Yes | Name new folder |

#### Get folder
Use this method to get all the folders in this directory.

Getting all folders with directories that are relative to the directory in which the user is located. You need to enter the full directory of the user's location and then the method will produce the following. Possible files with directories for the dictionary to go deep.

The method returns a dictionary of the form
```
{
    name folder: folder path
}
```
Where *name folder* is the name of the folder in this directory, and *folder path* is the path to this folder for the user.

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |
| user_id | Integer | Yes | Unique user id |
| user_dir | String | Yes | Directory in which the user wants to receive folders |

#### Get dir
Use this method to retrieve all the parent directories.

This method implements the submission of directories to the user in the format of the ordered dict The input is given the username of its unique number and the path to which it wants to get. The method checks whether there is such a path in the database and all parents with references to them, for further transfer to the user.

The method returns an OrderedDict of the form
```
{
    name directory: the path of this directory
}
```
Where *the path of this directory* is the path to each user's parent directory.

If the specified directory does not exist, the user receives an error message:

"There is no such directory"

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |
| user_id | Integer | Yes | Unique user id |
| pathway | String | Yes | The way to which the user wants to come |

#### Change dir name
Use this method to change the directory name.

You can change all directories except the parent "username". The new directory name replaces the old one in the database everywhere and gives `None` if all the actions are successful. 

To change the name you need all the directories in which there is this directory and their replacement the name of the new user created by the user.

If the directory does not exist, the method will return an error message:

"Directory with this name does not exist"

If the user tries to change the feed folder, then he will receive an error message:

"This directory can not be modified"

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |
| user_id | Integer | Yes | Unique user id |
| old_user_dir | String | Yes | The name of the directory you want to change |
| new_user_dir | String | Yes | New name directory |

#### Delete dir
Use this method to delete a directory.

Deleting a directory from the main cell and, if there are files lying in this directory, then deleting them from the database and the system. 

The method returns None, if the selected folder does not exist, the method returns an error message.

"This folder does not exist"

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |
| user_id | Integer | Yes | Unique user id |
| name_dir | String | Yes | The name of the directory you want to delete |

#### Delete user
The name of the directory you want to delete.

The name of the directory you want to delete.

The method returns the value None, if the selected user does not exist, then returns an error message.

| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| username | Integer or String | Yes | Unique username |
| user_id | Integer | Yes | Unique user id |
