# Trello Cards

Named: `<Feature Name>[ : <short description> [Bug|Improvement] ]`
eg: `Facebook Integration`, `Coloured Widgets : more colours Improvement`
	
## Card Description

The card description should include details required for a person without your context to understand the issue or feature.
It should not include remarks or opinions, tips or helpful snippets etc. These things can be added as comments.
Not all items from the Template are required, eg. you don't need an "Observed Behavior" for a new feature.

```
### Desired Behavior
- Short description of how it should behave

### Observed Behavior
- Short description of how it is behaving

### Reproduction
- Reproducable Steps
- That should cause the desired behavior
- But actually cause the observed behavior

### Affected Areas
- Things that could be affected by this change
- Including other features, areas, cards, etc.

> Path : To : Thing
**Identified:** version / environment
**Spec:** `/path/to/spec`
**Branch:** `<branch-name>` forks from `<version>`
**Merges:** list of branches, or cards
**Dev Time:** 0/1
**Next Action:** eg: @Bob to finish some card
```

## Comments

- Debugging notes, observations, tips, ideas, discussion, etc.

## Estimating

When work is done on a card, add the information:

- Time Spent
- Estimated Time Remaining

For example, say you originally thought an item would take 2 hours, but after spending 4 hours working on it, you think there's actually another 4 hours to go. The next day you spend 1 hour and finish it.

	Dev Time: 0/2, 4/4, 1/0

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
