Exercices MongoDB



1. Écrire la requête qui retourne tous les documents dans la collection "restaurants"

db.getCollection('restaurants').find({})

2. Retourner les champs restaurant_id, name, borough et cuisine pour tous les documents de la collection

db.getCollection('restaurants').find({},{restaurant_id:1,name:1,borough:1,cuisine:1})

3. Retourner les champs restaurant_id, name, borough et cuisine pour tous les documents de la collection, cette fois-ci, sans afficher le champs _id

db.getCollection('restaurants').find({},{_id:0,restaurant_id:1,name:1,borough:1,cuisine:1})

4. Retourner les champs restaurant_id, name, borough, cuisine et zip_code de tous les documents, sans le champs _id

db.getCollection('restaurants').find({},{_id:0,restaurant_id:1,name:1,borough:1,cuisine:1})

5. Retourner tous les restaurants qui sont dans le Bronx

db.getCollection('restaurants').find({borough:"Bronx"},{})

6. Retourner les 5 premiers restaurants qui sont dans le Bronx

db.getCollection('restaurants').find({borough:"Bronx"},{}).limit(5)

7. Retourner les 5 suivants

db.getCollection('restaurants').find({borough:"Bronx"},{}).skip(5).limit(5)

8. Retourner les restaurants avec un score supérieur à 90

db.getCollection('restaurants').find({"grades.score":{$gt:90}},{})

9. Retourner les restaurants avec un score supérieur à 80 et en-dessous de 100

db.getCollection('restaurants').find({$and:[{"grades.score":{$gt:80}},{"grades.score":{$lte:100}}]},{})

10. Retourner les restaurants situés à une latitude inférieure à -95.754168

db.getCollection('restaurants').find({"address.coord.0":{$lte:-95.754168}},{})

11. Retourner les restaurants qui (sans utiliser l'opérateur $and) :
    - Ne préparent pas de cuisine 'American'
    - Ont un score au dessus de 70
    - Une latitude inférieure à -65.754168

db.getCollection('restaurants').find({"cuisine":{$ne:"American "},"grades.score":{$gt:70},"address.coord.0":{$lte:-65.754168}},{})


12. Même requête avec l'opérateur $and

db.getCollection('restaurants').find({$and:[{"cuisine":{$ne:"American "}},{"grades.score":{$gt:70}},{"address.coord.0":{$lte:-65.754168}}]},{})

13. Retouner, ordonné par type de cuisine, les restaurants qui :
    - Ne préparent pas de cuisine 'American'
    - Ont une grade "A"
    - En dehors de "Brooklyn"

db.getCollection('restaurants').find({"cuisine":{$ne:"American "},"grades.grade":"A","borough":{$ne:"Brooklyn"}},{}).sort({ cuisine: 1})

14. Retourner l'id, le nom, le quartier et la cuisine des resraurants dont le nom commence par "Wil"

db.getCollection('restaurants').find({name: /^Wil/},{_id:0,restaurant_id:1,name:1,borough:1,cuisine:1})

15. Retourner l'id, le nom, le quartier et la cuisine des resraurants dont le nom termine par "ces"

db.getCollection('restaurants').find({name: /ces$/},{_id:0,restaurant_id:1,name:1,borough:1,cuisine:1})

16. Retourner l'id, le nom, le quartier et la cuisine des resraurants dont le nom contient "Reg"

db.getCollection('restaurants').find({name: /Reg/},{_id:0,restaurant_id:1,name:1,borough:1,cuisine:1})

17. Retourner les restaurants du Bronx qui servent de la cuisine américaine ou chinoise

db.getCollection('restaurants').find({$or:[
                                          {$and:[{"cuisine":"American "},{"borough":"Bronx"}]},
                                          {$and:[{"cuisine":"Chinese"},{"borough":"Bronx"}]}
                                        ]
                                    },{})

18. Retourner l'id, le nom, le quartier et la cuisine qui ne se situent à Staten Island ou à Brooklyn ou dans le Bronx

db.getCollection('restaurants').find({$or:[
                                          {"borough":"Staten Island"},
                                          {"borough":"Brooklyn"},
                                          {"borough":"Bronx"}
                                        ]
                                    },{_id:0,restaurant_id:1,name:1,borough:1,cuisine:1})

19. Retourner l'id, le nom, le quartier et la cuisine qui ne se situent ni à Staten Island, ni à Brooklyn et ni dans le Bronx

db.getCollection('restaurants').find({$and:[
                                          {"borough":{$ne:"Staten Island"}},
                                          {"borough":{$ne:"Brooklyn"}},
                                          {"borough":{$ne:"Bronx"}}
                                        ]
                                    },{_id:0,restaurant_id:1,name:1,borough:1,cuisine:1})

20. Retourner l'id, le nom, le quartier et la cuisine des resraurants avec un score inférieur à 10

db.getCollection('restaurants').find({"grades.score":{$lt:10}},{_id:0,restaurant_id:1,name:1,borough:1,cuisine:1})

21. Retourner l'id, le nom, le quartier et la cuisine des resraurants qui ne sont ni Chinois ou Américain; ou bien dont le nom commence par "Wil"

db.getCollection('restaurants').find({$and:[
                                          {$or:[{"cuisine":{$ne:"American "}},{"name": /^Wil/}]},
                                          {$or:[{"cuisine":{$ne:"Chinese"}},{"name": /^Wil/}]}
                                        ]
                                    },{_id:0,restaurant_id:1,name:1,borough:1,cuisine:1})

22. Retourner l'id, le nom et les grades des restaurants possédant une grade avec les valeurs:
    - Une grade "A"
    - Un score 11 s
    - "2014-08-11T00:00:00Z"

db.getCollection('restaurants').find({$and:[{"grades.grade":"A"},{"grades.score":11},{"grades.date": new Date("2014-08-11T00:00:00Z")}]},{_id:0,restaurant_id:1,name:1,grades:1})

23. Retourner l'id, le nom et les grades des restaurants dont 2eme élément de grades possède:
    - Une grade "A"
    - Un score 9
    - Une ISODate "2014-08-11T00:00:00Z"

db.getCollection('restaurants').find({$and:[{"grades.1.grade":"A"},{"grades.1.score":9},{"grades.1.date": new Date(ISODate("2014-08-11T00:00:00Z"))}]},{_id:0,restaurant_id:1,name:1,grades:1})

24. Retourner l'id, le nom et la position géographique dont le deuxième élément des coordonnées géographiques contient une valeur entre 42 et 52

db.getCollection('restaurants').find({$and:[
                                          {"address.coord.1":{$gt:42}},
                                          {"address.coord.1":{$lt:52}}
                                        ]
                                    },{_id:0,restaurant_id:1,name:1,"address.coord":1})

25. Ajoute tes 5 restaurants préférés en remplissant pour chacun :
    - Une adresse complète
    - Un quartier
    - Un type de cuisine
    - 3 notes au minimum
    - Un nom
    - Un id de restaurant (Pas l'_id mongo !)

db.getCollection('restaurants').insert({address:{building:"11",coord:[-73.11111,40.11111],street:"1st Avenue",zipcode:"11111"},
                                        borough:"Bronx",
                                        cuisine:"Japanese",
                                        grades:[
                                                {date: new Date("2019-10-28T00:00:00Z"),grade:"A",score:12},
                                                {date: new Date("2019-10-28T00:00:00Z"),grade:"B",score:9},
                                                {date: new Date("2019-10-28T00:00:00Z"),grade:"C",score:7}
                                              ],
                                        name: "Sushi shop",
                                        restaurant_id: "11111111"
                                      },
                                      {address:{building:"22",coord:[-73.22222,40.22222],street:"2nd Avenue",zipcode:"22222"},
                                        borough:"Long Island",
                                        cuisine:"French",
                                        grades:[
                                                {date: new Date("2019-10-28T00:00:00Z"),grade:"B",score:10},
                                                {date: new Date("2019-10-28T00:00:00Z"),grade:"B",score:11},
                                                {date: new Date("2019-10-28T00:00:00Z"),grade:"A",score:18}
                                              ],
                                        name: "Chez Amelie",
                                        restaurant_id: "22222222"
                                      },
                                      {address:{building:"33",coord:[-73.33333,40.33333],street:"3rd Avenue",zipcode:"33333"},
                                        borough:"Manhattan",
                                        cuisine:"Italian",
                                        grades:[
                                                {date: new Date("2019-10-28T00:00:00Z"),grade:"A",score:25},
                                                {date: new Date("2019-10-28T00:00:00Z"),grade:"A",score:15},
                                                {date: new Date("2019-10-28T00:00:00Z"),grade:"A",score:10}
                                              ],
                                        name: "Tutti frutti",
                                        restaurant_id: "33333333"
                                      },
                                      {address:{building:"44",coord:[-73.44444,40.44444],street:"4th Avenue",zipcode:"44444"},
                                        borough:"Brooklyn",
                                        cuisine:"Mexican",
                                        grades:[
                                                {date: new Date("2019-10-28T00:00:00Z"),grade:"A",score:16},
                                                {date: new Date("2019-10-28T00:00:00Z"),grade:"B",score:11},
                                                {date: new Date("2019-10-28T00:00:00Z"),grade:"A",score:21}
                                              ],
                                        name: "Salsa heaven",
                                        restaurant_id: "44444444"
                                      },
                                      {address:{building:"55",coord:[-73.55555,40.55555],street:"5th Avenue",zipcode:"55555"},
                                        borough:"Chinatown",
                                        cuisine:"Donuts",
                                        grades:[
                                                {date: new Date("2019-10-28T00:00:00Z"),grade:"B",score:8},
                                                {date: new Date("2019-10-28T00:00:00Z"),grade:"B",score:17},
                                                {date: new Date("2019-10-28T00:00:00Z"),grade:"A",score:28}
                                              ],
                                        name: "Donuts brothers",
                                        restaurant_id: "5555555"
                                      },
                                )

26. Ajoute 2 notes à chacun de ces restaurants
27. Supprime de la base les restaurants de Staten Island
28. Transfert tous les restaurants du Manhattan à Brooklyn (Pour info, appelle ça la gentrification)
29. Retourne la liste de tous les quartiers de la collection (Si tu as encore des restaurants dans Manhattan, retourne à la question 28 )
