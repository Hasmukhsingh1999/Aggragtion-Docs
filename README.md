# User Data Analysis

### 1. How many users are active?

- Answer: _[Insert Number Here]_

### 2. What is the average age of all users?

- Answer: _[Insert Average Age Here]_

### 3. List the top 5 most favorite fruits among the users?

```json
[
  {
    "$group": {
      "_id": "$favoriteFruit",
      "maxCountFavFruit": {
        "$sum": 1
      }
    }
  },
  {
    "$sort": {
      "maxCountFavFruit": -1
    }
  },
  {
    "$limit": 5
  }
]
```

### 4. Find the total numbers of males & females.

### 5. Which country has the highest number of registered users?

```json
[
  {
    "$group": {
      "_id": "$company.location.country",
      "registeredUser": {
        "$sum": 1
      }
    }
  },
  {
    "$sort": {
      "registeredUser": -1
    }
  }
]
```

### 6. List all unique eye colors present in the collections.

### 7. What is the average number of tags per user?

```json
[
  {
    "$unwind": "$tags"
  },
  {
    "$group": {
      "_id": "$_id",
      "numOfTags": {
        "$sum": 1
      }
    }
  },
  {
    "$group": {
      "_id": null,
      "average": {
        "$avg": "$numOfTags"
      }
    }
  }
]
```

### 8. How many users have "enim" as one of their tags?

```json
[
  {
    "$match": {
      "tags": "enim"
    }
  },
  {
    "$count": "tags"
  }
]
```

### 9. How Many Users have a phone number starting with '+1 (940)'?

```json
[
  {
    $match: {
      "company.phone": /^\+1\(940\)/,
    },
  },
  {
    $count: "userWithPhoneNumber",
  },
]

```

### 10. Who has registered the most recently?

```json
[
  {
    "$sort": {
      "registered": -1
    }
  },
  {
    "$limit": 4
  },
  {
    "$project": {
      "name": 1,
      "registered": 1,
      "favoriteFruit": 1,
      "company.phone": 1
    }
  }
]
```

### 11. Categorize users by their favorite fruit.

```json
[
  {
    "$group": {
      "_id": "$favoriteFruit",
      "users": {
        "$push": "$name"
      }
    }
  }
]
```

### 12. How many users have "ad" as the second tag in their list of tags?

```json
[
  {
    "$match": {
      "tags.1": "ad"
    }
  }
]
```

### 13. Find users who have both "enim" and "id" as their tags.

```json
[
  {
    "$match": {
      "tags": {
        "$all": ["enim", "id"]
      }
    }
  }
]
```

### 14. List all companies located in the USA with their corresponding user count.

```json
[
  {
    "$match": {
      "company.location.country": "USA"
    }
  },
  {
    "$group": {
      "_id": "$company.title",
      "userCount": {
        "$sum": 1
      }
    }
  }
]
```

# LOOKUP

```json
[
  {
    "$lookup": {
      "from": "authors",
      "localField": "author_id",
      "foreignField": "_id",
      "as": "author_details"
    }
  },
  {
    "$addFields": {
      "author_details": {
        "$arrayElemAt": ["$author_details", 0]
      }
    }
  }
]
```
