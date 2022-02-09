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
permalink: /blog/intro-to-product-recommendations-engine
---



Recommendation engines can rapidly increase online business revenue apart from boosting customer loyalty which is crucial for sustainable growth. In this blog post, we’ll go through the main challenges we faced implementing and deploying such solutions in a big fashion brand as well as pros and cons, approaches to implement recommendation engines, and best practices. 

First things first... what exactly is it?, and how can I take advantage of it and put it to work to drive those sales? Keep reading to find out.

## What's a product recommendation engine?


If you have twitter, Netflix or buy something on Amazon sometimes, you would probably notice how these platforms intensively use recommendation engines throughout every end-user application touchpoint. For example, twitter suggest who you should follow, content that you might like, and top trendings; Netflix recommend movies and series categorized by genre, top watched movies and so on, and Amazon shows purchasable items everywhere. How many time you *bought a gadget and add a (hand-carved wooden) case to the card just because the e-commerce suggest it and of course you need it.*


Product recommendation engines is a software component that analyze data about platform end-users to infrer what types of products may be interesting to them. Basically it consider user bahaivour, activity, preferences and feedback to generate personalized recommendations. It also take into account products/items chgaracteristics to generate these recoomendations. 

Modern Recommendation engines make use of AI and Deep Learning to infer personalized and contextual recommendation apart of being constanly evaluating and trying to improve its model results. You will get into how it measure accurace shortly... 


## Why your platform need a recommendation engine?

Many businesses have quickly understood the value and importance of solid recommendation systems. Our Machine Learning team has seen this reflected in the number of clients looking for one, and no matter your industry, recommendations systems might be a game-changer for your business's online platforms.

First and most importantly reason to adopt a recommendation engine: **increase revenue.** 

- Customer Loyalty: Recommendation systems enables a high level of personalization that makes the user feels the platform provides actual value.
- Platform engagement: Customer easily discover new items to watch, interact, buy and these makes user spend more time on the platform and as a result consume more.

Recommendation engines drastically boost conversion metrics, take a look at the image below that should its impact in many popular platforms. 

![Don't take our word for it, trust the numbers.](/images/recommendation-engines/REC-SYSTEMS.png)
Don't take our word for it, trust the numbers. 


> Is it worth investing in a recommendation system for my business? How much time or money will it take? Will I be able to see results quickly? Our experts can answer these and many other questions for you. Schedule a free consultation call to learn more opportunities you might be missing.

## How does a product recommendation engine work?

In a nutshell, modern recommendation engines collect customer data (previous purchases, checkout cart, favorites, viewed items, etc.) to generate personalized recommendations (according to business guidelines and objectives). Under the hood, there is a lot of complexity in developing recommendation systems. Collecting user data to know each user's taste is just the beginning, then the data should be processed, transformed, and structured in a way deep learning algorithms can generate the items that better fit these preferences. Finally, the recommendation should be shown to the user at the right moment. 

Something important to notice is that these processes never stop, the system is constantly gathering user data to be updated about shifting in user interests, transforming theese data, and updating the suggested items on a hourly, daily, weekly, monthly basis (which depends on the products needs, user activity and products catalog changes). 

Let's dive into each step...

### Step 1. Collecting Data

Enables the system to understand end-user taste and preferences. There are two types of data the user provides.

**Activity data provided implicitly:**

- Opening a promotional email.
- Searching by specific term.
- Viewing certain products.
- Being in a particular location/season.

**Data provided explicitly by app users:**

- Reviewing a product.
- Adding products to wish lists / favorites / Watch later / etc.
- Navigating among categories, applying content filters.
- Adding or removing items to shopping cart.

The collected data will be different depending on the nature and field of the business. For example, cart information does not make any sense for a streaming platform.

Each platform and business is unique so the data to be collected should be carefully analyzed to produce great predictions according to recommendation engine goals and metrics. 

Luckily, there are several SaaS solutions out there to seamlessly gather end-user activity and preferences such as [https://segment.com/](https://segment.com/) or [https://firebase.google.com/](https://firebase.google.com/). These tools do not require much effort to integrate since most tracked events and data can be configured rather than coded. 

**Imagen de segment (MATHI)**

### Step 2. Making Data Available

All these vast amount of collected data need to be accessible and consumed by ML models. There are experts dedicated to managing data at scale. Data Engineers build ETL systems that collect, manage and transform raw data into useful information. Recommendation engines need to perform these processes constantly, so data is updated and can deliver accurate recommendations.

[Airflow](https://airflow.apache.org/) is a popular ETL solution that allows to transform and structure data using data pipelines, but there are many others approaches to manage the data.

**imagen de Airflow pipeline**

### **Step 3.** Build the engine

There are several approaches, let's go through the three more populat ones, from the most simple to most powerful and complex. 

#### A. Content-based filtering.

Content filtering approach uses information about people and things as connective tissue for recommendations. It labels each person and item with some known attributes.

For instance, if we're a streaming service, we could tag each movie by genre (drama, terror, action, comedy, etc.). Then each user has a numerical score indicating how much they like a genre. Finally, we connect and cross this information to recommend movies.

Basically, this approach uses item features to suggest other items with similar characteristics as the image below shows. 

![Content-based Fitering](/images/recommendation-engines/content-filtering.png)

In the ilustration above, each row represents an app and each column represent a feature (the app category). Knowing apps installed and searched by the user and its categories we can provide the recommendations. 

Its major limitation is not using users’ similarities, this approach only uses items characteristics. Additionally, as we mentioned these items’ features are not automatically inferred so a domain expert is needed to create and set up them. 

Another limitation is the scope of the recommendation since it will be based on the past interests, which is the only information we have. 

An advantage is that it does not require complex data from other users, only data about the specific user we want to provide recommendations is needed (apart from items features :)). This allows the solution to scale up easier when working with a huge amount of users. 



#### B. Collaborative filtering

The idea behind collaborative filtering is simple; you would probably like the same things as people with similar tastes. So collaborative filtering not just use item features like contend-based filtering, it also considers similar users and what they like to generate recommendations. 

It tries to infer users’ features based on the preferences of other users similar to it. It;s important to notice that the features in this case, are not domain-based and could not be interpreted by a person. It’s a machine-learning algorithm that generates them using underlying patterns in the data. 

Which one is better? Collaborative filtering predicts the recommendation in the same way but is much more accurate in discovering features human beings can't. Not to mention its ability to update and adapt recommendations over time.

Notice that these two previuos approaches can be combined, it well known in the industry as hybrid recommendation systems. 

#### C. Deep Learning Model Solutions

Recommendation systems that make use deep-learing models normally outperforms the approaches presented above. Fist because it's super customizable and flexible, we provide user interactions and user non-interactions as examples to train the model, and its infers items with more probablility of being interacted with. 

Input data of the model could be a mix of domain-based data and deep learning learning, but typically the model by itself do everything or at least is capable of doing so. 

It's important to have a recurent cycle of testing and evaluating with real users, retraining and deploying the model. Normally there are MLOps that automatize these tasks and ensures the model keep updated with recent data and enhance its result.   

Unfortunately flexibility benefit comes with some downside, it's more complex to design, train and deploy. 

Input data should be carefully analyzed since it has a bi gimpact in the accuracy, it's important to have a strong knowledge of the domain to properly design the model, selecting the right input data to acieve the results.

In the most typicall design there are not hardcoded rules, the deep learning model learn from the data, we just have to provide precise training data. However sometimes teams decide to mix harcoded data with this approach achieving better results. 

[TensorFlow recommenders](https://www.tensorflow.org/recommenders) is a pretty popular ML solution in the industry that is worth viewing.

## Challenges building a Recommendations Engine (and how to address them)

### Choosing the right strategy

The north star of a recommendation engine is clear, it ultimately must drive revenue. The tough question is how to sucessfull prepare the data, design, train, evaluate and deploy the model? 

A consultancy company like us will help you navigate these challenges, understanding platform needs to create a feasible project plan. 

1. **Discovery stage:** We get into your company needs and goals, helping your team discover new opportunities, leveraging AI-powered solutions. We also agreed on the metrics to measure its prerformance. 
2. **Evaluating available data:** Gathering data and tracking users’ activity is vital as we explained before. According to desired outcomes and goals, we reveal data requirements. 
    1. Defining what data is required to provide recommendations. 
    2. Ensuring the data is provided on time and well structured. 
    3. Ensuring data storage, workflow, and data update rate is suitable according to project goals.
3. **UI improvements:** Enumerating screens that will show recommendations to the user. Evaluate UI stuff that needs change and its impact. Create low fidelity and then hi-fidelity design for each screen. 
4. **Agree on a potential solution:** Our specialists design a candidate solution, propose technology stack and services to build, train, deploy and monitor the recommendation system. 
5. **Feasible roadmap to go-to-market fast:** Considering everything below, we create a feasible roadmap and assign a dedicated team to work in each solution layer (Product, Data, ML model, UX). 

### People's tastes change over time

People's tastes evolve over time so solutions should be able to adapt to provide newer recommendations according to taste changes. Sometimes  product catalog is being constantly updated but these nust released items have no reviews neither ranking. But all these items need to be discovered as they are new products or fresh content.  

In order to improve the RE performance, its model should be contantly trained, evaluated and deployed. Likely some data preparation need to be done too. MLOps, that are essentially devops for the ML space, could handle these tasks and automate most, if not the whole, process.

The engineer team should decide when and how frecuently the model need to be uopdated according busness domain and needs. Having strategically chose the metric to measure model performance is crutial to  

Strategicaly define what metrics should be used to monitor and mesure recommendations accuracy is vital to redeploy a retrained  model. Engineer team should know when changes improve the system and what's the cause. 


### The product catalog is huge

Certain platforms have a long list of items. eBay and Amazon for instance have hundreds of thousands of items to recommend for a particular end-user.  **(Ayuda equipo tecnico de approach para solucionar el  problems de la escalabilidad).** 

### First-time users

But, what do we recommend new users if they've never been on the platform? The algorithm can provide the most popular items by location, related items according to search criteria, or the product the user's currently engaged with. The system tracks these user behaviors to provide more personalized recommendations as they continue using the platform. It's an incremental and continuous improvement process that aims to make its recommendations increasingly accurate and personalized.

Making recommendation for first-time users involve extra complexity. Not having yet its personal preference and tracked activity makes it naturally to show trending items, most purchased items end-user geolocation, and so on. As the user activity is gathered the recommendations become more personalized. 

### Not considering business insights

For a fashion e-commerce is crucial to consider the season, eventually some important data like Christmas where the demand for certain items increases. Customer preferences can eventually shift according to external factors anytime

### Not able to measure outcomes

If you cannot measure, you cannot improve it. Recommendation systems directly impact revenue and it must be measured with specific metrics to evaluate ROI and be able to update the recommendations engine from time to time. 

### Not considering every end-user touchpoint

Before starting to implement any recommendation engine, we should evaluate every change and benefit the end-user would get from that investment. 

Taking Amazon as an example, there are several views that show recommendations:

- Top sellers and most popular items on the homepage - if the user is not logged in.
- Several screen sections showing “More items to explore” - based on previous purchases, viewed items, etc.
    
    ![More items to explore](/images/recommendation-engines/amazon-re-1.png)
    
    ![“More items to explore 2](/images/recommendation-engines/amazon-re-2.png)

- “Frequently bought together” section in the item view.
    
    ![Frequently bought together](/images/recommendation-engines/amazon-re-3.png)
    
    
- When added a kindle item to the card
    
    ![Added a kindle item to the card](/images/recommendation-engines/amazon-re-4.png)
    

- During checkout steps
    
    ![During checkout steps](/images/recommendation-engines/amazon-re-5.png)
    
- Email

## Closing thoughts

If you read this far, you probably have a better understanding of how the recommendation system can boost your business. You would probably appreciate the complexity of building one that requires a wide range of specialists collaborating together. 

Each product is unique and the challenges can diverge accordingly. All the challenges we presented were experienced during years of developing these solutions to our clients. 

In the upcoming blog posts, we will be heading to details on how to implement them, different tools and approaches to solve each of the steps presented below as well as code and practical examples.

If you are considering leveraging recommendation engines....Don’t hesitate, get in touch to get a free consultation with our specialists. 

<div>
<a data-mode="popup" data-hide-footer="true" target="_blank" href="https://form.typeform.com/to/D1PhDJIR" class="button is-nav ipad-hidden typeform-share w-inline-block header-getintouch" style="opacity: 1;">
  <div class="button-text no-pointer">Let's talk</div>
</a>
</div>
<br />
<br />