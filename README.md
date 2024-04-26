# Aggragtion-Docs

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
