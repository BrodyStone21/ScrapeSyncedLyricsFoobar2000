# ScrapeSyncedLyricsFoobar2000
Backup of guide from Reddit on how to scrape synchronized lyrics using Foobar2000. All credit goes to original creator u/filthbeast on Reddit. 

I have a method for scraping lyrics into my files that works well due to the recent source scripts that have become available. It was a pain to narrow down my procedure and which scripts should be used and in which order. I want to save others that are interested in doing the same sort of thing for their collections as much hassle as I can. I tried to explain the reasoning behind the steps as much as possible so you can understand what I've learned and alter for your desired results. If anyone has ideas to make this procedure better that'd be great!

# GOAL
To batch download as many lyrics into the track tags as possible. Get both non-synced and synced lyrics - mapped to different tags - for maximum compatibility with various applications.

# SETUP
In foobar2000, use Lyrics Show 3 Panel and install Veksho's multi lyric source plugin. Lyrics Show 3 Panel adds a Download lyrics... option to the right-click menu of the tracks so that you can batch download lyrics when multiple tracks are selected, which is the main reason I use it rather than ESLyric.

In the Lyric Show 3 preferences go to the 'Lyric Saving' tab and check 'Enable automatic save' (I don't check 'Only save synced lyrics automatically').
Save Method: Save to tag
Synced lyric tag: SYNCED LYRICS
### NOTE: 
There was discussion on another thread about why to use this name for the tag, since it isn't standardized. It's not necessary to use it, but unless you have a reason to change it just go with it.
non-synced lyric tag: LYRICS
# FIRST PASS
Go to the Lyric Searching tab. Select 'Search for this type of lyric: Only synced (you'll change this later after all available synced lyrics are found, but the first run-through just get synced ones).

### NOTE: 
For some reason 'Search for this type of lyric:' Prefer synced doesn't actually prefer and grab synced lyrics when non-synced lyrics are available, so don't use that option.
The following search order includes only the sources that can actually provide synced lyrics.

#Tag Search (search ends here if tag is populated, otherwise goes to the next source)
I go into the 'Tag Search' Properties and for 'Read lyrics from these tags:' put only SYNCED LYRICS . The reason for this is that I may have good lyrics in the LYRICS tag from earlier scraping attempts and I don't want that tag being checked during the search or it will disregard whatever synced lyrics it finds! As the Note on the Lyric Saving tab says: "The automatic save will not overwrite existing lyrics' - but this is triggered even if they are found in a different tag than you're saving to! But for some reason, this step doesn't need to be changed for the second pass when you are searching for non-synced lyrics...
Multi DB: MiniLyrics
### NOTE: 
in 'properties' I like to check Insert URL into lyric body so that later I know the source - checking it in any source will apply the setting to all sources in the list. (Minilyrics URLs show as crintsoft.com)
Multi DB: QQ Music
Multi DB: MusixMatch
A great source, but will only allow a small amount of retrievals before denying access, so move it to the top of the source list for typical usage after batch scraping. See MusixMatch API section below.
Select all the files in your tracklist (CTRL-A) -> right-click the selection -> Download Lyrics... -> Start Search.

# SECOND PASS
You could use something like Mp3tag to sort by the LYRICS tag so if you already have lyrics for a track you don't need to add it to the tracklist for batch scraping.

To get non-synced lyrics select 'Search for this type of lyric:' Only non-synced

Then make the search order:

Tag Search (search ends here if tag is populated, otherwise goes to the next source)
Multi DB: MiniLyrics
Multi DB: QQ Music
Multi DB: Genius
DO NOT USE Genius during the synced lyric scraping first step above as it will put non-synced lyrics in the synced tag!

Multi DB: LoloLyrics
Multi DB: AZLyrics
I haven't had much luck with AZLyrics or DarkLyrics so not sure if one should be higher in the list than the other.

Multi DB: DarkLyrics
Multi DB: MusixMatch
A great source, but will only allow a small amount of retrievals before denying access, so move it to the top of the source list for typical usage after batch scraping. See MusixMatch API section below.

Associations search
Select all the files in your tracklist (CTRL-A) -> right-click the selection -> Download Lyrics... -> Start Search.

# TYPICAL USAGE
When you're done scraping all the lyrics and just want them to show up after all your hard work:

Go back into the 'Tag Search' Properties and for 'Read lyrics from these tags:' put SYNCED LYRICS;LYRICS so that lyrics from either tag will show in the panel. Because SYNCED LYRICS is first it has priority.

Edit source list:

Tag Search (search ends here if tag is populated, otherwise goes to the next source)
Multi DB: MusixMatch (see MusixMatch API key section below)
Multi DB: MiniLyrics
Multi DB: QQ Music
Multi DB: LoloLyrics
Multi DB: AZLyrics
I haven't had much luck with AZLyrics or DarkLyrics so not sure if one should be higher in the list than the other.
Multi DB: DarkLyrics
Associations Search
On the 'Lyric Searching' panel apply 'Search for this type of lyric:' No preference because then if no synced lyrics exist but non-synced ones do, they will appear right away without wasting time doing a search to populate the other tag. It will show the contents of the SYNCED LYRICS tag if both are available because it was listed first in the previous step.

I keep Genius off the search order list because I can't trust it to not populate my SYNCED LYRICS tag with non-synced lyrics - it's a good source but I only use it during my second pass to find non-synced lyrics.

### NOTES
NONE of the default scripts, like Online DB: Timestamped [1-6] that Lyrics Panel 3 comes installed with work, so don't bother ever having them in the active search list.
Even though I'm not using ESLyric here, I have it installed and uncheck all the search sources so it won't interfere at all. Preferences -> Tools -> ESLyric -> Search.
MusixMatch gets really good results and would be great in the search order, but it denies access for some period of time (I'm not sure how long) after a small amount of successive searches, so I don't bother with it being high on the source list when batch scraping lyrics. I put it at the top of the search for casually listening to music later though - and they often have synced lyrics! See section below to help improve your chances of it getting lyrics. Oh, another thing - it seems if you use a VPN MusixMatch will most likely block your searches, so turn it off when scraping if you don't want to worry about that.
#HOW TO GET YOUR OWN MUSIXMATCH API KEY
The MusixMatch source uses an API key to scrape lyrics. It doesn't allow more than about 10 downloads within a short window of time. If anyone else is using the MusixMatch source in Veksho's component, that will count towards the 10, so you should get your own API key to use:

Install MusixMatch through the Windows store (this method won't work with the normal executable), and open it.
Follow the instructions HERE. During the step where you select an apic result, the usertoken is under the header tab. Copy the usertoken.
Go into the properties for the MusixMatch source and paste your usertoken in the MusixMatch tab, then close the dialog box, and it has been applied.
You're done, and can uninstall MusixMatch unless you want to keep using it.

# Foobar2000 THEME
I use and highly recommend Ottodix's Eole skin, but it comes with ESLyric making use of the Now Playing tab, so I switch that out for Lyric Show 3:

Preferences -> Display -> Columns UI -> Layout -> scroll down to the Panel Stack Splitter with ESLyric under it.
Right Click on that Panel Stack Splitter -> Insert Panel -> Panels -> Lyric Show 3.
Right click and remove the ESlyric panel (and make sure Lyric Show 3 is below Spider Monkey Panel).
Now that panel doesn't match the rest of the Eole theme so some changes need to be made:

Right-click in the panel and select 'Panel Preferences...'.
Change to 'Background: Transparent' with the drop-down.

Then my personal preferences for the look of the lyrics is:

Select mode: Custom, which makes the following options available:
Font: Arial Regular 12.
Normal color: select white.
Highline colour: select the 3rd green down in the 3rd column.
Line spacing: 10.
Change any of those settings to your preference!

# GET A PORTABLE COPY OF MY FOOBAR2000 SETUP
Recently I switched to using as many portable apps as possible. I use SyMenu for as many as I can. I can't believe it's not more popular, I much prefer it over PortableApps which I still use for a couple apps that aren't available in SyMenu. If an app is unavailable for either of them I'll use a standalone portable app. Then, if portable is unavailable I install apps with Chocolatey. For the rest I use old-fashioned installers like some kind of caveman.

ANYWAYS, the point is that I have a portable version of my setup for those of you who want to check it out easily without messing with your current Foobar2000 installation. It is set up with the the 'typical usage' settings above. I'm not sure if it's the standard portable Foobar2000 because I'm taking it from the version SyMenu installs.

In addition to the components included with the EOLE theme, my Foobar2000 (version 1.6.2, all components up-to-date as of 2021-01-16) setup also includes:

Autosave & Autobackup

Seek)

Text Tools - with commands I made to make a list of my albums by genre and a few others

CLICK HERE TO DOWNLOAD my custom Fooobar2000 v1.6.3 with all components up to date as of 2021-01-22

Use VirusTotal or whatever you prefer to check that my contribution is safe.

For me VirusTotal had 3 hits (out of 53 engines) with my zip file: - BitDefenderTheta - Gen:NN.ZedlaF.34780.Cy4@a80oq3ai - Malwarebytes - Malware.Heuristic.1001 - Microsoft - Program:Win32/Wacapew.C!ml

Because of those 3 hits I scanned my system with Malwarebytes, ESET Internet Security, AppCheck Anti-Ransomware and EmsiSoft Emergency Kit and didn't get any suspicious results, so I'm hoping they're false positives!

If any of you use Calibre to scrape metadata for your eBooks, I also made a post with my Calibre method HERE
