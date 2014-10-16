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
- Reproducible Steps
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

---

## Tips

### Keyboard Shortcuts

Hover over a card and press:

    Space       Assign Self
    L           Label Picker
    M           Member Picker
    ?           Show Shortcuts

While Typing a Card Title

    ^           List postition

### Card Template Bookmarklet

``` Card Template Bookmarklet
javascript:var element=$("div.card-detail-edit textarea.field");element.height(600);var original_details=element.val();if(original_details) {original_details="\n\n---\nOriginal Card Details:\n\n" + original_details;}var details="### Desired Behaviour\n- Short description of how it should behave\n\n### Observed Behaviour\n- Short description of how it is behaving\n\n### Reproduction\n- Reproducible Steps\n- That should cause the desired behaviour\n- But actually cause the observed behaviour\n\n### Affected Areas\n- Things that could be affected by this change\n- Including other features, areas, cards, etc.\n\n> Path : To : Thing\n**Identified:** version / environment\n**Spec:** `/path/to/spec`\n**Branch:** `<branch-name>` forks from `<version>`\n**Merges:** list of branches, or cards\n**Next Action:** eg: @Bob to finish some card\n\n    Date       | Spent | Remaining | Note\n    -----------|-------|-----------|------\n    Mon 01 Jan | 0     | 1h        | Example First Estimate\n\n" + original_details;element.val(details);
```

#### Creating a new Bookmarklet

1. Update the Bookmarklet in `Trello Cards.md`
2. Copy this Bookmarklet Creator Snippet over the top of the existing Bookmarklet
3. Paste the template over the top of the word TEMPLATE
4. Replace all newlines with \n
5. Edit your bookmark button and paste in the new bookmarklet
6. Edit the `● ———— Template ———— ●` Card 

``` Bookmarklet Creator Snippet
javascript:var element=$("div.card-detail-edit textarea.field");element.height(600);var original_details=element.val();if(original_details) {original_details="\n\n---\nOriginal Card Details:\n\n" + original_details;}var details="TEMPLATE" + original_details;element.val(details);
```
