# Guess The State Trick
Have you seen the Rick Lax (aka the "Deception Expert") trick where he guesses which state you are thinking? If not, watch the trick performed [here](https://www.facebook.com/DeceptionExpert/videos/525098757671982/).

So did he correctly guess your state? There is actually a _very_ good chance that he got it right, and you may have already figured out why.

When he starts the trick, he has a 1 in 50 or 2% chance of guessing correctly (or more if he figures in uncommon states vs. well known, bigger states).

At this point, he just needs to pick the correct element of this list:
```{scala}
List("Alabama", "Alaska", "Arizona", "Arkansas", "California", "Colorado", "Connecticut", "Delaware", "Florida",
"Georgia", "Hawaii", "Idaho", "Illinois", "Indiana", "Iowa", "Kansas", "Kentucky", "Louisiana", "Maine", 
"Maryland", "Massachusetts", "Michigan", "Minnesota", "Mississippi", "Missouri", "Montana", "Nebraska", 
"Nevada", "New Hampshire", "New Jersey", "New Mexico", "New York", "North Carolina", "North Dakota", 
"Ohio", "Oklahoma", "Oregon", "Pennsylvania", "Rhode Island", "South Carolina", "South Dakota", "Tennessee",
"Texas", "Utah", "Vermont", "Virginia", "Washington", "West Virginia", "Wisconsin", "Wyoming")
```

Next Rick asks you to think about the last letter of your state. As it happens, all 50 states share the same 12 final letters. This means that if Rick were to guess the final letter of your state, he would have improved his chance of guessing it correctly to 1 in twelve (roughly). 

So really he only needs to pick the correct element of this list:
```{scala}
List('a', 'd', 'e', 'g', 'h', 'i', 'k', 'n', 'o', 's', 't', 'y')
```

Finally, Rick adds one more level of complication (which actually makes the trick a lot easier for him). He assigns the colors Red, White, and Blue to a set of letters. He then announces that he will be guessing the color which corresponds to the final letter of your state.

![Letter Colors](https://github.com/EvanOman/GuessTheStateTrick/blob/master/colors.PNG)

Here is where he really cements his advantage. While it may seem like the colors are assigned randomly, it turns out that 47 states belong to the red group while only 2 states belong to white group and 2 states belong to the blue group (they share Utah).

Thus Rick has to choose between 3 groups, one of which accounts for 47 or 94% of the states, while the other two groups only account for 6% of the states.

Additionally, Rick used New York and Utah as examples during his presentation, meaning that a lot of people would probably filter these out (intentionally or unintentionally) leaving only 48 states to choose from, 47 of which are covered by his red group of letters.

So in the end Rick has about a 94% chance of guessing the color which matches your state, but an even higher percentage if you either filtered out Utah and New York or haven't been to Utah lately. Thus the structure of the trick forces Rick to choose the correct state just about every time, regardless of any supernatural powers he may possess.

Now if he picked the wrong state every time, that would be impressive...

If you are interested in how computer programming can be used to aid the analysis above, check out [this notebook](http://www.evanoman.com/GuessTheState.html) which quickly finds the number of unique state-name-final-characters and the number of states in each of the red, white, and blue groups.
