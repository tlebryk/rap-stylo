# Rap Stylometry Project 

A casual statistical investigation into the validity of Drake's ghostwriting charges using some basic natural language processing techniques. 

## Navigation
Things are a bit messy right now but the general overview is as follows: 

- <ins>get_lyrics.ipynb</ins>: holds code to get an artist's discography from genius and convert songs into Jsons. 
 - *disclaimer*: please scrap responsably! Scrapping lyrics from genius should be [legal](https://www.theverge.com/2020/8/11/21363692/google-genius-lyrics-lawsuit-scraping-copyright-yelp-antitrust-competition). Still, if you're using this code, please don't spam Genius with a gagillion requests a second.
- <ins>data_exploration.ipynb</ins>: a work in progress trying to do more visualization and fun stats exploration
- <ins>gridsearch_class.ipynb</ins>: models using lyrics to predict authorship. The first six models can be run in about 5 minutes. The Nueral Net takes over 10 minutes but probably it is better to skip that as its performance is garbage.   
- <ins>/data</ins>: houses json files with songs from Drake and Quentin Miller. 
- <ins>writeup.md</ins>: Background on the project, methods and analysis of gridsearch_class. Meant to be accesible with limited NLP and statistics background. 
