# Website links
A complete list of websites/application links and a description of what they do

# Order check app
https://orderchecks-production.up.railway.app/ 

This website prompts the user for an inventory and an order. Then, it runs a check against what we have, what we need, and what needs to be propagated. Results are exportable in a .txt format for both the whole check and just the highest priority items. Rough route optimization has been implemented which groups plants of interest as well, so the user doesn't need to walk in inefficient paths. 

Future work will involve writting and implementation of an allocation algorithm based on order priority. 

# Inventory of space 
https://inventoryofspace.up.railway.app/

This code takes only one input; your inventory. It then compares it to an internally held file which contains carrying capacities of each bed in the nursery. Then, the output is the empty space. This is helpful for those planning where to put plants next, without having to go out into the field to see what's available. 

Future work will include an interactive map and functionality to include shade and irrigation units in both the inventory as well as the internal locations. 

# Cuttings finder
https://web-production-cd500.up.railway.app/

This code helps the user find cuttings throughout the nursery. First navigate to Plantiful and go to the Production tab. Then, in the 'Cuttings finder' view, export the inventory as a CSV. Once this is done, you'll also need a species specific cutting information document. An example can be found here for formatting. Then, once all of these are uploaded, click on the search bar to then find a specific plant. This then brings up the stats we have on that plant. This includes things like number ready, total, skipped, and cutted. Information is keyed to crop codes and can then be referenced later on. For example, if something was cut and needs time to recover, this information will be linked to the crop code. Thus, when you then are going back to check in the future whether or not you have something you can harvest, you know that the crop that was just cut will be unavailable for some amount of time. 


Digital cycle counting
**In progress**


