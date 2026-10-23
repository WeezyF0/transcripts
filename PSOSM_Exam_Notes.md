# PSOSM — Privacy & Security in Online Social Media
### Exam Notes (Explained) · NPTEL · Prof. Ponnurangam Kumaraguru (PK), Precog Lab, IIIT-Delhi · Lectures 1–34

**How to use these notes:** each topic opens with a short explanation of *what it is and why it matters*. **Bold** marks things likely to be asked. Boxes labelled **KEY TAKEAWAYS** sum up each topic, and **REMEMBER** boxes flag common exam traps. Where several lectures cover the same thing (e.g. Boston Marathon, Foursquare), they are merged into one place.

**The course's recurring method** (it applies to almost every study below):
1. Pick a **real event or problem** (Boston blast, Hurricane Sandy, police pages…)
2. **Collect data** from an OSM API (often by starting with a trending hashtag)
3. **Characterize** the data (how many tweets, users, URLs, geotags)
4. **Get ground truth** (human annotation or a trusted source)
5. **Extract features → build a model** (e.g. a classifier)
6. **Evaluate** and draw inferences

> **REMEMBER — the analysis frame used throughout the course:**
> **Who** posted · **When** · **Where** from · **What** about · **Why** · **How**.
> *Why* and *How* are the hardest to answer from data alone (you can rarely know why someone posted a rumour unless they confess).

---

## PART A — FOUNDATIONS

## 1. What is Online Social Media (OSM)?

OSM is any online platform where users create and share content. **Social networks** (Facebook, Twitter, LinkedIn) are just one type. Others are **publishing / crowdsourced** sites (Wikipedia), **social games** and **virtual games**.

**Each platform is built around one core "unit" of content:**
- **YouTube** – video (upload, like, share, channels, subscribe, report spam)
- **Flickr / Instagram** – images
- **Foursquare** – location (check-ins); *location-based social network*
- **LinkedIn** – professional *connections*; people post about jobs, not vacations
- **Pinterest** – images pinned to *boards*; one of the fastest-growing networks (its first 1M users came very quickly)
- **Periscope** – *live* video streaming (YouTube = upload first, Periscope = real time)
- **Tinder** – location-based dating (left/right swipe)
- **Google+** – friends are called *circles*; "+1" = like
- **Twitter** – *microblog*: posts limited to **140 characters**

**Newer categories:**
- **Ephemeral networks** – content **destroys itself** after some time (e.g. Snapchat)
- **Anonymous networks** – you **cannot tell who posted** (e.g. Whisper; see Section 17)

**Scale:**
- ~215–220 popular SN services exist
- In India ~1 in 13 people (now ~1 in 9–10) use SNs, driven by **mobile phones**
- **What happens online in 60 seconds (2013 → now):**

| Platform | 2013 | "Now" (2016) |
|---|---|---|
| Facebook posts | 2.5 million | 3.5 million (also quoted 3.3M) |
| Tweets | 278,000 | 420,000 |
| YouTube video uploaded | 100 hours | 400 hours |

### The 5 V's of OSM data
- **Volume** – the sheer *size* of content (400 hrs of video/min takes huge storage)
- **Velocity** – the *speed* at which content is generated
- **Variety** – different *types* of content and platforms
- **Veracity** – is it *true/legitimate*? (the core of the trust & credibility module)
- **Value** – the 5th, newer V: data is pointless without *value*

> **REMEMBER:** The original 4 V's are Volume, Velocity, Variety, Veracity. **Value** is the 5th, added more recently.

### Facebook vs Twitter (asked often)

| Feature | Facebook | Twitter |
|---|---|---|
| Direction | **Bidirectional**: a friend request must be *accepted* by both | **Unidirectional**: you can follow anyone (e.g. Amitabh Bachchan) without approval |
| Relationship | Friends | Followers / Following |
| Post length | Long text allowed | **140 characters** (microblog) |
| Interactions | Like, comment, share | Retweet, reply, like (earlier "favorite") |
| Other | Pages, groups (public/private) | Hashtags, trends, mentions, notifications |
| Data model | Everything stored as a **graph** | — |

- **Hashtag (#)** – tags a post to a topic so everyone following that topic sees it
- **Trends** – the hashtags or words that are popular right now in a location (e.g. Delhi trends)
- **Mention (@handle)** – putting a user's handle in a post **notifies** that user
- **Verified account (blue tick)** – Twitter confirms the account is genuine. Given to celebrities, accounts with many followers, or companies that pay. Only a small fraction of accounts (~1M) are verified.
- Top accounts on both FB and Twitter are mostly **sports and music** stars
- The "reality vs perception" video: what people post (great food, a run, a great presentation) differs from what they actually do → **don't blindly believe OSM content**

> **KEY TAKEAWAYS — OSM Basics**
> - Each network revolves around one content type (video, image, location, professional link…).
> - FB = bidirectional friendships; Twitter = unidirectional following.
> - Ephemeral = self-destructing content; anonymous = poster unknown.
> - The 5 V's describe OSM data: Volume, Velocity, Variety, Veracity, Value.

## 2. Real-World Incidents (why this course exists)

OSM can do great good (crisis help) and great harm (rumours, bullying, privacy leaks). These incidents come back throughout the course as examples.

**Positive uses:**
- **2009 US Airways plane landing on the Hudson River:** user *jkrums* tweeted "There's a plane in the Hudson. I'm on the ferry going to pick up the people. Crazy." This was the **first use of Twitter in a crisis**; citizens helped before first responders arrived. Until then Twitter was mostly chit-chat ("Monday morning, having coffee").
- **Lost child at an Indian railway station:** a photo tweet tagging the Railways Minister went viral → the child was **reunited with her parents in 20 minutes**. Organizations like "Find your missing child" now work purely through social media.
- **Nepal earthquake:** the government used OSM to coordinate relief
- **Egypt revolution:** organized largely through Twitter and Facebook

**Negative uses:**
- **Cyberbullying:** a teenager killed herself after being bullied on Facebook (she had posted about it)
- **UK/London riots:** OSM was used to *organize* the violence ("let's go to this street"); rumour that London Zoo animals had escaped
- **Boston Marathon blast rumours:** "RIP 8-year-old boy… running for the Sandy Hook kids" (no such child existed) and "**RT this and we'll donate $1**" (no money was ever paid)
- **Compromised verified account:** the **Associated Press** account was hacked and tweeted "*Breaking: Two explosions in the White House and Barack Obama is injured*". People trusted it because it was verified, and the stock market reacted.
- **Fake images:**
  - Chennai floods 2015: a **crocodile on the streets**
  - Hurricane Sandy: **shark** swimming in the streets
  - "**McDonald's in Virginia Beach flooded**": a real photo, but taken elsewhere years earlier
  - A **movie still** passed off as live
- Robin Williams: a **fake "goodbye" video** spread after his death
- **MI6 chief's wife** posted family photos on Facebook that became public → his appointment was affected (a privacy issue: *others* can reveal information about you)
- People **lost their jobs** over posts; employees leaked company projects online

> **KEY TAKEAWAYS — Incidents**
> - OSM problems seen: **misinformation/fake images, compromised accounts, cyberbullying, privacy leaks, organized crime/riots**.
> - **Verified ≠ always true**: a verified account can be hacked (AP tweet).
> - Fake images are often **real photos taken out of context** (McDonald's) or **movie stills**.

## 3. Data Collection Toolkit (Tutorials, in exam terms)

These tutorials are hands-on, but the *concepts* get asked.

### APIs and data formats
- **API (Application Programming Interface)** – a programmatic "tunnel" between your program and the platform: you ask for data, it returns data
- **Rate limit** – platforms cap how much data you can pull in a time window (companies don't want to give away everything)
- **JSON (JavaScript Object Notation)** – the format most OSM APIs return; **key–value pairs** with `{}` objects and `[]` lists. Tool to view it nicely: jsonviewer.stack.hu
- **XML (Extensible Markup Language)** – an older, similar structured format
- **Never share your API key, secret or access token**: anyone holding them can collect data *as you*

### Facebook Graph API
- FB stores everything as a **graph**: **objects = nodes** (users, pages, posts, photos), each with a **unique numeric ID**; **connections = edges** (friendships, likes, comments). That is why it's called the **Graph API**.
- **Access token** – an authentication string generated using the **OAuth** protocol; proves who you are
  - Analogy from the lecture: **the app is the door, the access token is the key**. You can't get a key without a door (an app).
- **Permissions** – each field (email, birthday, education, photos, friends, posts) needs explicit permission; missing permission → a debug error
- **Short-lived token** expires in ~1–2 hours. **Extended (long-lived) token** lasts **~60 days**: create your own app (App ID + App Secret) and call the `fb_exchange_token` endpoint.
- **Search** (`search?q=nptel&type=page/group/event/user/place`) returns **public content only**
- **Friends list** returns only friends who *also* used the same app (FB tightened this after privacy complaints)
- **Post ID** = `userID_postID`
- **Paging** – results come in pages of **25 by default**; follow the `paging.next` URL, or raise `limit`
- Older API versions (v2.0) returned more fields by default; newly created apps can only use the current version

### Twitter API
- Create an app at apps.twitter.com (needs a verified phone number) → **4 keys: consumer key, consumer secret, access token, access token secret**
- **REST API** – fetch user data, timelines, followers
- **Search API** – *past* tweets (`result_type=mixed` = popular + recent, `count=100`)
- **Streaming API** – *real-time* tweets; `track` = keyword, `follow` = user ID
- **Twython** – the Python wrapper used in the course

### Storing data

| | **MySQL** | **MongoDB** |
|---|---|---|
| Type | **Relational** (tables: rows & columns, SQL) | **Non-relational, document-based** (stores JSON documents) |
| Python library | MySQLdb | pymongo |
| Viewer tool | phpMyAdmin | RoboMongo |
| Notes | tweet_id as PRIMARY KEY; `INSERT IGNORE` skips duplicates | `_id` is the unique key; whole tweet JSON stored as-is |

### Text analysis with NLTK (Natural Language Toolkit)
- **Tokenization** – split a sentence into words (`word_tokenize`)
- **Frequency count** – most common words (`Counter`)
- **Stemming** – reduce a word to its root (course/courses → "course"; certify/certification → "certif"), using the **Porter stemmer**
- **Stopwords** – very common words (the, and, to) that carry no meaning; remove them
- **n-grams** – sequences of words: a **bigram** (2 words, e.g. "Barack Obama") or **trigram** ("to know more") captures phrases that single words miss
- **POS tagging** – labels each word's Part Of Speech (JJ = adjective, NN = noun, IN = preposition, CD = number) → sentence structure can be a feature for telling users apart
- Unicode errors when printing → `.encode('utf-8')`

### Visualization with Highcharts (interactive JavaScript charts)
- **Bar chart** – bar length ∝ value (e.g. posts per user)
- **Line chart** – points joined by lines; shows **change over time** (followers per month)
- **Scatter plot** – points *not* joined; shows a relation between two variables (followers vs friends)
- **Bubble chart** – scatter + a **3rd dimension shown as bubble size** (e.g. number of tweets)
- Followers = people who follow X; **friends** (on Twitter) = people X follows

> **KEY TAKEAWAYS — Toolkit**
> - Data pipeline: **API → JSON → store in MySQL/MongoDB → analyze (NLTK/Gephi) → visualize (Highcharts)**.
> - FB Graph API: nodes + edges, OAuth access tokens (short ≈ 1–2 hrs, extended ≈ 60 days), paging of 25.
> - Twitter: 4 keys; REST vs Search vs **Streaming (real time)**.
> - MySQL = relational; MongoDB = document/NoSQL.

## 4. Social Network Analysis (SNA) & Gephi

A social network can be drawn as a **graph**: **nodes** = users/pages/groups, **edges** = relationships (follows, likes). SNA measures this structure to find influential users, communities and so on.

**Ways to store a graph:**
- **Adjacency matrix** – an N×N grid with 1 where an edge exists. Easy to build, but **sparse and wasteful** when there are many nodes and few edges.
- **GraphML** – an XML file listing `<node id>` and `<edge source target>`
- **CSV** – a nodes file (column `Id`) + an edges file (`Source`, `Target`, optional `Type`)

**Key metrics (understand these):**
- **In-degree** – number of edges *coming into* a node (on Twitter = number of followers). A self-loop counts.
- **Out-degree** – number of edges *going out* (= number of accounts you follow)
- **Degree centrality** – the node with the highest in-degree is the most popular/influential
- **Betweenness centrality** – how many *shortest paths* between other nodes pass through this node → **"bridge"/broker** nodes
- **Closeness centrality** – the node with the *lowest total distance* to all others → can reach everyone fastest
- **Eigenvector centrality** – a node is important if it's connected to *important* nodes
- **Community** – a group of densely connected nodes. **Modularity** = the fraction of edges that fall *within* groups (higher = clearer communities).
- **Density** – how close the graph is to *complete* (everyone connected to everyone)
- **Clustering coefficient** – how much your neighbours are also connected to each other ("friends of friends are friends")
- **Average path length** – the average number of hops between two nodes
- **Assortativity** – do nodes connect to others of *similar degree*? A value **near 0 suggests a random graph**.
- **Network diameter**; **connected components** (strongly/weakly connected); **PageRank**

**Gephi** (open-source graph visualization tool):
- **Data Laboratory** = tables of nodes and edges · **Overview** = layout & statistics · **Preview** = final rendering and export (PDF/PNG/SVG)
- **Layouts:** Fruchterman–Reingold, ForceAtlas
- Colour nodes by **modularity class** (community); size them by **in-degree** (popularity)
- **Filters:** by attribute (e.g. followers 100–1000), by topology (degree, k-core), combined with intersection/union
- Data source for the tutorials: **twecoll** (collects your Twitter friends-of-friends network as a .gml file)

> **KEY TAKEAWAYS — SNA**
> - **In-degree = followers = popularity**; out-degree = following.
> - Betweenness = bridge; closeness = central reach; modularity = community strength.
> - **High degree + low clustering + short paths + assortativity ≈ 0 → random graph** (used for Whisper later).

---

## PART B — TRUST & CREDIBILITY

## 5. Misinformation and How to Detect It

**The problem:** during big events, rumours spread **faster** than the truth. The Boston blast graph (x = hours after the blast, y = log of tweets; **red = true information, green = rumour, blue = total**) shows rumours peaking within a couple of hours while true information arrived much later (~9 hours).

> **REMEMBER — two ways to fight rumours:**
> 1. **Bring the true information earlier**, and
> 2. **Make the rumour die out (flatten) faster.**

More misinformation examples: the **Ebola hoax** (salt water as a "cure"), **false shootout tweets causing panic in Mexico City**, London Zoo animals "escaped", fake Hurricane Sandy images.

### Case study 1: Hurricane Sandy (fake images)
- Event: **22–31 Oct 2012**, north-eastern US, ~**$75 billion** damage
- Data: **1,782,526 tweets**, ~**1 million unique users**, ~**622,000 tweets with URLs**
- **Ground truth problem:** to train a model you must know which tweets are fake. Solution: the **Guardian** newspaper published a list of fake and true images (**10,350 tweets with fake images**, posted by 10,215 users).
- **Network (diffusion) analysis:** drew who retweeted whom at hour *n* and hour *n+1*. The post spread massively within an hour, and **the person who started it was not necessarily the most central user later**.

### Three sources of features
Any user/post on Twitter offers three kinds of information:
1. **User profile** (who you are)
2. **Network** (who you are connected to)
3. **Content** (what you post)

**User features (F1, "source-based"):**
- Number of friends and number of followers
- **Follower–friend ratio** – a genuinely popular account is followed by many more people than it follows (PK follows ~176 but has ~1,156 followers)
- **Number of times listed** – Twitter *lists* group experts; being added to many lists suggests expertise
- Profile has a URL; **verified** account
- **Account age** – older accounts are more trustworthy. This idea comes from web security, where a newly registered domain is suspicious. A "Rajinikanth" account created yesterday is probably fake.

**Tweet features (F2, "message-based"):**
- Length of the tweet, number of words
- Contains **?** or **!**, and how many
- Happy or sad **emoticons**

### Classification results (Sandy)
- **5-fold cross-validation** – the data is split into 5 parts; train on 4, test on 1, rotate → more confidence in the accuracy figure
- **Naive Bayes** (probabilistic, based on Bayes' theorem) vs **Decision Tree** (a tree of decisions)
- **Best: Decision Tree with tweet features = 97.65% accuracy**
- **Tweet features worked better than user features**

### Case study 2: Credibility across many events (TweetCred research)
- Events: UK riots, Libya crisis, Virginia earthquake, US credit downgrade (data collected via trending topics)
- **Annotation via Amazon Mechanical Turk** (crowdsourcing: people worldwide do small tasks for small payments; CrowdFlower is similar)
  - **Step 1:** does the tweet contain information / is related but has no info / is unrelated / skip
  - **Step 2:** if informative → **definitely credible / seems credible / definitely incredible / skip**
- **Inter-annotator agreement:** each tweet labelled by **at least 3 people**; agreement measured by **Cronbach's Alpha**, and **≥ ~0.7 is considered acceptable**
- **Results:** **30% of tweets had information, only 17% had credible information, 14% were spam**
- Evaluation metric: **NDCG (Normalized Discounted Cumulative Gain)**. It measures *ranking* quality (normally used for search engines) and was used here to rank tweets by credibility.
- **Best feature set: tweet + user features → "what you post AND who you are" decides credibility**

### TweetCred (tool)
- A **Chrome browser extension** that shows a **credibility score from 1 to 7** next to every tweet in your timeline (also in search results and DMs)
- **User feedback:** you can agree or disagree with the score and suggest the right value → used to **retrain/improve the model**
- Uses **45 features that can be computed in real time** (some features, like analysing all of a user's followers, are too slow for real time). New ones include presence of **swear words**, positive/negative emotion words, the **WOT score** of a linked URL, and the like/dislike ratio of linked YouTube videos.
- **Top 10 most useful features:** number of characters, number of unique characters, number of words, user has a location in the profile, number of retweets, age of the tweet, tweet contains a URL, contains "via", statuses & followers, friends & followers
- **Who uses it:** emergency responders, firefighters, journalists/news media, general users

### Facebook Inspector (FBI)
- Same idea applied to **Facebook**. Facebook differs from Twitter: it is **bidirectional and personal**, so people **trust a friend's post more** than a stranger's, and the available features differ.
- Pipeline: Graph API → feature extraction → ground truth → feature vectors → **supervised learning model** → **RESTful API** → **Chrome/Firefox plugin** that marks posts as malicious or low-confidence
- **WOT (Web of Trust):** give it a **domain**, it returns a reputation rating (**excellent, good, satisfactory, poor, very poor**) + a confidence value. Used as a URL feature. Other domain features: how long the domain has been registered, who registered it.

> **KEY TAKEAWAYS — Trust & Credibility**
> - Rumours spread faster than truth → speed up truth, slow down rumours.
> - Features come from **profile, network, content**; tweet (content) features were strongest.
> - Decision Tree + tweet features = **97.65%** (Sandy).
> - Only **17% of event tweets carried credible information**.
> - **Cronbach's Alpha ≥ 0.7**, ≥3 annotators, **Mechanical Turk** for labels, **NDCG** for ranking quality.
> - **TweetCred** (Twitter, score 1–7, 45 features, user feedback) and **Facebook Inspector** (FB) put this into practice.

## 6. Boston Marathon Blast — Fake Content Study (merges L9, L10, L34)
Paper: **"$1/RT #PrayForBoston: Analyzing Fake Content on Twitter"**

**The event:** twin blasts at the marathon finish line on **15 April 2013** (~18:50 GMT). **3 killed, 264 injured.** The first tweet came within ~3 minutes; the first image within ~4 minutes.

**Data collection:**
- **~7.8–7.9 million tweets** from **~3.6 million users** (3.4M had URLs; ~62K geotagged, in line with Twitter's claim that **only ~1% of tweets are geotagged**)
- Keywords: #BostonMarathon, #PrayForBoston, #Watertown, #manhunt, Sean Collier, #BostonStrong, "boston explosions", "boston suspect"… This is **query expansion**: start with one trending hashtag, look at which other words co-occur, add them, and collect again.
- Collection started **45 minutes after** the blast, but early tweets were captured anyway because they were *retweeted* later → the largest known dataset for this event
- **Tweet spikes match real-world events:** 1 hour after the blast, when the **suspects' photos were released** (the Boston Police used their official account to ask the public for help), and when the "**manhunt is over**"

**Fake vs true content:**
- The **top 20 most viral tweets** (~400K tweets, ~6% of the data) were manually labelled:

> **REMEMBER:** **29% rumours/fake, 20% true, 51% generic** (opinions, condolences, #PrayForBoston, which alone had ~87K retweets).

- The two famous fakes:
  - "**For every retweet we will donate $1 to the Boston Marathon victims**" from the fake account **@_BostonMarathon** (~50K retweets)
  - "RIP to the 8-year-old boy…" (>30K retweets)
- **3,249 users** tweeted *both* true and fake information
- **Device/source:** **~75–76% of fake tweets came from mobile phones** (vs 64% for true, 51% for generic). Mostly iPhone; the web was used more for true content.
- **Rumour originators ("seeds")** usually had **few followers**. A rumour goes viral when a **popular or verified account retweets it without checking**.
- Accounts spreading fake content had the **lowest follower counts**; **verified accounts helped spread fake content early on**
- **Predicting virality:** combined user metrics (**social reputation, global engagement, topic engagement, likability, credibility**) into an *impact* score. **Linear regression achieved R² ≈ 0.7**, i.e. **you can predict how viral a fake tweet will become** from the users currently spreading it.

**Malicious / suspended accounts:**
- **~32,000 new accounts were created during the event; 19% were deleted or suspended** by Twitter within 2 months
- **~6,000 suspended profiles**; account creation **spiked right after the blast** (~1,400 in the first hours)
- Accounts get suspended when many users report them, or via government requests. Some fake accounts were still active during the study.
- **The fake accounts formed a closed, tightly connected community** (like phishing gangs). Interaction patterns found: **single links, closed community, star topology** (one account spreading to many), **self-loops** (accounts mentioning themselves)
- Malicious users **exploit events** for e-crimes like **impersonation and propaganda**

> **KEY TAKEAWAYS — Boston**
> - **29% fake vs 20% true** among viral tweets: fake beat true.
> - Fake content came mostly **from mobile (~76%)** and from **low-follower seeds**, amplified by popular/verified accounts.
> - **32K new accounts, 19% suspended**: attackers create accounts right after events.
> - **Virality of fake content is predictable (R² ≈ 0.7).**

---

## PART C — PRIVACY

## 7. What is Privacy? Definitions & Perceptions

**Privacy is contextual:** your expectations differ at home, in class, at work, at the movies. That is why it is so hard to define.

**Key definitions:**
- **Robert Post** (*Three Concepts of Privacy*): "Privacy is a value so complex, so entangled in competing and contradictory dimensions, so engorged with various and distinct meanings, that I sometimes despair whether it can be usefully addressed at all."
- **Alan Westin** (*Privacy and Freedom*, **1967**): "Privacy is the **claim of individuals, groups or institutions to determine for themselves when, how and to what extent information about them is communicated to others**."
  - Also: each individual constantly *balances* the desire for privacy against the desire for disclosure and communication.

> **REMEMBER:** At its core, **privacy = control over information about yourself.**

**Four forms of privacy:**
1. **Information privacy** – personal data, especially internet privacy (the focus of this course)
2. **Communication privacy** – phone calls, messages
3. **Territorial privacy** – your space: home, city, country
4. **Bodily privacy** – your physical self (e.g. **CCTV cameras** intrude on it)

Collectivist societies (like India) often talk about **group privacy**; individualistic societies protect **individual privacy** more.

### Westin's Privacy Categories (30+ years of US surveys)

| Category | Share | Behaviour |
|---|---|---|
| **Fundamentalists** | ~25% | Very strong privacy; share almost nothing (wouldn't even stand in a photo) |
| **Pragmatists** | ~57–60% | Decide **case by case**, weighing what they get in return (Amazon vs a bank site) |
| **Unconcerned** | ~15–18% | Would give away a password for a bar of chocolate |

(The lectures quote both 57/18% and 60/15%; know that pragmatists are the clear majority.)

- **The famous cartoon:** "On the Internet, nobody knows you're a dog" (mid-90s) → today you get personalized ads for your favourite dog food. **Your behaviour reveals who you are.**

### India Privacy Survey (PK's group)
- **10,427 respondents, 83 questions**, collected across all states but one (e.g. Tamil Nadu = 8.57%), plus 20 interviews and 4 focus groups. Collected mostly *offline* (malls, railway stations), one of the **largest privacy surveys anywhere**. Mostly aged 18–39; 67% male, 32% female.
- **Q42** (6,855 answers) – "How do you feel about the privacy of your info on OSM?"
  - **42%: "I have set my privacy settings, so my data is secure"** (a false sense of security)
  - 19% not a concern; 23% concerned even with settings; 8% concerned but still share; 6.7% concerned so don't share
- **Q43** (6,929 answers) – whose friend requests would you accept?
  - **27% accept anyone of the opposite gender**; 10.12% accept for a nice profile picture; 2.99% accept anyone
- **Facebook location sharing setting:** **everyone 39%**, friends 33%, friends-of-friends 12.5%, network 5.7%, customized 3.1% → most people expose their location widely
- **Regional-language "the number you are calling is switched off" message** (a Delhi number travelling in Mumbai gets the message in Marathi → reveals which state you're in): **54% consider it privacy-invasive**

### Nobody reads privacy policies
- If everyone read the privacy policy of each site they visit once a month: **244 hours per person per year** → **$781 billion/year** national opportunity cost in the US
- Hence the push for tools that help users make **informed decisions** (see Nudges, Section 10)

> **KEY TAKEAWAYS — Privacy Concepts**
> - Westin 1967: privacy = individuals determining **when, how and to what extent** their info is shared.
> - **4 forms: information, communication, territorial, bodily.**
> - **Fundamentalists / Pragmatists (majority) / Unconcerned.**
> - Indians: **42% wrongly trust privacy settings**; **27% accept opposite-gender friend requests**; **39% share location with everyone**.

## 8. Privacy Attack: Re-identifying People from Photos

**Re-identification** = taking data that *doesn't* name a person (an **unidentified source**) and linking it with data that *does* (an **identified source**) to work out exactly who they are, and then learn sensitive things about them.
- **Unidentified sources:** dating sites (match.com, shaadi.com), Flickr photos, CCTV, pseudonymous accounts
- **Identified sources:** Facebook, LinkedIn, government websites (real names)

**Why this became possible (4 converging trends):**
1. **More public self-disclosure** – billions of photos (2000: 100B photos shot worldwide; 2010: 2.5B photos uploaded to FB *per month*; now 1.8B/day across FB, Instagram, Flickr, Snapchat, WhatsApp)
2. **Better face recognition** – FB/Google/Microsoft/Apple bought face-recognition companies. FB is especially accurate because it only searches among your **friends** (a small search space).
3. **Cheap cloud computing**
4. **Better re-identification techniques** (k-anonymity came ~15–20 years ago, attacks keep improving)

### Latanya Sweeney's classic attack (k-anonymity)
- **Medical records** (ethnicity, visit date, diagnosis, procedure, medication, charges — no names) + **public voter list** (name, address, party, date registered/last voted)
- Both share **ZIP code + birth date + gender** → **most US citizens can be uniquely identified** from these three fields alone
- This led to the concept of **k-anonymity** (each record should be indistinguishable from at least k−1 others)

> **REMEMBER:** Each dataset is harmless alone; **combining** them breaks anonymity.

### The face re-identification experiments (Carnegie Mellon study)
Tools: **PittPatt** face recognizer (later **acquired by Google**); today you'd use **TensorFlow** (an open-source ML library).

**Experiment 1 – online ↔ online** (dating site vs Facebook):
- Identified: FB profiles from one US city (~270K profiles, ~274K images, ~110K faces)
- Unidentified: a dating site in the *same city* (~6K profiles, ~5K faces, pseudonyms)
- >500 million pairs compared; the best match was kept and verified by **Mechanical Turk** workers (Likert scale 1–7, ≥5 workers per pair)
- **Result: ~1 in 10 dating-site profiles re-identified** (6.3% "highly likely", 10.5% likely or better)

**Experiment 2 – offline ↔ online** (a person walking on campus vs Facebook):
- A booth on campus took **3 photos** of each student volunteer while they filled an online survey. *During the survey*, the cloud system matched their face against the university's FB network (~25K profiles, ~26K images, ~114K faces). The **last page of the survey showed their likely FB photos**.
- **Result: 38% of 98 participants matched to their correct FB profile**, in about the time it takes to fill a survey. One student who said he had no photo on FB was still found.

**Experiment 3 – predicting sensitive data:**
- Faces + public FB data → **predicted the first 5 digits of the Social Security Number for 27% of subjects within 4 attempts**
- The Indian equivalent would be the **Aadhaar number**

**pleaserobme.com:** a site that picked tweets where people were clearly *away from home* (account created in Delhi, tweeting about weather in Chennai) and listed them → "your home is empty". Taken down later, but it shows how **self-disclosed location** can be abused.

> **KEY TAKEAWAYS — Re-identification**
> - **Unidentified + identified data → re-identification.**
> - Sweeney: **ZIP + birth date + gender** identifies most Americans.
> - Face matching: **1 in 10** dating profiles; **38%** of students on camera; **27%** got SSN digits.
> - Your public photos + face recognition = **loss of anonymity offline too**.

## 9. Location Privacy: "We Know Where You Live" (merges L16, L29, L30, L32)

**Location-based social networks (LBSNs):** Foursquare, Yelp, Gowalla, plus Facebook check-ins and Twitter geotags.

### How Foursquare works (know the terms)
- **Check-in** – announcing you're at a place (via GPS). **Visible only to friends.**
- **Venue** – the place (airport, restaurant, college)
- **Mayor** – the person with the **most check-ins at a venue in the last 60 days**. Businesses give mayors perks like **discounts or free parking**.
- **Badges** – awards that **gamify** the platform (e.g. newbie badge, late-night check-in badge)
- **Tip** – a short review left at a venue ("food at Saravana Bhavan is good")
- **Done / To-do** – agreeing with a tip / planning to visit (like a "like")

> **REMEMBER:** Check-ins are friends-only, but **mayorships, tips and dones are PUBLIC** → anyone can collect them and **infer where you live**.

### Paper 1: "We Know Where You Live: Privacy Characterization of Foursquare Behavior"
- **Data (Aug–Oct 2011): ~13 million users** (almost all of Foursquare), 10M tips, 9M dones, 15M mayorships, 15M venues
- **Cleaning the data:** user home city (UHC) and venue location (VL) are free text, so invalid entries (e.g. "heart", points in the sea), ambiguous ones ("near Taj Mahal") and empty fields were removed. Locations were converted with **reverse geocoding** (Yahoo PlaceFinder: location ↔ latitude/longitude).
- **Power law / Pareto (80-20) principle:** a *few* users have most of the mayorships/tips/dones; most users have just one. The same skew appears per city. (This is typical of all social media data.)
- Mayorships and tips are **strongly correlated across cities (0.78)**
- **Behaviour findings:**
  - Many users post consecutive tips/dones **within 1 hour**, but long gaps (~20 days on average) are common too
  - Displacement between consecutive activities: ~36% ≈ 0 km, **70% within 150 km** (same region), ~10% up to ~6,000–7,000 km (international)
  - **Returning time shows peaks at every 24 hours** (daily routine: same office/college every day) and at **168 hours (weekly)**
  - **People don't move much** → their activity reveals home
- **Home inference method = majority vote:** the most frequent location among a user's mayorships, tips and dones is guessed as home
  - **Class 0:** only one activity → use it
  - **Class 1:** many activities with one **predominant location** → use it (most accurate)
  - **Class 2:** many activities, no dominant location → can't infer
- **Accuracy:** ~67% for home city (Class 1), ~70% state, higher for country (city is hardest, country easiest). Using mayorships alone: 51.6%.
- **Comparing inferred with declared home:** 46% within 50 km → **overall ~78% of users' home city correctly inferred within 50 km**

### Paper 2: "Beware of What You Share: Inferring Home Location in Social Networks"
Extends the idea to **three** networks:

| Network | Data used | **Home city accuracy** | Within 50 km |
|---|---|---|---|
| Foursquare | mayorships, tips, likes, friends | **67%** | 78.5% |
| Google+ | places lived, education, employment, friends (27M profiles) | **72%** | 64% |
| Twitter | **geotagged tweets** (120M tweets; only **0.5%** geotagged) | **82%** | 87% |

- **Twitter is most accurate** because geotags give exact coordinates
- **Exact residence:** Twitter **35% exactly (0 km)**, 73.67% within 20 km; Foursquare 52.7% within 5 km; Google+ only ~5% (it uses work/study places, not home)
- **Friend-model refinement:** ignore users with too few friends (not enough evidence) or too many (weak ties) → +21% accuracy for Google+
- Most profile locations are given at **city level** (~80% on Foursquare)

**How research papers are structured** (stressed in these lectures):
- **Abstract** → **Introduction** (big picture, gap, what we did, contributions) → **Related work** → **Dataset** (exploratory data analysis, so others can **reproduce** the work) → **Method** → **Results** → **Conclusion & limitations**
- Top venues: **WWW, ICWSM, COSN, CSCW**

> **KEY TAKEAWAYS — Location Privacy**
> - Public mayorships/tips/dones are enough to **find a user's home city (~78% within 50 km)**.
> - Majority vote over activity locations; Class 0/1/2 by whether one location dominates.
> - Twitter geotags give the best home inference (**82%**); Google+ the worst at exact residence.
> - OSM data follows a **power law (Pareto 80-20)**.

## 10. Privacy Nudges (helping users avoid regret)

**Goal:** prevent **regrettable posts** (like the MI6 wife's photos) by gently *nudging* users before they post.
- **Early example (MIT):** before sending to a mailing list, show the **profile pictures of everyone who will receive** it (bigger for people you interact with more). You see your real audience.

**Facebook nudges** (a Chrome extension tested on real users):
1. **Picture nudge** – shows **profile pictures of the people who can see your post** ("these people and anyone on the Internet can see this")
2. **Timer nudge** – "**You have 10 seconds to cancel** your post"
3. **Sentiment nudge** – warns "**others may perceive your post as negative**"

**Study method:** **IRB (Institutional Review Board)** approval is required for any study with human subjects. Participants recruited via flyers, email and Craigslist; **21 completed the field study, 13 gave exit interviews**. Measured: changes to privacy settings, cancelled/edited posts, post frequency, topic sensitivity.

**Results:**
- **Picture:** people **changed their audience** (e.g. "friends except acquaintances") or cancelled posts
- **Timer:** "annoying at times, handy at times", but **made people think** before posting
- **Sentiment:** sometimes wrong (lacked context), yet many cancelled posts; **posts dropped from 13 to 7**

> **KEY TAKEAWAYS — Nudges**
> - **Picture, Timer (10 s), Sentiment** nudges changed behaviour (fewer and more careful posts).
> - Design challenge: the right nudge depends on context (a timer annoys heavy posters).
> - Human-subject research needs **IRB approval**.

---

## PART D — POLICING & OSM

## 11. How Police Use Social Media

**Why it matters:** police can't be everywhere. OSM lets citizens report problems and lets police reach the public directly → **community policing** and safer cities.

- **#myNYPD fiasco:** NYPD asked people to post photos with officers; instead they got **photos of police brutality**, and it spread to #myLAPD → public campaigns can backfire
- **Indian police on OSM (since ~2010–11):**
  - **Bangalore City Police** (verified FB page) and **@CPBLR** (~10K tweets, follows only 60; followers grew **335K → 688K** by Aug 2016)
  - Delhi Traffic Police, Hyderabad City Police (verified), UP, Guwahati, Kolkata, Pune, Jaipur, Mumbai
  - Indian police pages **allow citizens to post** on them; YouTube use is small
- **Fake police handles** are common ("Delhi Traffic Polize", "Fake Kolkata Police", accounts with the default **"egg" profile picture**)
  - **How to tell the real one:** the **verified badge**, or a **link from the official .gov.in website**
  - Precog built a public list of ~80–85 police handles with a dashboard of their activity

### Study 1: Bangalore City Police Facebook page — "actionable information"
- **Question:** can OSM give police **actionable information** about crime and residents' opinions?
  - *Actionable* = something police can act on: a pothole, a traffic jam, a broken-down car, with the **time and location** included
- **Data:** BCP's FB page in 2014 → **255 posts, ~1,600 comments**
- **Coding scheme:** **24 categories** of citizen content, **2 styles** (formal/informal), **4 police response types:**
  - **Acknowledge** (thanks/like) – 21% ("we will take all possible legal measures")
  - **Reply** (suggest a solution) – 22% ("please lodge a complaint")
  - **Follow-up** (ask for details) – "please provide the police station details"
  - **Ignore** (no reply)
- **Top citizen topics:** neighbourhood concerns > appreciation of police > suggestions, auto drivers, fraud, traffic. **Likes were highest for satisfaction, appreciation and success stories.**
- Police replies were almost always **formal**; citizens' posts ranged from "Dear Sir, please take action" to "Kudos to the team!"
- **Response time: average 30 hrs, max 211 hrs, min 4 minutes** → huge variation
- **Word trees** on "worried", "why", "need", "want" reveal citizens' **fears, needs and wants**
- **Direct** (it's happening to me) vs **indirect** information (my friend's area has a problem)
- **Mutual accountability:** the public platform makes **both police and citizens accountable**

### Study 2: 85 police Facebook pages — how police and citizens communicate
- **Data:** 85 official police pages, 2010 – Apr 2015 → **85,408 police posts and 47,474 citizen posts**
- **4 research questions:** (1) **Topics** (2) **Engagement** (3) **Emotions** (4) **Cognitive & social orientation**
- **Tools:**
  - **n-grams** (unigram/bigram frequencies), **K-means clustering**
  - **LIWC (Linguistic Inquiry and Word Count)** – puts text into ~35–37 psychological categories (positive, anxiety, anger…)
  - **ANEW** dictionary
  - **Valence** = how positive/negative; **Arousal** = how intense
- **Findings:**
  - **Topics:** police posts = advisories, case status, rules/safety/violations; citizen posts = mainly "**please take action**"
  - **Police-initiated threads are focused** (awareness drives, safety campaigns, action reports); **citizen-initiated threads are diverse** (appreciation, news, complaints, neighbourhood problems, missing people)
  - **Engagement:** when police join a citizen's thread, the discussion **ends sooner** (fewer comments) because **police close the loop** (e.g. "please visit your nearest police station")
  - **Emotions** (citizen threads, with vs without police): negative affect and anger **higher**, **anxiety LOWER** (0.001 vs 0.003) when police respond → **police responses reassure citizens**
  - **Cognition:** citizens' posts are **self-focused** ("I" is the most used pronoun)
- **Why it matters:** police can sense community mood, offer emotional support, use **predictive analytics** and **early warning**, and give decision-makers records

> **KEY TAKEAWAYS — Policing**
> - OSM can provide **actionable information** (what, where, when) to police.
> - Police responses: **acknowledge, reply, follow-up, ignore**; response time **avg 30 hrs**.
> - **Police replies lower citizens' anxiety and close discussions faster.**
> - Real vs fake police handles: check **verification** or the **official website link**.

---

## PART E — E-CRIME & SECURITY

## 12. Types of e-Crime on Social Media

- **Phishing** – tricking someone into giving login details by sending them to a **fake website** that looks real
  - **Spear phishing / context-aware:** aimed at a *specific group* (e.g. a fake email from "PK" to this course's students)
  - **Whaling:** aimed at **CEOs / top executives**
  - **Vishing:** over **voice/phone**; **Smishing:** over **SMS**
  - **Social phishing:** uses details from your **social network** (see Section 14)
  - On OSM: fake "Facebook technical support" notices, a "new Facebook login system". **Facebook credentials are now prized** because they expose your friends, interests and habits.
- **Fake customer-service accounts** – you tweet a complaint tagging your bank; a **look-alike fake account replies** "as the bank" and asks you to log in via its link
- **Fake comments on popular posts** – scammers comment on viral posts (Olympics, PM's posts) with links to fake sites/malware, because those posts are seen by many
- **Fake live-streaming videos** – "Watch the match live here" (Olympics, cricket) → no video, just a scam
- **Fake online discounts** – a fake page posing as a real brand (e.g. "Netflix: 40% off for 6 months")
- **Fake online surveys and contests** – "personality test", "win Rs 1,000", used to harvest personal data
- **Fake Foursquare tips** – spam tips at venues with links unrelated to the venue (e.g. "XanGo mangosteen juice")
- **Social reputation manipulation** – your *influence* is now measured by likes, followers, reviews and endorsements, so people **fake** them (fake followers, fake Amazon/Flipkart reviews; **Amazon sued 1,000 people over fake reviews**; fake LinkedIn endorsements)
- **Clickbaiting** – misleading links that lure clicks
- **Hashtag hijacking** – riding a trending hashtag that has nothing to do with you, to promote a product
  - **Coca-Cola** used **#RoyalBaby** to sell Coke
  - **DiGiorno Pizza** used **#WhyIStayed** (a hashtag about domestic violence) and **had to apologize**
- **Compromised accounts** – a legitimate account taken over (AP's fake White House tweet)
- **Impersonation** – fake accounts copying a real person or organization (actress Kiran Rao filed a complaint; fake police pages)
- **Work-from-home scams** – "earn $5–40 per survey from home" (spread on Pinterest)

> **KEY TAKEAWAYS — e-Crime**
> - Know the phishing variants: **spear, whaling, vishing, smishing, social**.
> - Scammers **exploit popularity and trust**: popular posts, trending hashtags, events, brand names, verified-looking accounts.
> - **Hashtag hijacking = using an unrelated trending tag for promotion** (Coca-Cola #RoyalBaby, DiGiorno #WhyIStayed).

## 13. Spam & Link Farming on Twitter (merges L20, L22)

**PageRank** (Google's idea): a page ranks higher if many pages link to it, i.e. it has high **in-degree**.
**Link farming** = creating fake, non-genuine links between sites just to boost rank. This is spamming the search engine's index (**spamdexing**).

**Why link farming on Twitter?**
- Twitter is a "**web within the web**" and is **where news breaks**. People *search* Twitter, and results are ranked partly by the poster's connections and followers.
- **Number of followers = social reputation/influence** (see also the **Klout score**, 1–100 influence across OSM; PK's was 24)
- **On Twitter, link farming = following lots of people hoping they follow back** (**reciprocity**). More followers → higher in-degree → better search visibility and more influence.

> **REMEMBER — Web vs Twitter link farming:**
> - On the web, **only spammers** do it, and hyperlinks are rarely reciprocated.
> - On Twitter, **spammers AND legitimate popular users** do it, and follow-backs are *very likely*.

**Background research on Twitter spam:**
- *"Suspended Accounts in Retrospect"*: 1.1M accounts suspended over 7 months (1.8B tweets, 80M of them spam); spam campaigns controlling 145K accounts lasted for months; **77% of spam accounts are suspended within a day of their first tweet**
- *"@spam: The Underground on 140 Characters or Less"*: **8% of 25 million URLs** led to phishing, malware or scams; **click-through rate 0.13%**, *much higher than email spam*, because the link comes from someone **you chose to follow** (trust)
- *"Detecting and Analyzing Automated Activity on Twitter"*: **16% of active accounts are highly automated (bots)**. Detected by plotting posting minute-of-hour vs hour-of-day: a too-regular pattern = bot. **11% of accounts that claim to post "from the web browser" are bots spoofing their source.**

**The link-farming study** (entire Twitter graph of 2009: **54 million users, 1.9 billion links**):
- If B follows A: B is A's **follower**, A is B's **following**
- **Spam targets** = users a spammer follows · **Spam followers** = users who *follow the spammer back*
- **379,340 accounts suspended** (Aug 2009 – Feb 2011); 41,352 had posted blacklisted URLs shortened with **bit.ly / TinyURL** (URL shorteners became popular because of the 140-char limit, and they hide the real link)
- Spam targets ~13M; spam followers ~248K; **82% of spam followers were themselves spam targets**
- **Spammers rank high:** 7 spammers in the top 10K by PageRank, 304 in the top 100K, 2,131 in the top 1M
- **Top 100K spam followers gave 60% of all links spammers acquired**: a small group of users follows back almost every spammer
- Users with **few followers rarely follow back**; **the more followers you have, the more likely you follow back** (~0.7)
- **Who are the top link farmers?** Not spammers! Mostly **marketers, social media managers, "will follow back" accounts**, plus very popular accounts like **Barack Obama, Britney Spears, NPR Politics, UK PM, JetBlue**
  - Of the top 100K link farmers: 18,826 suspended, **76% still active, 235 verified**; a random check of 100 found 86 real people (business, internet marketing, entrepreneurship)
- **Profile of a link farmer:** very **high in-degree AND out-degree**, with an **in/out ratio ≈ 1** (just like normal users) → **hard to detect**. Their bios mention market, online, internet, social and promote their own business.

> **KEY TAKEAWAYS — Link Farming**
> - Twitter link farming = **follow-for-follow to raise in-degree** → visibility + influence.
> - **Legitimate, popular users do it too** (bloggers, marketers, celebrities, even Obama's account).
> - Spam on Twitter works better than email (**CTR 0.13%**) because it comes from trusted connections.
> - **16% of active accounts are bots.**

## 14. Phishing as a Semantic Attack & Social Phishing

**Bruce Schneier's three types of attack:**
1. **Physical** – attacking the machine itself (old style)
2. **Syntactic** – attacking software/logic (**denial of service, buffer overflow**)
3. **Semantic** – attacking **how humans interpret meaning** → **phishing** (you trust an email because it *looks* like it's from your professor)

**Semantic barrier** = the gap between the **user's mental model** (who I think I'm talking to, what I think this message means) and the **system model** (which remote machine I'm *actually* connecting to). **The bigger the gap, the easier the attack and the harder the fix.**

- Semantic attacks include phishing, **money mules**, **Nigerian 419 scams**
- Phishing themes: *update your information*, *verify your account*, *security alert*, *mortgage information*
- **Spotting a phishing email:** (1) suspicious **subject line**, (2) **urgency** ("your account will be suspended"), (3) a **link that goes somewhere else** (eBay "urgent notification from billing department" → kusi.org)
- Cost to a 100,000-employee organization ≈ **$3.76 million/year**. **APWG (Anti-Phishing Working Group)** and the FTC fight phishing.
- **ILOVEYOU virus** – an early famous email virus ("kindly check the attached love letter")

### The Indiana University Social Phishing Study (2005) — a classic
- **Idea:** does a phishing email work better if it seems to come **from a friend**?
- **Method:**
  1. **Harvest** public data from blogs and social networks
  2. **Correlate** it with the university address book to find friendships
  3. Send a **spoofed email** "from a friend" (Alice → Bob: "*This is cool! Hey, check this out*" + link)
  4. The link redirects to an attacker site (whuffo.com) asking for **university credentials**
  5. Credentials are **checked against the real university authenticator**
  6. Success → "**server overloaded, try again**"; failure → "authentication failed"
- **Groups:** control (email from an *unknown* @indiana.edu person) vs social (from a *friend*); students aged 18–24, April 2005

> **REMEMBER — the headline result:** **Control 16% vs Social 72%** fell for it.
> Even 16% is high, because the email came from a university address.

- **70% of credential entries happened in the first 12 hours** → **phishing sites must be taken down FAST**
- Many victims **entered credentials repeatedly** (some ~80 times!) because of the fake "server overloaded" message
- **Gender:** **females were more vulnerable**; emails were **more successful from the opposite gender** (male→female 78%, female→male 68%)
- **Age:** **younger students (freshmen) were most vulnerable**
- **Department:** the gap held for all majors; **Science showed the biggest gap (80% vs 0%)**, **Technology the smallest (~36%)**
- **Backlash:** participants called it **unethical, illegal, fraudulent**, claimed psychological harm, and demanded the researchers be fired. Many insisted *they* didn't fall for it → **people find it hard to admit being vulnerable** and **underestimate how much of their info is public**.
- **Recommended defences:** **education campaigns**, **browser-based warnings**, **faster takedown**, **digitally signed emails**, sharing less personal info

> **KEY TAKEAWAYS — Phishing**
> - Phishing is a **semantic** attack; it exploits the **mental vs system model gap**.
> - **Social context multiplies success (16% → 72%).**
> - **Speed matters**: 70% of victims fall within 12 hours.
> - Vulnerable: **females, opposite-gender senders, younger students**.

---

## PART F — IDENTITY & ANONYMITY

## 15. Identity Resolution / Profile Linking (merges L26, L33)

**The problem:** PK is *ponnurangam.kumaraguru* on Facebook, *ponguru* on Twitter and *ponguru* on LinkedIn. **Can we automatically tell these profiles are the same person?**

**Why it's useful:**
- **Advertising:** a page with 437K FB likes, 153K Twitter followers and 800K LinkedIn followers doesn't have 1.39M people; many overlap. Linking avoids **paying to reach the same person three times**.
- **Sentiment analysis:** count each person's opinion **once**, not once per network
- **Law enforcement:** is the person posting a malicious video on YouTube the same one posting on Twitter? Chase **one** suspect, not two.

**Why it's hard:** each network shows different information (YouTube = opinions/viewing, Tinder = personal, LinkedIn = professional, Facebook = personal). People also **change usernames**.

**Approach:**
1. List **common attributes** (name, username, profile picture, location, description, website, friends)
2. Compare them **syntactically** (text match), **semantically** (meaning) and by **graph** (common friends/followers)
3. High similarity → likely the same person
4. **Also use PAST values** (attribute history), not just current ones

**Easy wins: self-identification.** Users often link their own accounts: a Twitter bio linking to Tumblr, a personal website in both profiles, or a **Facebook album link posted on Twitter**. The **same post at the same time** on several networks also gives it away.

**Why usernames are a good attribute:** unique, **always public** (you can't hide your handle), length-limited, easy to collect.
- Platforms give each account a **permanent numeric user ID**. The handle can change but the ID doesn't, so you can track changes over time.
- **String similarity measures:** **Jaccard distance**, **edit distance** (e.g. "srishti_gupta123" vs "srishtigupta")

**Paper: "Other Times, Other Values: Leveraging Attribute History to Link User Profiles across OSNs"** (Paridhi Jain, PK's PhD student)
- Data: Twitter ↔ Instagram, Tumblr, Facebook; ~21K positive (same-person) pairs
- Features (~56): **username creation behaviour** (similar length, choice of characters, arrangement), **how usernames evolve over time**, **reuse patterns**
- Methods: exact match, substring match, and classifiers; **SVM with all features ≈ 76% accuracy**
- **Conclusion: using past usernames improves linking**
- If someone deliberately keeps two accounts totally separate, outsiders can't link them. **Facebook itself still can**, through IP address and access times.

### Username-changing behaviour
- **Facebook lets you change your username only once; Twitter allows unlimited changes**
- 376M users tracked: ~5–7% changed their screen name; over 2 months, ~35–40% of users changed their **profile picture ≥3 times**; almost nobody changes language or time zone
- Changing handles can make you **anonymous**: ponguru → explorer_pk → logicalTamilian

**Paper: "On the Dynamics of Username Changing Behavior on Twitter"**
- Seed set: **8.7 million users** (who tweeted about 17 events, Apr–Sep 2013), scanned **every 2 weeks**
  - **73.21% changed some profile attribute; ~10% (853,827) changed their username** in just 2 months
- Then 10,000 users who change names were scanned **every 15 minutes** for 14 months (scanning all would need 1,462 API tokens → **API rate limits**)
- **Pareto again: 20% of users made 85% of username changes**; one account changed **113 times** (bot-like)
- **65% choose a completely new name; 35% reuse an old one**
- **Popularity and activity are only weakly linked to how often people change names**
- **Space gain:** the median username is 11 characters; long names tend to be **shortened** (75%), short ones lengthened (61%). A short handle leaves **more room in the 140 characters** when people mention you.

> **REMEMBER — reasons for changing usernames:**
> - **Benign:** space gain, suit a **trending event** (IPL, football), **gain or lose anonymity**, adjust to life events (student → professor), avoid boredom.
> - **Malicious:** **obscured username promotion** (copy a popular handle to get attention) and **username squatting** (grab a name like "AmitabhBachchan" or PMOIndia to sell later; like domain squatting, e.g. housing.com).

- **Groups pass one username between several accounts** (e.g. "Peshawar_sms" moving across accounts in successive scans)
- **Limitation:** only 10K users could be scanned closely because of API restrictions

> **KEY TAKEAWAYS — Identity Resolution**
> - Link accounts by comparing attributes **now and in the past**; **usernames** are the best single attribute.
> - **Self-identification** (cross-links, same post on two platforms) makes linking easy.
> - **~10% of Twitter users change their username within 2 months; 20% of users make 85% of changes.**
> - Uses: ads deduplication, sentiment counting, **law enforcement**.

## 16. Anonymous Networks: The Whisper Study

**Anonymous network** = a platform where you **can't see who posted**: **4chan, Whisper, Secret, Yik Yak, Wickr**.

**Why people want them:** rising privacy awareness, **Snowden's revelations and PRISM** (government surveillance), and incidents (including in India) where a viral post had real consequences for its author. People want to speak **without attribution**.

**How Whisper (whisper.sh) works:**
- Posts ("**whispers**") are short texts **overlaid on an auto-chosen image** (a meme)
- Categories: popular, latest, LOL, confessions, relationships, OMG
- Reactions: **hearts** (like a "like"), **replies**, private messages
- **Nickname can be changed anytime**; a **PIN** replaces a password; it doesn't collect email or contacts
- **No persistent social links**: no friend/follower graph is stored, unlike FB/Twitter

**Four research questions:**
1. How do users interact in an anonymous environment?
2. Do users form **communities** like on traditional networks?
3. Does the lack of identity eliminate **strong ties** (people who always interact with each other)?
4. Does it eliminate **stickiness** (what keeps users engaged long-term)?

**Data (2014):** Whisper had no API, so it was **scraped**: **9M whispers, 15M replies, 1M GUIDs** (unique user IDs).
- The researchers showed Whisper that these IDs could be used to track users → **Whisper removed the GUID in June 2014** (research improving privacy)

**Findings:**
- **55% of whispers get no reply** at all; only 25% get a chain of ≥2 replies
- **54% of replies arrive within 1 hour, 94% within 1 day** → **if a whisper isn't noticed quickly, it never will be**
- 80% of users post fewer than 10 whispers+replies; 15% only reply; 30% only post

**Network structure compared with Facebook and Twitter:**

| Metric | **Whisper** | Facebook | Twitter | Meaning |
|---|---|---|---|---|
| Avg degree | **9.47** (highest) | 1.78 | 3.93 | interacts with many different people |
| Clustering coefficient | **0.033** (lowest) | 0.059 | 0.048 | the people you talk to don't know each other |
| Avg path length | **4.28** (shortest) | 10.13 | 5.52 | |
| Assortativity | **−0.011 (≈0)** | — | — | no preference for similar users |

> **REMEMBER:** These numbers mean **Whisper's interaction graph is essentially RANDOM**. There is no small-world/community structure, and **users interact with strangers**.

**Content deletion:**
- **18% of whispers were deleted** within 3 months (**vs ~4% on Twitter**)
- **Deletion ratio** of a word = whispers containing the word that were deleted ÷ all whispers containing it
- **Most deleted topics: sexting, selfies, chat** · **Least deleted: emotion, religion, entertainment, life stories, work, politics**
- **70% of deletions happen within 1 week**, mostly within 24 hours (peak 3–9 hours after posting)

**Location and engagement:**
- Interacting pairs are **close by: 90% in the same state, 75% within 40 miles**
- Total users keep growing, but **daily new posts stay flat**; new users contribute ~20% of content → **weak stickiness** (people try it, then leave)

> **KEY TAKEAWAYS — Anonymous Networks**
> - Whisper's graph is **random**: high degree, low clustering, short paths, assortativity ≈ 0 → **no strong ties, talking to strangers**.
> - **18% of content deleted** (vs 4% on Twitter), mostly sexting/selfie/chat, mostly within a day.
> - Attention is instant or never (**94% of replies within a day**).
> - Anonymity needs **content moderation**.

---

## FINAL REVISION SHEET — Most-Asked Facts

| Topic | Fact to remember |
|---|---|
| 5 V's | Volume, Velocity, Variety, Veracity, **Value** (5th) |
| FB vs Twitter | FB **bidirectional**; Twitter **unidirectional**, 140 chars |
| First crisis use of Twitter | **2009 Hudson River** plane (jkrums) |
| Credibility features | user (F1) vs tweet (F2); **tweet features better** |
| Sandy classifier | **Decision Tree + tweet features = 97.65%** |
| Credible tweets | **17%** credible info, 30% informative, 14% spam |
| Annotation agreement | **Cronbach's Alpha ≥ 0.7**, ≥3 annotators |
| TweetCred | Chrome extension, **1–7 score**, **45 features**, user feedback |
| WOT | domain → excellent/good/satisfactory/poor/very poor |
| Boston viral tweets | **29% fake, 20% true, 51% generic** |
| Boston fakes | ~**76% from mobile**; 32K new accounts, **19% suspended** |
| Westin 1967 | privacy = control over **when, how, to what extent** info is shared |
| Westin types | Fundamentalist ~25%, **Pragmatist majority**, Unconcerned ~15–18% |
| Forms of privacy | information, communication, territorial, bodily |
| India survey | 10,427 people; **42%** trust settings; **27%** accept opposite gender |
| Sweeney | **ZIP + birth date + gender** → unique ID; k-anonymity |
| Face re-ID | **1 in 10** dating · **38%** campus · **27%** SSN 5 digits |
| Foursquare mayor | most check-ins in the **last 60 days** |
| Home inference | **~78% within 50 km** (Foursquare); Twitter **82%**, G+ 72%, FSQ 67% |
| Privacy policies | **244 hrs/yr**, **$781B** |
| Nudges | **Picture, Timer (10 s), Sentiment**; IRB needed |
| Police response time | avg **30 hrs**, min 4 min, max 211 hrs |
| Police effect | police replies **lower anxiety**, close threads faster |
| Hashtag hijacking | Coca-Cola **#RoyalBaby**, DiGiorno **#WhyIStayed** |
| Twitter spam | 8% of URLs malicious; **CTR 0.13%** > email; **16% bots** |
| Link farming | follow-back for in-degree; done by **legit popular users too**; in/out ≈ 1 |
| Schneier | physical, syntactic, **semantic** (phishing) |
| Social phishing | **72% vs 16%**; 70% within 12 hrs; females & opposite gender more vulnerable |
| Username changes | **~10%** in 2 months; **20% users → 85% changes**; Twitter unlimited, FB once |
| Profile linking | SVM **~76%**; past usernames help |
| Whisper | **random graph**; 18% deleted; 55% no reply; GUID removed June 2014 |
