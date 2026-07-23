# Spam Detector

Final project for the Building AI course

## Summary

A simple classifier that estimates the probability that an email is spam based on the occurrence of suspicious words in its text. It uses the naive Bayes approach covered in the Building AI course project.

## Background

Spam makes up a large share of all email traffic, wasting users' time and sometimes carrying malicious content such as phishing links or malware. The motivation behind this project is to show that even a simple statistical model can reasonably distinguish spam from legitimate messages.

* spam clutters inboxes and reduces productivity
* some spam messages are dangerous (phishing, malware)
* manual filtering is time-consuming

## How is it used?

The user pastes the text of an email into the program. The program counts how often typical "spam" words (e.g. "win", "free", "click here") appear in the text, and uses Bayes' rule to return the probability that the message is spam. This can be useful for individuals or as an add-on to an email client.

```python
def spam_probability(words, spam_word_freq, ham_word_freq, p_spam=0.5):
    p_ham = 1 - p_spam
    for word in words:
        p_spam *= spam_word_freq.get(word, 0.01)
        p_ham *= ham_word_freq.get(word, 0.01)
    return p_spam / (p_spam + p_ham)


spam_words = {"win": 0.9, "free": 0.8, "click": 0.7}
ham_words = {"win": 0.05, "free": 0.1, "click": 0.05}

email = ["free", "click"]
print(spam_probability(email, spam_words, ham_words))
```

## Data sources and AI methods

In a real deployment, the model would need a training set of emails labeled as spam or ham (not spam), for example the publicly available [Enron Spam Dataset](https://www.cs.cmu.edu/~enron/). The technique used is a naive Bayes classifier.

| Method | Description |
| ----------- | ----------- |
| Naive Bayes | Calculates the conditional probability of spam based on word occurrences |
| Bag of words | Represents text as a count of individual word occurrences |

## Challenges

The project does not handle spam detection in images or attachments, nor sophisticated phishing attacks written without typical spam keywords. The model may also perform poorly on texts in other languages or containing slang it was not trained on.

## What next?

Future improvements could include training on a real-world dataset, support for multiple languages, and integration as a plugin for an actual email client.

## Acknowledgments

* inspiration: the Naive Bayes exercise from the Building AI course
* Enron Spam Dataset – publicly available training data
