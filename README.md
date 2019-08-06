# Movie-Recommender-System


What are recommender systems?

Amazon is a great example
if you go to their recommendations section, 
you can see that it will recommend things that you might be interested in
purchasing based on your past behavior on the site.

The recommender system might include things that you've rated, or things that
you bought, and other data as well.You can also
think of the people who bought this also bought feature on Amazon as a form of
recommender system.
The difference is that the recommendations you're seeing on your Amazon
recommendations page are based on all of your past behavior, whereas people
who bought this also bought or people who viewed this also viewed, things like
that, are just based on the thing you're looking at right now, and showing you
things that are similar to it that you might also be interested in. And, it turns out,
what you're doing right now is probably the strongest signal of your interest
anyhow.

Another example is from Netflix:

They have various features that try to recommend new movies or other movies
you haven't seen yet, based on the movies that you liked or watched in the past
as well, and they break that down by genre. They have kind of a different spin on
things, where they try to identify the genres or the types of movies that they
think you're enjoying the most and they then show you more results from those
genres. So, that's another example of a recommender system in action.
The whole point of it is to help you discover things you might not know about
before, so it's pretty cool. You know, it gives individual movies, or books, or
music, or whatever, a chance to be discovered by people who might not have
heard about them before. So, you know, not only is it cool technology, it also
kind of levels the playing field a little bit, and helps new items get discovered by
the masses. So, it plays a very important role in today's society, at least I'd like to
think so! 
There are few ways of doing this, and we'll look at the main ones in
this project.
## User-based collaborative filtering

First, let's talk about recommending stuff based on your past behavior. One
technique is called user-based collaborative filtering, and here's how it works:
Collaborative filtering, by the way, is just a fancy name for saying
recommending stuff based on the combination of what you did and
what everybody else did, okay? So, it's looking at your behavior
and comparing that to everyone else's behavior, to arrive at the
things that might be interesting to you that you haven't heard of yet.

. The idea here is we build up a matrix of everything that every user has ever
bought, or viewed, or rated, or whatever signal of interest that you want to
base the system on. So basically, we end up with a row for every user in our
system, and that row contains all the things they did that might indicate
some sort of interest in a given product. So, picture a table, I have users for
the rows, and each column is an item, okay? That might be a movie, a
product, a web page, whatever; you can use this for many different things.
2. I then use that matrix to compute the similarity between different users. So,
I basically treat each row of this as a vector and I can compute the
similarity between each vector of users, based on their behavior.
3. Two users who liked mostly the same things would be very similar to each
other and I can then sort this by those similarity scores. If I can find all the
users similar to you based on their past behavior, I can then find the users
most similar to me, and recommend stuff that they liked that I didn't look at
yet.
Let's look at a real example, and it'll make a little bit more sense:
Let's say that this nice lady in the preceding image watched Star Wars and The
Empire Strikes Back and she loved them both. So, we have a user vector, of this
lady, giving a 5-star rating to Star Wars and The Empire Strikes Back.
Let's also say Mr. Edgy Mohawk Man comes along and he only watched Star
Wars. That's the only thing he's seen, he doesn't know about The Empire Strikes
Back yet, somehow, he lives in some strange universe where he doesn't know
that there are actually many, many Star Wars movies, growing every year in fact.
We can of course say that this guy's actually similar to this other lady because
they both enjoyed Star Wars a lot, so their similarity score is probably fairly
good and we can say, okay, well, what has this lady enjoyed that he hasn't seen
yet? And, The Empire Strikes Back is one, so we can then take that information
that these two users are similar based on their enjoyment of Star Wars, find that
this lady also liked The Empire Strikes Back, and then present that as a good
recommendation for Mr. Edgy Mohawk Man.
We can then go ahead and recommend The Empire Strikes Back to him and he'll
probably love it, because in my opinion, it's actually a better film! But I'm not
going to get into geek wars with you here.
Limitations of user-based
collaborative filtering
Now, unfortunately, user-based collaborative filtering has some limitations.
When we think about relationships and recommending things based on
relationships between items and people and whatnot, our mind tends to go on
relationships between people. So, we want to find people that are similar to you
and recommend stuff that they liked. That's kind of the intuitive thing to do, but
it's not the best thing to do! The following is the list of some limitations of user-
based collaborative filtering:
One problem is that people are fickle; their tastes are always changing. So,
maybe that nice lady in the previous example had sort of a brief science
fiction action film phase that she went through and then she got over it, and
maybe later in her life she started getting more into dramas or romance
films or romcoms. So, what would happen if my Edgy Mohawk guy ended
up with a high similarity to her just based on her earlier sci-fi period, and
we ended up recommending romantic comedies to him as a result? That
would be bad. I mean, there is some protection against that in terms of how
we compute the similarity scores to begin with, but it still pollutes our data
that people's tastes can change over time. So, comparing people to people
isn't always a straightforward thing to do, because people change.
The other problem is that there's usually a lot more people than there are
things in your system, so 7 billion people in the world and counting, there's
probably not 7 billion movies in the world, or 7 billion items that you might
be recommending out of your catalog. The computational problem finding
all the similarities between all of the users in your system is probably much
greater than the problem of finding similarities between the items in your
system. So, by focusing the system on users, you're making your
computational problem a lot harder than it might need to be, because you
have a lot of users, at least hopefully you do if you're working for a
successful company.
The final problem is that people do bad things. There's a very real economic
incentive to make sure that your product or your movie or whatever it is
gets recommended to people, and there are people who try to game the
system to make that happen for their new movie, or their new product, or
their new book, or whatever.
It's pretty easy to fabricate fake personas in the system by creating
a new user and having them do a sequence of events that likes a lot
of popular items and then likes your item too. This is called a
shilling attack, and we want to ideally have a system that can deal
with that.
There is research around how to detect and avoid these shilling attacks in user-
based collaborative filtering, but an even better approach would be to use a
totally different approach entirely that's not so susceptible to gaming the system.
That's user-based collaborative filtering. Again, it's a simple concept-you look at
similarities between users based on their behavior, and recommend stuff that a
user enjoyed that was similar to you, that you haven't seen yet. Now, that does
have its limitations as we talked about. So, let's talk about flipping the whole
thing on its head, with a technique called item-based collaborative filtering.
Item-based collaborative filtering
Let's now try to address some of the shortcomings in user-based collaborative
filtering with a technique called item-based collaborative filtering, and we'll see
how that can be more powerful. It's actually one of the techniques that Amazon
uses under the hood, and they've talked about this publicly so I can tell you that
much, but let's see why it's such a great idea. With user-based collaborative
filtering we base our recommendations on relationships between people, but
what if we flip that and base them on relationships between items? That's what
item-based collaborative filtering is.
Understanding item-based
collaborative filtering
This is going to draw on a few insights. For one thing, we talked about people
being fickle-their tastes can change over time, so comparing one person to
another person based on their past behavior becomes pretty complicated. People
have different phases where they have different interests, and you might not be
comparing the people that are in the same phase to each other. But, an item will
always be whatever it is. A movie will always be a movie, it's never going to
change. Star Wars will always be Star Wars, well until George Lucas tinkers with
it a little bit, but for the most part, items do not change as much as people do. So,
we know that these relationships are more permanent, and there's more of a
direct comparison you can make when computing similarity between items,
because they do not change over time.
The other advantage is that there are generally fewer things that you're trying to
recommend than there are people you're recommending to. So again, 7 billion
people in the world, you're probably not offering 7 billion things on your website
to recommend to them, so you can save a lot of computational resources by
evaluating relationships between items instead of users, because you will
probably have fewer items than you have users in your system. That means you
can run your recommendations more frequently, make them more current, more
up-to-date, and better! You can use more complicated algorithms because you
have less relationships to compute, and that's a good thing!
It's also harder to game the system. So, we talked about how easy it is to game a
user-based collaborative filtering approach by just creating some fake users that
like a bunch of popular stuff and then the thing you're trying to promote. With
item-based collaborative filtering that becomes much more difficult. You have to
game the system into thinking there are relationships between items, and since
you probably don't have the capability to create fake items with fake ties to other
items based on many, many other users, it's a lot harder to game an item-based
collaborative filtering system, which is a good thing.
While I'm on the topic of gaming the system, another important thing is to make
sure that people are voting with their money. A general technique for avoiding
shilling attacks or people trying to game your recommender system, is to make
sure that the signal behavior is based on people actually spending money. So,
you're always going to get better and more reliable results when you base
recommendations on what people actually bought, as opposed to what they
viewed or what they clicked on, okay?
How item-based collaborative
filtering works?
Alright, let's talk about how item-based collaborative filtering works. It's very
similar to user-based collaborative filtering, but instead of users, we're looking at
items.
So, let's go back to the example of movie recommendations. The first thing we
would do is find every pair of movies that is watched by the same person. So, we
go through and find every movie that was watched by identical people, and then
we measure the similarity of all those people who viewed that movie to each
other. So, by this means we can compute similarities between two different
movies, based on the ratings of the people who watched both of those movies.
So, let's presume I have a movie pair, okay? Maybe Star Wars and The Empire
Strikes Back. I find a list of everyone who watched both of those movies, then I
compare their ratings to each other, and if they're similar then I can say these two
movies are similar, because they were rated similarly by people who watched
both of them. That's the general idea here. That's one way to do it, there's more
than one way to do it!
And then I can just sort everything by the movie, and then by the similarity
strength of all the similar movies to it, and there's my results for people who
liked also liked, or people who rated this highly also rated this highly and so on
and so forth. And like I said, that's just one way of doing it.
That's step one of item-based collaborative filtering-first I find relationships
between movies based on the relationships of the people who watched every
given pair of movies. It'll make more sense when we go through the following
example:
For example, let's say that our nice young lady in the preceding image watched
Star Wars and The Empire Strikes Back and liked both of them, so rated them
both five stars or something. Now, along comes Mr. Edgy Mohawk Man who
also watched Star Wars and The Empire Strikes Back and also liked both of
them. So, at this point we can say there's a relationship, there is a similarity
between Star Wars and The Empire Strikes Back based on these two users who
liked both movies.
What we're going to do is look at each pair of movies. We have a pair of Star
Wars and Empire Strikes Back, and then we look at all the users that watched
both of them, which are these two guys, and if they both liked them, then we can
say that they're similar to each other. Or, if they both disliked them we can also
say they're similar to each other, right? So, we're just looking at the similarity
score of these two users' behavior related to these two movies in this movie pair.
So, along comes Mr. Moustachy Lumberjack Hipster Man and he watches The
Empire Strikes Back and he lives in some strange world where he watched The
Empire Strikes Back, but had no idea that Star Wars the first movie existed.
Well that's fine, we computed a relationship between The Empire Strikes Back
and Star Wars based on the behavior of these two people, so we know that these
two movies are similar to each other. So, given that Mr. Hipster Man liked The
Empire Strikes Back, we can say with good confidence that he would also like
Star Wars, and we can then recommend that back to him as his top movie
recommendation. Something like the following illustration:
You can see that you end up with very similar results in the end, but we've kind
of flipped the whole thing on its head. So, instead of focusing the system on
relationships between people, we're focusing them on relationships between
items, and those relationships are still based on the aggregate behavior of all the
people that watch them. But fundamentally, we're looking at relationships
between items and not relationships between people. Got it?

### the data i used is from grouplens project https://grouplens.org/datasets/movielens/
