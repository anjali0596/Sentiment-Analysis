import pandas as pd
import numpy as np
from textblob import TextBlob
from wordcloud import WordCloud
import matplotlib.pyplot as plt

# Loading the Dataset
data = pd.read_csv("Sentiment_Analysis .csv")
data.head()
# define a function to analyse the sentiments

def get_sentiment(text):
    analysis = TextBlob(text)
    if analysis.sentiment.polarity>0:
        return "Positive"
    elif analysis.sentiment.polarity<0:
        return "Negative"
    else:
        return "Neutral"

data["Sentiment"]=data["Sentences"].apply(get_sentiment)
print(data)

data.to_csv("Sentiment Analysis Updated.csv",index=False)

print("Ready to Download")

def get_sentiment(text):
    analysis = TextBlob(text)
    if analysis.sentiment.polarity>0:
        return "Positive"
    elif analysis.sentiment.polarity<0:
        return "Negative"
    else:
        return "Neutral"

data["Sentiment"]=data["Sentences"].apply(get_sentiment)

# filtering only negative reviews

negative_review = data[data["Sentiment"]=="Negative"]
print(negative_review)

#Combine all negative sentences into one string

all_negative_text=" ".join(negative_review["Sentences"])

# Create the  wordcloud for the negative reviews:

anjali = WordCloud(width=800,height=400,background_color="White").generate(all_negative_text)

#plot the wordcloud

plt.figure(figsize=(10,6))
plt.imshow(anjali,interpolation="bilinear")
plt.title("Most Common words in Negative Sentiments")
plt.axis("Off")
plt.show()
