# Friend of a Friend

Disambiguation of filmographic creators based on identifying mutual "friends".

[Notebook](friend_of_a_friend.ipynb)

**Introduction**

A challenge facing film cataloguers is to accurately disambiguate similarly named creators based only on credit information. A popular example is the two different actors [Harrison Ford](https://en.wikipedia.org/wiki/Harrison_Ford_(silent_film_actor)) (1884-1957) and [Harrison Ford](https://en.wikipedia.org/wiki/Harrison_Ford) (1942-), although as the career of the latter started almost ten years after the death of the former, in practise it is quite easy to attribute credits appropriately. 

More difficult to distinguish are [George Miller](https://en.wikipedia.org/wiki/George_Miller_(filmmaker)) (1945-) and [George T. Miller](https://en.wikipedia.org/wiki/George_T._Miller) (1943-2023), both Australian film directors of similar age, and each individually responsible for iconic Australian films. 

There is also a problem when a name is so common that there are simply just many creators. For example, IMDB currently lists 300 distinct individuals called "Robert Smith".

**Method**

This notebook works on the assumption that, while it can be difficult to disambiguate creator names in isolation, it becomes significantly easier to make educated guesses if we can assume that any given creator is likely to work with the same person repeatedly. 

This thinking can be illustrated by the following example:

```
Is Max Schreck, who worked on Die Finanzen des Grossherzogs (1924), the same Max Schreck who worked on Nosferatu (1922)?
```

This is difficult to say in isolation, even though it is an unusual name, both films are German and made within the same time period.

```
Is Max Schreck, who worked with F W Murnau on Die Finanzen des Grossherzogs (1924), the same Max Schreck who worked with F W Murnau on Nosferatu (1922)?
```

A mutual collaborator, in this case, the director F W Murnau, gives some confidence that both Max Schrecks are indeed the same actor.

This is, of course, not always going to be fully reliable. I cannot find an online reference, but I do distinctly remember a hard-to-disambiguate (maybe this was the point!) collaboration between [Ben Frost](http://ethermachines.com/) [Australian noise composer] and [Ben Frost](https://www.benfrostisdead.com/about) [Australian street artist]. Another example, I have worked professionally with two distinct individuals called "Michael Smith". 

For these reasons, results from this process should be treated as indicative of possible overlaps, rather than being accepted at face value. Family members with similar names, who have frequently collaborated, are especially susceptible to false positives, as are individuals and companies which share similar names.

**Datasets**

A test dataset is provided, derived from the [ACMI API](https://github.com/ACMILabs/acmi-api). This is made possible by [ACMI's](https://www.acmi.net.au/) generous data licensing as [CC0](https://creativecommons.org/publicdomain/zero/1.0/).

If you wish to supply your own data, this is entirely possible. The data should be formatted as a parquet file with four columns, `agent_id` (agent identifier) and `agent_label` (agent name) for creators, and `work_id` (work identifier) and `work_label` (work title) for artistic works.

Name similarity is determined by a [Levenshtein distance](https://en.wikipedia.org/wiki/Levenshtein_distance) score of greater-than-or-equal-to 90. This can be adjusted depending on your desired tolerance for name variation.

**Extension**

Future considerations for development would be scoring matches to surface instances where multiple intermediate friends have been identified, as well as introducing weighting based on filmography size.

**License**

[CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/)



