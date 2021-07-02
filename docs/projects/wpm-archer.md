# WPM: Well Planning Management (Archer)
A well planning management application using the jQuery Resource Planner.

## Resources 
Resources are stored in root page SiteAssets in a folder called WPM ([link](https://archer.signin.no/SiteAssets/Forms/AllItems.aspx?RootFolder=%2FSiteAssets%2FWPM&FolderCTID=0x012000C7E410989548A14DB5B78F0F67452B8F&View=%7BFCED0165%2D2F8B%2D44E0%2D8F84%2DBD66768047A9%7D)). 

- WPM.js 
	- Main file where data is fetched, Resource Planner is initialized and user events are handled 
- dropdowns.js 
	- Simple dropdown manager using Select2 
- StateManager.js 
	- Simple state manager that makes it easier to keep track of the application’s state in the URL hash and load a state based on the URL hash 
- Constants.js 
	- Static options for data fetching, dropdown setup and other stuff 
- jquery.ResourcePlanner-WPM.js 
	- Minified version of the jQuery based Resource Planner that has some WPM specific changes made to it 
- getListItems.js 
	- Simplifies the use of SPServices with iQS 
- style.css 
- index.html

## Third-party tools
- jQuery ([link](https://jquery.com/))
- jQuery UI ([link](https://jqueryui.com/))
- TooltipJS
	- Dependant on Popper ([link](https://popper.js.org/docs/v2/))
- Select2 ([link](https://select2.org/))
- Microsoft Fabric UI ([link](https://developer.microsoft.com/en-us/fabric-js))
- Air Datepicker ([link](http://t1m0n.name/air-datepicker/docs/))
- dayjs ([link](https://day.js.org/))

## Terminology
All unconventional terminology used is related to the jQuery Resource Planner. See the [Terminology chapter](http://localhost:3000/#/resource-planner/introduction?id=terminology) of the jQuery Resource Planner documentation for information. 