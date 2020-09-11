## Background

In 2015, Meek Mill famously accused Drake of having a verse ghost-written by Quentin Miller. In the ensuing fallout, an extensive debate took place over the role of ghostwriting in hip-hop and the extent to which Drake relied on others for his lyrics. While Miller was given 4 credits on Drake's 2015 album *If You're Reading this it's too Late*, it was never fully settled how much of these songs were attributable to Miller or if Miller's influence spread past them. 

## Goals/ Research Questions

This project has two main goals: 
1. See how effective authorial classification can be on small-medium sized corpora such as song lyrics. 
2. Test if Drake's lyrical style across *If You're Reading This it's Too Late* or simply in the songs co-written by Miller diverged from Drake's lyrical style in other projects. 

## Methods 

I used seven types of models to classify songs by author. The first three used linear methods: logistic regression, support vector machines, and linear classification with stochastic gradient descent. Models three through six used ensemble methods: random forest, adaboost, and gradient boosting. All six of these models used a "bag of words" approach - songs transformed into vectors representing word frequency. During preprocessing, I removed obvious identifiers such as the words "Drake", "Miller", "Toronto" etc. I also cross-validated transformations using term-inverse document frequency - placing more importance on rare words that one author disporportionately uses and decreasing the importance of words that appear most of the documents. The seventh model was a convolutional neural network on the songs as word embedding - vectors that house all the words in sequence and attempt to tease out relationships between how close certain words appear to each other. As an eighth psuedo model, I crafted an ensemble model out of these seven models to aggregate predictions. 

## Results

Regarding the sucessfulness of authorial classification based on song word frequency, our models obtained 87 percent classification accuracy on a left out test set. The ensemble model improved test accuracy to 91 percent. However, due to the lack of empirical rigor behind the aggregation approach as well as lack of interpretability and slower run time, I elected logistic regression as the best model. I should note that the best model changed from run-to-run without random seeding, but logistic and SGD linear regression consistently the best. 

Overall, the linear models slightly outperformed the ensemble and deep learning approaches. Each had roughly 87 percent accuracy on the validation and test sets (with slight fluctations run to run). Interestingly, all linear models performed better with tf-idf transformations, whereas the ensemble methods performed better without tf-idf scaling. The superior performance of the linear models suggests that there are linear relationships bewteen how frequently a (tf-idf scaled) term appears and its author. However, I should qualify this observation with the fact that there were more unexplored hyperparameters on the non-linear models, meaning that perhaps with proper training, there are non-linear relationships bewteen frequency counts and the author. Furthermore, a deeper nueral network or even deeper random forest might have squeezed out more performance with more computing power. 

As for the second goal - better understanding Drake's lyrical style - I offer three cautious takeaways: 

1. The models suggest that two of the Drake's songs - "10 bands" and "No Tellin"- on *If You're Reading This it's Too Late* were closer to Miller's style than other Drake songs. As the qualification section points out, this is far from conclusive evidence. But, it is encouraging to see "10 Bands" be identified as being identified as more likely to come from Miller: "10 Bands" was one of the songs that had a Miller reference track leaked. Compared to the 3 other Quentin Miller reference tracks that got leaked, the "10 Bands" reference track most closely mirrored the eventual final product. In short, Miller wrote the first draft of "10 Bands." The song got edited (by some combination of people) before the final product. The fact that our models identified a certain Miller-esque style to the song even after editing suggests that our method does have some potential to detect latent influence or authorship even when it is not direct copy-and-paste style plagiarism. 

2. The models identified *If You're Reading This It's Too Late* as the most similar to Miller's style out of all the Drake albums. Many of the songs had over 40 percent probability of being written by Miller, which means either our model was simply unsure about which class to predict or found evidence that Miller's style permeated these songs. Again, the strength of this assertion is still relatively low, as we trained our data on songs, not on albums. The difference in "Drakeness" of IYRTITL could have been due to the fact that it was the only album held out of the training set in its entirety. Retraining the data and holding out a second album with our hyper parameters could provide more insight into this possibility. 

3. Based on the coefficients of the models, I found that the artists do employ slightly different vocabularies. Drake's songs sound more romantic in nature with more frequent use of 'girl,' 'baby' and 'love.' Meanwhile, the models identified some ad-libs and catch-phrases "wait wait," "yeah yeah" and "yuh" that distinguished Quentin Miller's work. 

### Qualifications/ Limitations

87 percent classification accuracy is good but not great. The baseline accuracy was 60 percent because of imbalance in the class sizes; a model that predicted Drake everytime and while learning nothing from the data would yield 60 percent accuracy. This was the case for our CNN: in predicting the leftout testset, the CNN predicted Drake with roughly 64 percent probability every time. 
Thus, 87 percent was only a 27 percent improvement over baseline. If the classes were more balanced or had we thrown other noise classes in (for example, adding another artist so the baseline accuracy is ~1/3), our accuracy score is liable to drop to less satisfying levels. 
Even as it is, the over 10 percent gap between training score (almost 100 percent in all but the nueral network) and validation/test sets suggests we're overfitting on the training set. We still sometimes falsely predict Miller as author on songs that (by all accounts) Miller couldn't have had anything to do with, which makes it hard to use these models as anything conclusive in terms of stating "this song had to be written by Miller" or even "this song clearly had Miller's fingerprints on it." For instance, our logistic model incorrectly predicted "DL4" from the test set had a 54 percent chance of being a Miller song when Miller and Drake's relationship had been severed by the time of its creation. It is worth noting, however, two other writers worked with Drake on the song, perhaps changing his style.  


## Future Work on the Drake-Miller Controversy

- <ins>Cleaning the data</ins>: some of the songs that were misclassified were 'outlier' songs in terms of being abnormally short or non-traditional (for example, a spoken word intro). These songs could be removed in future iterations to improve classification accuracy. Other preprocessing choices are available such as lemmatization over stemming or more aggressive removal of stop words.   
- <ins>Supplementing the data </ins>: The relative easiness of the binary classification problem limits how optimistic we can be about the results on the piece of ambiguous authorship. Even though our models suggest that portions of iyrtitl were more likely to be written by Quentin Miller than other Drake songs, it could well be that the album was simply differnt than other Drake projects and not actually closer to Miller's style. It could be that the album was closer to some other artist Drake was trying to imitate at the time. Future attempts might add 'noise' to the task by including other artists and turning it into a multi-class problem to see if iyrtitl's relative closeness to Miller's style still bears out. The data folder of this project already has albums from J. Cole -[an artist found to be close to Drake](https://pudding.cool/2017/09/hip-hop-words/)- and PartyNextDoor - a frequent collaborator who has also received writing credits on Drake songs. 
- <ins>Changing document size</ins>: So far, we've analyzed songs as documents. A different approach might scale upwards by looking at whole albums as a single document or scale downards by looking at individual verses, bars, or lines as documents. The latter few approaches could be interesting by trying to go beyond the bag of words or even basic word-embedding approach by attempting to learn rhyme scheme, assonance, consonance, and meter.
- <ins>Additional models</ins> Beyond improving the existing models with better hyperparameters, other classification strategies could provide further insight into the data. Based on the success of linear modeling, perhaps LDA (or even QDA) would also be a solid classifier. Other unsupervised methods (PCA, Clustering), could offer insight into similarities and better visualizations of the distance between individual songs and albums.
- <ins>Full stacking algorithm</ins>: The final model presented is a naive ensemble method that merely aggregates predictions of the 7 other models. There could be some advantages to this approach compared to simply picking a single model based on validation accuracy because of the disparate preprocessing procedures. At present, there was a small positive effect on test set performance which indicates there is some potential to the idea. One easy step to improve the current aggregate approach would be weighting sub-models based on their performance metrics. The most empircally robust approach, though, would be to implement a full stacking algorithm where we deploy models based on their effectiveness on subsets of the feature space. Stacking is generally conducted with weaker, more independent learners than those used in the present appraoch. Thus, stacking would require a substantial rework of the base learners. However, considering the size and sparsity of the feature space, it is very possible some models do better than others in certain cases, meaning there could be additional performance gains to be had through stacking. 
- <ins>Statistical approach</ins>: This method took a more machine learning-centric approach in optimizing on classification accuracy. We made relatively few assumpsions about the data by trying all sorts of differnt models. At present, each model had unique preprocessing. This choice limits the efficacy of our interpretive efforts and our ability to compare models beyond classification performance. For instance, the lack of standard scaling means that we really can't compare the magnitude of coefficients across models to determine which words are most influential beyond the fuzzy "15 most influential features" approach employed here. Now that we've found linear models to perform well, we could hone in on these methods and make further assumpsions to gain insight into how each author uses contextual and non-contextual words differently. 
- <ins>Further nueral network exploration</ins>: The current convolutional nueral network is a very simple model, in part due to limitations in processing power. Beyond experimentation with different architectures or hyperparameters, we could also try using pretrained word embeddings (eg GloVe, Fasttext, Word2Vec) to get better predictions while also keeping training time manageable. 


## Future Applications
- <ins>Ghostwriting in hip-hop</ins>: So far we've looked at the most famous example of ghostwriting in hip hop. This approach could be applied to rumored ghostwriting connections (see basically any Dr. Dre or P. Diddy song). It could also be applied to credited writers to see how much a song is a collaborative affair vs. a case of the credited writer doing most of the lifting with the artist just taking credit for it. The most ambitious application, however, would be a 'cold start' approach where we have to look for ghostwriting or plagiarism without knowing in advance who is the most likely ghost writer. For instance, what if Miller had never been outed? Could an algorithm have identified Miller out of a broad set of artists as the real author of "10 Bands?" As mentioned above, the multiclass problem increases the complexity immensely, so at present it seems unlikely 'cold start' identifications are possible. Probably somewhere in the middle - where a set of potential writers are identified in advance and then machine learning tries to find stylistic similarity/influence  - is the most promising area for future work. 