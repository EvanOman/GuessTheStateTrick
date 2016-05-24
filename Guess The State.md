

```scala211
import scala.collection.mutable.MutableList
def runAnalysis(): Unit =
{
    /* List of all 50 States */
    val states = Seq("Alabama", "Alaska", "Arizona", "Arkansas", "California", "Colorado", "Connecticut", "Delaware", "Florida","Georgia", "Hawaii", "Idaho", "Illinois", "Indiana", "Iowa", "Kansas", "Kentucky", "Louisiana", "Maine", "Maryland", "Massachusetts", "Michigan", "Minnesota", "Mississippi", "Missouri", "Montana", "Nebraska", "Nevada", "New Hampshire", "New Jersey", "New Mexico", "New York", "North Carolina", "North Dakota", "Ohio", "Oklahoma", "Oregon", "Pennsylvania", "Rhode Island", "South Carolina", "South Dakota", "Tennessee", "Texas", "Utah", "Vermont", "Virginia", "Washington", "West Virginia", "Wisconsin", "Wyoming")

    /* These are the (distinct) letters associated with each color from Jack's video */
    val redChars = List('a', 'y', 'd', 'o', 's', 't', 'e', 'i', 'y', 'd', 'n').distinct
    val whiteChars = List('b', 'f', 'h', 'h', 'w', 'k', 'l', 'p', 'r', 'v', 'z').distinct
    val blueChars = List('c', 'g', 'x', 'j', 'm', 'q', 'u', 'x', 'c', 'h').distinct

    /* 
        The "stateMap" object will be a mapping from characters to states with that character as the 
        last letter
        For example, stateMap('y') will eventually contain List("Kentucky", "New Jersey"), the states that end 
        in a 'y'
    */
    val stateMap = collection.mutable.Map[Char, MutableList[String]]()

    /*
        We will initialize stateMap by setting each element of the alphabet to an empty List
        So right now now stateMap('y') will contain List(), an empty list
    */
    ('a' to 'z').foreach(stateMap(_) = MutableList())

    /* 
        Populates the stateMap by adding each state to list corresponding to its final char
        The final char is obtained by the bit: state.charAt(state.size - 1)
    */
    states.foreach(state => stateMap(state.charAt(state.size - 1)) += state)
    
    /* 
        Filters out letters with no associated state-ending, prints them
            - Scala stores maps as collections of (k, v) tuples, this filter removes (k, v) pairs where
            the second element, corresponding to the list of states, is empty
            - We then map each (k, v) tuple to just k, the key (ie the character)
            - Thus we are getting those keys which map to a non-empty list
    */
    val stateLastLetters = stateMap.filter(x => x._2.size > 0).map(x => x._1).toList.sorted
    val numLastLetters = stateLastLetters.size
    println(s"All 50 states share the same $numLastLetters final letters: $stateLastLetters\n\n")

    /*
        Now we can aggregate the states associated with each color
            - Here the List.map function plugs each element of the list into the stateMap, returning the list
            of states for each char in the red/white/blue collections
            - After the map operation we have a list of lists, the List.reduce(_++_) simply combines this list
            of lists into a single lists (by concatenating them all together)
            - We then use List.distinct to remove duplicates and then use List.sorted to sort
            the states alphabetically
    */
    val redStates = redChars.map(stateMap).reduce(_++_).distinct.toList.sorted
    val whiteStates = whiteChars.map(stateMap).reduce(_++_).distinct.toList.sorted
    val blueStates = blueChars.map(stateMap).reduce(_++_).distinct.toList.sorted
    
    /* Grabs the number of states associated with each color */
    val redCount = redStates.size
    val whiteCount = whiteStates.size
    val blueCount = blueStates.size

    /* Now we print out the states are associated with each color: */
    println(s"There are $redCount Red States, they are:\n$redStates\n\n")
    println(s"There are $whiteCount White States, they are:\n$whiteStates\n\n")
    println(s"There are $blueCount Blue States, they are:\n$blueStates\n\n")
}
```


    [32mimport [36mscala.collection.mutable.MutableList[0m
    defined [32mfunction [36mrunAnalysis[0m



```scala211
runAnalysis()
```

    All 50 states share the same 12 final letters: List(a, d, e, g, h, i, k, n, o, s, t, y)
    
    
    There are 47 Red States, they are:
    List(Alabama, Alaska, Arizona, Arkansas, California, Colorado, Connecticut, Delaware, Florida, Georgia, Hawaii, Idaho, Illinois, Indiana, Iowa, Kansas, Kentucky, Louisiana, Maine, Maryland, Massachusetts, Michigan, Minnesota, Mississippi, Missouri, Montana, Nebraska, Nevada, New Hampshire, New Jersey, New Mexico, North Carolina, North Dakota, Ohio, Oklahoma, Oregon, Pennsylvania, Rhode Island, South Carolina, South Dakota, Tennessee, Texas, Vermont, Virginia, Washington, West Virginia, Wisconsin)
    
    
    There are 2 White States, they are:
    List(New York, Utah)
    
    
    There are 2 Blue States, they are:
    List(Utah, Wyoming)
    
    



    



```scala211
/* Condensed version */
import scala.collection.mutable.MutableList
def runAnalysis2(): Unit =
{
    /* List of states to check */
    val states = Seq("Alabama", "Alaska", "Arizona", "Arkansas", "California", "Colorado", "Connecticut", "Delaware", "Florida",
                 "Georgia", "Hawaii", "Idaho", "Illinois", "Indiana", "Iowa", "Kansas", "Kentucky", "Louisiana", "Maine", 
                 "Maryland", "Massachusetts", "Michigan", "Minnesota", "Mississippi", "Missouri", "Montana", "Nebraska", 
                 "Nevada", "New Hampshire", "New Jersey", "New Mexico", "New York", "North Carolina", "North Dakota", 
                 "Ohio", "Oklahoma", "Oregon", "Pennsylvania", "Rhode Island", "South Carolina", "South Dakota", "Tennessee",
                 "Texas", "Utah", "Vermont", "Virginia", "Washington", "West Virginia", "Wisconsin", "Wyoming")

    /* List of (distinct) letters associated with each color */
    val redChars = List('a', 'y', 'd', 'o', 's', 't', 'e', 'i', 'y', 'd', 'n').distinct
    val whiteChars = List('b', 'f', 'h', 'h', 'w', 'k', 'l', 'p', 'r', 'v', 'z').distinct
    val blueChars = List('c', 'g', 'x', 'j', 'm', 'q', 'u', 'x', 'c', 'h').distinct

    /* A map/dictionary to facillitate our last letter -> state mapping */
    val stateMap = collection.mutable.Map[Char, MutableList[String]]()

    /* Initialially maps each char to an empty, mutable list*/
    ('a' to 'z').foreach(stateMap(_) = MutableList())

    /* Populates the state map by mapping each state to its last char */
    states.foreach(state => stateMap(state.toList.takeRight(1)(0)) += state)
    
    /* Figures out how many different final chars there are */
    val stateLastLetters = stateMap.filter(x => x._2.size > 0).map(x => x._1).toList.sorted
    val numLastLetters = stateLastLetters.size
    println(s"All 50 states share the same $numLastLetters final letters: $stateLastLetters\n\n")

    /* Now we can aggregate the states associated with each color */
    val redStates = redChars.map(stateMap).reduce(_++_).distinct.toList.sorted
    val whiteStates = whiteChars.map(stateMap).reduce(_++_).distinct.toList.sorted
    val blueStates = blueChars.map(stateMap).reduce(_++_).distinct.toList.sorted
    
    val redCount = redStates.size
    val whiteCount = whiteStates.size
    val blueCount = blueStates.size

    /* Now we can see which states are associated with each color: */
    println(s"There are $redCount Red States, they are:\n$redStates\n\n")
    println(s"There are $whiteCount White States, they are:\n$whiteStates\n\n")
    println(s"There are $blueCount Blue States, they are:\n$blueStates\n\n")
}
```


    [32mimport [36mscala.collection.mutable.MutableList[0m
    defined [32mfunction [36mrunAnalysis2[0m

