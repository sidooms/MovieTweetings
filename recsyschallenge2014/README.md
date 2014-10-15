#The RecSys Challenge 2014 Dataset

This dataset is an extended version of the MovieTweetings dataset. So data also originated from users of the IMDb iOS app that rated movies and shared the rating on Twitter. By querying the Twitter API on a daily basis for tweets containing the keywords '*I rated #IMDb*', tweets were collected and relevant information was extracted. For more information on the MovieTweetings dataset see [this github website](https://github.com/sidooms/MovieTweetings), [this slideshare presentation](http://www.slideshare.net/simondooms/movie-tweetings-a-movie-rating-dataset-collected-from-twitter) or [this paper](http://crowdrec2013.noahlab.com.hk/papers/crowdrec2013_Dooms.pdf).

The dataset was used in the ACM RecSys Challenge 2014 which focused on *user engagement as evaluation*. Please cite the following papers if you make use of this dataset. Some introduction slides about the dataset and the challenge are available on [slideshare](http://www.slideshare.net/simondooms/rec-syschallenge2014intro). For more information about the challenge we refer to the [ACM RecSys Challenge 2014 website](http://2014.recsyschallenge.com).

    @inproceedings{Said:2014:RSC:2645710.2645779,
    author = {Said, Alan and Dooms, Simon and Loni, Babak and Tikk, Domonkos},
    title = {Recommender Systems Challenge 2014},
    booktitle = {Proceedings of the 8th ACM Conference on Recommender Systems},
    series = {RecSys '14},
    year = {2014},
    isbn = {978-1-4503-2668-1},
    location = {Foster City, Silicon Valley, California, USA},
    pages = {387--388},
    numpages = {2},
    url = {http://doi.acm.org/10.1145/2645710.2645779},
    doi = {10.1145/2645710.2645779},
    acmid = {2645779},
    publisher = {ACM},
    address = {New York, NY, USA},
    keywords = {benchmarking, challenge, competition, context-aware, dataset, recommender systems},
    } 

    @conference{Dooms13crowdrec,
    author = {Dooms, Simon and De Pessemier, Toon and Martens, Luc},
    title = {MovieTweetings: a Movie Rating Dataset Collected From Twitter},
    booktitle = {Workshop on Crowdsourcing and Human Computation for Recommender Systems, CrowdRec at RecSys 2013},
    year = {2013}
    }

In its original form MovieTweetings contained only user ids, item ids, ratings and timestamps similar to the well-known MovieLens dataset. For the challenge however, all of the metadata of the tweets (as provided by the [Twitter API](https://dev.twitter.com/docs/api/1.1/get/statuses/show/%3Aid)) was provided, allowing us to focus on the *engagement* of the ratings in the form of *retweet* and *favorites* counts. The goal of the challenge was to rank the tweets (for each user) by engagement which was defined as being the sum of the number of retweets and favorites obtained by a tweet. 

#Statistics

    ----------------------------------------------------------------------------
    Dataset    | Users  | Items  | Tweets  | Tweets published between           
    ----------------------------------------------------------------------------
    Training   | 22,079 | 13,618 | 170,285 | 28/02/2013 14:43 - 8/01/2014 22:06 
    Test       | 5,717  | 4,226  | 21,285  | 8/01/2014 22:06 - 11/02/2014 15:49 
    Evaluation | 5,514  | 4,559  | 21,287  | 11/02/2014 15:49 - 24/03/2014 9:57 
    ----------------------------------------------------------------------------
    All        | 24,924 | 15,142 | 212,857 | 28/02/2013 14:43 - 24/03/2014 9:57 
    ----------------------------------------------------------------------------

#The Data files

For the challenge, the dataset was chronologically split in three subsets: training set, test set and evaluation set, as illustrated in the following figure.

![Dataset split in train, test, and evaluation set](dataset_split.png)

The training set consists of the first 80% tweets and could be used as input for the training of models and predictive algorithms. The test and evaluation sets both contain 10% of the remaining tweets and were used for the weekly evaluation by participants (test set) or for the final evaluation by the organizers (evaluation set).

##The training set (for training)
Consists of 1 file: **training.dat**. The file is CSV formatted with every line containing the following information:

twitter user id,IMDb item id,rating,scraping timestamp,tweet data

<table>
    <tr>
        <td>Twitter user id</td>
        <td>The actual twitter user id.</td>
    </tr>
    <tr>
        <td>IMDb item id</td>
        <td>The id of the rated movie, id is the actual IMDb id as used in the URL: www.imdb.com/title/ttxxx/</td>
    </tr>
    <tr>
        <td>Rating</td>
        <td>The numeric rating on a 10-star scale, extracted from the tweet text.</td>
    </tr>
    <tr>
        <td>Scraping timestamp</td>
        <td>A linux timestamp indicating the moment the Twitter API was queried for the tweet information. So it is not the posting time of the tweet itself but rather the moment at which the data of the tweet was collected. This may be important to take into account since it reflects how long the tweet has been *online* and may therefore influence the number of retweets or favorites (the longer a tweet has been online, the more its exposure).</td>
    </tr>
    <tr>
        <td>Tweet data</td>
        <td>The tweet metadata in JSON format. Includes all data available through the Twitter API except for the tweet text itself (set to empty string).</td>
    </tr>
</table>

The retweet and favorite information can be found in the tweet data as the fields: *retweet_count* and *favorite_count*. The following is an example of one line of the training dataset:

    296041028,0444778,8,1391030896,{"contributors": null, "truncated": false, "text": "", "in_reply_to_status_id": null, "id": 307139025897152512, "favorite_count": 0, "source": "<a href=\"http://itunes.apple.com/us/app/imdb-movies-tv/id342792525?mt=8&uo=4\" rel=\"nofollow\">IMDb Movies & TV on iOS</a>", "retweeted": false, "coordinates": null, "entities": {"symbols": [], "user_mentions": [], "hashtags": [{"indices": [48, 53], "text": "IMDb"}], "urls": [{"url": "http://t.co/oSoACtR7Pb", "indices": [25, 47], "expanded_url": "http://www.imdb.com/title/tt0444778", "display_url": "imdb.com/title/tt0444778"}]}, "in_reply_to_screen_name": null, "id_str": "307139025897152512", "retweet_count": 0, "in_reply_to_user_id": null, "favorited": false, "user": {"follow_request_sent": false, "profile_use_background_image": true, "id": 296041028, "verified": false, "profile_text_color": "333333", "profile_image_url_https": "https://pbs.twimg.com/profile_images/3635577628/2fded110fafbe2389f074fc50831a59e_normal.jpeg", "profile_sidebar_fill_color": "EFEFEF", "is_translator": false, "geo_enabled": true, "entities": {"description": {"urls": []}}, "followers_count": 114, "protected": false, "location": "\u0e17\u0e35\u0e48\u0e40\u0e14\u0e34\u0e21~", "default_profile_image": false, "id_str": "296041028", "lang": "en", "utc_offset": 25200, "statuses_count": 47133, "description": "They said I could be anything.. So I became your Friend.// Mr.149", "friends_count": 474, "profile_link_color": "000000", "profile_image_url": "http://pbs.twimg.com/profile_images/3635577628/2fded110fafbe2389f074fc50831a59e_normal.jpeg", "notifications": false, "profile_background_image_url_https": "https://si0.twimg.com/profile_background_images/810193743/85c3b06e5a58288065117440931884a3.jpeg", "profile_background_color": "FFFFFF", "profile_banner_url": "https://pbs.twimg.com/profile_banners/296041028/1367973819", "profile_background_image_url": "http://a0.twimg.com/profile_background_images/810193743/85c3b06e5a58288065117440931884a3.jpeg", "name": "\u0e21\u0e34\u0e2a\u0e40\u0e15\u0e2d\u0e23\u0e4c\u0e1a\u0e25\u0e39\u0e02\u0e2d\u0e1a\u0e32\u0e22\u0e2a\u0e4c\u2667", "is_translation_enabled": false, "profile_background_tile": true, "favourites_count": 679, "screen_name": "Nat_ta_gun", "url": null, "created_at": "Tue May 10 03:03:19 +0000 2011", "contributors_enabled": false, "time_zone": "Bangkok", "profile_sidebar_border_color": "000000", "default_profile": false, "following": false, "listed_count": 2}, "geo": null, "in_reply_to_user_id_str": null, "possibly_sensitive": false, "lang": "en", "created_at": "Thu Feb 28 14:43:44 +0000 2013", "in_reply_to_status_id_str": null, "place": null}

##The test set (for weekly progress)

Consists of 3 files: **test.dat**, **test_empty.dat**, **test_solution.dat**

###test.dat 
The same structure as the training set, so CSV formatted, one line per tweet and the datafields: twitter user id, IMDb item id, rating, scraping timestamp and tweet data. This file contains the 10% tweets chronologically occuring after the 80% training tweets. 

###test_empty.dat
Again similarly structured as the **test.dat** and **training.dat** files, but here the important tweet data fields *favorite_count* and *retweet_count* have been cleared (i.e., set to empty string). This file is the task file i.e., it contains all tweets and users for which the engagement (=favorite\_count \+ retweet\_count) must be ranked (for the weekly evaluation).


###test_solution.dat
The solution file for the **test_empty.dat** file. It reflects what the result should be, given the **test_empty.dat** file. The file is CSV formatted with every line containing the following information:

userid,tweetid,engagement

<table>
    <tr>
        <td>Userid</td>
        <td>The Twitter userid.</td>
    </tr>
    <tr>
        <td>Tweetid</td>
        <td>The id of the tweet itself. Can be found in the tweet data as the *id* field (e.g., 307139025897152512 in the above example tweet JSON data).</td>
    </tr>
    <tr>
        <td>Engagement</td>
        <td>The sum of the two fields: *favorite_count* and *retweet_count*, indicating the engagement of the tweet.</td>
    </tr>
</table>

The file is sorted on userid (descending), then on engagement (descending), then on tweetid (descending). It contains all users contained in the **test_empty.dat** file and ranks all contained tweets by engagement. The weekly evaluation score was calculated by comparing this file with your own solution using the nDCG [RecSysChallenge Evaluator](https://github.com/recsyschallenge/RSChallengeEval/releases).

##The evaluation set (for final evaluation)
The evaluation set consists of the final 10% of the tweets used in the challenge. Its tweets were posted chronologically after the ones contained in the training and test sets. At the end of the challenge, particpants were provided with an **evaluation_empty.dat** file (structured similarly as the **test_empty.dat** file) and requested to generate a solution file (structured as **test_solution.dat**) which was evaluated against the **evaluation_solution.dat** by the organizers to calculate the final score. The **evaluation_solution.dat** file was of course kept private.

#Python example code

Here's some Python code that helps with the processing of the dataset. It reads the **training.dat** file and creates a List structure that contains the information.


    import json
    def read_the_dataset(the_dataset_file):
        tweets = list()
        header = True
        with file(the_dataset_file,'r') as infile:
            for line in infile:
                if header:
                    header = False
                    continue #skip the CSV header line
                line_array = line.strip().split(',')
                user_id = line_array[0]
                item_id = line_array[1]
                rating = line_array[2]
                scraping_time = line_array[3]
                tweet = ','.join(line_array[4:]) # The json format also contains commas
                json_obj = json.loads(tweet) # Convert the tweet data string to a JSON object
                #Use the json_obj to easy access the tweet data
                #e.g. the tweet id: json_obj['id']
                #e.g. the retweet count: json_obj['retweet_count']
                tweets.append((user_id, item_id, rating, scraping_time, json_obj))
        return tweets

Here's a complete script reading the training set, _empty file and generating a solution file. Engagement is determined by the random generator. This approach did not win the challenge obviously, but it may serve as an example.

    import json
    import random
    
    def read_the_dataset(the_dataset_file):
        tweets = list()
        header = True
        with file(the_dataset_file,'r') as infile:
            for line in infile:
                if header:
                    header = False
                    continue # Skip the CSV header line
                line_array = line.strip().split(',')
                user_id = line_array[0]
                item_id = line_array[1]
                rating = line_array[2]
                scraping_time = line_array[3]
                tweet = ','.join(line_array[4:]) # The json format also contains commas
                json_obj = json.loads(tweet) # Convert the tweet data string to a JSON object
                # Use the json_obj to easy access the tweet data
                # e.g. the tweet id: json_obj['id']
                # e.g. the retweet count: json_obj['retweet_count']
                tweets.append((user_id, item_id, rating, scraping_time, json_obj))
        return tweets
        
    def read_todo_from_emtpy_file(the_dataset_file):
        todos = list()
        header = True
        with file(the_dataset_file,'r') as infile:
            for line in infile:
                if header:
                    header = False
                    continue # Skip the CSV header line
                line_array = line.strip().split(',')
                tweet = ','.join(line_array[4:]) # The json format also contains commas
                json_obj = json.loads(tweet) # Convert the tweet data string to a JSON object
                user_id = line_array[0]
                tweet_id = json_obj['id']
                todos.append((user_id,tweet_id)) # The todo (user,tweet) pair
        return todos

    def write_the_solution_file(solutions, the_solution_file):
        lines = list()
        lines.append('userid,tweetid,engagement' + '\n')
        # Prepare the writing...
        for (user,tweet,engagement) in solutions:
            line = str(user) + ',' + str(tweet) + ',' + str(engagement) + '\n'
            lines.append(line)
        # Actual writing
        with file(the_solution_file,'w') as outfile:
            outfile.writelines(lines)
    
    # Execution flow starts here ...
    if __name__ == "__main__":
        # Read the training file
        tweets = read_the_dataset('training.dat')
    
        # Read the _empty file (the task)
        todos = read_todo_from_emtpy_file('test_empty.dat')
    
        # For all (user,tweet) pairs, generate their engagement
        solutions = list()
        random.seed(1)
        for (user,tweet) in todos:
            # Random guess the engagement between 0-50
            engagement = random.randint(0,50)
            solutions.append((user,tweet,engagement))
    
        # Sort the solutions on user id (desc), engagement (desc) and tweet id (desc)
        solutions = sorted(solutions, key=lambda data: (-int(data[0]), -int(data[2]), -int(data[1])))
    
        # Write the _solution file
        write_the_solution_file(solutions, 'random_solution.dat')
    
        print 'done.'
    

That's it! Remember to follow me on [Twitter](https://twitter.com/sidooms) and tell me how much you like this. By the way, if you liked this you might also like my other Github projects: [Twitter-ratings](https://github.com/sidooms/Twitter-ratings) and [Recsys-frontend](https://github.com/sidooms/Recsys-frontend).
