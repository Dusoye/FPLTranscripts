## Text analysis on Fantasy Football video transcripts

No one has time now adays to listen through the podcasts or youtube videos for the dozens of content creators out there, so this extracts the transcripts since the last gameweek and summarises their findings. Initially this will just be youtube transcripts as there doesn't appear to be a way to automate extracting transcripts through either Apple or Spotify podcasts.

The YouTube API is used to extract both the channel_id's and video_id's from each of a given set of content creators, and then the YouTubeTranscriptApi will attempt to extract the transcripts for each video after a specified time (last gameweek). I'll then plug the transcripts into either Claude or ChatGPT API to summarise.