# Guard List (PSS)
A shift management application using the [jQuery Resource Planner](resource-planner/introduction). It’s used on the guardlist and tryggby subsites on PSS. 

## Resources
Resources are stored in the root page SiteAssets in a folder called GuardList ([link](https://psssecuritas.signin.no/SiteAssets/Forms/AllItems.aspx?RootFolder=%2FSiteAssets%2FGuardList&FolderCTID=0x012000C7E410989548A14DB5B78F0F67452B8F&View=%7BFCED0165%2D2F8B%2D44E0%2D8F84%2DBD66768047A9%7D))
- GuardList.js 
	- Main file where data is fetched, Resource Planner is initialized and user events are handled 
- jquery.ResourcePlanner.js 
	- Minified version of the jQuery based Resource Planner 
- style.css 
- index.html 

Other resources are referenced in the index.html 

## Third-party tools
- jQuery ([link](https://jquery.com/))
- jQuery UI ([link](https://jqueryui.com/))
- TooltipJS
	- Dependant on Popper ([link](https://popper.js.org/docs/v2/))
- Microsoft Fabric UI ([link](https://developer.microsoft.com/en-us/fabric-js))
- Air Datepicker ([link](http://t1m0n.name/air-datepicker/docs/))
- dayjs ([link](https://day.js.org/))

## Terminology
All unconventional terminology used is related to the jQuery Resource Planner. See the [Terminology chapter](http://localhost:3000/#/resource-planner/introduction?id=terminology) of the jQuery Resource Planner documentation for information. 