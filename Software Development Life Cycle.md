# Software Development Life Cycle

### Goal
Minimise the amount of time between when an item is completed, and when it's released.

## Summary

![Funny Comic about Test Procedure](http://curtis.lassam.net/comics/cube_drone/20.gif)

### Requirements
Before a new version can be released to production:

- New items must pass Developer, Peer, and QA Testing
- The new version must pass a Full QA Cycle

### Workflow
- Work Planning determines the next Key Feature
- When an item is completed, the Developer & QA both test it against the other completed items in the new version
- When a Key Feature passes Developer, & QA testing, a Full QA Cycle is performed
- When a Full QA Cycle completes, the version is released
- When the version is released, we do Work Planning

### Terms
- Development Cycle -- Period of time between one production release and the next
- Key Feature -- Primary goal of a development cycle
- Item -- A Feature, Bug, or Improvement. Has a card and a branch
- Testing -- Requires that the item has been merged into the version
- Developer Testing -- Testing by the developer who worked on the item
- Peer Testing -- Tesing by another developer
- QA Testing -- Testing by a non developer
- Full QA Cycle -- Peer Testing of all items, and End-to-end QA testing

### Version Names

	<Major>.<Feature>.<Build>

- Major -- `1`
- Feature -- Incremented on feature release
- Build -- Increments which each merged (or re-merged) item

Most builds will be internal QA releases.
When a build passes a Full QA Cycle, it will become a production release.

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
- `Planning` -- Not yet ready for development to commence
- `Improvements` -- Improvements to existing features
- `Bugs` -- Bugs. (Assigned to creator or QA if can't reproduce)
- `Features` -- New Features
- `Version <Major>.<Feature>` -- The version under current development

#### Housekeeping
- Triage cleared before stand-up each morning
- All cards / lists reviewed prior to Work Planning

### Version List
- Named `Version <Major>.<Feature>`
- Items are moved to top of list upon completion

### Version Branch
- Named `version.<Major>.<Feature>`
- Forks from production version tag
- Only used for merging and tagging

### Version Tags
- Named `<Major>.<Feature>.<Build>`
- Created when an item is completed and merged into the Version Branch
- Used to test the item

### Version Cards
- Named `<Major>.<Feature>.<Build>`
- Created at the top of the Version List when the version is tagged
- Can contain changelog
- New & Changed Items go above Version Card

---

## Scenarios

### Beginning an Item

	Assign yourself
	Add `WIP` label
	Do the work

### Completing an Item
	
	Move to top of version list
	Merge into version branch (eg. version-1.12)
	Tag the version branch (eg 1.12.5)
	Create Tag card
	Developer Testing
	Create Package
	QA Testing
	If Key Feature
		Peer Testing
		Full QA Cycle
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

### QA Testing

	Upgrade QA Environment to new version
	Test feature
	If OK
		Add `QA OK` label
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

### Full QA Cycle

	Check merged branches match release list
	Test install on fresh environment
	Test upgrade on clone of production
	Peer Testing of all items
	QA testing of standard functionality
	
### Production Release

	Deploy to production
	Delete merged branches
	Delete obsolete tags
	Move Version List to "Live" Board

### Item Fails Full QA Cycle

	If Key Item or quick to fix
		Fix it
	Else
		Move failed cards out of Version List
		Revert merge of failed branches
	Perform Full QA Cycle

### New Item is completed during Full QA Cycle

	Put it in a list for the next version
	If Full QA Cycle fails
		Consider bringing it back into this release

### Critical Bug found on Production
Due to time-sensitivity of these issues, Peer Programming will replace a Full QA Cycle.

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
- *Unit Testing?*
