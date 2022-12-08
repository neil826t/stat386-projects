---
layout: post
title:  "Summary: Spotify API and Playlist Analytics"
date:   2022-12-08
author: Neil Thompson
description: A data science journey to make my Focus playlist better for focusing
image: assets/images/work-listening.png
---

## Introduction
Months ago I began this series of blog posts with a large question, "What can information can I glean from a Spotify playlist by getting it into a Pandas dataframe?" The most interesting playlist of mine (in terms of size and variety but also sharing a consistent theme) was the one I use for focusing, aptly named [_Focus_](https://open.spotify.com/playlist/45JTnzWMn7TW1VJW69Wl6T). It has almost 800 songs in it, which gave me plenty of interesting phenomena to look at. You can find my discoveries in [my last post](https://neil826t.github.io/stat386-projects/2022/11/18/PlaylistEDA.html). This post is about how this whole project came together to help me answer this question: "What is it about the songs in my playlist that help me focus?" 

## Getting the Data
[My first post](https://neil826t.github.io/stat386-projects/2022/10/21/SpotifyAPI.html) in this series expressed my fascination with the simplicity of the Spotify API interface library called [_Spotipy_](https://spotipy.readthedocs.io/en/master/). Through Spotify's website I was easily able to get authorization to ethically use the Spotify API. I passed in those credentials to _Spotipy_, and was able to start querying my playlist and info about all the songs in it. Check out my code [here](https://github.com/neil826t/Spotify_API_stats386/blob/main/spotify_scraping.ipynb). 

A review of my steps to make the dataframe of my playlist:
- Getting all my playlists with `spotify.user_playlists(my_username)['items']`
- Getting the URI associated with my focus playlist
- Getting all the songs from that playlist with `spotify.playlist_items(focus_playlist_uri)['items']`
- Putting all those songs into a pandas DataFrame with `pd.DataFrame.from_dict()`
- Building new columns with `pd.Series.apply`

<img src="https://neil826t.github.io/stat386-projects/assets/images/playlist_df_img_1.png" alt="df" style="width:800px;"/>


## Data Exploration
In [my next post](https://neil826t.github.io/stat386-projects/2022/11/18/PlaylistEDA.html) I visualized my dataframe, trying to get a good visual sense of the trends that were going on. I found cool connections between classical composers and the performers of their compositions. I found that songs were **not** equally distributed among principal artists, but that a few artists (~10%) were responsible for the vast majority of the songs on the playlist. Guess I have a type ¯\\_(ツ)\_/¯.

## The Story
After doing the neat Exploratory Data Analysis, I felt like I was missing a piece of the puzzle to grasp the differences between songs, and what made them different from songs outside the playlist. Then it hit me - the **genre**. Genre is how normal humans classify songs, regardless of popularity, length, or any of the other numerical stats I queried earlier. After getting the song's first listed genre I noticed that there were so many, some of which I had never heard of, so I did the unthinkable and manually classified them into one of 5 categories that generally define the genres I focus best with - classical (from Baroque to modern), electronic (including drum n bass, a favorite of mine), ambient/chill, soundtrack (film score), and jazz. 

The graphic below tells the story of the kinds of songs in my playlist, with the features that are most relevant to my focusing. Long songs help me focus for longer, and the genre greatly affects how much I can think about my work vs the song itself. I found that the most common length for a song is between 5 and 6 minutes, but that for songs longer than this, it drops off pretty quickly. Classical music is great for focusing, but the songs don't last near as long as jazz or electronic songs, so should I have less of them? These are some of the little stories I found just from this graphic. What others stories can you find that are being told here?

<img src="https://neil826t.github.io/stat386-projects/assets/images/DataStorySongLengthGenre.png" alt="data_story" style="width:800px;"/>

## Conclusion
Did I really answer my question, "What is it about the songs in my playlist that help me focus?" I got somewhere, but I think there is a lot more to explore. Spotify has tons more data about each song than I showcased throughout this project, and I could dive into deeper musical elements. I could also compare with other playlists. Hopefully, however, this gave you as good of a sense as it me of what kind of cool stories these tools are capable of telling. This project has definitely changed my life in terms of my willingness to dive into an API or any data journey I might not have thought was possible or worth my time before. Please comment below with any ideas you have that could make this project/story more interesting or useful.

See all the code used for this project in [my Github repository](https://github.com/neil826t/Spotify_API_stats386). Feel free to clone and use it for your own projects.
