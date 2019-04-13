```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-gwiznn@email.com",
    "username": "author-gwiznn",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-gwiznn@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1nd2l6bm4iLCJpYXQiOjE1NTUxODYwMDYsImV4cCI6MTU1NTM1ODgwNn0.TO5unCFaIBk-IQBuILAfhQNi9aZfvdSc0Li9uPj_xMk",
    "username": "author-gwiznn",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-n7kdsf@email.com",
    "username": "authoress-n7kdsf",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-n7kdsf@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy1uN2tkc2YiLCJpYXQiOjE1NTUxODYwMDYsImV4cCI6MTU1NTM1ODgwNn0.b1oMCbzjPXgnHYTMc13IROZd3KPjnD9T46O7XMVbGVw",
    "username": "authoress-n7kdsf",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-dfofnp@email.com",
    "username": "non-author-dfofnp",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-dfofnp@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3ItZGZvZm5wIiwiaWF0IjoxNTU1MTg2MDA2LCJleHAiOjE1NTUzNTg4MDZ9.YTYqQYOp1bqlhPgTfPSoP6mBLGurQQJ-_K-0W2c4DZU",
    "username": "non-author-dfofnp",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ew3nf3",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186006239,
    "updatedAt": 1555186006239,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-o18p7u",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186006293,
    "updatedAt": 1555186006293,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-ew3nf3
```
```
200 OK

{
  "article": {
    "createdAt": 1555186006239,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-ew3nf3",
    "updatedAt": 1555186006239,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-o18p7u
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1555186006293,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-o18p7u",
    "updatedAt": 1555186006293,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/wi4tod
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [wi4tod]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-o18p7u

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1555186006293,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-o18p7u",
    "updatedAt": 1555186006293,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-o18p7u

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1555186006293,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-o18p7u",
    "updatedAt": 1555186006293,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-o18p7u

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1555186006293,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-o18p7u",
    "updatedAt": 1555186006293,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-o18p7u

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title-o18p7u

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title-o18p7u

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title-o18p7u

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title-o18p7u]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-o18p7u

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-gwiznn]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-ew3nf3/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1555186006239,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-ew3nf3",
    "updatedAt": 1555186006239,
    "favoritedBy": [
      "non-author-dfofnp"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-ew3nf3
```
```
200 OK

{
  "article": {
    "createdAt": 1555186006239,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-ew3nf3",
    "updatedAt": 1555186006239,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-ew3nf3/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-ew3nf3_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-ew3nf3_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-ew3nf3/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1555186006239,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-ew3nf3",
    "updatedAt": 1555186006239,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-ew3nf3
```
```
200 OK

{}
```
```
GET /articles/title-ew3nf3
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-ew3nf3]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title-o18p7u
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-gwiznn]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "g8z45q",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-7s26pp",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186007456,
    "updatedAt": 1555186007456,
    "author": {
      "username": "authoress-n7kdsf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "g8z45q",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "130mk5",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-12f8e8",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186007494,
    "updatedAt": 1555186007494,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "130mk5",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "cyjbwn",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-yk7dye",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186007530,
    "updatedAt": 1555186007530,
    "author": {
      "username": "authoress-n7kdsf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "cyjbwn",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "f7185g",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-iu4az0",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186007571,
    "updatedAt": 1555186007571,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "f7185g",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "7iponm",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-fwh47t",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186007608,
    "updatedAt": 1555186007608,
    "author": {
      "username": "authoress-n7kdsf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "7iponm",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "d9sl3g",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ea1ojd",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186007646,
    "updatedAt": 1555186007646,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "d9sl3g",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "8uoag2",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-wmj73l",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186007690,
    "updatedAt": 1555186007690,
    "author": {
      "username": "authoress-n7kdsf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "8uoag2",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "vetwrq",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-p0n75l",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186007728,
    "updatedAt": 1555186007728,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "vetwrq",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "xf8qyd",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ye0p3b",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186007764,
    "updatedAt": 1555186007764,
    "author": {
      "username": "authoress-n7kdsf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "xf8qyd",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "c7xg4j",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-69a4nc",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186007801,
    "updatedAt": 1555186007801,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "c7xg4j",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "4lniyj",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-2cuzd7",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186007860,
    "updatedAt": 1555186007860,
    "author": {
      "username": "authoress-n7kdsf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "4lniyj",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "daoj8g",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-myftie",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186007898,
    "updatedAt": 1555186007898,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "daoj8g",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "r7edge",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ondol0",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186007939,
    "updatedAt": 1555186007939,
    "author": {
      "username": "authoress-n7kdsf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "r7edge",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "fhvxa5",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-426x4d",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186007970,
    "updatedAt": 1555186007970,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "fhvxa5",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tnoo7m",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-mrag2b",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186008001,
    "updatedAt": 1555186008001,
    "author": {
      "username": "authoress-n7kdsf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tnoo7m",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "19t0i3",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-qr8lwe",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186008040,
    "updatedAt": 1555186008040,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "19t0i3",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "k2gjm0",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-513gi",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186008069,
    "updatedAt": 1555186008069,
    "author": {
      "username": "authoress-n7kdsf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "k2gjm0",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "zij7dk",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-942i6j",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186008108,
    "updatedAt": 1555186008108,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "zij7dk",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "qufbl",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-kzroal",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186008136,
    "updatedAt": 1555186008136,
    "author": {
      "username": "authoress-n7kdsf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "qufbl",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "rxubbf",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-e4eup3",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186008178,
    "updatedAt": 1555186008178,
    "author": {
      "username": "author-gwiznn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "rxubbf",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "rxubbf",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186008178,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-e4eup3",
      "updatedAt": 1555186008178,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qufbl",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186008136,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kzroal",
      "updatedAt": 1555186008136,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "zij7dk"
      ],
      "createdAt": 1555186008108,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-942i6j",
      "updatedAt": 1555186008108,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "k2gjm0",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186008069,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-513gi",
      "updatedAt": 1555186008069,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "19t0i3",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186008040,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qr8lwe",
      "updatedAt": 1555186008040,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "tnoo7m"
      ],
      "createdAt": 1555186008001,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mrag2b",
      "updatedAt": 1555186008001,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fhvxa5",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186007970,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-426x4d",
      "updatedAt": 1555186007970,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r7edge",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007939,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ondol0",
      "updatedAt": 1555186007939,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "daoj8g",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1555186007898,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-myftie",
      "updatedAt": 1555186007898,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4lniyj",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186007860,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2cuzd7",
      "updatedAt": 1555186007860,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c7xg4j",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007801,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-69a4nc",
      "updatedAt": 1555186007801,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "xf8qyd"
      ],
      "createdAt": 1555186007764,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ye0p3b",
      "updatedAt": 1555186007764,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "vetwrq"
      ],
      "createdAt": 1555186007728,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p0n75l",
      "updatedAt": 1555186007728,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8uoag2",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007690,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wmj73l",
      "updatedAt": 1555186007690,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "d9sl3g",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1555186007646,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ea1ojd",
      "updatedAt": 1555186007646,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7iponm",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186007608,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fwh47t",
      "updatedAt": 1555186007608,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "f7185g",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007571,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-iu4az0",
      "updatedAt": 1555186007571,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cyjbwn",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1555186007530,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yk7dye",
      "updatedAt": 1555186007530,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "130mk5",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186007494,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-12f8e8",
      "updatedAt": 1555186007494,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g8z45q",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007456,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7s26pp",
      "updatedAt": 1555186007456,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "vetwrq"
      ],
      "createdAt": 1555186007728,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p0n75l",
      "updatedAt": 1555186007728,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "zij7dk"
      ],
      "createdAt": 1555186008108,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-942i6j",
      "updatedAt": 1555186008108,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "tnoo7m"
      ],
      "createdAt": 1555186008001,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mrag2b",
      "updatedAt": 1555186008001,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "daoj8g",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1555186007898,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-myftie",
      "updatedAt": 1555186007898,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "xf8qyd"
      ],
      "createdAt": 1555186007764,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ye0p3b",
      "updatedAt": 1555186007764,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "d9sl3g",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1555186007646,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ea1ojd",
      "updatedAt": 1555186007646,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cyjbwn",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1555186007530,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yk7dye",
      "updatedAt": 1555186007530,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-n7kdsf
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "qufbl",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186008136,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kzroal",
      "updatedAt": 1555186008136,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "k2gjm0",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186008069,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-513gi",
      "updatedAt": 1555186008069,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "tnoo7m"
      ],
      "createdAt": 1555186008001,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mrag2b",
      "updatedAt": 1555186008001,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r7edge",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007939,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ondol0",
      "updatedAt": 1555186007939,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4lniyj",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186007860,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2cuzd7",
      "updatedAt": 1555186007860,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "xf8qyd"
      ],
      "createdAt": 1555186007764,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ye0p3b",
      "updatedAt": 1555186007764,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8uoag2",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007690,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wmj73l",
      "updatedAt": 1555186007690,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7iponm",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186007608,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fwh47t",
      "updatedAt": 1555186007608,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cyjbwn",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1555186007530,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yk7dye",
      "updatedAt": 1555186007530,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g8z45q",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007456,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7s26pp",
      "updatedAt": 1555186007456,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-dfofnp
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-gwiznn&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "rxubbf",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186008178,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-e4eup3",
      "updatedAt": 1555186008178,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "zij7dk"
      ],
      "createdAt": 1555186008108,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-942i6j",
      "updatedAt": 1555186008108,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-gwiznn&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "19t0i3",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186008040,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qr8lwe",
      "updatedAt": 1555186008040,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fhvxa5",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186007970,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-426x4d",
      "updatedAt": 1555186007970,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "rxubbf",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186008178,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-e4eup3",
      "updatedAt": 1555186008178,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qufbl",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186008136,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kzroal",
      "updatedAt": 1555186008136,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "zij7dk"
      ],
      "createdAt": 1555186008108,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-942i6j",
      "updatedAt": 1555186008108,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "k2gjm0",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186008069,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-513gi",
      "updatedAt": 1555186008069,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "19t0i3",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186008040,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qr8lwe",
      "updatedAt": 1555186008040,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "tnoo7m"
      ],
      "createdAt": 1555186008001,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mrag2b",
      "updatedAt": 1555186008001,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fhvxa5",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186007970,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-426x4d",
      "updatedAt": 1555186007970,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r7edge",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007939,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ondol0",
      "updatedAt": 1555186007939,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "daoj8g",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1555186007898,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-myftie",
      "updatedAt": 1555186007898,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4lniyj",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186007860,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2cuzd7",
      "updatedAt": 1555186007860,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c7xg4j",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007801,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-69a4nc",
      "updatedAt": 1555186007801,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "xf8qyd"
      ],
      "createdAt": 1555186007764,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ye0p3b",
      "updatedAt": 1555186007764,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "vetwrq"
      ],
      "createdAt": 1555186007728,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p0n75l",
      "updatedAt": 1555186007728,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8uoag2",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007690,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wmj73l",
      "updatedAt": 1555186007690,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "d9sl3g",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1555186007646,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ea1ojd",
      "updatedAt": 1555186007646,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7iponm",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186007608,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fwh47t",
      "updatedAt": 1555186007608,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "f7185g",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007571,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-iu4az0",
      "updatedAt": 1555186007571,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cyjbwn",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1555186007530,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yk7dye",
      "updatedAt": 1555186007530,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "130mk5",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186007494,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-12f8e8",
      "updatedAt": 1555186007494,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g8z45q",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007456,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7s26pp",
      "updatedAt": 1555186007456,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-n7kdsf/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-n7kdsf",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "qufbl",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186008136,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kzroal",
      "updatedAt": 1555186008136,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "k2gjm0",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186008069,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-513gi",
      "updatedAt": 1555186008069,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "tnoo7m"
      ],
      "createdAt": 1555186008001,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mrag2b",
      "updatedAt": 1555186008001,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r7edge",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007939,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ondol0",
      "updatedAt": 1555186007939,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4lniyj",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186007860,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2cuzd7",
      "updatedAt": 1555186007860,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "xf8qyd"
      ],
      "createdAt": 1555186007764,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ye0p3b",
      "updatedAt": 1555186007764,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8uoag2",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007690,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wmj73l",
      "updatedAt": 1555186007690,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7iponm",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186007608,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fwh47t",
      "updatedAt": 1555186007608,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cyjbwn",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1555186007530,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yk7dye",
      "updatedAt": 1555186007530,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g8z45q",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007456,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7s26pp",
      "updatedAt": 1555186007456,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-gwiznn/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-gwiznn",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "rxubbf",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186008178,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-e4eup3",
      "updatedAt": 1555186008178,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qufbl",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186008136,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kzroal",
      "updatedAt": 1555186008136,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "zij7dk"
      ],
      "createdAt": 1555186008108,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-942i6j",
      "updatedAt": 1555186008108,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "k2gjm0",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186008069,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-513gi",
      "updatedAt": 1555186008069,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "19t0i3",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186008040,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qr8lwe",
      "updatedAt": 1555186008040,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "tnoo7m"
      ],
      "createdAt": 1555186008001,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mrag2b",
      "updatedAt": 1555186008001,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fhvxa5",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186007970,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-426x4d",
      "updatedAt": 1555186007970,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r7edge",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007939,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ondol0",
      "updatedAt": 1555186007939,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "daoj8g",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1555186007898,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-myftie",
      "updatedAt": 1555186007898,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4lniyj",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186007860,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2cuzd7",
      "updatedAt": 1555186007860,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c7xg4j",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007801,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-69a4nc",
      "updatedAt": 1555186007801,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "xf8qyd"
      ],
      "createdAt": 1555186007764,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ye0p3b",
      "updatedAt": 1555186007764,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "vetwrq"
      ],
      "createdAt": 1555186007728,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p0n75l",
      "updatedAt": 1555186007728,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8uoag2",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007690,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wmj73l",
      "updatedAt": 1555186007690,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "d9sl3g",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1555186007646,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ea1ojd",
      "updatedAt": 1555186007646,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7iponm",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186007608,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fwh47t",
      "updatedAt": 1555186007608,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "f7185g",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007571,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-iu4az0",
      "updatedAt": 1555186007571,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cyjbwn",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1555186007530,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yk7dye",
      "updatedAt": 1555186007530,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "130mk5",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1555186007494,
      "author": {
        "username": "author-gwiznn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-12f8e8",
      "updatedAt": 1555186007494,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g8z45q",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1555186007456,
      "author": {
        "username": "authoress-n7kdsf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7s26pp",
      "updatedAt": 1555186007456,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "tag_8",
    "tag_mod_2_0",
    "tag_mod_3_2",
    "xf8qyd",
    "rxubbf",
    "tag_19",
    "tag_mod_2_1",
    "tag_mod_3_1",
    "qufbl",
    "tag_18",
    "tag_mod_3_0",
    "fhvxa5",
    "tag_13",
    "tag_7",
    "vetwrq",
    "d9sl3g",
    "tag_5",
    "tag_17",
    "zij7dk",
    "g8z45q",
    "tag_0",
    "k2gjm0",
    "tag_16",
    "f7185g",
    "tag_3",
    "r7edge",
    "tag_12",
    "8uoag2",
    "tag_6",
    "tag_14",
    "tnoo7m",
    "daoj8g",
    "tag_11",
    "c7xg4j",
    "tag_9",
    "tag_a",
    "tag_b",
    "4lniyj",
    "tag_10",
    "7iponm",
    "tag_4",
    "cyjbwn",
    "tag_2",
    "130mk5",
    "tag_1",
    "19t0i3",
    "tag_15"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-3buw46@email.com",
    "username": "author-3buw46",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-3buw46@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci0zYnV3NDYiLCJpYXQiOjE1NTUxODYwMDksImV4cCI6MTU1NTM1ODgwOX0.54dr7WgMeMfm98UmeUg-gkznn-kBEnt0Cx3XC5Tb8f4",
    "username": "author-3buw46",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter--z55z6y@email.com",
    "username": "commenter--z55z6y",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter--z55z6y@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci0tejU1ejZ5IiwiaWF0IjoxNTU1MTg2MDA5LCJleHAiOjE1NTUzNTg4MDl9.cMgcKvZNggVgSyonN_zdp0ApLCFyRTa9qbzBG310iZk",
    "username": "commenter--z55z6y",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-nk3bxh",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1555186009802,
    "updatedAt": 1555186009802,
    "author": {
      "username": "author-3buw46",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-nk3bxh/comments

{
  "comment": {
    "body": "test comment 89m2rf"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "5c54da88-f058-4bca-a068-f14d23216fc4",
    "slug": "title-nk3bxh",
    "body": "test comment 89m2rf",
    "createdAt": 1555186009837,
    "updatedAt": 1555186009837,
    "author": {
      "username": "commenter--z55z6y",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nk3bxh/comments

{
  "comment": {
    "body": "test comment -z4o6mh"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "f45d3e7c-f7c3-41e1-a768-ef8657665e38",
    "slug": "title-nk3bxh",
    "body": "test comment -z4o6mh",
    "createdAt": 1555186009871,
    "updatedAt": 1555186009871,
    "author": {
      "username": "commenter--z55z6y",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nk3bxh/comments

{
  "comment": {
    "body": "test comment vmlxwv"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "2791f41e-f946-482e-bff2-bb24f575a447",
    "slug": "title-nk3bxh",
    "body": "test comment vmlxwv",
    "createdAt": 1555186009901,
    "updatedAt": 1555186009901,
    "author": {
      "username": "commenter--z55z6y",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nk3bxh/comments

{
  "comment": {
    "body": "test comment 8pcoid"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "abe0a0da-691c-4685-b627-6a72a8aa421c",
    "slug": "title-nk3bxh",
    "body": "test comment 8pcoid",
    "createdAt": 1555186009930,
    "updatedAt": 1555186009930,
    "author": {
      "username": "commenter--z55z6y",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nk3bxh/comments

{
  "comment": {
    "body": "test comment 9j51pa"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "22aafd1f-e2c9-4036-9496-b80aff0aeb1c",
    "slug": "title-nk3bxh",
    "body": "test comment 9j51pa",
    "createdAt": 1555186009963,
    "updatedAt": 1555186009963,
    "author": {
      "username": "commenter--z55z6y",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nk3bxh/comments

{
  "comment": {
    "body": "test comment efrb61"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "cd404e04-97b1-46b4-bb93-0933e2c11ebe",
    "slug": "title-nk3bxh",
    "body": "test comment efrb61",
    "createdAt": 1555186010002,
    "updatedAt": 1555186010002,
    "author": {
      "username": "commenter--z55z6y",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nk3bxh/comments

{
  "comment": {
    "body": "test comment zahx92"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "3e1c1a08-fe81-4f13-9ccd-b4101f0813d3",
    "slug": "title-nk3bxh",
    "body": "test comment zahx92",
    "createdAt": 1555186010042,
    "updatedAt": 1555186010042,
    "author": {
      "username": "commenter--z55z6y",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nk3bxh/comments

{
  "comment": {
    "body": "test comment l31f42"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "7d240410-0aa0-48ba-9093-d76dd1120c1b",
    "slug": "title-nk3bxh",
    "body": "test comment l31f42",
    "createdAt": 1555186010074,
    "updatedAt": 1555186010074,
    "author": {
      "username": "commenter--z55z6y",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nk3bxh/comments

{
  "comment": {
    "body": "test comment z4ob6m"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "66e819ff-4bb8-48d0-994c-769ef814254b",
    "slug": "title-nk3bxh",
    "body": "test comment z4ob6m",
    "createdAt": 1555186010101,
    "updatedAt": 1555186010101,
    "author": {
      "username": "commenter--z55z6y",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nk3bxh/comments

{
  "comment": {
    "body": "test comment zh1mt9"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "e1c5bc71-e18e-4e1e-9c83-48f3815df1f6",
    "slug": "title-nk3bxh",
    "body": "test comment zh1mt9",
    "createdAt": 1555186010131,
    "updatedAt": 1555186010131,
    "author": {
      "username": "commenter--z55z6y",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-nk3bxh/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-nk3bxh/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment rqq2pv"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-nk3bxh/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1555186010131,
      "id": "e1c5bc71-e18e-4e1e-9c83-48f3815df1f6",
      "body": "test comment zh1mt9",
      "slug": "title-nk3bxh",
      "author": {
        "username": "commenter--z55z6y",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1555186010131
    },
    {
      "createdAt": 1555186009871,
      "id": "f45d3e7c-f7c3-41e1-a768-ef8657665e38",
      "body": "test comment -z4o6mh",
      "slug": "title-nk3bxh",
      "author": {
        "username": "commenter--z55z6y",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1555186009871
    },
    {
      "createdAt": 1555186009837,
      "id": "5c54da88-f058-4bca-a068-f14d23216fc4",
      "body": "test comment 89m2rf",
      "slug": "title-nk3bxh",
      "author": {
        "username": "commenter--z55z6y",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1555186009837
    },
    {
      "createdAt": 1555186009901,
      "id": "2791f41e-f946-482e-bff2-bb24f575a447",
      "body": "test comment vmlxwv",
      "slug": "title-nk3bxh",
      "author": {
        "username": "commenter--z55z6y",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1555186009901
    },
    {
      "createdAt": 1555186010002,
      "id": "cd404e04-97b1-46b4-bb93-0933e2c11ebe",
      "body": "test comment efrb61",
      "slug": "title-nk3bxh",
      "author": {
        "username": "commenter--z55z6y",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1555186010002
    },
    {
      "createdAt": 1555186009963,
      "id": "22aafd1f-e2c9-4036-9496-b80aff0aeb1c",
      "body": "test comment 9j51pa",
      "slug": "title-nk3bxh",
      "author": {
        "username": "commenter--z55z6y",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1555186009963
    },
    {
      "createdAt": 1555186009930,
      "id": "abe0a0da-691c-4685-b627-6a72a8aa421c",
      "body": "test comment 8pcoid",
      "slug": "title-nk3bxh",
      "author": {
        "username": "commenter--z55z6y",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1555186009930
    },
    {
      "createdAt": 1555186010074,
      "id": "7d240410-0aa0-48ba-9093-d76dd1120c1b",
      "body": "test comment l31f42",
      "slug": "title-nk3bxh",
      "author": {
        "username": "commenter--z55z6y",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1555186010074
    },
    {
      "createdAt": 1555186010101,
      "id": "66e819ff-4bb8-48d0-994c-769ef814254b",
      "body": "test comment z4ob6m",
      "slug": "title-nk3bxh",
      "author": {
        "username": "commenter--z55z6y",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1555186010101
    },
    {
      "createdAt": 1555186010042,
      "id": "3e1c1a08-fe81-4f13-9ccd-b4101f0813d3",
      "body": "test comment zahx92",
      "slug": "title-nk3bxh",
      "author": {
        "username": "commenter--z55z6y",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1555186010042
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-nk3bxh/comments/5c54da88-f058-4bca-a068-f14d23216fc4
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-nk3bxh/comments/f45d3e7c-f7c3-41e1-a768-ef8657665e38
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter--z55z6y]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-nk3bxh/comments/f45d3e7c-f7c3-41e1-a768-ef8657665e38
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-nk3bxh/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.q5ormsog9s@email.com",
    "username": "user1-0.q5ormsog9s",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.q5ormsog9s@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucTVvcm1zb2c5cyIsImlhdCI6MTU1NTE4NjAxMCwiZXhwIjoxNTU1MzU4ODEwfQ.7sDu2feDR5HNirIXrYbRTkWIDKw4GY7Jwp1pYSc8zOo",
    "username": "user1-0.q5ormsog9s",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.q5ormsog9s@email.com",
    "username": "user1-0.q5ormsog9s",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.q5ormsog9s]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.q5ormsog9s@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.q5ormsog9s@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.q5ormsog9s@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.q5ormsog9s@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucTVvcm1zb2c5cyIsImlhdCI6MTU1NTE4NjAxMCwiZXhwIjoxNTU1MzU4ODEwfQ.7sDu2feDR5HNirIXrYbRTkWIDKw4GY7Jwp1pYSc8zOo",
    "username": "user1-0.q5ormsog9s",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.y1jkajlhda9",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.y1jkajlhda9]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.q5ormsog9s@email.com",
    "password": "0.fp6lhsvgkul"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.q5ormsog9s@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucTVvcm1zb2c5cyIsImlhdCI6MTU1NTE4NjAxMCwiZXhwIjoxNTU1MzU4ODEwfQ.7sDu2feDR5HNirIXrYbRTkWIDKw4GY7Jwp1pYSc8zOo",
    "username": "user1-0.q5ormsog9s",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.q5ormsog9s
```
```
200 OK

{
  "profile": {
    "username": "user1-0.q5ormsog9s",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.cd583unhxn
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.cd583unhxn]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE1NTUxODYwMTAsImV4cCI6MTU1NTM1ODgxMH0.my50IJzd1OwRDhsjWCt8RUI6t3ZUl2xkJSGfNSiCC_4",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.5wnbah3xkfb",
    "email": "user2-0.5wnbah3xkfb@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.5wnbah3xkfb@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuNXduYmFoM3hrZmIiLCJpYXQiOjE1NTUxODYwMTAsImV4cCI6MTU1NTM1ODgxMH0.f0FqQ0hnToChXdfmPM8xEzhmvLxf8TaBU7tVTELJwGM",
    "username": "user2-0.5wnbah3xkfb",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.q5ormsog9s@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.q5ormsog9s",
    "email": "updated-user1-0.q5ormsog9s@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucTVvcm1zb2c5cyIsImlhdCI6MTU1NTE4NjAxMCwiZXhwIjoxNTU1MzU4ODEwfQ.7sDu2feDR5HNirIXrYbRTkWIDKw4GY7Jwp1pYSc8zOo"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.q5ormsog9s",
    "email": "updated-user1-0.q5ormsog9s@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucTVvcm1zb2c5cyIsImlhdCI6MTU1NTE4NjAxMCwiZXhwIjoxNTU1MzU4ODEwfQ.7sDu2feDR5HNirIXrYbRTkWIDKw4GY7Jwp1pYSc8zOo"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.q5ormsog9s",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucTVvcm1zb2c5cyIsImlhdCI6MTU1NTE4NjAxMCwiZXhwIjoxNTU1MzU4ODEwfQ.7sDu2feDR5HNirIXrYbRTkWIDKw4GY7Jwp1pYSc8zOo"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.q5ormsog9s",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucTVvcm1zb2c5cyIsImlhdCI6MTU1NTE4NjAxMCwiZXhwIjoxNTU1MzU4ODEwfQ.7sDu2feDR5HNirIXrYbRTkWIDKw4GY7Jwp1pYSc8zOo"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.qvsg8kih14c@email.com",
    "username": "user2-0.qvsg8kih14c",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.qvsg8kih14c@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAucXZzZzhraWgxNGMiLCJpYXQiOjE1NTUxODYwMTEsImV4cCI6MTU1NTM1ODgxMX0.mU-XP97BUxGs4CkoG1fmoQ_IHmU-QSmX4xQeHnkDB5s",
    "username": "user2-0.qvsg8kih14c",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.qvsg8kih14c@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.qvsg8kih14c@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2019-04-13T20:06:51.208Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
