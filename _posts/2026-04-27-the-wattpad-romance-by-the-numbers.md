---
layout: post
title: "The Wattpad Romance - By The Numbers"
date: 2026-04-27
image:	
tags: research python claude_ai project romance smut fan-fiction books reading data statistics wattpad
---

> TL;DR, you can find all the data and simplified take-aways at [Wattpad Analysis](https://idleendeavor.com/wattpad-analysis.html). And yes, I am aware that AO3 is the go-to place for fan-fictions at the moment, but when I first had the idea; it was very much Wattpad. I might do the same data-analyis with AO3 at some point. (If you steal my idea, both sides of your pillow will be war for 7 years)

I've had this idea at the back of my head and later in my 'sometime' todo list for years at this point, never got around to doing it, and I've always been bummed about that.

However, having finished my last assessment project for the university year, which did include a lot of AI assistance in coding; I suddenly realised that AI would be a great way to automate a lot of the subjective aspects of this project which had always kept me from attemting to do it.

The idea when I first had it, in all honesty, was to analyse Wattpad fan-fictions to become the most attractive man possible. Since then my understanding of what 'attractiveness' is and what I 'want to be' have changed a lot, so the goal has shifted to just wanting to do the research to see what data it would come out with.

So I sat down and finally did the work, which took about 3 days to complete with a lot of back and forth with Claude, manual tweaking, graph building, and solving API implemetation and biling errors.

Anyway, you're here for the most common traits of the male and female characters. They are:

#### The Composite Heroine
She is 22 to 25 and working class, often a student, with little romantic experience to her name.
- **Age:**
22 to 25 (11/25)
- **Wealth:**
Working Class (7/25)
- **Build:**
petite / small (5/25)
- **Independence:**
Moderate (10/25)
- **Experience:**
Inexperienced (13/25)
- **Emotional maturity:**
Moderate (17/25)
- **Top traits in the prose:**
    - guarded (8)
    - fierce (7)
    - sassy (7)
    - resilient (7)
    - warm (6)
    - loyal (6)

#### The Composite Hero
He is 26 to 30 and very wealthy — tall, and almost always fiercely independent.
- **Age:**
26 to 30 (12/25)
- **Wealth:**
Very Wealthy (13/25)
- **Build:**
tall (9/25)
- **Independence:**
Fiercely Independent (22/25)
- **Experience:**
Experienced (16/25)
- **Emotional maturity:**
Moderate (13/25)
- **Top traits in the prose:**
    - broody (17)
    - cold (13)
    - protective (12)
    - possessive (7)
    - reserved (4)
    - controlling (4)

You can find a much more polished display of the full data at [Wattpad Analysis](https://idleendeavor.com/wattpad-analysis.html).

### The Nitty Gritty

I started by using Wattpad's built in list of the 25 most popular books from the Romance category (excluding foreign language entries and getting the 26th and 27th entries instead), then I _acquiring_ epub exports of the books and then wrote a python scropt which counted regex-matched vocabulary on roughly 40 different trait categories. This gave me the basic traits and a solid base to start off of. Here's all the code surrounding the vocabulary that was matched:

{% raw %}

    # ---- Personality vocabulary ----
    "confidence": [
        r"\bconfiden(?:t|ce|tly)\b", r"\bbold\b", r"\bassertive\b",
        r"\bfearless\b", r"\bstrong-?willed\b", r"\bsure of (?:her|him)self\b",
    ],
    "shyness": [
        r"\bshy\b", r"\btimid\b", r"\bnervous(?:ly)?\b", r"\bblush(?:ed|ing|es)?\b",
        r"\bstammer(?:ed|ing)?\b", r"\bstutter(?:ed|ing)?\b", r"\bawkward(?:ly)?\b",
    ],
    "innocence": [
        r"\binnocen(?:t|ce)\b", r"\bnaive\b", r"\bvirgin\b", r"\bpure\b",
        r"\bsheltered\b", r"\buntouched\b", r"\binexperienced\b",
    ],
    "sass": [
        r"\bsass(?:y|iness)?\b", r"\bsnark(?:y|ily)?\b", r"\bsarcas(?:m|tic|tically)\b",
        r"\bwitty\b", r"\bsmart-?mouth\b", r"\bretort(?:ed|ing)?\b",
    ],
    "intelligence": [
        r"\bsmart\b", r"\bintelligent\b", r"\bbrilliant\b", r"\bclever\b",
        r"\bbookworm\b", r"\bnerd(?:y)?\b", r"\bgenius\b", r"\bstudious\b",
    ],
    "kindness": [
        r"\bkind(?:ness|-hearted)?\b", r"\bsweet\b", r"\bgentle\b",
        r"\bcompassionate\b", r"\bcaring\b", r"\bselfless\b",
    ],
    "stubbornness": [
        r"\bstubborn(?:ly|ness)?\b", r"\bheadstrong\b", r"\bdefiant(?:ly)?\b",
        r"\brebell(?:ious|ed|ing)\b", r"\bdefy(?:ing)?\b",
    ],
    "vulnerability": [
        r"\bvulnerab(?:le|ility)\b", r"\bbroken\b", r"\bfragile\b",
        r"\bdamaged\b", r"\bscarred\b", r"\btrauma(?:tised|tized|tic)?\b",
    ],
    "independence": [
        r"\bindependen(?:t|ce|tly)\b", r"\bself-?reliant\b", r"\bself-?sufficient\b",
        r"\bon (?:her|his) own\b", r"\bdoesn'?t need (?:anyone|anybody)\b",
    ],
    "anger": [
        r"\bangr(?:y|ily)\b", r"\bfur(?:y|ious|iously)\b", r"\brage(?:d|ing)?\b",
        r"\bsnap(?:ped|ping)\b", r"\bgrowl(?:ed|ing)?\b", r"\bglare(?:d|ing)?\b",
    ],
    "dominance": [
        r"\bdominant\b", r"\bdominat(?:e|ed|ing)\b", r"\balpha\b", r"\bcommanding\b",
        r"\bauthoritative\b", r"\bin (?:control|charge)\b",
    ],
    "submission": [
        r"\bsubmissiv(?:e|ely)\b", r"\bobey(?:ed|ing)?\b", r"\byield(?:ed|ing)?\b",
        r"\bgive in\b", r"\bsurrender(?:ed|ing)?\b",
    ],

    # ---- Wealth / class cues ----
    "wealth": [
        r"\brich\b", r"\bwealthy\b", r"\bmillionair(?:e|es)\b", r"\bbillionair(?:e|es)\b",
        r"\bmansion\b", r"\bpenthouse\b", r"\bluxur(?:y|ious)\b", r"\bprivate jet\b",
        r"\bdesigner (?:dress|bag|suit|clothes)\b", r"\bchauffeur\b",
    ],
    "poverty": [
        r"\bpoor\b", r"\bbroke\b", r"\bstruggl(?:e|ing|ed) to (?:afford|pay)\b",
        r"\bpaycheck to paycheck\b", r"\bcan'?t afford\b", r"\brent was due\b",
        r"\bscholarship\b", r"\bworking-?class\b",
    ],

    # ---- Occupations (vocabulary, not assignment) ----
    "occ_student": [
        r"\bcollege\b", r"\buniversity\b", r"\bhigh school\b", r"\blecture\b",
        r"\bdorm\b", r"\bprofessor\b", r"\bcampus\b", r"\bsemester\b",
    ],
    "occ_corporate": [
        r"\bCEO\b", r"\bboss\b", r"\bcorporation\b", r"\bexecutive\b",
        r"\bboardroom\b", r"\bbusinessman\b", r"\bbusinesswoman\b", r"\bmerger\b",
    ],
    "occ_creative": [
        r"\bwriter\b", r"\bauthor\b", r"\bartist\b", r"\bpainter\b",
        r"\bmusician\b", r"\bsinger\b", r"\bdancer\b", r"\bphotographer\b",
    ],
    "occ_service": [
        r"\bwaitress\b", r"\bwaiter\b", r"\bbartend(?:er|ing)\b", r"\bbarista\b",
        r"\bretail\b", r"\bshop assistant\b",
    ],
    "occ_medical": [
        r"\bdoctor\b", r"\bnurse\b", r"\bsurgeon\b", r"\bhospital\b",
        r"\bpaediatric\b", r"\bpediatric\b", r"\bER\b",
    ],
    "occ_athletic": [
        r"\bquarterback\b", r"\bfootball player\b", r"\bteam captain\b",
        r"\bhockey player\b", r"\bbasketball player\b", r"\bjock\b", r"\bcoach\b",
    ],
    "occ_criminal": [
        r"\bmafia\b", r"\bmob(?:ster)?\b", r"\bhitman\b", r"\bcartel\b",
        r"\bcriminal\b", r"\bgang\s?leader\b", r"\bunderground\b",
    ],

    # ---- Appearance vocabulary ----
    "appearance_petite": [
        r"\bpetite\b", r"\bsmall frame\b", r"\btiny\b", r"\bshort\b", r"\bdelicate\b",
    ],
    "appearance_tall": [
        r"\btall\b", r"\blong legs\b", r"\blong-?legged\b", r"\btowered\b", r"\btowering\b",
    ],
    "appearance_curvy": [
        r"\bcurv(?:y|es|aceous)\b", r"\bvoluptuous\b", r"\bhourglass\b", r"\bfull (?:hips|figure)\b",
    ],
    "appearance_slim": [
        r"\bslim\b", r"\bslender\b", r"\bthin\b", r"\blithe\b",
    ],
    "appearance_muscular": [
        r"\bmuscul(?:ar|ature)\b", r"\babs\b", r"\bbiceps\b", r"\bbroad shoulders\b",
        r"\bripped\b", r"\bchiseled\b", r"\bpecs\b",
    ],
    "appearance_hair_dark": [
        r"\b(?:black|dark|raven|ebony|jet-?black) hair\b", r"\bbrunette\b",
    ],
    "appearance_hair_light": [
        r"\bblond(?:e)? hair\b", r"\bblonde\b", r"\bgolden hair\b",
    ],
    "appearance_hair_red": [
        r"\bred hair\b", r"\bredhead\b", r"\bauburn\b", r"\bginger hair\b",
    ],
    "appearance_eyes_blue": [r"\bblue eyes\b", r"\bocean eyes\b", r"\bsapphire eyes\b"],
    "appearance_eyes_green": [r"\bgreen eyes\b", r"\bemerald eyes\b"],
    "appearance_eyes_brown": [r"\bbrown eyes\b", r"\bhazel eyes\b", r"\bchocolate eyes\b"],
    "appearance_eyes_grey": [r"\bgr[ae]y eyes\b", r"\bsilver eyes\b", r"\bsteel eyes\b"],
    "appearance_tattoos": [
        r"\btattoo(?:s|ed|ing)?\b", r"\bink(?:ed)?\b", r"\bsleeve(?:s)? of\b",
    ],
    "appearance_scars": [
        r"\bscar(?:s|red)?\b", r"\bscarring\b",
    ],

    # ---- Background / context ----
    "bg_bad_family": [
        r"\babusive\b", r"\bdrunk(?:en)? (?:father|mother|dad|mom)\b",
        r"\bfoster (?:care|home|family)\b", r"\borphan(?:ed)?\b",
        r"\bran away from home\b", r"\bdead (?:mother|father|parent)\b",
    ],
    "bg_new_town": [
        r"\bnew (?:town|city|school)\b", r"\bjust moved\b", r"\bfirst day\b",
        r"\btransfer(?:red)? (?:here|student)\b",
    ],
    "bg_grief": [
        r"\bfuneral\b", r"\bgrief\b", r"\bgrieving\b", r"\bmourning\b",
        r"\bpassed away\b", r"\bcancer\b",
    ],

    # ---- Relationship dynamic vocabulary ----
    "dyn_bad_boy": [
        r"\bbad boy\b", r"\bmotorcycle\b", r"\bleather jacket\b",
        r"\bgang\b", r"\bfight(?:ing|ers?)\b",
    ],
    "dyn_enemies": [
        r"\benemies\b", r"\bhate(?:d)? (?:him|her)\b", r"\brival\b",
        r"\bcan'?t stand\b",
    ],
    "dyn_protective": [
        r"\bprotect(?:ive|ed|ing)?\b", r"\bmine\b", r"\bpossessive\b",
        r"\bjealous(?:y|ly)?\b",
    ],
    "dyn_age_gap": [
        r"\bolder than (?:me|her)\b", r"\byears older\b", r"\bage gap\b",
    ],
    "dyn_arranged": [
        r"\barranged marriage\b", r"\bbetrothed\b", r"\bcontract marriage\b",
        r"\bforced marriage\b",
    ],

    # ---- Heat / explicitness ----
    "heat_kiss": [
        r"\bkiss(?:ed|ing|es)?\b", r"\blips (?:on|against|met)\b",
    ],
    "heat_explicit": [
        r"\bmoan(?:ed|ing|s)?\b", r"\bnaked\b", r"\bthrust(?:s|ing|ed)?\b",
        r"\borgasm\b", r"\bclimax(?:ed)?\b", r"\bthrobbing\b",
    ],
    "heat_tension": [
        r"\bblush(?:ed|ing)?\b", r"\bheart raced\b", r"\bbreath(?:less|hitch)\b",
        r"\bbutterflies\b", r"\btingl(?:e|ed|ing)\b",
    ],

{% endraw %}


To collect data on subjective points, I wrote another python script which sent excerpts (opening, four mid-slices and closing) to Claude Sonnet 4.6 via their API to fill out a fixed schema covering both protagonists and the relationship: age, occupation, wealth origin, personality, baggage, arc, dynamic, power balance, POV, heat level. Didn't end up costing that much actually. Here's all the code surrounding the AI matched fields:

{% raw %}

    FMC_FIELDS = [
        "fmc_age_range", "fmc_occupation", "fmc_wealth_origin",
        "fmc_personality_type", "fmc_independence", "fmc_emotional_maturity",
        "fmc_experience_level", "fmc_dominant_traits",
        "fmc_height_build", "fmc_hair", "fmc_eyes", "fmc_distinguishing_features",
        "fmc_family_situation", "fmc_baggage", "fmc_arc",
    ]

    MMC_FIELDS = [
        "mmc_age_range", "mmc_occupation", "mmc_wealth_origin",
        "mmc_personality_type", "mmc_independence", "mmc_emotional_maturity",
        "mmc_experience_level", "mmc_dominant_traits",
        "mmc_height_build", "mmc_hair", "mmc_eyes", "mmc_distinguishing_features",
        "mmc_family_situation", "mmc_baggage", "mmc_arc",
    ]

    REL_FIELDS = [
        "rel_dynamic", "rel_meeting_context", "rel_power_balance",
        "rel_main_conflict", "rel_pov", "rel_heat_level",
    ]

{% endraw %}

{% raw %}

    Schema:
    {
    "fmc_age_range": "under_18" | "18_21" | "22_25" | "26_30" | "30_plus" | "unclear",
    "fmc_occupation": "<short lowercase label, e.g. 'student', 'waitress', 'intern', 'artist', 'unclear'>",
    "fmc_wealth_origin": "poor" | "working_class" | "middle_class" | "wealthy" | "very_wealthy" | "unclear",
    "fmc_personality_type": "<2-3 word snake_case label, e.g. 'shy_bookish', 'sassy_confident', 'guarded_wounded', 'fierce_ambitious'>",
    "fmc_independence": "dependent" | "moderate" | "independent" | "fiercely_independent" | "unclear",
    "fmc_emotional_maturity": "low" | "moderate" | "high" | "unclear",
    "fmc_experience_level": "innocent" | "inexperienced" | "average" | "experienced" | "unclear",
    "fmc_dominant_traits": "<<= 80 chars, 3 traits comma-separated, e.g. 'kind, stubborn, anxious'>",
    "fmc_height_build": "<<= 40 chars, e.g. 'petite', 'tall and slim', 'curvy', 'unclear'>",
    "fmc_hair": "<<= 30 chars, e.g. 'long dark', 'short blonde', 'red curls'>",
    "fmc_eyes": "<<= 20 chars, e.g. 'brown', 'green', 'unclear'>",
    "fmc_distinguishing_features": "<<= 80 chars or 'none'>",
    "fmc_family_situation": "<<= 100 chars, brief on parents/siblings/home>",
    "fmc_baggage": "<<= 100 chars, key trauma/wound/insecurity, or 'none'>",
    "fmc_arc": "<<= 100 chars, what she learns/changes>",

    "mmc_age_range": "under_18" | "18_21" | "22_25" | "26_30" | "30_plus" | "unclear",
    "mmc_occupation": "<short lowercase label>",
    "mmc_wealth_origin": "poor" | "working_class" | "middle_class" | "wealthy" | "very_wealthy" | "unclear",
    "mmc_personality_type": "<2-3 word snake_case label, e.g. 'broody_protective', 'cocky_charming', 'cold_powerful', 'soft_devoted'>",
    "mmc_independence": "dependent" | "moderate" | "independent" | "fiercely_independent" | "unclear",
    "mmc_emotional_maturity": "low" | "moderate" | "high" | "unclear",
    "mmc_experience_level": "innocent" | "inexperienced" | "average" | "experienced" | "unclear",
    "mmc_dominant_traits": "<<= 80 chars, 3 traits comma-separated>",
    "mmc_height_build": "<<= 40 chars>",
    "mmc_hair": "<<= 30 chars>",
    "mmc_eyes": "<<= 20 chars>",
    "mmc_distinguishing_features": "<<= 80 chars or 'none'>",
    "mmc_family_situation": "<<= 100 chars>",
    "mmc_baggage": "<<= 100 chars or 'none'>",
    "mmc_arc": "<<= 100 chars>",

    "rel_dynamic": "<short snake_case label, e.g. 'enemies_to_lovers', 'bad_boy_good_girl', 'boss_employee', 'forced_proximity', 'friends_to_lovers', 'second_chance', 'arranged_marriage', 'fake_dating', 'age_gap'>",
    "rel_meeting_context": "<<= 80 chars, where/how they first meet>",
    "rel_power_balance": "fmc_higher" | "mmc_higher" | "balanced" | "shifting" | "unclear",
    "rel_main_conflict": "<<= 100 chars, what keeps them apart>",
    "rel_pov": "fmc_first" | "fmc_third" | "mmc_first" | "alternating" | "unclear",
    "rel_heat_level": "clean" | "mild" | "steamy" | "explicit" | "unclear"
    }

    Excerpts from the book titled "{title}":

{% endraw %}


I've included some photos from the dashboard and terminal below.

![Python Script in Terminal](/images/wattpad-analysis-terminal.png)

![Claude API Dashboard](/images/wattpad-analysis-claude.png)

There are of course, some obvious caveats. 25 isn't a random sample, it's the top of a popularity list, which measures what gets read, not what gets written. AI labels were forced into a fixed enum to keep them comparable, which sanded off nuance. Personality clusters are pulled from free-text trait fields, so they reflect both the books' tendencies and the AI's vocabulary. The sample is also completely biased towards heterosexual romance as Wattpad classifies LGBTQIA+ stories under its own category (which I might explore separately at some point). Also, unlike Wattpad books from the past, modern ones don't seem to have detailed explanations of character appearances, due to this, most of the code around apearance matching amounted to no useable data.

That's about it, until next time!