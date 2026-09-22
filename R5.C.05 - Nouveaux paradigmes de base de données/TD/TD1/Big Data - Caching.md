# Big Data - Caching

## 3 Exercises

### 3.1 Cache hits and misses

`
A Web (PHP for instance) application is used to store and retrieve movies using their IMDB Identifiers. To
improve performance, a caching mechanism is deployed using Redis. To start with the cache is cold (there is
no data within the cache).
The size of the cache is currently considered as unlimited.
`

    Users are submitting the following queries: tt0325980, tt1477834, tt0325980, tt1477834, tt0325980, tt1477834, tt0325980. 

1. What is the number of cache hits?

        2
        
2. What is the number of cache misses?

        5

3. What is the content of the cache at the end ?

       tt0325980, tt1477834

### 3.2 Replacement

`
The cache system uses a LRU (Least Recently Used) replacement (or eviction) policy and is used to consider the sequence of movie request
`

        tt0468569 tt0108052 tt0068646 tt0111161 tt0468569 tt0108052 tt0110912 tt0468569 tt0108052 tt0068646 tt0111161 tt0110912

1. What is the number of cache hits/misses with a cache of size 3 ?

        2 hits / 10 misses

2. What is the number of cache hits/misses with a cache of size 4 ?

        4 hits / 8 misses

### 3.3 The cache system now uses a FIFO (First In First Out) replacement policy

1. What is the number of cache hits/misses with a cache of size 3 ?

        3 hits / 9 misses

2. What is the number of cache hits/misses with a cache of size 4 ?

        2 hits / 10 misses

## 5 Exercices

### 5.1 Full result caching / Query caching

`
Let the query SELECT * FROM MOVIE WHERE RUNTIME=143 associated to the following records:
`

        tt0325980,Pirates of the Caribbean: The Curse of the Black Pearl,2003-07-09,143,140000000,655011224,htt
        tt1477834,Aquaman,2018-07-06,143,160000000,1148461807,https://image.tmdb.org/t/p/original/xLPffWMhMj1l5
                
1. What is the cache entry if the result is stored as a string in the CSV format?

        "SELECT * FROM MOVIE WHERE RUNTIME=143" 
        "idimdb;title;release;runtime;budget;revenue;poster;
        tt0325980;Pirates of the Caribbean: The Curse of the Black Pearl;2003-07-09;143;140000000;655011224;htt...
        tt1477834;Aquaman;2018-07-06;143;160000000;1148461807;https://image.tmdb.org/t/p/original/xLPffWMhMj1l5..."
        

2. What is the cache entry if the result is stored as a string in the JSON format?

        "SELECT * FROM MOVIE WHERE RUNTIME=143" {
                {
                        idimdb: "tt0325980",
                        title: "Pirates of the Caribbean: The Curse of the Black Pearl",
                        release: 2003-07-09,
                        runtime: 143,
                        budget: 140000000,
                        revenue: 655011224,
                        poster: "htt..."
                },
                {
                        idimdb: "tt1477834",
                        title: "Aquaman",
                        release: 2018-07-06,
                        runtime: 143,
                        budget: 160000000,
                        revenue: 1148461807,
                        poster: "https://image.tmdb.org/t/p/original/xLPffWMhMj1l5..."
                };
        };

### 5.2 Individual result caching / Tuple caching

`
Let the 83 minute movie ’Snow White and the Seven Dwarfs’, released on 1937-12-21, associated with the id
tt0029583. Its budget was 1488423$, its revenue is 184925486 $ and its rating is 7.6. Its cover can be seen at
https://image.tmdb.org/t/p/original/1P9eGGlT7eV7kAAvvSh9jfygr1C.jpg.
`

1. What is the cache entry if the result of ’Snow White and the Seven Dwarfs’ as stored as a CSV string

        idimdb;title;release;runtime;budget;revenue;poster;overview;rating;last_update
        tt0029583;"Snow White and the Seven Dwarfs";1937-12-21;83;1488423;184925486;https://image.tmdb.org/t/p/original/1P9eGGlT7eV7kAAvvSh9jfygr1C.jpg;"A beutiful girl ...";7.6
