# Big Data - Redis

## 3 Basic commands

1. Store and then retrieve a string ”Aldo Maccione”associated to the key ”actor:1”.

        SET actor:1 "Aldo Maccione"

2. Store in a list ”movies:sw”the movies ”The phantom menace”and ”Attack of the Clones”.

        RPUSH movies:sw "The phantom menace" "Attack of the Clones"
    
3. Return the length of the list ”movies:sw”.

        LLEN movies.sw

4. Return (and remove) the element from the head of the list ”movies:sw.

        LPOP movies:sw

## 3.1 Queues and stacks

1. Implement a queue (FIFO) using a list (for example with values 1, 2, 3, 4 and 5) using LPUSH. In particular how to design ”enqueue” and ”dequeue”.

        LPUSH FIFO "1" "2" "3" "4" "5"
        LPUSH FIFO "<value>"
        RPOP FIFO

2. Implement a queue using RPUSH.

        RPUSH FIFO "1" "2" "3" "4" "5"
        RPUSH FIFO "<value>"
        RPOP FIFO
        
3. Implement a stack (LIFO) using a list (for example with values 1, 2, 3, 4 and 5) using LPUSH. In particular how to design ”push” and ”pop”.

        LPUSH LIFO "1" "2" "3" "4" "5"
        LPUSH LIFO "<value>"
        LPOP LIFO

4. Implement a stack using RPUSH

        RPUSH LIFO "1" "2" "3" "4" "5"
        RPUSH LIFO "<value>"
        RPOP LIFO

## 4 Data caching

## 4.3 Validation

### 4.3.1 Full result caching / Query caching
`
        Let the query SELECT * FROM MOVIE WHERE RUNTIME=143 associated to the following records:
        tt0325980,Pirates of the Caribbean: The Curse of the Black Pearl,2003-07-09,143,140000000,6 ⌋
        55011224,https://image.tmdb.org/t/p/original/z8onk7LV9Mmw6zKz4hT6pzzvmvl.jpg,8,→
        tt1477834,Aquaman,2018-07-06,143,160000000,1148461807,https://image.tmdb.org/t/p/original/x ⌋
        LPffWMhMj1l50ND3KchMjYoKmE.jpg,6.9,→
`
1. Store the previous query as a string in the CSV format.

        SET "SELECT * FROM MOVIE WHERE RUNTIME=143"
        "idimdb;title;release;runtime;budget;revenue;poster;rating;\n
        tt0325980;Pirates of the Caribbean: The Curse of the Black Pearl;2003-07-09;143;140000000;655011224;https://image.tmdb.org/t/p/original/z8onk7LV9Mmw6zKz4hT6pzzvmvl.jpg;8;\n
        tt1477834;Aquaman;2018-07-06;143;160000000;1148461807;https://image.tmdb.org/t/p/original/xLPffWMhMj1l50ND3KchMjYoKmE.jpg;6.9;"

2. Store the previous query as a string in the JSON format.

        SET "SELECT * FROM MOVIE WHERE RUNTIME=143" '[
                {
                        "idimdb": "tt0325980",
                        "title": "Pirates of the Caribbean: The Curse of the Black Pearl",
                        "release": "2003-07-09",
                        "runtime": 143,
                        "budget": 140000000,
                        "revenue": 655011224,
                        "poster": "https://image.tmdb.org/t/p/original/z8onk7LV9Mmw6zKz4hT6pzzvmvl.jpg",
                        "rating": 8
                },
                {
                        "idimdb": "tt1477834",
                        "title": "Aquaman",
                        "release": "2018-07-06",
                        "runtime": 143,
                        "budget": 160000000,
                        "revenue": 1148461807,
                        "poster": "https://image.tmdb.org/t/p/original/xLPffWMhMj1l50ND3KchMjYoKmE.jpg",
                        "rating": 6.9
                }
        ]'

### 4.3.2 Individual result caching / Tuple caching
`
Let the 83 minute movie ’Snow White and the Seven Dwarfs’, released on 1937-12-21, associated with the id
tt0029583. Its budget was 1488423$, its revenue is 184925486 $ and its rating is 7.6. Its cover can be seen at
https://image.tmdb.org/t/p/original/1P9eGGlT7eV7kAAvvSh9jfygr1C.jpg.
`
1. Store ’Snow White and the Seven Dwarfs’ as a CSV string.

        SET "movie:tt0029583"
        "idimdb;title;release;runtime;budget;revenue;poster;rating;\n
        tt0029583;Snow White and the Seven Dwarfs;1937-12-21;143;1488423;184925486;https://image.tmdb.org/t/p/original/1P9eGGlT7eV7kAAvvSh9jfygr1C.jpg;7.6;"

2. Retrieve the size of this CSV like entry.

        2. STRLEN "movie:tt0029583"

3. Store ’Snow White and the Seven Dwarfs’ as a hash.

        HSET "movie:tt0029583" 
                idimdb "tt0029583" 
                title "Snow White and the Seven Dwarfs" 
                release "1937-12-21" 
                runtime 83 
                budget 1488423 
                revenue 184925486 
                poster "https://image.tmdb.org/t/p/original/1P9eGGlT7eV7kAAvvSh9jfygr1C.jpg" 
                rating 7.6

4. Retrieve the size of this hash entry.

        HLEN "movie:tt0029583"
        
## 4.4 Web application acceleration
`
The objective of this activity is to provide a simple web application with acceleration using data caching.
`
1. Propose a simple baseline web architecture with for example a Relational Data Base Management System (DBMS).

        .

2. Integrate a caching layer is the previous architecture.

        .

3. Define an experimental protocol to compare the two solutions

        .
