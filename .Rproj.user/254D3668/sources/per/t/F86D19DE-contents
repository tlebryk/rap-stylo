library(stylo)
raw.corpus <- load.corpus(files='all', corpus.dir = 'data/texts')

tokenized.corpus <- txt.to.words.ext(raw.corpus, corpus.lang = "English.all", 
                                     preserve.case = FALSE)

corpus.no.pronouns <- delete.stop.words(tokenized.corpus,
                                        stop.words = stylo.pronouns())

corpus.char.2.grams <- txt.to.features(corpus.no.pronouns, ngram.size=2)

frequent.features <- make.frequency.list(corpus.no.pronouns, head = 500)

freqs <- make.table.of.frequencies(corpus.no.pronouns, features = frequent.features)

stylo(corpus.dir = "data/texts", mfw.min = 200, mfw.max = 200,
      analysis.type = "PCR", sampling = "normal.sampling", sample.size = 100,
      gui = FALSE)
stylo(frequencies = freqs, analysis.type = "PCR",
      custom.graph.title = "drake vs quintin miller", gui = FALSE)
stylo.results = stylo()

training.texts <- c('Drake_Care.txt',
                    #'Drake_Certified.txt',
                    'Drake_Comeback.txt',
                    'Drake_Dark.txt',
                    'Drake_Drake.txt',
                    #'Drake_If.txt',
                    'Drake_More.txt',
                    'Drake_Nothing.txt',
                    'Drake_Room.txt',
                    'Drake_Scary.txt',
                    'Drake_Scorpion.txt',
                    'Drake_So.txt',
                    #'Drake_So1.txt',
                    'Drake_Take.txt',
                    'Drake_Thank.txt',
                    'Drake_The.txt',
                    'Drake_Views.txt',
                    'Quentin_Essentials,.txt',
                    'Quentin_Falco.txt',
                    #'Quentin_Gunmetal.txt',
                    'Quentin_Hey!.txt',
                    #'Quentin_Hey!1.txt',
                    'Quentin_Na.txt',
                    'Quentin_No(thanks).txt',
                    'Quentin_Qm.txt',
                    'Quentin_Shredded.txt',
                    'Quentin_Unreleased.txt',
                    'Quentin_Weekends.txt',
                    'Quentin_Xx.txt')

training.set <- freqs[(rownames(freqs) %in% training.texts),]

test.set <- freqs[!(rownames(freqs) %in% training.texts),]

delta.results = classify(training.frequencies = training.set, test.frequencies = test.set, 
         mfw.min = 50,mfw.max = 500, mfw.incr = 50, classification.method = "nsc", cv.folds=20, 
         gui = FALSE)

summary(delta.results)

bayes.results <- perform.naivebayes(training.set, test.set)

