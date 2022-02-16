---
layout: post
title: How recommendation engines boost your online business
date: '2022-02-07T10:00:00.000-03:00'
author: Martin Barreto
tags: [Recommendation Engine, Recommendation Systems, Recommendation engine challenges]
author_id: mtnBarreto
show: true
category: machine-learning
featured_image: /images/taskflow/taskflow-blogpost.jpg
permalink: /blog/intro-to-product-recommendations-engine/
---



Recommendation engines can rapidly increase online business revenue and boost customer loyalty, both crucial for sustainable growth. In this blog post, we’ll go through the main challenges, and pros and cons we faced implementing and deploying such solutions for a big apparel brand, the different approaches to implement recommendation engines, and best practices.```

First things first... what exactly is a product recommendation engine? And how can I take advantage and put it to work so it drives those sales? Keep reading to find out.

## What's a product recommendation engine?


You probably have Twitter, Netflix, or buy browse through Amazon. All these three platforms use recommendation engines intensively throughout every end-user application touchpoint. Twitter suggests who you should follow, content you might like, top trendings topics, etc.; Netflix recommends movies and series categorized by genre, top watched, Amazon shows related, and “Frequently bought together” items, and so on.


A product recommendation engine is the software component that analyzes data about a platform's end-users to infer what type of products they may be interested in. It considers the user's behavior, activity, preferences, feedback, and products features to generate personalized recommendations.

Modern Recommendation engines use AI and Deep Learning to infer personalized and contextual recommendations **and** constantly evaluate and improve their model results.


## Why your platform need a recommendation engine?

Many businesses have quickly understood the value and importance of solid recommendation systems. Our Machine Learning team has seen this reflected in the number of clients looking for one, and no matter your industry, recommendations systems might be a game-changer for your business's online platforms.

THe most important reason to adopt a recommendation engine is simple: **increase revenue.**. However, there are many other secondary reasons such as:

- Customer Loyalty: Recommendation systems enables a high level of personalization that makes the user feels the platform provides actual value.
- Platform engagement: Customers quickly discover new items to watch, interact and buy, making users spend more time on the platform and consume more.

![Don't take our word for it, trust the numbers.](/images/recommendation-engines/REC-SYSTEMS.png)
Don't take our word for it, trust the numbers. 

> Is it worth investing in a recommendation system for my business? How much time or money will it take? Will I be able to see results quickly? Our experts can answer these and many other questions for you. Schedule a free consultation call to learn more opportunities you might be missing.

## How does a product recommendation engine work?

In a nutshell, modern recommendation engines collect customer data (previous purchases, checkout cart, favorites, viewed items, etc.) to generate personalized recommendations (according to business guidelines and objectives). Under the hood, there is a lot of complexity in developing recommendation systems. Collecting user data to know each user's taste is just the beginning. Then the data should be processed, transformed, and structured in a way deep learning algorithms can generate the items that better fit these preferences. Finally, the recommendation should be shown to the user at the right moment. 

Notice that this workflow never stops. The system constantly gathers new user data to be updated about shifting user interests, transforming these data, and updating the suggested items on an hourly, daily, weekly, monthly basis (which depends on the product needs, user activity, and products catalog changes). 

Let's dive into each step...

### Step 1. Collecting Data

Enables the system to understand end-user taste and preferences. There are two types of data the user provides.

**Activity data provided implicitly:**

- Opening a promotional email.
- Searching by a specific term.
- Viewing certain products.
- Being in a particular location/season.

**Data provided explicitly by app users:**

- Reviewing a product.
- Adding products to wish lists / favorites / Watch later / etc.
- Navigating among categories, applying content filters.
- Adding or removing items to the shopping cart.

The collected data will be different depending on the business domain For example, cart information does not make any sense for a streaming platform.

Each platform and business is unique, so gathered data should carefully be analyzed to produce great predictions according to recommendation engine goals and metrics. 

Luckily, there are several SaaS solutions out there to seamlessly gather end-user activity and preferences, such as [https://segment.com/](https://segment.com/) or [https://firebase.google.com/](https://firebase.google.com/). These tools do not require much effort to integrate since most tracked events and data can be configured rather than coded. 

**Imagen de segment (MATHI)**

### Step 2. Making Data Available

All these vast amounts of collected data need to be accessible and consumed by ML models. There are experts dedicated to managing data at scale. Data Engineers build ETL systems that collect, manage and transform raw data into useful information. Recommendation engines need to perform these processes constantly, so data is updated and can deliver accurate recommendations.

[Airflow](https://airflow.apache.org/) is a popular ETL solution that allows to transform and structure data using data pipelines, but there are many others approaches to manage the data.

**imagen de Airflow pipeline**

### **Step 3.** Build the engine

There are several approaches; let's go through the three more popular ones, from the most simple to most powerful and complex. 

#### A. Content-based filtering.

The Content-filtering approach uses information about people and things as connective tissue for recommendations. It labels each person and item with some known attributes.

For instance, if we're a streaming service, we could tag each movie by genre (drama, terror, action, comedy, etc.). Then each user has a numerical score indicating how much they like a genre. Finally, we connect and cross this information to recommend movies.

Basically, this approach uses item features to suggest other items with similar characteristics as the image below shows. 

![Content-based Fitering](/images/recommendation-engines/content-filtering.png)

In the illustration above, each row represents an app, and each column represents a feature (the app category). Knowing apps installed by the user and their categories allows the algorithm to provide recommendations. 

Its major limitation is not using users’ similarities; this approach only uses items characteristics. Additionally, as we mentioned, these items’ features are not automatically inferred, so a domain expert is needed to create and set them up. 

Another limitation is the scope of the recommendation since it's based on past interests which is the only it has. 

An advantage is that it does not require complex data from other users; only data about the user we want to generate the recommendations is needed (apart from items features :)). This allows the solution to scale up easier when working with a considerable amount of users. 


#### B. Collaborative filtering

The idea behind collaborative filtering is simple; you would probably like the same things as people with similar tastes. So collaborative filtering not just uses item features like content-based filtering; it also considers similar users and what they like to generate recommendations. 

It tries to infer users' features based on the preferences of other users similar to it. It's important to notice that the features, in this case, are not domain-based and could not be interpreted by a person. It's a machine-learning algorithm that generates them using underlying patterns in the data. 

Which one is better? Collaborative filtering predicts the recommendation in the same way but is much more accurate in discovering features human beings can't. Not to mention its ability to update and adapt recommendations over time.

Notice that these two previous approaches can be combined; it is well-known as hybrid recommendation systems in the industry. 

#### C. Deep Learning Model Solutions

Recommendation systems that make use deep-learing models normally outperforms the approaches presented above. Fist because it's super customizable and flexible, we provide user interactions and user non-interactions as examples to train the model, and its infers items with more probablility of being interacted with. 

Input data of the model could be a mix of domain-based data and deep learning, but typically the model by itself does everything or at least is capable of doing so. 

It's essential to have a recurrent cycle of testing and evaluating with real users, retraining, and deploying the model. Typically, MLOps automatize these tasks and ensure the model keeps updated with recent data and enhances its results.   

Unfortunately, flexibility benefit comes with some downside; it's more complex to design, train and deploy.  

Input data should be carefully analyzed since it has a significant impact on the accuracy; it's essential to have a strong knowledge of the domain to properly design the model, selecting the correct input data to achieve the results.

In the most typical design, there are no hardcoded rules; the deep learning model learns from the data; we just have to provide precise training data. However, sometimes teams mix hardcoded data with this approach to achieve better results. 

[TensorFlow recommenders](https://www.tensorflow.org/recommenders) is a pretty popular ML solution in the industry that is worth viewing.

## Challenges building a Recommendations Engine (and how to address them)

### Choosing the right strategy

The north star of a recommendation engine is clear; it ultimately must drive revenue. The tricky question is how to successfully prepare the data, design, train, evaluate and deploy the model? 

A consultancy company like us will help you navigate these challenges, understand the platform needs and create a feasible project plan.

1. **Discovery stage:** We get into your company needs and goals, helping your team discover new opportunities leveraging AI-powered solutions. We also agreed on the metrics to measure its performance.  
2. **Evaluating available data:** As we explained before, gathering data and tracking users’ activity is vital. According to desired outcomes and goals, we reveal data requirements. 
    1. Defining what data is required to provide recommendations. 
    2. Ensuring the data is provided on time and well structured. 
    3. Ensuring data storage, workflow, and data update rate are suitable according to project goals.
3. **UI improvements:** Enumerating screens that will show recommendations to the user. Evaluate UI stuff that needs change and its impact. Create low fidelity and then hi-fidelity design for each screen. 
4. **Agree on a potential solution:** Our specialists design a candidate solution, propose a technology stack and services to build, train, deploy and monitor the recommendation system. 
5. **Feasible roadmap to go-to-market fast:** Considering everything below, we create a feasible roadmap and assign a dedicated team to work in each solution layer (Product, Data, ML model, UX). 

### People's tastes change over time

People's tastes evolve over time, so solutions should adapt the RE to provide newer recommendations according to taste changes. Sometimes the product catalog is constantly updated, but these newly released items have no reviews or ranking. But all these items need to be discovered as they are new products or fresh content.  

To improve the RE performance, its model should be contantly trained, evaluated, and deployed. Likely some data preparation needs to be done too. MLOps, which are essentially DevOps for the ML space, could handle these tasks and automate most, if not the whole, process.

According to business domain and goals, the engineering team should decide when and how frequently the model needs to be updated. Having strategically chosen the metric to measure model performance is crucial to improve it. Strategically defining what metrics should be used to monitor and measure recommendations, accuracy is vital to redeploy a retrained model. The engineering team should know when changes improve the system and what's the cause.


### The product catalog is huge

Certain platforms have a long list of items. eBay and Amazon, for instance, have hundreds of thousands of items to recommend for a particular end-user.

This makes it difficult for the model to determine which items to recommend. A possible solution could be categorizing the items in families of products reducing the candidate items to recommend. The model suggests a product family to then choose an item within the family.

### First-time users

Making recommendations for first-time users involves extra complexity. Not having its personal preference and tracked activity yet, makes it natural to show trending items, most purchased items, and so on. As the user activity is gathered, the recommendations become more precise and personalized. 

The more the user interacts with the platform, the better recommendations the system can provide. It's an incremental and continuous improvement process that makes its recommendations increasingly accurate and personalized.

Depending on the business domain, it could be okay to recommend the most popular items for other new users. 

### Not considering business insights

A fashion e-commerce would need to consider the season, eventually some important data like Christmas where the demand for certain items increases. Customer preferences can eventually shift according to external factors anytime. 

Deep Learning-based recommendation systems can learn these patterns by themselves, but the engineering team can facilitate these business rules explicitly. 

The engineering team can tweak input or output data to generate better results or filter undesired items accordingly. 

### Not able to measure outcomes

If you can't measure it, you can't improve it. As simple as that!
Recommendation systems must be measured with specific metrics to evaluate ROI, evaluate its success, and update the recommendations engine from time to time. 

Evaluating the business value of a recommender system mainly depends on the company’s business strategy and its business domain. 

The most common metrics could be categorized in:

**Click-throught rates:**

Basically, when an item is recommended and viewed.... Was it clicked? How often? Notice it strongly depends on where the recommended items are displayed, if there are more recommended items around, etc.

**User behavior and engagement:**

For a streaming platform, the recommended engine makes the audience spend more time watching series or movies?? Is there any increase in "Save to watch later" list? etc. 

**Revenue Indicators:**

Recommendations make users spend more money? Are users adding more items to the cart? Revenue indicators are great to measure overall RE performance. 

**Adoption and conversion Rates:**

Click-through rates are okay, but we are also interested if these suggested items were purchased, added to the cart, or watched. This indicator reflects whether the recommendation engine is useful to the end-user or not. Otherwise, they can be interested in navigating to the recommendation item but never consume it. It's actually a waste of time for the user. 


### Not considering every end-user touchpoint

Evaluating every change and benefit the end-user would experience by implementing the RE is crucial.
Taking Amazon as an example, several views show recommendations:

- Top sellers and most popular items on the homepage - if the user is not logged in.
- Several screen sections showing “More items to explore” - based on previous purchases, viewed items, etc.
    
    ![More items to explore](/images/recommendation-engines/amazon-re-1.png)
    
    ![“More items to explore 2](/images/recommendation-engines/amazon-re-2.png)

- “Frequently bought together” section in the item view.
    
    ![Frequently bought together](/images/recommendation-engines/amazon-re-3.png)
    
    
- When added a kindle item to the card
    
    ![Added a Kindle item to the card](/images/recommendation-engines/amazon-re-4.png)
    

- During checkout process
    
    ![During checkout steps](/images/recommendation-engines/amazon-re-5.png)
    
- Email

## Closing thoughts

If you read this far, you probably have a better understanding of how the recommendation system can boost your business. You would probably appreciate the complexity of building one that requires a wide range of specialists collaborating together. 

Each product is unique, and the challenges can diverge accordingly. All the challenges we presented were experienced during years of developing these solutions for our clients. 

In the upcoming blog posts, we will be heading to details on how to implement them, different tools and approaches to solve each of the steps presented below, as well as code and practical examples.

If you are considering leveraging recommendation engines...Don’t hesitate, get in touch to get a free consultation with our specialists. 

<div>
<a data-mode="popup" data-hide-footer="true" target="_blank" href="https://form.typeform.com/to/D1PhDJIR" class="button is-nav ipad-hidden typeform-share w-inline-block header-getintouch" style="opacity: 1;">
  <div class="button-text no-pointer">Let's talk</div>
</a>
</div>
<br />
<br />