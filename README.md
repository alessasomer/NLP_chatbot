# Chatbot

The goal of this project was to build a dialogue system that makes movie recommendations to a user. We used a frame-based approach and implemented both rule-based and machine-learning based modules.  


## Goal with example 

The goal of the chatbot is to provide movie recommendations to a user. In order to do so, the chatbot:
 
1. Extracts and transforms a user's input 
2. Predicts the sentiment of a user's input about movies 
3. Gathers 5 sentiment ratings from the user to predict a new movie 

Here's an example of what an interaction between the chatbot and a human user might look like.

```
chatbot> Hi! I'm MovieBot! I'm going to recommend a movie to you. First I will ask you about your taste in movies. 
Tell me about a movie that you have seen.

user> I really liked Moneyball.
```
The bot gets confused because it only recognizes movies in quotation marks. 

```
chatbot> Sorry, I don't understand. Tell me about a movie that you've seen with the title in quotation marks. 

user> I really liked "Moneyball".

chatbot> You liked "Moneyball". Thank you! Tell me about another movie you have seen.

user> I was completely amazed at how "Rush Hour" was pretty much the most ridiculous thing I've seen in my entire life.
``` 
The sentence above was too hard for the bot to predict sentiment, but the bot recovers. 

```
chatbot > I'm sorry, I'm not quite sure if you liked "Rush Hour". Tell me more about "Rush Hour".

user> I hated "Rush Hour".

chatbot> Ok. You disliked "Rush Hour." There are multiple Rush Hours. 
Did you mean "Rush Hour (1998)", "Rush Hour 2 (2001)", or "Rush Hour 3 (2007)"?

user> "Rush Hour 2"

chatbot> Ok. You meant "Rush Hour 2 (2001)" 
```
Above, the chatbot is able to disambiguate between multiple movies that match "Rush Hour" in its movie database. 

```
chatbot> I want to hear more about movies! Tell me about another movie you have seen.

user> I didn't like "The Notebook".
```
... the bot proceeds to gather sentiment ratings from the user for 5 movies. 

```
chatbot> Thanks! That's enough for me to make a recommendation. 
I suggest you watch "In the Heart of the Sea".

user> Great. Thanks! 

chatbot> Would you like to hear another recommendation? (Or enter :quit if you're done.)

user> :quit

chatbot> Thanks! It was fun chatting with you!  

```
Your goal is to write the code that will interact with users in this manner and beyond. 

## REPL 

Dialogue systems can be decomposed into four primary modules ([Norvig 1991](https://github.com/norvig/paip-lisp)) which are called the Read-Eval-Print-Loop (REPL): 

1. Read the input.
2. Extract relevant information from the input, which can be domain specific – as in our movie recommender chatbot.
3. Transform the input into a response – users normally expect a response in the given domain.
4. Print the response.

In `repl.py` we have implemented 1 and 4 for you. In `chatbot.py` you'll implement 2 and 3. 

## Getting started

To get started: 

1. Activate `cs375` by typing on the command line 
	
	```
	conda activate cs375
	```

1. In this directory, type the following command to start the chatbot 
 
	```
	python repl.py 
	```

1. You can test your chatbot with `.txt` files containing the user input as follows: 

	```
	python repl.py < testing/simple.txt
	```
	
	As you can see, each line of `simple.txt` is entered consecutively into the chatbot. However, the script terminates once it hits `:quit` and any lines afterwards will not be executed.
	
	Files like `simple.txt` are useful when you want to test the same script multiple times and we encourage you to write your own. We will be manully testing your code with similar (but not the same) scripts as the ones provided in `testing/`.

4. Now it's your turn. Open the `chatbot.py` file and follow the instructions in the function docstrings. You can see more about the grading breakdown below. 

## Data

Three datasets used in `chatbot.py`. 

### Sentiment lexicon 

In `data/sentiment.txt`, there is a sentiment lexicon that you can use to extract sentiment from the input. It consists of 3624 words with their associated sentiment (positive or negative) extracted from Harvard Inquirer (Stone et al. 1966). The lexicon is stored for your convenience in a dictionary/hash map, where the word is the key and the sentiment the value.

### Rotten Tomatoes Reviews

In `data/rotten_tomatoes.pkl`, there is a subset of the [Rotten Tomatoes dataset from Kaggle.](https://www.kaggle.com/competitions/sentiment-analysis-on-movie-reviews/data). This dataset includes reviews in the form of text and class labels "fresh" and "rotten". 


### Movie recommendation database 

The `movie database` consists of two files: 

- `data/movies.txt` 
- `data/ratings.txt`

This data comes from [MovieLens](https://movielens.org/) and consists of a total of 9125 movies rated by 671 users. Feel free to browse this data in a text editor. 

The file `data/ratings.txt` includes a 9125 x 671 utility matrix that contains ratings for users and movies. The ratings range anywhere from 1.0 to 5.0 with increments of 0.5. The code will binarize the ratings as follows:

```
+1 if the user liked the movie (3.0-5.0)
-1 if the user didn’t like the movie (0.5-2.5)
0 if the user did not rate the movie
```

There is also `data/movies.txt`, a list with 9125 movie titles and their associated movie genres. The movie in the first position in the list corresponds to the movie in the first row of the ratings matrix. An example entry looks like:

```
['Blade Runner (1982)', 'Action|Sci-Fi|Thriller']
```

### Debug mode 
The debug method in the `Chatbot()` class can be used to print out debug information about the internal state of the chatbot that you may consider relevant, in a way that is easy to understand. 
```
:debug on
```
and type

```
:debug off
```
to disable it. 


### Testing

```
python repl.py < testing/simple.txt
```







