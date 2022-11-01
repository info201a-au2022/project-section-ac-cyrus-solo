# *MTG cardknower*: Accessible Analysis for Arbitrary *Magic* Answers

## Metadata 

##### Table 0: Identifying information
|Code name | `krasis-alpha` |
|----|----
|Project title| MTG cardknower |
|Author | [Cyrus Eosphoros](mailto:cyrusae@uw.edu) |
|Affiliation |  INFO-201: Technical Foundations of Informatics - The Information School - University of Washington |
|Date | Autumn 2022|

### Abstract
The immense complexity and thirty-year history of card game *Magic: the Gathering* create a wealth of cumulative data about the game. While freely available, such data is not optimized for analytics purposes by researchers, nor is it accessible to laypeople with questions about a game they enjoy. This project implements a prototype of an open-source analytics dashboard for information about printed cards across *Magic*'s history and demontrates the proof of concept with example research questions.

#### Keywords 
Magic: the Gathering; trading card games; game design; fandom; open data 

## Introduction

*Magic: the Gathering* (hereafter *Magic*) is a collectible trading card game originally created by Richard Garfield and now owned by Wizards of the Coast (itself owned by Hasbro). Its thirty-year history produces a wide span of game design and culture shifts while having earned it a large, heterogenous audience. Much information reflecting that timespan and of potential interest to those populations is freely available. Less has been collated and optimized for analysis, either for research or casual curiosity. This project is part of a larger approach to changing the latter.

## Problem Domain

The rules text of *Magic*, while written to be read by a human audience as natural language, constitutes a Turing-complete (*see* Churchill et al) system of formal logic. It finds use in games research as a (theorized) demonstration of the highest possible play complexity in human-made games (Ibid.; *see also* Biderman). It is also a site of emotional, social, and economic investment for its players, who participate in gameplay within the system created cumulatively by thirty years of printed cards. Timing, quantity, design priorities, and many other factors of how those cards are printed and released have changed over time. 

### Key Terms in Context

Personal experience with the game is not required to understand this project; however, some high-level knowledge of the topic will assist in understanding the data. These terms are metadata relative to the language of the game itself; see also Manis for a detailed (albeit outdated) view of game terms from a player perspective.

#### Card

Cards are printed and reprinted in *sets*, collections of cards released on a specific date in randomized packs. Defining cards matters beyond the tautological "gameplay objects of the card game" sense due to the nature of *Magic*'s rules: a card is a persistent gameplay object defined by a unique name. Cards' behavior may change contingent on game state but the physical card itself, and the rules object identified by its name, is unchanged. Game objects such as *tokens* and *emblems* are printed alongside cards for player convenience (and tracked by the source providing this project's data as a matter of curiosity) but they are not cards.

#### Mechanical information

Beyond the name as a unique identifier, cards are printed with a variety of features (constituting many of the variables in this project's data) defining their impact on the game. The majority of information conveyed to a player by a card is mechanical. In terms of space, however, at least half of a card is taken up by illustrations, decorations, and sometimes thematic quotes. Other details present on a card that affect player perception but do not alter gameplay are *flavor*.

#### Mechanical uniqueness 

The only part of a card's text obligated to be unique is its name; the rules impact when played may be distinctive, but the first card printed with a given rules text does not have a whole or partial monopoly on the gameplay action it describes. The difference in impact between reprinting a card and printing a mechanically identical one with a new name in a set is nontrivial but nebulous.

#### Card features
An explanation of each of these terms is out of bounds for this document, but in the interest of providing examples of variables that are mechanical information of a card but either a subset of or separate from its *rules text*: all cards have a *color identity* and most have one or more *colors*. These features are usually dictated by the card's *casting cost*. A card must have one or more *types*; some have *supertypes* and *subtypes*. 

### Direct and Indirect Stakeholders

#### As Fan Project

The direct target audience, and thus the most immediate stakeholders, are people interested in *Magic* for *Magic*'s sake: the community of players, fans, and people who are invested in the game somehow but don't identify as either. As an object of curiosity and a tool for playing with data, the project's orientation towards those stakeholders is specifically one of demystifying data science and making it more accessible to laypeople. 

#### As Open Data 

Not all of the above stakeholders, of course, are actually laypeople. Beyond the aforementioned research on specific things that *can be* orchestrated in a game of Magic as mentioned above, there are avenues of inquiry where cross-referencing cards mechanically over time is necessary (see for example Magruder). No tool that I know of currently exists to do this, and the available data is clean and well-documented (see *The Dataset*) but not optimized for programatic analysis as opposed to human reading of rules text. 

Researchers who would benefit from that not being the case are direct stakeholders, albeit harder-to-isolate ones. Insofar as the goal of benefitting such researchers is subsequently accomplished, people affected by work in their fields become indirect stakeholders by proxy.

#### In Relation to a Corporate Product

This project is not associated with the company that owns *Magic* as intellectual property, and in its current form cannot be. Wizards of the Coast is unlikely to directly see impact from even the most successful version of this project in a way that is quantifiable for the corporate entity. They are also, still, intractably, a party with a stake in the outcome.

### Human Values

The driving value for this project, as with the topic itself, is one often considered frivolous: it's about a game, and games are for fun. Of course, what people do for fun--with each other--with their time and energy--has immense weight on their personal human lives; *Magic* matters to approach from an analytic perspective, as much as any other one, because it matters to people. 

Beyond that, the authorial/developer intent is about moving the possibility of play one step closer to that analysis. Anyone who enjoys *Magic* is the kind of person who, whatever their personal reasons, gets something out of a game designed by a mathematics PhD which technically qualifies as a computer. Anyone who plays the game for longer than two to three months sees turnover in new cards and gets to determine how that impacts their interaction with the game. Virtually any player could come up with a data-oriented question concrete enough to be interesting, if not necessarily substantive research, simply by being given time and space to articulate what the amount of time they've spent with the game in their life makes them wonder. People who care about this game are disproportionately likely to be interested in analysis of it, but that doesn't magically make data science more accessible to them. They deserve access to this *being fun*, too.

### Potential Benefits and Harms

This is a relatively low-risk project in terms of human impact, which should not be confused with contending that it doesn't impact humans. However, on its face, the proximate possible benefit of its success is that people interested in *Magic* see something that interests them, and failure would leave the world largely unchanged. Larger-scale impacts are more in relation to the nature of the game and its ecosystem than to the nature of the project.

*Magic* as a whole is extremely centered on its English text. The nature of the game excludes people who are not comfortable with at least enough English to learn it as technical vocabulary, either outright due to lack of access or eventually due to a limited subset of cards receiving translations. An axis of harm to bear in mind is the likelihood of *`cardknower`* replicating this; conversely, allowing for analysis of *Magic* in translation over time potentially provides quantifiable data for examining that disparity.

Wizards of the Coast's business model relies both directly and indirectly on what is functionally volunteer labor. As a fan project (both literally and legally speaking), this is no exception. Any effort put into this project and any achievements that result are inextricable from that context.

## Research Questions 

These questions are fundamentally best considered examples and tools for a relevant thought exercise; they are *the kind of question* that *`cardknower`* is designed to enable answering. The purpose of its development is to provide that resource to interested parties (see *Stakeholders*); these and other questions are tests of whether the design ultimately prototyped can accomplish that goal.

### 1. How has color developed over time?
*Color* has been a central mechanical concern in *Magic* since its inception; color symbols in *costs* determine when in a game a card can be played, *multicolor* and *colorless* cards' introductions provided a substantial increase in rules complexity, and the five-color *color pie*--the available palette--groups cards together thematically. All of these functions were developed iteratively over time, including the consolidation of specific themes and mechanics as belonging to one color more than others. This is qualitatively well-documented; can it be seen in the machine-readable data?

### 2. How has support for non-English languages changed over time?
While there is a decisive focus on English as the language in which *Magic* gameplay's syntax is defined, some sets see printings in translation internationally. Which languages and what level of consistency can be determined from data about the translated cards themselves but has not previously been aggregated as such.

### 3. How are card prices affected across reprints of a single card?
Reprints, by definition, inject a new supply of a given card into the secondary market. At the same time, they're not physically unique to older printings, and may have completely different visual designs, aesthetics, or other flavor details. The data provides a snapshot of prices across multiple mainstream markets at time of download; for cards with a large number of reprints, what variance appears in that snapshot from one printing to another?

*(Note: additional considerations are needed in terms of the possible audience of price-related reesearch. See `Limitations`.)*

## The Dataset

This section provides an overview of the raw data in context, the entity providing access to the data, and the additional processing employed for this project specifically. 

> **Note:** While this data is retrieved from a series of public API endpoints, Scryfall explicitly forbids hotlinking download URIs; in accordance with their wishes, direct links to the data files are not provided. An interested reader will find an up-to-date download link, and much more, in the referenced documentation, with links [repeated when relevant](https://scryfall.com/docs/api) for ease of access.

### Source of Truth

As opposed to retrieving information about the game directly from the company producing it, *`cardknower`* depends on data from the fan-maintained repository **Scryfall**, whose API is documented [here](https://scryfall.com/docs/api) and made public specifically for the purpose of enabling other fan projects in turn. (This does not imply participation, endorsement, or knowledge of this project on behalf of Scryfall.) The nature of the resulting dataset used for this project is thus entirely defined by the data model it inherits from its source of truth. 

Scryfall provides a large amount of information about each entity of interest. However, the intent of the repository is fundamentally different from this project's needs. Scryfall provides access to the data powering its website, meaning some variable measurements are not intended to be machine-readable (for example, rules data in [Rulings](https://scryfall.com/docs/api/rulings) objects)--and, more importantly, that observations are overwritten whenever a measurement changes over time. 

For more details on understanding when and how this is relevant, see *Limitations.*

#### Relevant terms 
- **Oracle ID**: Scryfall internal identifier belonging to a mechanically unique card. UUID.
- **Oracle name**: Mechanically unique English card name. String.
- **Object**: Used here in the sense inherited from [the Scryfall API documentation](https://scryfall.com/docs/api/): one observation relative to one of their datasets. Objects referred to as children are contingent within the data on objects of another type (parents).

The following tables provide an overview of the Scryfall API endpoints used and the steps needed to manage the resulting data. The process used by this project is a truncated one adapted from the larger project it complements. Information relevant to estimating the frequency and computing cost of updates to records is less relevant to the "time capsule" approach taken by this project, but is provided for perspective. See also *Limitations*.

##### Table 1: Scryfall sources queried directly

|Scryfall name/documentation | Purpose | Frequency of major updates (approximate) | Number of records (order of magnitude)|
|------ |-------|------|------
| [Sets](https://scryfall.com/docs/api/sets) | Set (product release) data | Monthly | Hundreds|
| [Bulk data](https://scryfall.com/docs/api/bulk-data) | Current URI for retrieving `Card` object data | Twice daily | Five records *(see Table 2)*|

##### Table 2: Relevant bulk data files
| Name | Description | Size of JSON file | Minimum number of usable records expected (approx.)|
|------ |--------|------|-----
|Default cards | One `Card` object for every (English) printing of a card or token | 285 MB | 25,000|
|All cards | One `Card` object for every printing of a card or token in any language | 1.5 GB | 350,000|

*(See the `Card` object [documentation](https://scryfall.com/docs/api/cards).)*

##### Table 3: Logistics of query results 
|Queried source | Logistics of processing | Purpose | Outcome | Resource consumption|
|----|-----|-----|----|----
|Bulk data | JSON trivially parseable in memory | Retrieve addresses needed to download card information | Query results deleted | Low|
|Sets data | Resulting table small enough to clean in memory | Correlate information about sets with their cards | Clean CSV saved, raw query results discarded | Moderate|
|Bulk: Default cards | Download and save JSON file before cleaning step | Majority of card information | Clean CSV saved, raw query results retained as needed | High|
|Bulk: All cards | Download and save JSON file before cleaning step | Card information contingent on language | Clean CSV saved, raw query results retained as needed | Extreme|

*(See also `Limitations`.)*

##### Table 4: Minimum required libraries

*(Many other dependencies can be expected for quality-of-life improvements and for future project requirements. These three are highlighted due to being essential to processing the raw data, and, in two cases, successfully opening files.)*

|R Library | Use case | Notes|
|--------|--------|--------
|RcppSimdJson | Parses Scryfall's returned JSON | Earlier iterations of a related project used jsonlite; use of jsonlite takes several hours, during which time crashes are increasingly likely. |
|data.table | Required for tabular data after JSON is parsed | Keyed joins are necessary for cross-referencing parent objects with their child datasets (e.g., cards by Oracle ID).|

The Scryfall data contains variables which consist of nested JSON (requiring further parsing), observations of objects not relevant to this project (such as tokens), variables embedded in strings (such as the words of a *type line*), and other features that are predictable but will require predictable wrangling.

*`cardknower`* is also designed to use a subset of Scryfall's data corresponding to mainstream releases of official cards in paper. The following are excluded by this:

* Cards printed as jokes, holiday promotions, or prizes
* Tokens, emblems, and other non-card objects printed alongside cards
* Cards which exist exclusively in a digital format
* Sets consisting exclusively of joke, promotional, or prize cards
* Set objects used by Scryfall to collect tokens, emblems, and other non-card objects
* Variables exclusively relevant to any of the observations excluded 

## Expected Implications 


More generally and assuming this prototype contributes effectively to longer-term development, *`cardknower`* belongs to a project/collection of projects aiming to make data analysis of *Magic* more accessible to anyone close enough to the game to have questions. Success on this level bodes well for utility for researchers in fields where *Magic* is a useful case study (see References) and for increasing access for laypeople.

## Limitations

### Scope of INFO 201

This project is, to the best of my ability, retrofitted into the scope of this class in one quarter. This produces time/energy limitations (the prototype gets a month of development) and resource constraints. The resource constraints bear further discussion.

INFO 201 final projects are generally hosted on shinyapps.io, which does not provide persistent writeable storage. Shiny app design in general is oriented towards data that isn't necessarily static, but which is updated elsewhere. *`cardknower`* has to function independently of the database design that supports its predecessor/cousin, which cannot be realistically implemented in SQLite (otherwise common Shiny solution) and would be counterproductive if it could (SQLite does not have persistent storage).

#### Subsetting Scryfall data

As mentioned above, this prototype drops a nontrivial amount of data. Some of it *is* included in the existing dimensional database (digital cards); some is excluded indirectly by the fact that the app version cannot update itself over time.

#### "Time capsule" analysis

Because of the above, the product of this quarter is locked to the version of its data generated at build time. It cannot run its own update scripts on the otherwise-convenient server options available.

### Access to sources of truth

There is a universe where the API being used is one provided by the company whose internal records are theoretically the most complete on the game itself. (With one topical exception; see below.) We do not live in that world. The comparison between Scryfall and Gatherer (the most analogous public-facing product to the fan repository that Wizards maintains) is such that one would not generally consider this a limitation per se, but it does, if nothing else, lock in relying on a third party for the data independently from relying on a company for the game.

#### User interests in conflict

*Magic: the Gathering*, as the first modern trading card game, has a history defined in large part by player participation in the secondary (resale) market. Members of the fan community (with the exception of one group that will be addressed shortly) use price fluctuation as a proxy for general consensus on cards' power and desirability, and someone's experience of the game is in large part defined by what cards they have access to.

Employees of Wizards of the Coast, who are often *Magic* fans in their own right, are legally prohibited from having any knowledge of secondary market price dynamics. Any integration of pricing data into the project either entirely prevents a small but valid part of the possible target audience from accessing it (recreationally, in their personal lives), or requires substantial work to delineate it without losing the ability to use the data in question.

### Loss of time-mediated data

Scryfall overwrites its own records as opposed to preserving change over time; cards banned or unbanned don't have a start and end date to that state, prices are accurate to when prices were updated, Oracle text is always rendered with the most up-to-date syntax and wording regardless of the words in the scanned image depicting a card. The above "time capsule" effect prevents an update-and-refresh process from compensating for that by recording changes to Scryfall data on import.

## References

Biderman, S. (2020). Magic: the Gathering is as Hard as Arithmetic. arXiv. 
https://doi.org/10.48550/arXiv.2003.05119

Churchill, A., Biderman, S., and Herrick, A. (2019). Magic: the Gathering is Turing Complete. arXiv. https://doi.org/10.48550/arxiv.1904.09828

Magruder, D. S. (2022). A Conservative Metric of Power Creep. Games and Culture, 17(5), 721–751. https://doi-org.offcampus.lib.washington.edu/10.1177/15554120211050812

Manis, M. (2012). The “Magic: the Gathering” Lexicon (Order No. 1510404). ProQuest Dissertations & Theses Global. (1016132546). https://www.proquest.com/dissertations-theses/magic-gathering-lexicon/docview/1016132546/se-2

---

# Appendix A: Questions

- The Canvas assignment says that including either the API documentation or the CSV files is acceptable but the grading rubric only gives instructions for the files. The brief does give some instructions that can be generalized to providing information about APIs but they're not possible for mine (Scryfall literally forbids openly recording the address of their files at any given time, hence the multi-step query structure). What did you want from me there and was this sufficient?
- I think a lot of my sections are more technical in their emphasis than the design brief intended, because of the nature of the actual project entails it (see also next bullet point). I have questions in the sense that is a natural result of doing exploratory analysis to understand my data, but this is first and foremost prototyping something intended as open-source software allowing *other* people to answer their own questions. (See also next bullet point.) Am I striking that balance usefully? Is there something I can do to make it work more for you? Conversely, should I be *more* explicit about the full-scale project this is a prototype of a dashboard for part of instead of less?
- Prof. Winegarden said on the first day of class when I asked that "existing personal project but it's pop culture/recreational" was fine. However, I have still been swimming uphill somewhat against the instructions as written, in terms of trying to guess how to adapt them into something that actually makes sense with my data but also is satisfactory to you. This most of all is what I was attempting to talk to you about until I found out I wasn't supposed to try to talk to you before turning in the proposal. Do you have suggestions/feedback/complaints on that axis now?
- Same question as the above, but for the fact that finding ways to shoehorn the topic into a frame where relating it to the available traditional academic literature was possible was a struggle; the best I could do that felt intellectually honest was leaning on the existing literature to demonstrate that study of the game exists. The above is also why the citations are formatted as *see [related]* as opposed to a single key pull quote being available verbatim; the topic is the same but the domains are mutually exclusive. This is the kind of thing I want to know how to address in P02/P03.
- As detailed in the *Limitations* section, the project was designed to support automatic updates but the structure of this class and the nature of services offered by shinyapps.io make implementing that aspect here impossible. This is also why I've opted to leave out information about digital-only cards: the database architecture I've used to support including them is untenable in SQLite, shinyapps.io doesn't support persistent storage, and my experience has been that attempting to provide hosting on my own server for class projects where that isn't an expected part of the project will end in tears. How explicitly do you want me to acknowledge this going forward? 
- Even aside from that, there's a lot of information that I think is important, that seemed to logically belong in *Limitations*, and that conflicts with the instructions' specifying that the section in question is for the proposal only. I would appreciate any thoughts on what to adapt/keep for the final product and how to do so that you may have.
- I think I copied everything out of the repo that I couldn't actually submit because it was under 201b. I *think*. Please let me know if I missed anything when committing this. *(`Edit:` Found things stuck in old files. Moved. Let me know if I missed anything* else, *rather.)*
- This one *is* allowed to be public, right? I have a friend I want to show things.

**Edit:** Thought of a better way to articulate a question underlying most of the above specific ones. The nature of this project means the paper that belongs with what I said on day one that I was committing to write is *the whitepaper for the open-source software*. I did/do need at this stage *to* be prototyping what giving other people access to analytics/a dashboard backed by my database looks like, which is why I said I'd do it. The overall purpose is lowering barriers to entry for data analysis, which lets other people ask and answer their own research questions; I don't think that's rationally extricable from how I go about documenting work I do on it. What I need to know is how it would benefit you for me to make that work within the hyperspecific research paper formula we've been given in practice.
