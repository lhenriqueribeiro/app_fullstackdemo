# app_fullstackdemo .NetCore DDD/SOLID + Angular 8.2 Material + React Native MobileApp.
* Note: This Documentation is also available in Portuguese. Scrool down for it.
* Nota: Essa documentação está também disponível em Português, role pra baixo para acessar.

* Note 2: I've also recorded some Vídeos (Youtube tutorials) that shows how to RUN this app, how to prepare
your envoirnment, and also explaining how this Architecture was developed. Links Below.

* Note 3: We have this system published ONLINE, you can access and test it on a URL without installing or
set-up Dev-envoirnment. Scrool down for URLs.

------------------------------------------------------------------------------------------------------------
.NET Core BackEnd (With Rich Arquitecture) DDD/SOLID/CQRS + WebApi.
Web-Panel using Angular 8.2 Version with Material with Rich Arquitecture.
Mobile App using React-Native.

### More Details about this Architecture you can find going on this doc...
------------------------------------------------------------------------------------------------------------

## Business Logic:

How it works: WebPanel (Angular) and MobileApp (React) will have a Login-Screen, that will communicate with
the backend, to login and Store the Token (JWT) with the Claims. Once Logged:

**MobileApp** can "register" the Device on backend, registering the Manufacturer (Motorola, LG, Samsung, Xiaomi),
Model (S7, S8, S9, RedMi9, RedMi10), IMEI number and some other information. MobileApp will have a cool screen
to show some important informations from Device - once registered, will store the ID taken from backend. You
could use your Real Device or also an Emulator (like Android Studio or Genymotion) to test it. Once it's React
Native, you can also work to compile it to iOS and iPhone.

**FrontEnd** will also Login and get the Token (JWT with Claims). On Panel you will have a DashBoard (showing 
graphics with Number of Devices per AndroidVersion, and Number of Devices per Manufacturer). Users logged on
Panel will be allowed to create Another Users that can also Login into Panel and MobileApp. So the Users
Screen will comes with a "CRUD" function to List, Create, Edit and Delete Users.

On UserScreen (List) will be a button to LIST all the Devices for that user. So when you Login in a Mobile
Device, so once user Login in MobileApp and Register the Device, it will be available with Details on Panel.
Angular Panel is also ready to work with the Token, with a Interceptor Layer to Deal with 401/403 codes,
show good messages, alerts, ballon messages, modals and a lot of cool things with a nice Material-Interface.

**BackEnd** will manage Automatically the Manufacturers > Models of devices. So new Manufacturers and new models
will be generate by the BackEnd, attaching the Device to the Right "relationship". So basically: A Device will
belong to a Model, and a Model will belong to a Manufacturer. One Manufacturer has N Models, One Model has
N devices. This relationships will be generated on Entities, and also, replicated by EF on Database.

The Screen on Panel to Manage (CRUD) this Manufacturers > Models will also be Available. So we have at least
3 Cruds: Users, Manufacturers and Models. And more + Screen for Devices (List and Details) - also available.

**Under the hood**: The BackEnd .NET Core with RichArchitecture will be running providing all this data for both apps.

:+1: (Note: Add some PrintScreens of App Here) :shipit: (ALSO CREATE A DIAGRAM EXPLAINING IT)

### License and USE of this App in a RealWorld:
Note: This App is FREE and FULL OpenSource. You can Use it as a base for your system, or you can also colaborate
with me to improve it. In a REAL-WORLD, this App needs to be better thinked:

Users should belong to a Company (or even better - User should belong to a Real-Entity like Employee or something),
Claims should have Profiles (like Master, Admin...) where the Claims will be connected (not right to the user). We
also need a screen to manage the CRUD of the Claims (that we don't have on this app). Create category for the Devices:

We also need to implement things like RefreshToken Logic, WelcomeEmail, Register Page on Panel, Recover Password
and go on and on - lot of other things to use this app in a Real-scenario. We need to adapt lot of things to a 
REAL-WORLD-Scenario of Real-Business needs Logic.

But for now: Remember that this app is a "demo" of Programming, Architecture and Techinical Skills - NOT a demo of
Real-World App. So we will keep the business-stuff simple to Focus on Techinical stuff. Anyway, you can use it as a
BASE of a Architecture, and start your own system under it, following the patterns already implemented on it. You can
use it as a "skeleton" for your next Real-Software. Good luck :cake:

**Note about the CLAIMS**: System comes with a Claim Table and have 5 base claims: dashboard, manufacturer, devicemodel,
user and equipment. The "right" way to implement it should be granulated (user.list, user.create, user.edit) and
the system needs a Screen to Edit the Claims, and a way to "link" the User to the Claims. In my personal opinion
system should have "Profiles" (like Master, Admin, Users...) and user will receive claims based on a Profile.

Anyway, as we describe, this system is not a Sample of Business rules. You should improve it according to your needs.
So basically when a User is created, on the "UserHandler" the claims (all of them) will be gave to the User, and it
will have all accesses. Anyway, if you want to test a "forbidden" and Angular Interceptor, you can delete it from
"UserClaim" table (that links Claims to the Users). Than just logout (to delete token) and go on...

------------------------------------------------------------------------------------------------------------

## BackEnd:

### .NET Core 3.1 C# + EF Core (SQLServer). Rich Architecture DDD/SOLID using:

Rich Modeling (Models-Entities, Enums, ValueObjects) (read below for the Business Logic)

Api REST + Handlers to Deal with the Requests + DI

JWT Token to Auth Parts + Claims + JSON to Data

CQRS to Receive Queries and Comands and Return Results

Handler Layer (you can also call it as "Service") to "orchestrate" the requests

Repositories Layer + Unit of Work + 3 CRUDS (EF Code First)

Validation by Contracts

Pattern (BaseCommandResult) for the Returns of the API on a Well-defined type

Shared Project (classlib) for Field Formaters, Validations, Cryptografy

Unit-Tests for Commands, Queries, Repositories, Entities and Handlers

* Note: DataBase can be Easily replaced (to Postgres, MySQL) once layers are very well separated.

## FrontEnd:

### Angular 8 + Angular Material Panel + Login + Auth + 3 Full-CRUDS:

Complete Panel to Login + DashBoard + 3 Entire CRUDS (read below for the Business Logic)

Nice Interface using Angular Material, Modals, MatTable, Chartlist and more...

CQRS Models and Interfaces based on BackEnd (Queries, Commands and Results)

Layer for the Services and API Communication - Capable to Catch Results and Display Messages (and backend-errors)
without programming separated code to catch messages for each service/screen (httpinterceptor).

Separated Modules and Rotes Files for better Organization.

Shared Services for Dialogs, Notification Messages, Modal Screens, Enum Description.

Capability to catch BaseCommandResult and show good message or array of errors from BackEnd.

Auth Guard / Auth Interceptor to Deal Perfectly with the Tokens, Authentication, Headers (401/403).

## Mobile:

### React-Native + Device-Info:

Login Screen that Will Communicate with the BackEnd for Auth and Store the JWT.

DashBoard to Show the Device Basic Information about the Device (Brand, Model, Android Version, Device Id):
DashBoard will also add the Device to the BackEnd, so the Panel will display a List of Devices per Users.

------------------------------------------------------------------------------------------------------------

## How to RUN it and Technical Information:

- You can Develop and Run it on Windows, Linux and MacOs.
In My Machine: I've Used Linux Ubuntu 18.04 and VS Code as Code-Editor. In My Repository there's a project
called **"docsamples"** and inside it **"generaldocs"**. I use it as my own-manual to configure my envoirment, so
inside "vscode" you'll find witch EXTENSIONS i use, witch FONTS and also my "settings.json". There are other
files and folders on "generaldocs" for my Angular Env, my React-Native, .Net Core, GitHub with the main
commands i use and a lot of other useful informations.

I also use "Insomnia" to TEST API, but you can use Postman or if you prefer, install some integrated tool
like Swagger. I also use "Azure Data Studio" to check the DataBase in case of need. Note: I've also tested
all this APP and Envoirment using Windows 10 and it also works perfect, also in VS Community 2019. Basically
chooose your favorite :trollface:

### Tutorial vídeos on Youtube:
(1) How to Prepare your Envoirment and Machine: 
(2) How to RUN this App and How it Works:
(3) Technical Explanation - understanding what's under the Hood:


### User to Access the App:
During the Migration of the API will be created an User with a Devices (Xiaomi Mi Max 2) just for test, you can use
this user to login and create another users, or also to test the system. If you don't want it, comment the method-
call on the Context.

Login: admin
Password: admin

If you just want to **TEST** this system as a USER, without setting (or having) an envoirnment, we published it
**ONLINE**. This system is published and ONLINE for test with the same user account below. You can test the Panel,
and you can also test the APK file by installing it on your own Mobile or even an Emulator. Feel free at:

www.futuradata.com.br/appfullstackdemo/panel (login on panel to see AngularApp)
www.futuradata.com.br/appfullstackdemo.apk (you can download an run on your device)
www.futuradata.com.br/appfullstackdemo/backend (you can use Insomnia to test the API)


## How to RUN it OUT of the Docker Containner (100% on local operational system):

## (1) BackEnd:
**Note**: SQLServer Connection string for the BackEnd is on "BackEnd>AppFullStackDemo.Api>appsettins.json", so please
set-up your SQL Connection Server info before try to RUN the APP.

## How to RUN it with the Docker-Compose integrated Envoirnment:
Note: Need to be done on Future. Once i don't know (even if it's possible) to encapsulate inside a Containner the
"React Native" (Mobile) part. Once app needs to Run on Machine (to access the Device and install the APK), i don't
know how to make it runs inside a docker and make it automatically. Maybe it's possible to run "npm start" and 
"react-native run-android" inside the docker containner and install on local mobile. Well, to be checked...