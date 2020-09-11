# Rap Stylometry Project 

A casual statistical investigation into the validity of Drake's ghostwriting charges using some basic NLP techniques. 

## Navigation
Things are a bit messy right now but the general overview is as follows: 

- get_lyrics: holds code to get an artist's discography from genius and convert songs into Jsons. 
 - *disclaimer*: please scrap responsably! Scrapping lyrics from genius should be [legal](https://www.theverge.com/2020/8/11/21363692/google-genius-lyrics-lawsuit-scraping-copyright-yelp-antitrust-competition). Still, if you're using this code, please don't spam Genius with a gagillion requests a second.
    
- data_exploration: a work in progress trying to do more visualization and fun stats stuff to 
   
- gridsearch_class: models using lyrics to predict authorship of artists and a more extensive write up of the results. Should take less than 30 minutes to run on a modern laptop, depending on number of folds and iterations chosen on gridsearch.  
- /data folder: houses json files with songs from Drake and Quentin Miller, as well as a few other artists. 
- writeup.md: Basically a repeat of the analysis from gridsearch_class with some background on the project. 

