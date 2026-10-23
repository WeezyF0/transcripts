# PSOSM — Privacy & Security in Online Social Media (Exam Notes)
NPTEL · Prof. Ponnurangam Kumaraguru (PK) · Precog, IIIT-Delhi · Lectures 1–34, overlapping content merged

---

## 1. OSM Basics
- **Social media types:** social networks (FB, Twitter, LinkedIn), publishing/crowdsourced (Wikipedia), social games, virtual games
- **Platform → core unit:**
  - YouTube: video (upload, like, share, channel, subscribe, report spam)
  - Flickr / Instagram: images
  - Foursquare: location (check-in, tip, done, mayor, badges)
  - LinkedIn: professional *connections*
  - Pinterest: images pinned to *boards*; fastest growing (first 1M users came fast)
  - Periscope: live video streaming
  - Tinder: location-based left/right swipe
  - Google+: *circles*, "+1"
  - Twitter: microblog, 140 chars
- **New categories:** *ephemeral* (content self-destructs, e.g. Snapchat), *anonymous* (poster unknown, e.g. Whisper)
- ~215–220 popular SN services; India: ~1 in 13 → 1 in 9–10 people use SNs (driven by mobile phones)
- **Online in 60 s (2013 → now):** FB 2.5M → 3.5M posts (also quoted 3.3M) · Twitter 278K → 420K tweets · YouTube 100 → 400 hrs of video uploaded
- **5 V's:** Volume (size) · Velocity (speed of generation) · Variety (types) · Veracity (is it true?) · Value (5th, newer: useless without value)
- **Facebook:** *bidirectional* (friend request must be accepted); posts = text/image/video; likes, comments, shares; pages; groups (public/private); data stored as a **graph**
- **Twitter:** *unidirectional* (follow anyone); followers / following; timeline; notifications; hashtags; trends (location-based, hashtags or plain words); retweet, reply, like (earlier "favorite"); **mention** (@handle → notifies that user)
- **Verified account (blue tick):** for celebrities, high-follower accounts, or paying marketing firms; only a small fraction (~1M users) are verified
- Top FB/Twitter accounts are mostly sports and music stars
- "Reality vs perception" video: what people post ≠ what they actually do

## 2. Incidents (positive & negative)
- **2009 Hudson River plane landing:** jkrums tweet "There's a plane in the Hudson…" → first use of Twitter in a crisis; citizens helped before first responders arrived
- Lost child at an Indian railway station reunited with parents in 20 min (photo tweet tagging the Railways Minister went viral); "Find your missing child" uses only social media
- Teen suicide after **cyberbullying** on FB
- **UK/London riots:** OSM used to *organize* the violence; rumour that London Zoo animals had escaped
- Nepal earthquake: government used OSM for relief; **Egypt revolution:** organized via Twitter/FB
- **Boston bombing fakes:** "RIP 8-yr-old boy… running for Sandy Hook kids" (no such child); "$1 per RT" donation scam
- **AP verified account hacked:** "Two explosions in White House, Obama injured" → market impact
- **Fake images:** Chennai floods 2015 crocodile on streets; Hurricane Sandy shark in water, "McDonald's Virginia Beach flooded" (old photo), movie still
- Robin Williams fake goodbye video; Ebola hoax / "salt water cure"; false shootouts → panic in Mexico City
- **MI6 chief's wife** posted FB photos → privacy scandal, his appointment was hit
- People lost jobs over posts; employees leaked company projects
- FB knowing who you are → personalization, targeted ads

## 3. Data Collection Toolkit (tutorials, merged)
- **API (Application Programming Interface):** programmatic "tunnel" to OSM data; every API has **rate limits**
- **Never share** API key / secret / access token: anyone holding them collects data as you
- **Data formats:** **JSON** (JavaScript Object Notation, key–value; used by most OSM) · XML (Extensible Markup Language) · viewer: jsonviewer.stack.hu
- **Setup:** VirtualBox + Ubuntu 14.04 (1 GB RAM, 8 GB disk, NAT network; partitions = swap 1 GB (= RAM) + ext4 at `/`); `sudo` = super user do; `apt-get update`; `pip`; `requests.get()` → HTTP **200 = OK**
- **Facebook Graph API:**
  - Objects = nodes with unique numeric IDs (users, pages, posts, photos); connections = edges (friendship, likes, comments)
  - Graph API Explorer: **access token** = auth string issued via **OAuth**; *app = door, token = key*
  - Permissions: email, user_birthday, user_education_history, user_photos, user_friends, user_posts; a missing permission → debug error
  - Short-lived token lasts ~1–2 hrs; **extended token ~60 days** via `oauth/access_token?grant_type=fb_exchange_token&client_id=<App ID>&client_secret=<App Secret>&fb_exchange_token=<short token>` (registering as a developer needs phone verification)
  - Queries: `me?fields=id,name`, `me/posts`, `search?q=nptel&type=page|group|event|user|place` (returns **public data only**), `<page>/feed` (reverse chronological; pinned post on top), `<post>/reactions?type=LOVE` (case-sensitive)
  - Post ID = `userid_postid`
  - **Paging:** default limit 25; `paging.next` / `paging.previous` URLs; raise the `limit` parameter
  - Friends list returns only friends who also used the app (privacy change)
  - v2.0 returns more default fields than v2.6; new apps can't use old versions
- **Twitter API:**
  - Create app at apps.twitter.com (needs verified phone)
  - **4 keys:** consumer key, consumer secret, access token, access token secret
  - APIs: **REST** (user data, timelines, followers), **Search** (past tweets; `result_type=mixed` = popular + recent, `count=100`), **Streaming** (real-time; `track=` keyword or `follow=` user ID)
  - **Twython** = Python wrapper
- **Storage:**
  - **MySQL:** relational, rows/columns, SQL; Python lib MySQLdb; tweet_id as PRIMARY KEY; `INSERT IGNORE` skips duplicate keys; `SELECT COUNT(*)`; viewer **phpMyAdmin**
  - **MongoDB:** open-source, non-relational, document-based; Python lib **pymongo**; stores the whole tweet JSON; `_id` = unique record ID; an empty DB isn't listed in `show dbs`; `db.tweets.count()/find()/findOne()`; viewer **RoboMongo**
- **NLTK (text):**
  - `.encode('utf-8')` fixes Unicode print errors; `nltk.download()` (`punkt` for the tokenizer; "all" ≈ 10 GB)
  - `word_tokenize` → lowercase → `Counter.most_common`
  - **Stemming** (PorterStemmer: course/courses → course; certify/certification → "certif")
  - **Stopwords** (the, and, to…); drop tokens shorter than 2 chars (punctuation)
  - **n-grams** (bigram "Barack Obama", trigram "to know more")
  - **POS tagging** (JJ adjective, NN noun, IN preposition, CD number, VBP verb) → grammar as a feature
- **Highcharts (visualization):**
  - Interactive JS charts; Python wrapper `python-highcharts`; output is HTML
  - **Bar** (length ∝ value) · **Line** (connected points, change over time) · **Scatter** (unconnected points, e.g. followers vs friends) · **Bubble** (x, y + z = bubble size)
  - Highcharts Cloud: paste CSV → chart
  - Followers = people who follow X; friends = people X follows

## 4. Social Network Analysis (SNA) + Gephi
- Graph = nodes (users/pages/groups) + edges (follows/likes)
- **Representations:**
  - Adjacency matrix: N×N, 1 if an edge exists; sparse and wasteful when edges are few
  - **GraphML:** XML; node `id`, edge `source`/`target`
  - CSV: nodes file needs an `Id` column; edges file needs `Source`, `Target` (+ optional `Type`: directed/undirected)
  - Gephi also reads GML, Pajek NET, UCINET DL, Excel
- **twecoll:** `init` (consumer key/secret + PIN) → `fetch` (friends of friends) → `edgelist` → `.gml` file
- **Degree:** in-degree (edges entering; a self-loop counts) · out-degree · total = in + out
- **Centrality:**
  - In-degree: most followed / most influential
  - Out-degree: follows the most accounts
  - **Betweenness:** number of shortest paths passing through the node
  - **Closeness:** lowest total distance to all other nodes
  - Eigenvector centrality
- **Community** = strongly connected group; **modularity** = fraction of edges falling inside groups
- **Other metrics:**
  - Network diameter
  - **Density:** how close the graph is to complete
  - Clustering coefficient
  - Average path length
  - **Assortativity:** do nodes link to nodes of similar degree? Near 0 → random graph
  - Connected components (strong/weak); PageRank
- **Gephi:** open-source
  - Tabs: Data Laboratory · Overview · Preview (curved/straight edges, labels, export PDF/PNG/SVG)
  - Layouts: Fruchterman–Reingold, ForceAtlas/ForceAtlas 2, contraction, no-overlap
  - Colour by modularity class, size by in-degree
  - **Filters:** attribute (equal / partition / range), edge (weight, type, self-loop), topology (k-core, degree, components), operators (intersection / union / complement)
  - Export a filtered graph to a new workspace

## 5. Trust & Credibility / Misinformation
- **Boston graph** (x = hours after blast, y = log tweets; red = true, green = rumour, blue = total): rumours peak within ~2 hrs, true info lags (~9 hrs) → two goals: **bring true info earlier, flatten rumours faster**
- **Generic methodology:** collect data → characterize → extract features → ground truth → build model → evaluate
- **Analysis frame:** **who, when, where, what, why, how** (why/how are hardest)
- **Data collection:** start from a trending hashtag → add co-occurring words = **query expansion**
- Tweet volume **spikes match real-world events** (blast, suspect photos released, "manhunt is over")
- ~1% of tweets are geotagged (Twitter's figure)
- **3 information sources:** user profile · network · content posted
- **User features (F1, "source-based"):**
  - #friends, #followers, **follower–friend ratio** (popular accounts follow far fewer than follow them)
  - #times listed (Twitter **lists** signal expertise)
  - Has URL, verified
  - **Account age** (like domain age in web security)
- **Tweet features (F2, "message-based"):** length, #words, contains ? / !, count of ? / !, happy/sad emoticons
- **Hurricane Sandy** (22–31 Oct 2012, ~$75B damage, NE US):
  - 1,782,526 tweets; ~1M unique users; ~622K tweets with URLs
  - Ground truth = the **Guardian's** list of fake/true images (10,350 tweets / 10,215 users with fake images)
  - **5-fold cross-validation**; **Naive Bayes** (Bayes' theorem) vs **Decision Tree** (graph-based)
  - Best: **Decision Tree + tweet features = 97.65%**; tweet features beat user features
- **Network/diffusion analysis:** compare spread at hour n vs n+1; the originator isn't necessarily the most central node later
- **Annotation:**
  - ≥3 annotators per tweet; inter-annotator agreement measured by **Cronbach's Alpha ≥ ~0.7**
  - Crowdsourcing via **Amazon Mechanical Turk** ("turkers", paid small amounts) or CrowdFlower
- **Multi-event study** (UK riots, Libya crisis, Virginia earthquake, US downgrade):
  - Step 1 labels: contains info / related but no info / unrelated / skip
  - Step 2 labels: definitely credible / seems credible / definitely incredible / skip
  - Result: 30% of tweets have info, **17% credible**, 14% spam
  - Metric: **NDCG** (Normalized Discounted Cumulative Gain, a ranking-quality measure)
  - Best features: tweet + user → **"what you post + who you are"**
- **TweetCred:**
  - Chrome extension; real-time **credibility score 1–7**; users agree/disagree → feedback retrains the model
  - **45 real-time features**, incl. swear words, positive/negative emotion words, **WOT** score of the URL, YouTube like/dislike ratio
  - **Top 10 features:** #chars, #unique chars, #words, user has location, #retweets, tweet age, contains URL, contains "via", statuses & followers, friends & followers
  - Users: emergency responders, firefighters, journalists/news media, general public
- **Facebook vs Twitter:** FB is bidirectional and personal → a friend's post is trusted more; features and API data differ
- **Facebook Inspector (FBI):**
  - TweetCred equivalent for FB: Graph API → features → ground truth → feature vectors → **supervised** model → **RESTful API**
  - Chrome & Firefox plugin; flags malicious / low-confidence posts
- **WOT (Web of Trust):** input a domain → rating (excellent / good / satisfactory / poor / very poor) + confidence score; other domain features: age, registrant

## 6. Boston Marathon Paper ("$1/RT #PrayForBoston: Analyzing Fake Content on Twitter") — merges L9, L34
- **Event:** twin blasts at the finish line, **15 Apr 2013**, ~18:50 GMT; **3 killed, 264 injured**; first tweet within ~3 min, first image within ~4 min
- **Data:**
  - **7.8–7.9M tweets**, 3.6M users, 3.4M with URLs, ~62K geotagged
  - Streaming API with keywords (#bostonmarathon, #prayforboston, #watertown, #manhunt, Sean Collier, #BostonStrong, #oneboston, "boston explosions", "boston suspect"…)
  - Collection started **45 min after** the blast, but later retweets captured earlier tweets → largest known dataset
- Boston Police used its official account to share suspect photos and ask the public for help
- **Annotation:**
  - Top 20 viral tweets (~400K tweets ≈ 6% of all): **29% rumour/fake, 20% true, 51% generic** (opinions, condolences; #PrayForBoston ~87K RTs)
  - Earlier version: 6 rumours / 7 true / 7 generic
- "$1 per RT" came from fake account **@_BostonMarathon**, ~50K RTs; "8-yr-old" rumour >30K RTs
- 3,249 users tweeted both true and fake content
- **Source:** **~75–76% of fake tweets posted from mobile** (true 64%, generic 51%); mostly iPhone; web used more for true/generic
- **Rumour seeds** mostly had few followers (one seed had ~73K); spread when popular/verified accounts retweeted without checking
- **Fake-content followers** lowest (below true, below N/A); verified accounts pushed fake content early on
- **Virality prediction:**
  - Impact metric from social reputation, global engagement, topic engagement, likability, credibility
  - **Linear regression R² ≈ 0.7** → can predict how viral a fake tweet will become from its current propagators
- **Suspended profiles:**
  - **~32,000 new accounts** created during the event; **19% deleted/suspended** within 2 months
  - ~6,000 suspended profiles; spike right after the blast (~1,400 in the first hours)
  - Some fake accounts still active during collection
  - Suspension happens via mass user reports or government request
- **Network of fake accounts:** a closed, tightly connected community (like phishing gangs); 69 of 6,000 had edges
  - Interaction types: single links, closed community, **star topology**, self-loops (mentioning themselves)
- Malicious users exploit events for e-crimes: impersonation, propaganda

## 7. Privacy — Concepts & Perceptions
- Privacy is **contextual**: different at home, class, work…
- **Robert Post** (*Three Concepts of Privacy*): "a value so complex, so entangled in competing and contradictory dimensions… I despair whether it can be usefully addressed at all"
- **Alan Westin** (*Privacy and Freedom*, **1967**): "claim of individuals, groups or institutions to **determine for themselves when, how and to what extent** information about them is communicated to others"; each person keeps balancing the desire for privacy against disclosure → **privacy = control over information**
- **Westin's 3 categories** (30+ yrs of US surveys):
  - **Fundamentalists ~25%** — share nothing
  - **Pragmatists ~57–60%** — trade-off depending on the situation
  - **Unconcerned ~15–18%** — would give a password for a chocolate bar
- Collectivist societies emphasize group privacy; individualistic societies protect individual privacy
- **4 forms:** **information** (internet) · **communication** (phone) · **territorial** (home/city/country) · **bodily** (self; e.g. CCTV)
- Cartoon "On the Internet, nobody knows you're a dog" (mid-90s) → now you get personalized dog-food ads (profiling from behaviour)
- **Privacy policies:** nobody reads them; reading each visited site's policy monthly = **244 hrs/yr** per person → **$781B/yr** US national opportunity cost
- **India privacy survey:**
  - 20 interviews, 4 focus groups, **10,427 respondents**, **83 questions**, all states but one (TN 8.57%); collected offline (malls, stations) + online
  - Demographics: mostly 18–39; 67% male / 32% female
  - **Q42** (6,855 responses), FB privacy: **42% "privacy settings set → data secure"** (a false belief), 19% not a concern, 23% concerned despite settings, 8% concerned but still share, 6.7% concerned so don't share
  - **Q43** (6,929 responses), accept friend request from: **27% opposite gender**, 10.12% nice profile picture, 2.99% anyone
  - **FB location setting:** everyone 39%, friends 33%, friends-of-friends 12.5%, network 5.7%, customized 3.1%
  - **Regional-language "phone switched off" message** (reveals your state): 54% call it privacy-invasive, ~22% disagree, rest neutral

## 8. Privacy — Face Re-identification (photos + public data)
- **Photo stats:**
  - 2000: 100B photos shot worldwide
  - 2010: 2.5B photos/month uploaded on FB
  - Now: 1.8B/day across FB, Instagram, Flickr, Snapchat, WhatsApp
  - FB/Microsoft/Google/Apple bought face-recognition companies
- **4 converging trends:**
  1. Rising public self-disclosure
  2. Better face-recognition accuracy (FB only has to search among your friends)
  3. Cheap cloud computing
  4. Better re-identification techniques
- **Re-identification** = combine *unidentified* data (dating sites like match.com/shaadi.com, Flickr, CCTV, pseudonyms) with *identified* data (FB, LinkedIn, government sites) → uniquely identify people + infer sensitive info
- **Latanya Sweeney (k-anonymity):**
  - Medical data (ethnicity, visit date, diagnosis, procedure, medication, charges) + voter list (name, address, date registered, party, last voted)
  - Shared fields **ZIP + birth date + gender** → uniquely re-identifies most US citizens
- **Tools:** **PittPatt** (face recognition, later bought by Google); now **TensorFlow** (open-source ML library)
- **Exp 1 (online–online):**
  - FB profiles from one US city (~270K profiles, ~274K images, ~110K faces) vs a dating site in the same city (~6K profiles, ~5K faces)
  - >500M pairs compared; best match kept; MTurk validation (Likert 1–7, ≥5 turkers per pair)
  - Result: **highly likely 6.3%, likely+ 10.5% → ~1 in 10** dating profiles re-identified
- **Exp 2 (offline–online):**
  - Campus booth, 3 photos per participant, 3 days; FB college network ~25K profiles / ~26K images / ~114K faces
  - Matching ran in the cloud while participants filled a survey; matches shown on its last page
  - Result: **98 students → 38% matched to the correct FB profile** (even one who said he had no FB photo)
- **Exp 3:** faces + public data → **SSN first 5 digits for 27% of subjects in ≤4 attempts** (Indian analogue: Aadhaar)
- **pleaserobme.com:** flagged users posting from away (account created in Delhi, posts about Chennai weather) → home likely empty → burglars; site later taken down

## 9. Privacy — Location (LBSNs) — merges L16, L29, L30, L32
- **LBSNs:** Foursquare, Yelp, Gowalla, FB check-ins, Twitter geotags
- **Foursquare:**
  - **Check-in** (visit via GPS; visible to friends only) at **venues**
  - **Mayor** = most check-ins at a venue in the **last 60 days** (perks: discounts, free parking)
  - **Badges** (gamification, e.g. newbie)
  - **Tips** (venue reviews); **done / to-do** (agree with a tip / plan to visit)
  - **Mayorships, tips and dones are PUBLIC** → information leakage
- People don't move much → home is inferable within a few km
- **Paper 1: "We Know Where You Live: Privacy Characterization of Foursquare Behavior"**
  - Data Aug–Oct 2011: **~13M users** (≈ all of Foursquare), 10M tips, 9M dones, 15M mayorships, 15M venues
  - Fields: UHC (user home city), VL (venue location), GI (geographic info); pruned invalid (e.g. "heart", mid-sea), ambiguous, non-geographic, empty entries
  - Reverse geocoding (Yahoo PlaceFinder)
  - Mayorships/tips/dones per user and per city are heavily skewed → **power law / Pareto 80-20**
  - Mayorship–tip correlation across cities **0.78**
  - Top tip cities: New York, Jakarta, São Paulo; top done cities: New York, Chicago, San Francisco
  - Maps: mayorships densest (79K cities, even Svalbard) > tips > dones (tourist/developed areas)
  - Inter-activity gap: ~50% of users post consecutive tips/dones ≤1 hr apart; avg gap ≥450 hrs (~20 days) for 50%; max gap ≤167 hrs (~1 week) for 80%
  - Displacement: ~36% ≈ 0 km; 70% avg ≤150 km; ~10% max ~6,000–7,000 km (international)
  - **Returning time:** multiples of **24 hrs** (daily routine), bump at 168 hrs (weekly)
  - **Home inference = majority vote** over the locations of a user's mayorships/tips/dones
    - **Class 0** = single activity · **Class 1** = many activities, one predominant location · **Class 2** = no predominant location (can't infer)
  - Accuracy: mayorship alone 51.6% (Class 0); Class 1 ~67% city, ~70% state, higher for country (city < state < country)
  - Inferred vs declared home: 46% within 50 km → overall **~78% of users' home city correct within 50 km**
- **Paper 2: "Beware of What You Share: Inferring Home Location in Social Networks"** (Foursquare + Google+ + Twitter)
  - **Home city accuracy:** Foursquare **67%**, Google+ **72%**, Twitter **82%**
  - **Within 50 km:** 78.5% / 64% / 87%
  - **Data:**
    - Foursquare: same 13M-user dataset (~16M venues, 15M mayorships, ~11M tips, ~10M likes/dones); home city = free text ≤100 chars; venue city 30 / address 127 chars
    - Google+: 27M profiles crawled; 7M list places lived, 5K an address, 7M education, 6M employment
    - Twitter: Streaming API Apr–Jun 2012, 120M tweets, ~20M users; only **0.5% geotagged** (~700K tweets, ~300K users)
  - Most location info is at **city level** (Foursquare ~80%, G+ 79.6%, Twitter 62.5%)
  - Heavy tails again: 90% of users have ≤10 mayorships; <5% of Twitter users post >10 geotagged tweets
  - Models: Foursquare (mayorship, tip, like, friends); Google+ (friends, education, employment); Twitter (geotagged tweets)
  - **Friend-model refinement:** drop users with < k_min or > k_max friends (noise) → +21% for Google+
  - **Residence (exact home):** Twitter 35% exact (0 km), 73.67% within 20 km; Foursquare 52.73% within 5 km, 77% within 20 km; Google+ only 5.23% exact (uses work/study places)
  - Twitter is best because geotags give exact coordinates
- **Research paper structure:**
  - Abstract → Introduction (30,000-ft view, gap, what we did, contributions) → Related work → Dataset (exploratory data analysis; aids **reproducibility**) → Method → Results → Conclusion/limitations
- Venues for this research: **WWW, ICWSM, COSN, CSCW**

## 10. Policing & OSM — merges L16, L17, L18
- **#myNYPD:** NYPD asked for photos with officers → flooded with brutality photos, spread to #myLAPD
- **Indian police on OSM since ~2010–11:** Bangalore City Police (verified FB page), **@CPBLR** (~10K tweets, follows 60; followers 335K → 688K by Aug 2016), Delhi Traffic Police, Hyderabad City Police (verified), UP, Guwahati, Kolkata, Pune, Jaipur, Mumbai
- Indian police pages **allow citizens to post**; YouTube use is small
- **Fake police handles** ("Delhi Traffic Polize", fake Kolkata Police); **"egg" profile** = default Twitter avatar; only verification or a link from the official .gov.in site confirms a handle
- Precog keeps a list of ~80–85 police handles + dashboard (posts/likes/comments over time)
- **Bangalore City Police FB study:**
  - Goal: can OSM give police **actionable information** (time, location, problem) about crime and residents' opinions?
  - Data (2014): ~1,600 comments, 255 posts
  - Coding: **24 citizen content categories, 2 styles (formal/informal), 4 police response types** — acknowledged 21% · reply/suggest solution ("please lodge a complaint") 22% · follow-up (asks details) · ignored
  - Top citizen topics: neighbourhood concerns > appreciation > suggestions, auto drivers, fraud, traffic; most likes on satisfaction/appreciation/success-story posts
  - Police style almost always **formal**
  - **Response time: avg 30 hrs, max 211 hrs, min 4 min**
  - Geo heat maps; **word trees** ("worried", "why", "need", "want"); direct vs indirect info (about self vs a friend/area)
  - **Mutual accountability** (police ↔ citizens); community policing; understanding fears, needs, wants
- **85 police FB pages study (2010 – Apr 2015, avg page age ~3 yrs):**
  - **85,408 police posts, 47,474 citizen wall posts** (~24K with ≥1 comment)
  - **4 RQs:** topical · engagement · emotional exchange · cognitive & social orientation
  - **Methods:** n-grams, **K-means** clusters, **valence** (positive/negative sentiment), **arousal** (intensity); tools **LIWC** (Linguistic Inquiry & Word Count, ~35–37 categories), **ANEW** dictionary, NLTK
  - **Topics:** police → advisories, case status (P+C threads discuss rules, safety, violations); citizens → **"please take action"**
  - **Police-initiated threads are focused** (awareness drives, safety campaigns, action reports, advisories); citizen-initiated are diverse (appreciation, news, tips/complaints, neighbourhood problems, missing people)
  - **Engagement:** when police join citizen threads, comments drop (~26% lower total, 9.49% lower avg) → **police close the loop early**
  - **Emotions** (citizen-initiated, with vs without police): negative affect higher (0.021 vs 0.018), **anxiety lower (0.001 vs 0.003)**, anger higher (0.006 vs 0.005), arousal higher
  - **Cognition:** citizen posts are self-focused ("I" is the top pronoun)
  - **Why it matters:** community sensing, emotional support, consensus decisions, predictive analytics, **early warning**, records for decision-makers

## 11. eCrime on OSM — Types
- **Phishing:** tricks you into giving login details on a fake site
  - **Spear phishing / context-aware:** targets a specific group (e.g. this course's students)
  - **Whaling:** targets CEOs
  - **Vishing:** voice/phone; **Smishing:** SMS
  - **Social phishing:** uses info from social networks
  - On OSM: timeline links, "Facebook technical support", "Facebook new login system"
  - **FB credentials** are now prized (reveal friends, interests, usage patterns)
- **Fake customer-service accounts:** look-alike handles reply to genuine complaints that tag a bank
- **Fake comments on popular posts** (e.g. Olympics) → fake site/malware
- **Fake live-streaming videos** (Olympics, cricket, Rio)
- **Fake online discounts** (fake Netflix "40% off")
- **Fake surveys & contests** (personality tests, "win Rs 1000")
- **Fake Foursquare tips** (XanGo mangosteen juice link unrelated to the venue)
- **Social reputation manipulation:** fake likes, reviews (**Amazon sued 1,000 people** over fake reviews; Flipkart), fake followers, LinkedIn endorsements
- **Clickbaiting**
- **Hashtag hijacking:** using an unrelated trending tag to sell — Coca-Cola **#RoyalBaby**; DiGiorno Pizza **#WhyIStayed** (a domestic-violence tag) → had to apologize
- **Compromised accounts** (AP White House tweet)
- **Impersonation:** fake accounts of individuals (Kiran Rao complaint) and organizations (police)
- **Work-from-home scams** (Pinterest: "$5–40 per survey")

## 12. Spam & Link Farming on Twitter — merges L20, L22
- **PageRank:** rank rises with in-links (high in-degree)
- **Link farming** = creating non-genuine links to inflate rank = spamming a search engine's index (**spamdexing**)
- Twitter = "web within the web", where news breaks; Twitter search ranking uses connections, followers, verified status, PageRank-like scores → top results get the clicks
- **#followers = social reputation**; **Klout score** (1–100 online influence; PK = 24)
- **On Twitter:** spammers follow many users hoping they follow back (**reciprocity**) → higher in-degree → more search visibility
- **Web vs Twitter:**
  - Web: done only by spammers; hyperlinks are rarely reciprocated
  - Twitter: done by spammers **and legitimate popular users**; follow-backs are likely
- **Literature:**
  - *"Suspended Accounts in Retrospect"*: 1.1M suspended accounts over 7 months; 1.8B tweets (80M from spam accounts); spam campaigns of 145K accounts persist for months; **77% of spam accounts suspended within a day of their first tweet**
  - *"@spam: The Underground on 140 Characters or Less"*: **8% of 25M URLs** → phishing/malware/scams; **click-through 0.13%**, far above email spam (because it comes from people you follow)
  - *"Detecting and Analyzing Automated Activity on Twitter"*: **16% of active accounts highly automated** (minute-of-hour vs hour-of-day plot); **11% of "browser-only" accounts are bots spoofing their source**
- **Dataset:** entire Twitter 2009 — **54M users, 1.9B links**; edge B→A means B follows A (B = follower, A = following)
- **Terms:** *spam targets* (users a spammer follows), *spam followers* (users who follow the spammer back), *targeted followers*
- **Numbers:**
  - 379,340 accounts suspended (Aug 2009 – Feb 2011)
  - 41,352 posted ≥1 blacklisted URL shortened with **bit.ly / TinyURL** (shorteners popular because of the 140-char limit)
  - Spam targets ~13M, targeted followers ~1M, spam followers ~248K; **82% of spam followers are also spam targets**
  - Spammers rank high on PageRank: **7 in the top 10K, 304 in the top 100K, 2,131 in the top 1M**
  - **Top 100K spam followers supply 60% of all links** spammers get; top ones reciprocate almost every follow
  - Low in-degree users rarely follow back; **responsiveness rises with in-degree** (~0.7)
- **Top link farmers:** Larry Wentz (internet affiliate marketing), Judy Rey Wasserman, Chris Latko ("will follow back"), Paul Merriwether, Aaron Lee (social media manager); high-PageRank ones include Barack Obama, Britney Spears, NPR Politics, UK PM, JetBlue
- **Top 100K link farmers:** 18,826 suspended, 4,768 not found, **76% still alive, 235 verified**; of 100 random ones, 86 were real (business, internet marketing, entrepreneurship, money, social media)
- **Link farmer profile:**
  - **Very high in-degree AND out-degree** compared with spammers and random users
  - **In/out ratio ≈ 1** (same as normal users) → **hard to detect**
  - Bios: market, online, internet, social; promote their business with external links (random users: life, music, love)
- **Conclusion:** legitimate, popular, active users (bloggers, experts) do link farming → boosts their **social capital & influence**

## 13. Phishing & Semantic Attacks (Social Phishing) — L24
- **Bruce Schneier's attack types:**
  - **Physical:** access to the machine
  - **Syntactic:** software flaws (DoS, buffer overflow)
  - **Semantic:** target how *humans* assign meaning → phishing
- **Semantic barrier** = gap between the user's **mental model** (who the other party is, what the message means) and the **system model** (actual remote machine) → the larger the gap, the harder to fix
- Semantic attacks: phishing, money mules, **Nigerian 419** scams
- Phishing categories: update info, verification, security alert, mortgage info
- **Phishing email cues:** subject line, **urgency**, deceptive link (eBay "urgent notification from billing department" → kusi.org)
- Cost to a 100K-employee org ≈ **$3.76M/yr**; **APWG** (Anti-Phishing Working Group), FTC
- **ILOVEYOU** virus ("kindly check the attached LOVELETTER")
- **Indiana University social phishing study (Apr 2005, ages 18–24):**
  - Harvested blogs/SNS → correlated with the university address book → spoofed email "from a friend" ("This is cool! Hey, check this out") → redirect to attacker site (whuffo.com) → credentials checked with the university authenticator → shown "server overloaded, try again" (phished) / "auth failed"
  - **Control (unknown @indiana.edu sender) 16% vs Social (friend) 72%**
  - **70% of authentications in the first 12 hrs** → **takedown must be fast**
  - Repeated logins (some ~80 times) because of the fake "overloaded" message
  - **Gender** (18,294 M / 19,527 F): **females more vulnerable**; **opposite-gender sender works better** (M→F 78%, F→M 68%)
  - **Younger (freshmen) more vulnerable**; significant across all majors; **Science largest gap (80% vs 0%)**, Technology smallest (~36%)
  - **Backlash:** "unethical, illegal", psychological cost, calls to fire the researchers; victims denied falling for it; people underestimate how much is public
  - **Fixes:** education campaigns, browser solutions, faster takedown, **digitally signed emails**, share less personal info

## 14. Privacy Nudges — L23
- Goal: help users make informed decisions and **avoid regrettable disclosures**
- MIT tool: shows profile pictures of a mailing list's recipients before sending (frequent contacts shown bigger)
- **FB nudges (Chrome extension):**
  - **Picture nudge:** shows profile pics of who will see the post (friends, friends-of-friends, anyone on the internet)
  - **Timer nudge:** 10 s to cancel
  - **Sentiment nudge:** warns the post reads as negative
- **Method:** **IRB** (Institutional Review Board) approval for human-subject studies; recruited via flyers, email, Craigslist; **21 completed** the field study, **13 exit interviews**
- **Metrics:** changes to inline privacy settings, cancelled/edited posts, post frequency, topic sensitivity
- **Results:**
  - Picture nudge → users narrowed the audience (e.g. "friends except acquaintances"), cancelled posts
  - Timer nudge → "annoying at times, handy at times", made people think
  - Sentiment nudge → missed context (errors), many cancelled posts, **posts dropped 13 → 7**
- More work needed on which nudge works in which context (a timer is a nuisance for frequent posters)

## 15. Identity Resolution / Profile Linking — merges L26, L33
- **Question:** are FB *ponnurangam.kumaraguru*, Twitter *ponguru* and LinkedIn *ponguru* the same person?
- **Paper:** *"Other Times, Other Values: Leveraging Attribute History to Link User Profiles across OSNs"* (Paridhi Jain)
- **Uses:**
  - Avoid **duplicate audience** in ads (437K FB likes / 153K Twitter / 800K LinkedIn overlap)
  - Count **unique sentiment** (don't double-count one person)
  - **Law enforcement** (same person posting malicious content on YouTube & Twitter)
- **Challenge:** each network exposes different info (YouTube = opinions, Tinder = personal, LinkedIn = professional)
- **Approach:** list common attributes → compare values (**syntactic, semantic, graph-based**) → high similarity = same person; use **past values (history)** too
- **Why usernames:** unique, always public, length-limited, easy to collect
- **Self-identification:** a profile links another account (Twitter bio → Tumblr), FB album link cross-posted to Twitter, same post at the same time
- Track the **permanent user ID**: the handle changes, the ID doesn't
- **Similarity:** Jaccard distance, edit distance
- **Features:** username creation behaviour (similar length, character choice, arrangement), temporal evolution, occasional reuse; ~56 features (26 also mentioned)
- **Data:** Twitter–Instagram / Tumblr / Facebook; 21K positive pairs; ~140K with past usernames on Twitter only
- **Methods:** exact match, substring match, classifiers; **SVM ≈ 76% accuracy**; past attributes improve linking
- FB itself can link accounts via IP address and access time
- **Username changes:**
  - FB allows a username change **once**; Twitter **unlimited**
  - 376M users: ~5–7% changed screen names (peaks ~2010–Jan 2011)
  - 8M users over 2 months: ~6–7% changed username; ~35–40% changed profile pic ≥3 times; ~35% changed description ≥2 times; almost nobody changes language/time zone
- **Paper: "On the Dynamics of Username Changing Behavior on Twitter":**
  - Seed **8.7M users** (from 17 events, 1 Apr – 3 Sep 2013); **fortnightly scans** Oct–Nov 2013
  - **73.21% changed some profile attribute; ~10% (853,827) changed username** ≥ once in 2 months (usernames are case-insensitive; case changes ignored)
  - 711,609 changers filtered; **10,000 sampled, scanned every 15 min for 14 months** (a full scan would need 1,462 auth tokens) → 4,198 changed, **14,880 changes**
  - **Pareto:** **20% of users trigger 85% of changes** (≥5 changes each, 12,648 changes); one user changed **113 times** (bot-like)
  - ~20% of changes within a day of the previous one; 10% within an hour
  - **65% pick an unrelated new name, 35% reuse an old one**
  - **Weak positive correlation** of change frequency with popularity (followers; excluding >1M and <1) and activity (#tweets)
  - **Median username length 11:** 75.19% of long names → shorter/same; 60.87% of short names → longer
  - **Benign reasons:** **space gain** (140 chars; mentions eat space), suit a trending event, gain/lose anonymity (ponguru → explorer_pk → logicalTamilian), adjust to life events (grad student → professor), avoid boredom
  - **Malicious reasons:** **obscured username promotion** (mimic a popular handle), **username squatting** (hold a name to sell later, e.g. PMOIndia; housing.com domain); squatting is against Twitter rules
  - **Groups share/rotate one username** across accounts (Peshawar_sms); event-driven renames (pwifanclub → ForceIndia)
  - Survey tweets to users drew hostile reactions; Wikipedia rename reasons: privacy, abuse, link accounts, real name, shorter name
  - **Limitation:** API limits → only 10K users in the 15-min scan

## 16. Anonymous Networks (Whisper) — L27
- **Anonymous** = can't tell who posted: **4chan, Whisper, Secret, Yik Yak, Wickr**
- **Why they exist:** rising privacy awareness, **Snowden / PRISM**, Indian incidents where viral posts had consequences
- **Whisper (whisper.sh):**
  - Categories: popular, latest, LOL, confessions, relationships, OMG
  - Text is overlaid on an auto-picked stock image (a meme); **hearts** (= likes), replies, private messages
  - Nickname changeable anytime; PIN instead of password
  - No email/contacts harvested, no user history, **no persistent social links**
- **4 RQs:** how users interact · do communities form like traditional OSNs · does lack of identity remove **strong ties** · does it remove **stickiness** (long-term engagement)?
- **Data (2014, Feb–May, scraped; no API):**
  - Fields: whisper ID, timestamp, text, nickname, location tag, #replies, hearts
  - **9M whispers, 15M replies, 1M GUIDs** (globally unique IDs); researchers told Whisper → **GUID removed in June 2014**
- **Activity:**
  - **55% of whispers get no reply**; 25% have a reply chain ≥2
  - Replies: **54% within 1 hr, 94% within 1 day**, 1.3% after ≥1 week → no early attention means no attention
  - 80% of users post <10 whispers+replies; 15% only reply; 30% only post whispers
- **Graph (Whisper vs FB vs Twitter):**

| Metric | Whisper | FB | Twitter |
|---|---|---|---|
| Nodes | 690K | 707K | 4.317M |
| Avg degree | **9.47** (highest) | 1.78 | 3.93 |
| Clustering coeff | **0.033** (lowest) | 0.059 | 0.048 |
| Avg path length | **4.28** (lowest) | 10.13 | 5.52 |
| Assortativity | **−0.011** (≈0) | | |

  → Whisper is a **random graph**, no small-world structure; users talk to **strangers**
- **Deletion:**
  - **1.7M deleted in 3 months = 18%** (Twitter ~4%)
  - **Deletion ratio** = deleted whispers containing a word ÷ all whispers containing it; 2,324 keywords (after removing stopwords and words in <0.05% of whispers)
  - **Most deleted topics:** sexting, selfie, chat; **least:** emotion, religion, entertainment, life story, work, politics
  - **70% of deleted whispers go within 1 week**; 2% last >1 month; re-crawl of 200K → 32,153 deleted, **peak at 3–9 hrs**, most within 24 hrs
- **Interacting pairs:** 90% in the same state, **75% within 40 miles**; smaller local population and more posts → more encounters; repeated (>10) interactions are rare
- **Engagement:** ~80K users/week; cumulative users rise but **daily new posts stay flat**; new users ≈ 20% of content → weak stickiness
- **Conclusion:** unlike traditional OSNs — no strong ties, interaction with strangers; **content moderation needed**

---

### Quick-Recall Numbers
| Item | Value |
|---|---|
| Westin F/P/U | 25% / 57–60% / 15–18% |
| India survey | 10,427 people, 83 Qs; 42% trust settings; 27% accept opposite gender |
| Sandy DT accuracy | 97.65% |
| Credible tweets (multi-event) | 17% (30% info, 14% spam) |
| Cronbach's α | ≥ 0.7 |
| TweetCred | 1–7 score, 45 features |
| Boston viral tweets | 29% fake / 20% true / 51% generic |
| Fake tweets from mobile | ~75–76% |
| New accounts at Boston | 32K, 19% suspended |
| Virality regression | R² ≈ 0.7 |
| Face re-ID | 1 in 10 (dating), 38% (campus), 27% SSN 5 digits |
| Twitter 2009 dataset | 54M users, 1.9B links |
| Spam URLs / CTR | 8% of 25M / 0.13% |
| Automated accounts | 16% |
| Social phishing | 72% vs 16% control; 70% in 12 hrs |
| Privacy policy cost | 244 hrs/yr, $781B |
| Home city (FSQ / G+ / Twitter) | 67 / 72 / 82% |
| Username changers | ~10%; 20% of users → 85% of changes |
| Whisper | 18% deleted; 55% no reply; random graph |
| Police response time | avg 30 h, min 4 min, max 211 h |
| Profile-linking SVM | ~76% |
