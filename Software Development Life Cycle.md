# Software Development Life Cycle

### Goal
Minimise the amount of time between when an item is completed, and when it's released.

## Summary

![Funny Comic about Test Procedure](http://curtis.lassam.net/comics/cube_drone/20.gif)

### Requirements
Before a new version can be released to production:

- New items must pass Developer, Peer, and User Acceptance Testing
- The new version must pass QA

### Workflow
- When an item is completed, the Developer & UAT both test it against the other completed items in the new version
- When a Key Feature passes Developer Testing & UAT, QA is performed on the version
- When a version passes QA, it is released

### Terms
- Development Cycle -- Period of time between one production release and the next
- Key Feature -- A Feature worthy of causing a QA & Release Cycle
- Item -- A Feature, Bug, or Improvement. Has a card and a branch
- Testing -- Requires that the item has been merged into the version
- Developer Testing -- Testing of an item by the developer who worked on the item
- Peer Testing -- Tesing of an item by another developer
- UAT (User Acceptance Testing) -- Testing of an item by a non developer
- QA -- Peer Testing of all items, and an End-to-end UAT of the entire system

### Version Names

	<Major>.<Feature>.<Build>

- Major -- `1`
- Feature -- Incremented on feature release
- Build -- Increments which each merged (or re-merged) item

Most builds will be internal QA releases.
When a build passes QA, it will become a production release.

--- 

## Trello & Git

### Dev Cards
Named: `<Feature Name>[ : <Short Description> <Bug|Improvement> ]`
eg: `Facebook Integration`, `Coloured Widgets : More Colours Improvement`
	
#### Properties
Not all properties are required, depending on whether it's a bug, feature, etc.

- Component: eg. `Front Screen : Right Toolbar : "New" Button`
- Desired Behaviour
- Observed Behaviour
- Reproduction
- Version Identified
- Next Action eg. `@Alice to spec`, `@Bob to finish <other card>`, etc.
- Spec: `<path to spec>`
- Branch: `<branch-name> forks from <version>[, merges <branch-name>[...]]`
- Affected Areas / Things to QA
- Dev Time: `<hours spent>/<estimated hours remaining>[, ...]`

#### Comments
- Debugging notes, observations, tips, ideas, discussion, etc.

#### Estimating
When work is done on a card, add the information:

- Time Spent
- Estimated Time Remaining

For example, say you originally thought an item would take 2 hours, but after spending 4 hours working on it, you think there's actually another 4 hours to go. The next day you spend 1 hour and finish it.

	Dev Time: 0/2, 4/4, 1/0

This method requires very little time spent estimating, and gives the up-to-date and honest estimates available at a glance. It also provides a historical record of how good you are at estimating!

#### Labels
- Yellow -- `WIP`
- Green -- `QA OK`
- Blue -- `Peer Tested`
- Red -- `Failed Testing`

### Dev Branches
- Named `dev.<developer>.<feature-name>[.<bugfix|improvement>]`
- Feature branches fork from latest production version tag
- Bugfix and Improvement branches can fork from feature branches	
- Can merge other dev branches if required to resolve conflicts

### Lists
- `Triage` -- Dumping ground for ideas / bugs, etc.
- `Planning` -- Ordered list of items which need planning before work can commence
- `Backlog` -- Ordered list of items which are ready to be worked on (or WIP)
- `Version <Major>.<Feature>` -- The version under current development

#### Housekeeping
- Triage cleared before stand-up each morning
- All cards / lists reviewed prior to Work Planning

### Version List
- Named `Version <Major>.<Feature>.<Build>`
- Items are moved to top of list upon completion
- List name is updated each new tagged release

### Version Branch
- Named `version.<Major>.<Feature>`
- Forks from production version tag
- Only used for merging and tagging

### Version Tags
- Named `<Major>.<Feature>.<Build>`
- Created when an item is completed and merged into the Version Branch
- Used to test the item, and the version

---

## Scenarios

### Beginning an Item

	Assign yourself
	Add `WIP` label
	Do the work

### Completing an Item
	
	Move to top of version list
	Merge into version branch (eg: version-1.12)
	Tag the version branch (eg: 1.12.5)
	Update version list name (eg: Version 1.12.5)
	Developer Testing
	Create Package
	User Acceptance Testing
	If Key Feature
		Peer Testing of Item
		QA
		Production Release

### Developer Testing

	Checkout Version Tag on Dev Environment
	Test feature
	Ensure affected areas are documented in card
	If OK
		Remove `WIP` label
	Else
		Fix it
		GOTO "Completing an Item"

### User Accepance Testing

	Upgrade QA Environment to new version
	Test feature
	If OK
		Add `UAT OK` label
	Else
		Add reproduction instructions
		Add `Failed Testing` label

### Peer Testing

	Review Spec
	Review Code Changes
	Use QA Environment
	Test feature
	If OK
		Add `Peer Tested` label
	Else
		Add `Failed Testing` label
		Discuss with Developer

### QA

	Check merged branches match release list
	Test install on fresh environment
	Test upgrade on clone of production
	Peer Testing of all items
	User Acceptance Testing of standard functionality
	
### Production Release

	Deploy to production
	Delete merged branches
	Delete obsolete tags
	Move Version List to "Live" Board

### Item Fails QA

	If Key Item or quick to fix
		Fix it
	Else
		Move failed cards out of Version List
		Revert merge of failed branches
	Perform QA

### New Item is completed during QA

	Put it in a list for the next version
	If QA fails
		Consider bringing it back into this release

### Critical Bug found on Production
Due to time-sensitivity of these issues, Peer Programming will replace QA.

	Checkout production tag & reproduce bug on Dev
	Create Card with Repro instructions
	Peer Program a fix
	Move the previous Version List back to the Board
	Move item to top of previous Version List
	Upgrade QA & Test
	Release to Production
	Merge into current Version & List

---

## Considerations
- *Why not have a `qa` branch instead of having a `version-<Major>.<Minor>` branch for each release?*
	- That would make patching a production release more complicated
- *Why not have a `dev` branch for developer testing?*
	-  No value in separating from QA
- *Why not have Sub-versions for internal builds?*
	-  The value of having public feature releases end with a .0 does not justify complicating the QA procedure
- *What if another Key Feature becomes more important and we want to get it out first?*
	- Same procedure as "Item Fails Testing"
- *Automation?*
	- [QA Automation](QA Automation.md)
- *Unit Testing?*
- *What if the Backlog and Planning lists are too huge to prioritise?*
	- Use `▲—— Urgent ——▲` and `▼  —— Non-Urgent —— ▼` dividers in the list
	- Unprioritised things go inbetween the two diviers, and are generalised into "urgent" or "non-urgent" periodically.
	- When the Urgent section approaches completion, pick the next (20) non-urgent items and prioritise them above the line.
- *Why not add an "Under Assessment" list for features that aren't decided whether they should be worked on or not?*
	- These belong in "Planning"
