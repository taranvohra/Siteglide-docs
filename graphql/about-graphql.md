Although it can feel like a big leap at first, using custom GraphQL gives you ultimate control over dynamic data. We'll guide you through.

# Introduction

Firstly, let's go through a few frequently asked questions about GraphQL. In the next article, we'll then get started on our first Query on a new Starter Site.

![](https://downloads.intercomcdn.com/i/o/180518656/3a3397466b2d8026621681a8/image.png)

# What is it?

GraphQL is an open-source querying language which was originally developed by Facebook. The general idea was to create a language which allowed Developers to **quickly** develop **flexible** requests for data, while being **efficient** and only asking for exactly the data they needed. You can read about the open-source project on their website here: <https://graphql.org/>

# How does Siteglide use GraphQL?

It's worth noting that you **don't need to learn GraphQL to use our features**. Most of the time, Siteglide does the querying for you. However, learning GraphQL will allow your Agency to take on more challenging projects- see the next question.

Although the language is open source, actual implementations of it can be quite different across platforms. This is because a GraphQL implementation has two parts:

*   The Schema - this defines different types of Query you can use, which parameters you can add, and what sort of output you can request. It reflects, in part, the database structure that the Platform uses, so it varies from Platform to Platform. Siteglide runs on platformOS and we use [platformOS's implementation](https://documentation.platformos.com/api-reference/graphql/glossary) of GraphQL.

*   The Query Language - This is the syntax for writing queries- it is exactly the same across platforms, but can feel very different when the Schema is different. 

If you've used GraphQL before with a different Schema, you will start to see lots of similarities. 

# How do Liquid and GraphQL work together?

Liquid is a templating language; GraphQL is a query language.&#x20;
To put it another way, think of GraphQL as a re-usable question.

Liquid will both ask the question- and listen to the answer, using it to build a dynamic website. The question itself is in a different language: GraphQL.

GraphQL files are stored inside the marketplace\_builder folder. They can be called by Liquid and re-used as many times as you like.&#x20;

# How can I learn GraphQL?

GraphQL can be tricky to get started with, but most of our Developers report that at a certain stage, it just 'clicks' for them. We want to help any Agency who wants to learn to get there. 

We'll provide a series of Tutorials, starting off simple and becoming progressively more challenging. As part of this, we'll aim to give you the skills you need to carry out further learning yourself- often this will mean learning to read the platformOS schema- finding the type of query you need, and experimenting with how to make it work.

Every time we add a new GraphQL Tutorial, you'll be able to access increased support on that topic via the Forum. You can see an overview of the topics we've covered so far [here](https://developers.siteglide.com/tutorial-overview)

In the next Tutorial, we'll show you how to use the GraphQL sandbox to test out Queries. [Let's go](https://developers.siteglide.com/tutorial-1-your-first-query)

# I'm stuck. Can you help me build a Site with Custom GraphQL?

We want to give you all the tools you need to learn GraphQL and we'll give our general tips, tricks and links to help you solve problems. Unfortunately, we can't build a custom Page for you or assist with custom GraphQL questions - we want to stick to providing first class support on the core product and it wouldn't be fair on other Agencies.

If you're stuck, here are some things you can try:

*   Help us improve our general documentation on GraphQL. We'll keep adding and improving on our articles.

*   Ask the Community on the Forum. We have an ever-growing Community of developers from around the globe, join the discussion.

*   Ask us to recommend a Partner who might be able to build this for you.

*   Maybe this particular solution isn't suited to custom GraphQL, maybe it's better as an official feature? You can request features on the Roadmap.

# When should I use Custom GraphQL?

Writing GraphQL queries gives you ultimate control over your dynamic data. Now, for a small Site, it's probably faster to use Siteglide's pre-built features to cover this for you.

Here are some examples of where some custom GraphQL could open some doors for your Agency. We'll update this list with tutorials and suggestions in the future:

*   **Get any data**. 

*   **Reporting**- Your Client wants several bespoke, complex queries of data, all organised into tables and charts? GraphQL can help you be this **flexible** and if implemented well, can maintain **page speed.**

*   **GraphQL works inside workflow and autoresponder emails**. With mutations, it can also send transactional notifications and API calls from anywhere in your Site.

*   **Performance optimisation**- We do our best to make sure all Siteglide features are delivered to you with the maximum flexibility and performance, but for very bespoke Sites we couldn't possibly make the Platform guess your priorities. Understanding GraphQL could help you **optimise** your most complex features for faster Page load time, while using ready-built features to save development time in other areas.

*   **Front End Mutations- *****Use at your own risk!*** With mutations, you can change data in the database and trigger this with Liquid. This can make a lot of complex projects possible- see the platformOS GraphQL schema for a full list: <https://documentation.platformos.com/api-reference/graphql/mutations>

*   **Update data without loading the Page**- When changing Page in WebApp results, you currently have to wait for the Page to reload. Using Siteglide-CLI and GraphQL you can build an XHR endpoint to get updated data after the Page has loaded. (Note: you can do this with CLI, without GraphQL- GraphQL just gives you more flexibility.)

*   **Jump ahead of the Roadmap**- We're always updating our Roadmap with new functionality and Community requests. But what if you have that one Client that cannot wait? It'll take more time to Develop and may not be as re-usable as a fully tested official feature, but with GraphQL and Liquid understanding, you've got the power to build your own solutions. 

# Start Learning now!

Our first tutorial will get you set up on the GraphQL playground/ sandbox which we make available through Siteglide-CLI.

