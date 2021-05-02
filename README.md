# [WIP] Tentative de reconstruction de la doc  de l'API Chronos



Ce document a pour objectif de documenter l'api de chronos disponible a l'adresse suivante: 

```
https://v2ssl.webservices.chronos.epita.net/api
```



# Requetes

### Headers

Il faut renseigner les 2 champs suivant:

"accept": "*/*"

"auth-token": votre token (jvai pas vous donner le mien bande de fous)



**Liste des différentes requêtes qui peuvent être faites pour utiliser l'API Chronos**

### Get groups

```
https://v2ssl.webservices.chronos.epita.net/api/v2/Group/GetGroups
```

#### renvoie

```json
[
    {
        "Groups": [
            {
                "Groups": [
                    {
                        "Groups": [
                            {
                                "Groups": null,
                                "Id": 408,
                                "Name": "Computer Security [FP]",
                                "ParentId": 384,
                                "Type": 1
                            },
                            {
                                "Groups": null,
                                "Id": 417,
                                "Name": "Computer Security [SP]",
                                "ParentId": 384,
                                "Type": 1
                            },
                            {
                                "Groups": null,
                                "Id": 477,
                                "Name": "IS Management [FP]",
                                "ParentId": 384,
                                "Type": 1
                            },
```

Renvoie une array d'objet Groups avec les champs suivants:

```json
"Groups": une liste de groupes qui sont inclus dans ce sous groupe (le groupe de s3d2 est inclus dans le sous groupe par ex)
"Id": ID unique du groupe, utile pour faire la requete qui permettra d avoir l emploi du temps du groupe associé
"Name": String pour le nom du groupe
"ParentId": ID du groupe parent
"Type": toujours à 1, son role reste à determiner
```

### Get rooms

```
https://v2ssl.webservices.chronos.epita.net/api/v2/Room/GetRooms
```

#### Renvoie

```json
[
    {
        "Id": 66,
        "Name": "ETNA",
        "ParentId": -1,
        "Rooms": [
            {
                "Id": 67,
                "Name": "amphi/ETNA",
                "ParentId": 66,
                "Rooms": null,
                "Type": 3
            },
            {
                "Id": 68,
                "Name": "salle machine/ETNA",
                "ParentId": 66,
                "Rooms": null,
                "Type": 3
            },
            {
                "Id": 69,
                "Name": "salle 1/ETNA",
                "ParentId": 66,
                "Rooms": null,
                "Type": 3
            },
            {
                "Id": 70,
                "Name": "salle 2/ETNA",
                "ParentId": 66,
                "Rooms": null,
                "Type": 3
            }
        ],
        "Type": 3
    }
]
```

Renvoie une array d'objet Rooms avec les champs suivants:

```json
"Id": ID unique
"Name"
"ParentID": ID du room parent, -1 si pas la
"Rooms": array de rooms descendantes de la room
"Type": toujours set a 3, utilité non déterminée
```

### Get Staff

```
https://v2ssl.webservices.chronos.epita.net/api/v2/Staff/GetStaff
```

#### Renvoie

````Json
[
    {
        "Id": 481,
        "Name": "ACU",
        "ParentId": 0,
        "Type": 2
    }
]
````

Avec un Id unique, un nom, un ParentId qui est logiquement toujours nul et un type qui vaut 2

### Get Week

Requête tres intéressante qui permet d'avoir une liste des cours a partir d'une ID et d'un numero de semaine

```
https://v2ssl.webservices.chronos.epita.net/api/v2/Week/GetWeek/<WEEK>/<ID>/1
```

##### Avec

- **WEEK**: numéro de semaine
- **ID**: ID du groupe auquel on veut avoir l'emploi du temps

#### Renvoie

```json
{
    "DayList": [
        {
            "CourseList": [
                {
                    "BeginDate": "2021-05-11T12:00:00Z",
                    "Code": null,
                    "Duration": 60,
                    "EndDate": "2021-05-11T13:00:00Z",
                    "GroupList": [
                        {
                            "Groups": null,
                            "Id": 1397,
                            "Name": "INFOS2A2-2",
                            "ParentId": 0,
                            "Type": 1
                        }
                    ],
                    "Id": 20782,
                    "Info": "",
                    "Name": "TIM",
                    "RoomList": [
                        {
                            "Id": 107,
                            "Name": "VB 13",
                            "ParentId": 0,
                            "Rooms": null,
                            "Type": 3
                        }
                    ],
                    "StaffList": [
                        {
                            "Id": 265,
                            "Name": "Frank Steve",
                            "ParentId": 0,
                            "Type": 2
                        }
                    ],
                    "Type": null,
                    "Url": null
                },
```

##### Avec:

- **Daylist**: Une liste avec un array par jour (je crois)
  - **ID**: numero de semaine
- **CourseList**: Une liste de cours
- **BeginDate** et **EndDate**: date et heures du cours
- **Duration**: en minute
- **GroupList**: Array de groupes qui participent à la séance
- **RoomList**: Array de rooms dans laquelle il y a classe
- **StaffList**: Array de profs qui donnent le cours
- **Type** et **Url**: Toujours set à nul à ma connaissance

### Get Current Week

Pareil que **Get Week** mais sans préciser la semaine

```
https://v2ssl.webservices.chronos.epita.net/api/v2/Week/GetCurrentWeek/1290/1
```



