---
layout: post
title: Workout Music Recommender
tags: [galvanize]
---

<iframe width="600" height="600" frameborder="0" scrolling="no" src="//plot.ly/~jcream31/120.embed"></iframe>

Being tired of the continuous hunt to find new workout music to push me through at the gym, I sought out to pinpoint features of my current playlists and seek out similar songs using the Spotify API. The biggest challenges of this project for me was 1. building a dataset of newish workout songs and 2. working with an API that requires user authentication to access private data.   

To build the dataset, I built a recursive algorithm that utilizes the API's "find similar artists" endpoint. I considered that people like to workout to a variety of music, but the artists typically fall into the genres of hip hop and rock. Using 6 differnt starting artists ('Macklemore', 'Beyonce', '30 Seconds to Mars', 'Disturbed', 'Calvin Harris', and '2 Chainz'), I found their 10 most similar artists, and then those artists' most similar artists, etc. For each artist in the dataset, I used the "get top tracks" endpoint to populate the song database.    

I originally set out to derive my own audio features from the audio analysis of each song, but after dealing with the authentication issue mentioned above, I didn't have a whole lot of time. Instead, I opted to use features already available from the API including a song's danceability, energy, valence, acousticness, and instrumentalness. 

Using Euclidean distance, the algorithm takes a user's playlist and finds the most similar song in the database to all the songs in the playlist. The distances are continously weighted as the user likes and dislikes song recommendations. The user can also set their heart rate to find slower or more upbeat songs. 

After trying my app out at the gym, I realized that the tempo of a song is not always the _perceived_ tempo. Most electronic songs have a tempo of around 128 beats per minute, while slower R&B songs can have a tempo of 180 bpm. Thus, to make this app a better recommender, I need to better capture the _perceived_ tempo of a song, perhaps by more strongly weighting the energy feature.
