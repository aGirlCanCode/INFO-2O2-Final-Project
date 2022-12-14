
**ABSTRACT**

In this day of overwhelming information and associated collections, categorization helps in not only information organization but also more efficient navigation, finding, and analyses. In this project, my 3-fold objective is as follows: 
Make a collection of most controversial posts on the popular subreddit r/Futurology using a web scraper
Organize the collection into computationally-created and individually-named labels/categories by using a topic modeling approach
Analyze and compare the aforementioned categories on the basis of the information needs that they serve

Keywords: Categorization, Information Need guided Categorization, Computationally-Created Categories vs Individually Created Categories, Topic Modelling


**METHODOLOGY**

**Data Collection**

r/Futurology subreddit data was crawled using the reddit API wrapper library praw. According to Reddit, this popular forum is devoted to the field of Future(s) Studies and speculation about the development of humanity, technology, and civilization. For the ease of analysis, I collected only the top thousand ‘controversial’ tagged posts which are defined by the highest number of upvotes and downvotes on the platform. The attributes of posts collected include - ['idstr', 'created_datetime', 'flair_text', 'flair_css_class', 'author', 'title', 'selftext', 'distinguished', 'textlen']. For data collection, I made use of the scraper code referenced [1] at the end of this report. 
Total number of (raw) posts collected: 978

**Data Cleaning**

I made use of the nltk and re python libraries to tokenize and remove the common English stop words, punctuation marks and numbers from the data. Furthermore, I use part-of-speech tagging to retain only the nouns, verbs and adjectives in the posts. This cleaning pipeline was applied only to the ‘selftext’ attribute of posts. On analyzing the data, I discovered that our attribute of concern, ‘selftext’ had a few missing values. I replaced those with the ‘title’ attribute values which also contained meaningful information about the subject/topic of the posts. 

**Topic Modelling**

The cleaned data was fed into the topic model for categorization and topic discovery. The python package Bertopic was used for categorizing the collection into topics. The advantage of using this topic model is that it takes context into account. The number of topics was set as ‘auto’. 
The fine-tuned model discovered a total of 23 topics and categories. I also performed dynamic topic modelling to analyse the spread of computationally-created categories over time as shown in Fig 1.  

![Alt text](figures/dynamic_tm.jpg?raw=true "Dynamic Topic Modelling Results of Top Controversial Posts on r/Futurology")


**QUALITATIVE ANALYSIS**

**Labelling Topic Model Categories - Individually-Named Categories**

The topic model discovered a total of 23 topics and the detailed output can be found in the topic_model_output.txt file. The original output of the topic model has numbers as categories for a cluster of terms. Each cluster of terms was studied and qualitatively labeled by me - these formed the individually-named categories. My next objective was to study these in the light of Reddit posts own ‘flair_text’ which are another set of computationally-created categories and analyze the difference between them in terms of the information needs that they may serve. 

**Qualitative Analysis of Reddit Flairs with Individually-named Categories**

A) Reddit flairs

I analyzed the different tagged categories (flairs) marked by Reddit. The flair_text field is one of the resources of the platform that supports filtering interaction. My collection had a total of 35 unique categories with top 20 categories (based on the frequency of occurrence in our collection) shown in Fig 2. Please note that link_flairs are a relatively new concept for Reddit and there were quite a few posts with missing link_flair fields. Such posts were marked with ‘unknown’ tag by me.

![Alt text](figures/top_flairs.jpg?raw=true "Top 20 Reddit Tagged ‘flair_text’")


B) Individually Named Categories

Based on the terms in each topic, I formed a list of 23 categories independent of the Reddit flairs. Using the fine-tuned topic model, I scored each post in the collection into a particular category as discovered by the topic model. Each topic number was assigned a label by me and these labels were in turn used for every post.  These categories were - 

AI',  'Technology', 'Society', 'Robots, Jobs and Automation', 'Climate Change', 'Reddit', 'Food', 'Elon and Trump', 'Renewable Energy', 'Self Driving Cars', 'Cryptocurrency', 'People', 'Life Science', 'Science Fiction', 'Nuclear Energy',  'Science Fiction', 'Gender', 'World Politics and Guns', 'Aliens', 'Income', 'Covid Research',  'Life Science',  'Space Travel'

Fig. 3 shows the distribution of computationally-created categories with respect to the Reddit flairs. The y-axis represents the Reddit Flairs while the coloured labels represent the computationally-created categories or the topics discovered by the model. By default, each topic is represented by the model with the top terms in the topic. 

![Alt text](figures/topics_per_flair.jpg?raw=true "Topics per Reddit Flair Text")


C) Comparison of Reddit Flairs with Individually-Named Categories 

Using Fig. 3, we can see that there is a decent overlap between the Reddit created flairs and the categories discovered by my topic model with the exception of certain flairs like - ‘image’, ‘video’, and ‘text’. This kind of categorization boils down to the information need of the channel which not only categorizes the data based on content but also on the data type. This may be useful to the platform for further analysis of only image posts or only text posts. Interestingly, there were quite a few ‘other’ flairs by the platform that were labeled well by the topic model I trained. A direct comparison of the flairs and the labels I created can be found in the file TopicsPerFlair.txt. The information need of these flairs is solely to organize the posts into categories for ease of navigation by the user. Since, it is difficult to maintain a large number of these categories - the cardinality is expected to be low. Surprisingly, even 35 categories is a huge number for any platform. It will be interesting to see how these evolve over time and if new theme posts will be included in existing categories or grouped under ‘other’. [ORGANIZING SYSTEM, CATEGORIES]. The supported interactions included filtering posts based on these marked link_flairs or categories. 

In the list of additional categories discovered by the topic model, the most interesting ones included 'Elon and Trump' and ‘Guns and World Politics’ - which demonstrate the granularity of the topic model. Of course these are directly tied to my information need of categorizing posts solely based on their ‘content’ and underlying interesting themes. It was amusing to see how Elon and Trump were grouped under the same topic by the model. 

**References**

[1]https://github.com/dlab-berkeley/Data-Science-Social-Justice/blob/main/lessons/optional/reddit_api.ipynb
