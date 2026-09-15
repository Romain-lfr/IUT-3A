# Exercises

## 1 Cache hits and misses

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

## 2 Replacement

`
The cache system uses a LRU (Least Recently Used) replacement (or eviction) policy and is used to consider the
`
