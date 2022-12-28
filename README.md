# <b><font face = 'Garamond' color = #A78A68 size=8> @we_rate_dogs Data Wrangling </font> <font face = 'Garamond' size=6>and Analysis</font></b>

<img src = "https://www.elderresearch.com/wp-content/uploads/2020/10/Data-Wrangling.bmp" width=80% height=30%>
<p>
<b><font face = 'Garamond' color = #A78A68 size=5>Introduction:</font></b><p>

<font face = 'Lucida Bright' size=3>Real-world data rarely comes clean. In this project, using Python and its libraries, I gathered data from a variety of sources and in a variety of formats, assessed its quality and tidiness, then cleaned it. This is called <font face = "Garamond" size = 4 color=#A78A68> Data Wrangling.</font></font> <p>
<font face = 'Lucida Bright' size=3>The dataset used for my wrangling (and analyzing and visualizing) efforts is the tweet archive of Twitter user [@dog_rates](https://twitter.com/dog_rates), also known as [WeRateDogs](https://en.wikipedia.org/wiki/WeRateDogs). WeRateDogs is a Twitter account that rates people's dogs with a humorous comment about the dog.</font><p>
<font face = 'Lucida Bright' size=3>I had to access some needed but missing data by querying Twitter's API using the <font size=4.5>`tweepy`</font> library, even though, I could not access the API eventually due to approval hitches, I had to manually download the data as provided by <b>Udacity</b> and did a bit of web scrapping using Python's <font size=4.5>`requests`</font> library, this is in conjuction with other basic python libraries needed to complete the workflow (eg. numpy, pandas, matplotlib, seaborn etc.). This report briefly summarizes my wrangling efforts.</font><p>
    
<b><font face = 'Garamond' color = #A78A68 size=5>Project Details:</font></b><p>
    
<font face = 'Lucida Bright' size=3>The data wrangling tasks completed in this project include:</font><p>
<font face = 'Lucida Bright' size=3>
- Gathering data 
- Assessing Data 
- Cleanig Data

<br><b><font face = 'Garamond' color = #A78A68 size=5>Gathering Data</font></b><p>
The data used for this project consisted of three different datasets that were obtained as following:

1. <b><font face = 'Garamond' color = #A78A68 size=4>Twitter archive file:</font></b> This dataset was provided by <b>Udacity</b> in the project guideline which I downloaded manually. I then uploaded it to my workspace by clicking on the jupyter icon then on upload. I imported the python's pandas library as 'pd' and used pandas' read_csv() function to read the file into a dataframe named <font face = 'Garamond' size=5>`archive`</font>.<p>

2. <b><font face = 'Garamond' color = #A78A68 size=4>Tweet image prediction file:</font></b> I imported Python's requests libraries. With the get() function of the requests library, I got the data through its url and saved it in a response variable. <br> Using Python's with open function, I wrote the response’s content to a tsv file in the same working directory. I then read the downloaded tsv file into a dataframe which I named <font face = 'Garamond' size=5>`image`</font>.<p>

3. <b><font face = 'Garamond' color = #A78A68 size=4>Tweet Json (text) file:</font></b> I was supposed to create a Twitter developer account and create an application that will give me access to missing data for the project, which I did, but, even as at the time of this report, my account is yet to be apporoved. In order to carry on with the project, I had to manually download the json (.txt) file that contains the needed data provided by <b> Udacity </b>. Reading the json file into a pandas dataframe required that I read each tweet line by line and passed it into an empty list, assessing each tweet record's line using pythons' with open function, parsing it to a file handler by iterating over each line with a for loop. When the empty dictionary had been populated with the needed data/columns (tweet_id, retweet_count, favorite_count, created_at) I then converted it to a Pandas dataframe which I named <font face = 'Garamond' size=5>`json`</font> using Pandas' pandas.Dataframe() function. I ensured to save the dataframe to a csv file.<p>

<br><b><font face = 'Garamond' color = #A78A68 size=5>Assessing Data</font></b><p>
    
Once the three datasets were gathered, I assessed the datasets as following:

- <b><font face = 'Garamond' color = #A78A68 size=4>Visual Assessment:</font></b> I printed the three dataframes in seperate cells in a Jupiter notebook and scrolled through to spot quality and tidiness issues as much as I could. To augment this visual assessment effort, I opened the csv files in an Excel spreadsheet and visually assessed the datasets for issues.<p>

- <b><font face = 'Garamond' color = #A78A68 size=4>Programmatic Assessment:</font></b> I conducted various programmatic assessments making use of various python commands and functions (eg. `.info()`, `.describe()`, `.isnull()`, `.head(),`, `.sample()`, `.duplicated()`, `.value_counts()`).</p>

Some of the issues detected with the datasets include:<p>
<b><p><font face = 'Optima' size=4 color=#A78A68>Quality issues</font></b>
    
#### The `archive` table

1. The table contained (irrelevant) data about retweets and replies (the project required that I work with only original tweets)
2. The 'expanded_url' column had missing data
3. The 'timestap' was entered in a wrong data type of object. It should have been in datetime
4. The 'tweet_id' column was also in a wrong data type. It should have been an object type instead of integer
5. Invalid (outrageous) 'rating_numerator' and 'rating_denominator' values detected
6. Some Dog names was invalidly entered as "None", "a", "an", "such", "the", "quite" etc.

#### The `image` table
7. Non-descriptive column names (eg. p1, p1_conf, p1_dog, p2, p2_conf, p2_dog, p3, p3_conf, p3_dog)
8. p1, p2, and p3 columns had their values entered in inconsistent formats (lower and proper cases in the same columns)
9. The 'tweet_id' column was in a wrong data type (integer instead object, for the sake of consistency)

#### The `json` table
10.  The 'tweet_id' column was entered in a wrong data type (integer instead object, for the sake of consistency across tables)<p>

<br><b><font face = 'Garamond' color = #A78A68 size=5>Cleaning Data</font></b><p>
    
<font face = 'Lucida Bright' size=3> After detecting some issues with the datasets, I approached cleaning following a predefined</font> `define`, `code`, `test` <font face = 'Lucida Bright' size=3>framework which guided how I;</font><p>
- `define:` describe the quality or tidiness issue detected with a particular dataset<p>
- `code:` write python commands with an attempt to clean the detected issue and make the data conform to the rules of [tidy data](https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html)<p>
- `test:` check if my cleaniing efforts were truly effected, and that the issue previously detected had been resolved<p> 
    
#### Generally, the steps I took to clean the datasets are summarised below:
    

1. Firstly, I made a copy of each of the original datasets using the `.copy()` method
2. Next, I removed data about retweets and replies from the archive table - since I was to work with only original tweets. To achieve this, I;
> - subset the dataframe for empty rows in the irrelevant columns using the `isnull()` method to access empty rows in the columns
> - then, I dropped (irrelevant) columns about retweet and replies using the `.drop()` method
3. After which I dropped missing rows from the expanded_urls column using the `dropna()` method
4. Next, I Converted the *timestamp* column in the `archive_clean` dataframe from **object** to **datetime** calling Pandas' `to_datetime()` function
5. After that, I changed the tweet_id columns in all three tables from int64 datatype to object datatype using `as_type(str)` on the columns affected
6. Next, I dropped rows with outrageous values in the rating_numerator and rating_denominator columns of the `archive` table. I set the boundary of acceptable values to between 1 and 20 and subset the dataframe for records only where the rating_numerator and rating_denominators fall between 1 and 20.
7. Next, I dealt with invalid dog names in the `archive_clean` table (which I guessed were missing entries represented by a random word, but I couldn't confirm this despite the hours spent on researching this issue). But due to their large number, I couldn't drop them. Rather, I replaced every instance of an invalid name with "None" which was the best alternative I could think of.<br> To achieve this, firstly I discovered a useful hint while assessing the data to track the invalid names, and that is that all such names began with a lower case character. So, I used that property to track all invalid names. Then, I wrote a **for** loop to track, pick, and append every invalid name to an empty list I had previously created. Next, i used the `.replace()` method to replace every invalid name in the list with the character ***"None"***
8. After that, I renamed non-descriptive columns (eg. p1, p1_conf, p1_dog, p2, p2_conf, p2_dog, p3, p3_conf, p3_dog) to something more assessible to non-technical minds using... **You guessed right!** the `.rename()` method
9. I then changed how p1, p2, and p3 columns have their values entered in inconsistent formats (lower and proper cases in the same columns) and changed all rows to the same ***proper case*** using the `.title()` method
10. After all these were done, I then flattened the four wide columns in the `archive` table (doggo, floofer, pupper, puppo) which contained data about just one variable (dog_stage) and needed to be unpivoted if the data would conform to the rules of [tidy data](https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html) as propounded by [Hadley Wickham](https://en.wikipedia.org/wiki/Hadley_Wickham).
11. Finally, I merged the three dataframes to one master dataframe on the column they had in common - `tweet_id`.

<br><b><font face = 'Garamond' color = #A78A68 size=5>Storing the Data</font></b><p>
After gathering, assessing and cleaning the data, I then stored the merged data in a csv file named `twitter_archive_master.csv.`

#### NB: Click and open the ***`wrangle&analyze.ipynb`*** file to view the notebook for the project
