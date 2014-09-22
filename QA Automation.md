# QA Automation

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
	
		If card is not in version list
			email developer with error
			end
			
		If the card has no dev branch defined
			email developer with error
			end
			
		If unit tests on dev branch fail
			email developer with error
			end
			
		If no version branch exists
			create version branch from production tag
			
		merge dev branch into version branch
		if conflict
			undo merge
			email developer
			end
		
		If unit tests on version branch fail
			undo merge
			email developer with error
			end
			
		tag version branch
		create package
		deploy package to QA environment
		send email to developers and QA staff

## Email Template

The email will list all branches merged into the tag. If the branch belongs to a card (which it should) the Card Name will be displayed as a link.

	Subject: <version> Deployed to QA with <Card Name>
	
	Body:
		<Developer> has marked <Card Link> as done.

		<Developer's Comment>
		
		<version> contains:
		- <Card Link 1>
		- <Card Link 2>
		- <branch-name-3>
		- [...]

## Considerations

- _How long does all this stuff take to do manually?_
- _How long will it take to automate it?_
- _Will automating it save us time in the long run?_
