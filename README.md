# Website links
A complete list of websites/application links and a description of what they do

## Order check app
https://orderchecks-production.up.railway.app/ 

This website prompts the user for an inventory and an order. Then, it runs a check against what we have, what we need, and what needs to be propagated. Results are exportable in a .txt format for both the whole check and just the highest priority items. Rough route optimization has been implemented which groups plants of interest as well, so the user doesn't need to walk in inefficient paths. 

Order csv: Obtained by going to Plantiful > Sales > Line items. Then, go to the order check view, and in the search bar, type in the order number of the order you're trying to check. For example; 28176. Then, wait for the view to load, and export the csv when you're done. Importantly, you'll have to rename the order csv to 28176_order.csv. The code reads the numbers associated with the order when it's doing some of the behind the scences work!

Inventory csv: Obtained by going to Plantiful > Production, and then using the Timesaver view. Then, just export this and wait! No need to name it anything special 

Catalog csv (Optional but highly recommended): Obtained by going to Plantiful > Catalog, then clicking on the order check view. This brings in information about the availability of certain line items across the nursery, so it's then up to the user on how they disperse the existing inventory. If for example we have a deficit of a given product overall but we have an existing amount of product that could satisfy one order, it will flag this in the 'Caution' status. 

Meanings of Statuses
1. Ready : We have enough existing available inventory that's in the correct size and meets the quantity demand of the order. Additionally, the total remaining inventory quantity (taking into account all orders placed on that item) is positive. 
2. Caution : We have enough existing available inventory that's in the correct size and meets the quantity demand of the order. However, the total remaining inventory quantity (taking into account all orders placed on that item) is negative.
3. Short : We have a sufficient quantity of material in the nursery, but it's not in the right size.
4. Propagate : We do not have enough plant material in the nursery at an equal or smaller size than the requested variant. That is, we just need to propagate or buy more!

You then have the option to generate a few reports.
1. The full report is extremely comprehensive, giving a summary table and then information on all plants throughout the nursery which could possibly be used for the given order. 

2. The Short/propagate report will essentially give you the full report but filtered for those plants which have a short/propagate status. This is the "action report", which also gives suggested actions that one can take in order to fulfill the order. 

3. The customer facing report exports ONLY the summary table from the full report and replaces some of the status names with more outward friendly nomenclature. For each of the following equivalencies, the internal status is the first in the group and the customer facing status is the second: (Ready, Ready), (Short, In production), (Propagate, Currently propagating), and (Caution, Available). 

Note that some customers ask for a liner size of some plant, and while we may not have exactly the liner size they're looking for, we may have another liner size that's satisfactory for them. In this case, we internally flag this with a "Liner ready" status, but on the customer facing report, it shows up as "Ready". 

## Inventory of space 
https://inventoryofspace.up.railway.app/

This code takes only one input; your inventory. It then compares it to an internally held file which contains carrying capacities of each bed in the nursery. Then, the output is the empty space. This is helpful for those planning where to put plants next, without having to go out into the field to see what's available. The inventory file is simply the Timesaver view in the production tab on Plantiful. 

Future work will include an interactive map and functionality to include shade and irrigation units in both the inventory as well as the internal locations. 

## Cuttings finder 9000
https://web-production-cd500.up.railway.app/

This code helps the user find cuttings throughout the nursery. First navigate to Plantiful and go to the Production tab. Then, in the 'Cuttings finder' view, export the inventory as a CSV. Once this is done, you'll also need a species specific cutting information document. An example can be found here for formatting. Then, once all of these are uploaded, click on the search bar to then find a specific plant. This then brings up the stats we have on that plant. This includes things like number ready, total, skipped, and cutted. Information is keyed to crop codes and can then be referenced later on. For example, if something was cut and needs time to recover, this information will be linked to the crop code. Thus, when you then are going back to check in the future whether or not you have something you can harvest, you know that the crop that was just cut will be unavailable for some amount of time. 

## Route optimization 
https://web-production-7f1e1.up.railway.app/

This code mainly has one function but two ways of going about it. Given a list of locations within the nursery, it will order them in the most efficient path. This uses a low-n assumption about going to n stops (s.t. n<10), but better algorithms are being researched and implemented. The user can specify if they're using a cart or walking on foot. Furthermore, there are two ways to give information on locations. You can either just type them out one by one, separated by commas, OR, the user can upload a file with locations. In the case that a file is uploaded, the file will be returned, now with orders in sequential order according to the route optimization. The app is now somewhat matured, but the logic is mainly being used in a package form that's being uploaded to other projects. 

(Note: right now, nets are placed around graph theoretical nodes to allocate bed locations. Beds in the same net are returned in smallest to greatest number, which may not always be the case. Refine the mesh and pray!) 

## Inventory auto-formatter
https://web-production-cd05a.up.railway.app/

This tool allows the user to convert formats for a few different pieces of data. The most obvious one is the inventory, but there's a capability to format invoices too. 
1. The website catalog formats the Plantiful inventory in a way that's readily usable by the Squarespace website (https://nativewest.squarespace.com/config/). The user must replace un-translated common names from botanical names if they don't all come through, although there's a back-end way to add things to the translation at a later time.
2. The striven inventory tool allows the user to get a correctly formatted striven upload for regular communication between the sites that we use the most. It first requires the user to upload the catalog from Plantiful > Catalog in the 'Plantiful qty to Striven' view (https://app.plantiful.ai/organizations/native-west-nursery/catalog/availability?viewId=e9fc8bf0-43c8-439e-a95e-2de02f079bd1). Then, you'll need to get the Striven inventory by navigating to this site (https://nwn.striven.com/next/reports#/custom-reports/57880/viewer) and then exporting from here. Now you have the files necessary to upload to the tool! Upon doing so, you'll be prompted to upload any un-seen items into the Striven inventory seperately here (https://nwn.striven.com/Order/Items/ItemsImport.aspx?nav=1). Striven won't take "Inventory adjustments" on non-existing inventory which is why the user needs to do this. Upon uploading non-existing items, 500 cell long files fitting the expected format of the import will be available to the user to upload here (https://nwn.striven.com/Accounting/InventoryAdjustments/InventoryAdjustment.aspx?nav=1). If all goes well, you're done! If all is not well, let me know and we can sort it out.
3. The invoicing component allows the user to take shipping and line item information from the sales tab in Plantiful and upload it to Striven in the form of invoices. The user should first  decide on a date range that will be used throughout the invoice production. Make sure these are held consistent across all files pulled. Navigate to Plantiful > Sales > Shipments, then pick the 'Invoice Plantiful to Striven' view. Make sure to edit the filters to match the date range that you're interested in before exporting! Then, go to Plantiful > Sales > Line items and use the 'Invoice to Striven' view. Here, again, edit the date ranges to align with the time frame you're interested in, then export! Now you have the essentials and can head over to the website. Upon successfully running the tool, the user will be given some information about the run. It'll first tell you, if any, what cities are listed in the export but aren't recognized for tax purposes by Striven. You then have two options. Either edit the city name to be something recognized manually, or let me know and I can add some code behind the scenes that automatically converts some of these cities to other recognized ones for Tax code equivalency purposes (i.e., La Jolla = San Diego). When these are resolved, you can then scroll down and see the names of shipments which had no listed shipping city. Whenever this occurs, we assume that the shipping city is San Diego for tax purposes, since it usually means that they're picking up the plants at the nursery - formally in San Diego. Finally, the uploadable CSVs should be formatted correctly for importability into Striven. Navigate here (https://nwn.striven.com/Utilities/InvoicesImport.aspx?nav=1) and import away! 

## Pre-emergent application automation 
https://web-production-dfbd5.up.railway.app/

This code can be used to generate a list of plants which need some kind of treatment. Right now (6/9/26) this can only handle pre-emergent, however in the future we can outline other functions for this list such as rootshield and fertilizer. Note that you cannot change the number of weeks you're looking back. The default is 3 but this can be changed as needed. Additionally, this code allows you to banish certain rows from the list that are not relevant for the export. That is, if something shouldn't be on the list for whatever reason, there's an easy way to manually remove it from the list before generating the export. 

## The Finer Liner Finder
https://web-production-42f6d.up.railway.app/

This code allows the user to find liners for the products that are the most in the negative. It will then allow the user to customize the exportable file to include or not include certain parts of the report. If say, you only want to go look at the Salvia mellifera liners, there is an easy way to do so! Upon checking the boxes on the left side of the program, that catalog item's liners will be added to the report. the user then has the option to add or take out certain beds depending on their needs. Then, the user is given the option to export the report. This includes liner information on the selected plants such as location, species, size, qty, quoted qty, deficit, crop code, and notes. As for required files, you'll need to take the 'In the negative' inventory from the catalog tab in plantiful, and then you'll also need the timesaver inventory from Plantiful in the production tab. Importantly, once you upload a file, click either *Upload catalog* or *Upload Timesaver* immediately depending on which one was just uploaded. This 'locks it in', so to speak. If you go on without doing this, the upload won't save and you'll be mildly sad. 

## Digital cycle counting
https://glochidbeard.github.io/cycle_counts

_HOSTED ON GITHUB PAGES, NOT RAILWAY_ This app is usable as an application without internet connection for a tablet based interface out in the field. The main use is being able to do inventory cycle counts without a paper trail. Note that while this does technically run on the computer, it is not configured whatsoever for visual appeal. In fact, the interface kind of breaks and is generally not recommended. For use on the tablet however, the user will first need to navigate to the website linked above on the tablet and then go to the top right hand corner of the screen to the kebab. Scrolling nearly all the way to the bottom, there is then an option to add to home screen. Upon doing this, you should now have a nice app on the home screen which can be readily accessed any time. Note that the download for the inventory is necessary to have prior to actually taking the tablet out into the field, but once out in the field, no more connection is necessary. 

## Plursery - The nursery planner
https://nurseryplanner-production.up.railway.app/

This app allows for one to create Polygons for roads, structures, and features to efficiently plan space in the nursery. It starts you off in Yuma for some reason but you'll have to scroll to the nursery (or potential new site?!) of interest. You can then design how everything should look in a self explanatory way. To save the maps you have to export them - and then next time you want to work on it, you'll have to import them back in. 







