# PR Response Doc — CineLog Watchlist Feature

## AI Usage

<!-- Fill in at the end — how you used AI tools during this project -->

## Comment 1 — Rename

**What I did:** Used Ctrl + F to find all occurences of save_to_watchlist() and changed them to add_to_watchlist.
**How I verified:** Tracked down the add to watchlist route and manually verified that each point on trying to add a film to watchlist uses add_to_watchlist(). So verified from add_film function on routes/watchlist to watchlist_service. Also when importing watchlist service method, the import showed now add_to_watchlist().

## Comment 2 — Deduplication

**What I did:** Added a check to verify if a film is not already on user's watchlist. An AlreadyonWatchListError is thrown incase a film that's already on the user's watchlist is trying to be added again.
**How I verified:**Used Claude to test the POST /watchlist/<user_id>/add endpoint using curl with a duplicate film that already exists on a user's watchlist.
Process:
Had Claude first add 3 films to a user's watchlist in this format

```
Request: POST /watchlist//add
  {"film_id": 2}  Response: 201 Created
  {
      "date_added": "2026-07-15T18:09:32.606152",
      "film_id": 2,
      "id":
  "243b803e-a438-4da1-a0f9-034016230152",
      "public": true,
      "user_id":
  "921121fd-3428-40b3-9b8d-f98c4734cea1"
  }
```
Current watchlist before duplicate
```
View Watchlist

  Request: GET /watchlist/<user_id> (no body)

  Response: 200 OK
  [
      {
          "average_rating": 0.0,
          "date_added":
  "2026-07-15T18:04:14.140360",
          "director": "Christopher Nolan",
          "genre": "Sci-Fi",
          "id": 1,
          "poster_url": null,
          "public": true,
          "title": "Inception",
          "year": 2010
      },
      {
          "average_rating": 0.0,
          "date_added":
  "2026-07-15T18:09:32.606152",
          "director": "Bong Joon-ho",
          "genre": "Thriller",
          "id": 2,
          "poster_url": null,
          "public": true,
          "title": "Parasite",
          "year": 2019
      },
      {
          "average_rating": 0.0,
          "date_added":
  "2026-07-15T18:04:28.519804",
          "director": "Francis Ford Coppola",
          "genre": "Crime",
          "id": 3,
          "poster_url": null,
          "public": true,
          "title": "The Godfather",
          "year": 1972
      }
  ]
```
Now tried adding {film_id: 2} again and POST /watchlist/add responded by throwing AlreadyInWatchListError
```
Request: POST /watchlist/<user_id>/add
  {"film_id": 2}

  Response: 409 Conflict
  {"error": "Film '2' is already in this user's
  watchlist"}
```

## Comment 3 — Missing test
**What I did:**Added more tests for watchlist following the test structure of
test_add_to_watchlist_duplicate_raises
test_collection including: test_add_to_watchlist_creates_entry, test_add_to_watchlist_nonexistent_film_raises, test_add_to_watchlist_sets_default_public and test_add_to_watchlist_sets_date_added
**How I verified:**Run pytest tests/test_watchlist.py -v and the 5 watchlist test cases passed, run the whole test suite as well to verify that nothing broke and all the total 9 test cases passed.

## Comment 4 — Default visibility

**My position:**
**Reasoning:**
**Tradeoff acknowledged:**

## Comment 5 — Sort order

**My position:**
**Reasoning:**
**Engagement with reviewer's point:**

## Comment 6 — Rebase

**What conflicted:**
**How I resolved it:**
**How I verified no conflict remains:**

## PR Description

<!-- Written at the end — feature overview, design decisions, manual testing steps -->
