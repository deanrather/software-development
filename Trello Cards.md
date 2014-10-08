# Trello Cards

Named: `<Feature Name>[ : <short description> [Bug|Improvement] ]`
eg: `Facebook Integration`, `Coloured Widgets : more colours Improvement`
    
## Card Description

The card description should include details required for a person without your context to understand the issue or feature.
It should not include remarks or opinions, tips or helpful snippets etc. These things can be added as comments.
Not all items from the Template are required, eg. you don't need an "Observed Behaviour" for a new feature.

```
### Desired Behaviour
- Short description of how it should behave

### Observed Behaviour
- Short description of how it is behaving

### Reproduction
- Reproducable Steps
- That should cause the desired behaviour
- But actually cause the observed behaviour

### Affected Areas
- Things that could be affected by this change
- Including other features, areas, cards, etc.

> Path : To : Thing
**Identified:** version / environment
**Spec:** `/path/to/spec`
**Branch:** `<branch-name>` forks from `<version>`
**Merges:** list of branches, or cards
**Next Action:** eg: @Bob to finish some card

    Date       | Spent | Remaining | Note
    -----------|-------|-----------|------
    Mon 01 Jan | 0     | 1h        | Example First Estimate

```

## Comments

- Debugging notes, observations, tips, ideas, discussion, etc.

## Estimating

When work is done on a card, add the information:

- Time Spent
- Estimated Time Remaining
- A Note about the work done (optional)

For example, say you originally thought an item would take 2 hours, but after spending 4 hours working on it, you think there's actually another 4 hours to go. The next day you spend 1 hour and finish it.

    Date       | Spent | Remaining | Note
    -----------|-------|-----------|------
    Mon 05 Jun | 0     | 2         | Should be easy, just use the API (Mon 2 Jun)
    Tue 06 Jun | 4     | 4         | Had to rewrite the API(Tue 3 Jun)
    Thu 08 Jun | 1     | 0         | It just worked (Thu 5 Jun)

This method requires very little time spent estimating, and gives the up-to-date and honest estimates available at a glance. It also provides a historical record of how good you are at estimating!

## Labels

- Yellow -- `WIP`
- Blue -- `User Tested`
- Green -- `Peer Tested`
- Red -- `Failed Testing`

## Recommended Plugins

- [GMail to Trello](https://chrome.google.com/webstore/detail/gmail-to-trello/oceoildfbiaeclndnjknjpfaoofeekgl?hl=en)

### Not Recommended Plugins

I tried these and didn't like them :(

- Plus for Trello
- Scrum for Trello

----

## TODO

- Tidy up the estimating example
