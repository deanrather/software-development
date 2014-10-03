# Software Development Life Cycle

This document outlines how a small team can use Git and Trello to rapidly develop Quality Software.

### Goal

- To minimise the amount of time between works completion and release, while ensuring Quality.

### Requirements

- All changes must pass Developer, Peer, and User Testing
- New versions must pass End-to-end Testing

---

![Funny Comic about Test Procedure](http://curtis.lassam.net/comics/cube_drone/20.gif)

---

## Procedure

1. When a developer completes work, they merge with the rest of the completed work and test it
2. Then the item can be User Tested
2. When a Key Item passes Developer and User Testing the development version is locked down and QA begins
3. QA involves Peer Testing each of the items, and end-to-end testing of the entire system
3. When a version passes QA, It is released

### Planning an Item
	
	Choose Card from top of Planning List
	If you can spec the work yourself
		Spec the work
		Have a Peer review the spec
	else
		Prepare Work Planning Notes
		Do Work Planning (probably produces many Backlog Cards)
	Move to Backlog

See: [Work Planning](Work Planning.md)

### Working on an Item

	Choose Card from top of Backlog
	Assign yourself to the card
	Add `WIP` label
	Do the work

### Completing an Item
	
	Move to top of Version List
	Merge into Version Branch
	Tag the Version Branch with new version number
	Update Version Card with version number
	Perform Developer Testing
	Remove `WIP` label
	Create Package

See: [Developer Testing](Testing.md)
	
### User Testing

	For each Card in Version List without any labels
		Perform User Testing
		If OK
			Add `User Tested` label
		Else
			Add reproduction instructions
			Add `Failed Testing` label
			
See: [User Testing](Testing.md)
			
### Version Lockdown & QA

	If All Items (including Key Item) have `User Tested` label
		Lock Down Version
		For each item in version
			Perform Peer Testing
			If OK
				Add `Peer Tested` label
			Else
				Add `Failed Testing` label
				Discuss with Developer
		Perform End-to-end Testing

See: [Peer Testing](Testing.md), [End-To-End Testing](Testing.md)

### Item Fails QA

	If Key Item or quick-to-fix
		Fix it
	Else
		Move failed cards back to Backlog
		Revert merge of failed branches into Version or create new Version
	Perform QA

### New Item is completed during QA

	Create a new Version List
	Use that List

### Version Passes QA & Production Release

	Mark version as Stable
	Deploy to version production
	Merge Git Version Branch into Master
	Delete branches merged into Master
	Delete unstable build tags
	Move Version List to "Live" Board

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

### Nomenclature

- Item - _A Feature, Bug, or Improvement. Has a Trello Card and a Git Branch_
- Key Item - _An Item worth doing a release for_
- Current Development Version- _The version of the application currently under development_
- Developer Testing - _The Item's Developer testing it against the Current Development Version_
- User Testing - _A Non-Developer testing an Item_
- Peer Testing - _Another Developer Reviewing and testing an Item_
- End-to-end Testing - _Test of the entire application_
- Lockdown - _A version goes into lockdown for QA. While in lockdown, any changes to the version require restarting QA_
- Patch - _An update to a previous release_

#### Version Names

	<Major>.<Feature>.<Build>

- Major -- The application version. Typically `1`
- Feature -- Incremented with new (non patch) release
- Build -- Incremented each time changes are merged in

Most builds will be internal testing releases
When a build passes QA, it will become a production release

--- 

## Trello & Git

Trello's Version List should mimic Git's Version Branch, and Trello Cards should correspond to Git Dev Branches.
In this way, merging a branch into the version involves dragging the card to the top the list.

### Trello Lists

- `Inbox` -- Dumping ground for ideas / bugs, etc.
- `Planning` -- Ordered list of items which need planning before work can commence
- `Backlog` -- Ordered list of items which are ready to be worked on, or currently being worked on
- `Version <Major>.<Feature>` -- The version under current development

Inbox should be tidied out and Unprioritised cards prioritised before stand-up each morning

### Items

Items have Trello Cards and Git Dev Branches to track the progression of the item.

#### Trello Cards

Named: `<Feature Name>[ : <short description> [Bug|Improvement] ]`
eg: `Facebook Integration`, `Coloured Widgets : more colours Improvement`

- [Full Spec](Trello Cards.md)

#### Git Dev Branches

Named `dev.<developer>.<feature-name>[.[bugfix|improvement]`
eg: `dev.dean.facebook-integration`, `dev.dean.coloured-widgets.improvement`

- Feature branches fork from latest production version tag
- Bugfix and Improvement branches can fork from feature branches
- Can merge other dev branches if required

### Versions

Versions have Trello Lists and Git Version Branches to track the contents of the version.
They also have Trello Version Cards and Git Version Tags to tag stable points in the version.

#### Trello Version List

- Named `<Major>.<Feature>`
- Items are moved to top of list upon completion

#### Git Version Branch

- Named `<Major>.<Feature>`
- Forks from production version tag
- Only used for merging and tagging

#### Trello Version Card

- Named `# ———— <Major>.<Feature>.<Build> ———— #`
- Lives at the top of the Version List
- Updated each time a change is merged into the Git Version Branch
- Contains `git merge` snippet to reproduce Git Version Branch
- Contains Changelog

#### Git Version Tags

- Named `<Major>.<Feature>.<Build>`
- Created when an item is completed and merged into the Version Branch
- Used to test the item, and the version

---

## Considerations

- _Why not have a `qa` branch instead of having a `version-<Major>.<Minor>` branch for each release?_
	- That would make patching a production release more complicated
- _Why not have a `dev` branch for developer testing?_
	-  No value in separating from QA
- _Why not have Release Candidate versions for internal builds?_
	-  The value of having public releases look like x.y.0 does not justify complicating workflow
- _What if another Key Item becomes more important and we want to get it out first, and there's broken features in the WIP release?_
	- Either back out the broken features, or make another version list.
- _How much of this can we automate?_
	- [QA Automation](QA Automation.md)
- _What if the `Backlog` and `Planning` lists are too huge to prioritise?_
	- Use `▲ ———— Prioritised ———— ▲` and `▼ ——— Not Important ——— ▼` dividers in the list
	- Unprioritised things go inbetween the two diviers, and are sorted into "prioritised" or "Not Important" periodically.
	- When the prioritised section approaches completion, pick the next ~20 "Not Important" items and prioritise them.
- _Why not have an "Under Assessment" list for items we don't know whether or not to do?_
	- These belong in "Planning" under "Unprioritised"
