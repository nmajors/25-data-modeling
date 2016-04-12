# Instructions

In each section below, you'll have some data described to you. List the models you would create, the fields those models would have, the data type for each field and a description of what the field is for. For example, if I said I wanted to model a todo, I might write something like:

## Todo Model
1. item - string - the actual description of what they want to do
2. completed - boolean - the status of whether it's completed or not
3. user_id - integer - the id for the user who owns this todo
4. created_at - datetime - when the todo was created

NOTE! For all of these, assume you have a User model that represents the person logged into the website.



# Quest 1 - Medium Clone

Let's start with an easy one. I've provided you with the minimum number of models, you just need to provide the field information. If you can think of additional normalized data that needs another model, don't feel restricted by what's here.

You're creating a simple Medium clone where people can write blog posts and comment on other people's blog posts. You want to have enough information to show the latest blog posts, blog posts for specific authors, and blog posts for specific categories. Categories and Authors need to match exactly for us to do this, so we'll make them their own models.

## Blog Post Model
1. id - number - the id for this blog post
2. created_at - string - when the blog post was created
3. updated_at - string - if/when the blog post was updated
4. author_id - number - the id for the author of this post <!--do I need to qualify if the user_id is for the author versus user_id in comment-->
5. image_id - number - the id of the image
6. title - string - the title of the blog post
7. content - string - the content of the blog post
8. post_categories - string - categories assigned to this post <!--array?-->

  image
  1. image - string - the image source url
  <!-- 2. blogpost_id - string - the id of the post this image is assigned to -->
  3. caption - string - the caption for this image
  <!-- id, created_at, updated_at? -->

  Post Categories <!--has many through?-->
  1. blogpost_id - number - id for blog post
  2. category_id - number - id for category

## Comment Model
1. blogpost_id - number - the id for the blog post the comment is about
2. user_id - number - the id for the user who made the comment
3. comment - string - the content of the comment
4. id - number - the id assigned to this specific comment
5. created_at - string - when this comment was created
6. updated_at - string - when this comment was updated

## Author Model
1. id - number - the id of the author of a post
2. first_name - string - the first name of the post's author
3. last_name - string - the last name of the post's author

## Category Model
1. name - string - the name of the category
2. id - number - the id assigned to this category



# Quest 2 - Twitter Clone

You're creating a Twitter clone. People can create tweets, follow other people and have followers. Keep in mind, unlike the blog post example where a comment is a separate entity, tweets responding to other tweets are still just tweets. Also, think about how Twitter turns a tweet into useful information. Do you think they scan tweets for @mentions and hashtags, or are they storing that kind of thing as additional fields? What models do we need to recreate Twitter?

## Tweet Model
1. id - number - the id of this specific tweet
2. created_at - string - when this tweet was created
3. updated_at - string - when this tweet was edited
4. user_id - number - the user who created this tweet
<!-- 5. retweet_id - number - the id of the retweet, can be null if tweet is not a retweet
6. reply_id - number - the id of the original tweet that is being replied to, can be null if tweet is not a reply -->
7. content - string - tweet content

## Reply Model
1. user_id - number - the user who created this reply
2. tweet_id - number - the id of the tweet this reply belongs to

## Retweet Model
1. user_id - number - the user who created this retweet
2. tweet_id - number - the id of the original tweet being retweeted

## User Model
1. id - number - the unique identifier for the user currently logged in
2. profile_id - number - the id of the profile that belongs to this user.

## Profile Model
1. id - number - the unique identifier for this profile
2. first_name - string - the first name of the person who owns this profile
3. last_name - string - the last name of the person who owns this profile
4. display_name - string - the name that the person who owns this profile wishes to have displayed
5. username - string - the @username for this profile
6. image - string - the image source of the profile picture for this person

## Followers Model
1. user_id - number - the current user
2. profile_id - number - the profile of a person who is following the current user  

## Following Model
1. user_id - number - the current user
2. profile_id - number - the profile of a person who the current user is following

## Mentions Model
1. profile_id - number - the id of the profile of the person mentioned in a tweet
2. tweet_id - number - the id of a tweet that mentions this profile

## Hashtag Model
1. tweet_id - number - the id of a tweet that contains a hashtag
2. hashtag - string - the text of a hashtag <!--how do i actually explain this I am too old for hashtags-->






# Quest 3 - Car Makes and Models

You're building a site that associates data with specific variations of specific cars. You need to break the data down from the manufacturer to the specific model. In other words, you need to model in such detail that the system knows that a 2007 Mustang and a 2013 Mustang are the _same_ thing (from the 5th Generation, 2005-2014), but that a 2015 Mustang is different from both of those. The car models should also know general information about the cars.

## Car


## Make Model
1. id - number - the unique identifier for a particular manufacturer
2. name - string - the name of a particular manufacturer

## Models Model
1. id - number - the unique identifier for a particular model
2. name - string - the name of this model
3. make_id - number - the make of this particular model<!--model is specific to a make-->

## Generations Model
1. name - string - the name of a generation
2. model_id - number - the id of the model that this generation belongs to<!--generation is specific to a particular model-->
3. start_year - number - the first year this generation was made
4. end_year - number - the last year this generation was made

## Cars Model  
1. id - number - the unique identifier for the particular car
2. generations_id - number - the generation this car belongs to <!--generations ID contains model_id which contains make id-->
3. year - number - the year a specific car was made






# Quest 4 - DC Comics

You've used the Marvel API quite a bit. Let's model a comic site of our own for DC. You'll need to think about the fact that there are characters (the superheroes), comics (the actual issues), series (the collections of issues), events (which consist of many issues), artists, writers, et cetera. This is an incredibly deep rabbit hole. Create at least 5 models that would be able to provide enough information for someone to build all of our Marvel apps, but in the DC universe.

## Event Model
1. id - number - the unique identifier for an event
2. name - string - the name of this event
3. description - string - the description of this event
4. image - string - the url of the event image

## Series Model
1. id - number - the unique identifier for a series
2. name - string - the name of this series

## Issue Model
1. id - number - unique identifier for an issue
2. name - string - the name of this issue
3. series_id - number - the id of the series this issue belongs to
4. event_id - number - the id of the event this issue belongs to
5. artist_id - number - the id of the artist who illustrated this issue
<!-- 6. writer_id - number - the id of the writer who wrote this issue -->

## Artist Model
1. id - number - unique identifier for an artist
2. first_name - string -  the first name of this artist
3. last_name - string - the last name of this artist

## Writer Model
1.  id - number - unique identifier for a writer
2. first_name - string -  the first name of this writer
3. last_name - string - the last name of this writer

## IssueWriter Model
1. issue_id - number - the id of an issue
2. writer_id - number - the id of a writer who contributed to this issue

<!--I don't know a thing about comics so I'm making an assumption here that an issue might have multiple writers but only one artist.  If that's not how it's done and there are multiple artists I'd make an IssueArtist Model in the same manner as the IssueWriter Model-->

## Character Model
1. id - number - unique identifier for a character
2. name - string - the name of this character
3. description - string - this character's description
4. image - string - the url of the character image

## CharacterEvents Model
1. character_id - number - the id of a character, may have and belong to many events
2. event_id - number - the id of an event this character is in.  <!--'has many through' relationship-->

## Appearances Model
1. id - number -the unique identifier for an appearance
2. character_id - number - the id of the specific character who makes an appearance in a specific issue
3. issue_id - number - the id of specific issue this character appears in
<!--general questions/comments - is the id the only property that we use in a table to access another table, or are we using it because we assume it is the primary key?  For example, could I use "series_name" in the "series model" and if not, why?

-->
