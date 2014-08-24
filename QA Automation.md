# Qa Automation

## Goal
Automation of as much of the QA procedure as possible

## Summary
When a developer finishes an item, it is automatically prepared for QA.

## Requirements
- Trello integration
	- hook into 'comment made' event
	- read card information (incl list)
- ability to send email
- automated package creation
- automated deployment
- automated Unit Testing


## Procedure

	When a developer comments on a card `#done`
	If card is not in list named "Version <n>.<n>"
		end
	If the card has no branch defined
		email developer with error
		end
	If no version branch exists
		create version branch from production tag
	merge card branch into version branch
	if conflict
		cancel merge
		email developer
		end
	tag version branch
	create package
	deploy package to QA
	email all developers and QA

## Email Template
The email will list all branches merged into the tag. If the branch belongs to a card (which it should) the Card Name will be displayed as a link.

	Subject: <version> Deployed to QA with <Card Name>

	Body:
		<Developer> has marked <Card> as done.

		<Developer's Comment>
		
		<version> contains:
		- <Card Name 1>
		- <Card Name 2>
		- <branch-name>
		- [...]

## Considerations
- *How long does all this stuff take to do manually?*
- *How long will it take to automate it?*
- *Will automating it save us time in the long run?*