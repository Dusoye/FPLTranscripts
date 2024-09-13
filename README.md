## Text analysis on Fantasy Football video transcripts

No one has time now adays to listen through the podcasts or youtube videos for the dozens of content creators out there, so this extracts the transcripts since the last gameweek and summarises their findings. Initially this will just be youtube transcripts as there doesn't appear to be a way to automate extracting transcripts through either Apple or Spotify podcasts. 

The YouTube API is used to extract both the channel_id's and video_id's from each of a given set of content creators, and then the YouTubeTranscriptApi will attempt to extract the transcripts for each video after a specified time (last gameweek). Summarisation will then either be done using Facebook's BART model and tokeniser (bart-large-cnn) or by plugging it into Claude API. 

The maximum token length using BART is 1024, so chunking the transcripts will be required even after preprocessing. Whereas the maximum token length through Claude will be 100,000 (including prompt) so chunking shouldn't be necessary. Preprocessing includes removing automated tags such as [music] or [applause], along with filler words such as "basically" and "I mean". More can be done to reduce the token count by creating abbreviations for common terms, for example replacing "fantasy premier league" with "fpl", but a balance needs to be made between stripping out tokens but maintaining context.

There are obvisouly going to be some issues with the automated speach-to-text transcripts that are generated by youtube, especially with regards to player names which are unlikley to be accurately transcribed, which is another area where the Claude API is likely to outperform BART.

Below shows a an example week for a set of youtubers, displaying the word count stats along with the reduction seen after preprocessing the transcripts.

| channel_name         |   word_count_mean |   word_count_max |   word_count_sum |   num_videos |   word_count_process_mean |   word_count_process_max |   word_count_process_sum |   percent_reduction |
|:---------------------|------------------:|-----------------:|-----------------:|------------:|--------------------------:|-------------------------:|------------------------:|---------------------:|
| fantasyfootballfixYT  |              3881 |             7224 |            19405 |           5 |                    3714.6 |                     6702 |                   18573  |              4 |
| alwayscheating        |             15940.5|            18387 |            63762 |           4 |                   14316.8 |                    16483 |                   57267  |             10 |
| elitefpl              |             10317  |            12072 |            30951 |           3 |                    9773   |                    11432 |                   29319  |              5 |
| AboveAverageFPL       |             14401  |            16072 |            28802 |           2 |                   13386.5 |                    15097 |                   26773  |              7 |
| FFScout_              |              9945.5|            10001 |            19891 |           2 |                    9368.5 |                     9446 |                   18737  |              5 |
| FPLBlackBox           |             15252  |            27897 |            30504 |           2 |                   14131   |                    25788 |                   28262  |              7 |
| FPLFocal              |              2209  |             2428 |             4418 |           2 |                    2194.5 |                     2414 |                    4389  |              0 |
| TheArmbandFPL         |             13227  |            13294 |            26454 |           2 |                   12033   |                    12090 |                   24066  |              9 |
| fplblackbox           |             15252  |            27897 |            30504 |           2 |                   14131   |                    25788 |                   28262  |              7 |
| FMLFPL                |             18514  |            18514 |            18514 |           1 |                   16396   |                    16396 |                   16396  |             11 |
| fplbanger             |             10304  |            10304 |            10304 |           1 |                    9557   |                     9557 |                    9557  |              7 |