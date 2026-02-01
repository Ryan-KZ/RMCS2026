# Module 2: Predictive Logistics
## "Arctic Resupply" Scenario

**Duration:** ~30 minutes
**Objective:** Design a workflow where a Supply Chain Agent queries inventory data and an Action Agent auto-drafts DD Form 1348 requisitions.

---

## SCENARIO BRIEF

You are the assistant supply officer at FOB POLAR SENTINEL, a forward operating base in Deadhorse, Alaska. A severe Arctic storm is approaching - temperatures will drop to -70°F with wind chills below -120°F. Your resupply window closes in 3 days and won't reopen for 7-10 days.

Your mission: Use Kaizen to analyze inventory levels against the incoming weather, identify critical shortfalls, and generate DD Form 1348 requisitions for emergency resupply before the storm hits.

**Available Data Files:**
- `inventory_catalog.csv` - Master catalog of Arctic supplies with NSN, specs, pricing
- `base_inventory.csv` - Current stock levels, min/max, days of supply
- `weather_forecast.csv` - 14-day forecast with operational impacts
- `vendor_catalog.csv` - Vendor info, lead times, shipping methods
- `item_vendor_mapping.csv` - Which vendor supplies each item
- `dd1348_field_reference.csv` - Field specifications for requisition forms
- `base_info.csv` - Base details for shipping address

---

## PHASE 1: WEATHER ASSESSMENT (3-5 min)

**Goal:** Understand the incoming weather and its operational impact.

### Sample Prompts

**Natural language approach:**
What's the weather looking like for the next two weeks? I need to know when the storm hits, how bad it gets, and when we can expect resupply flights again. Just the weather data for now.

**More specific prompts:**
Show me the weather forecast. When does the severe weather start and how long does it last?

What are the coldest temperatures and wind chills we're expecting? What's the operational impact?

When is our last window for resupply before the storm closes us in?

**What You Should Find:**
- Blizzard warning starts Day 4-5
- Extreme cold (-70°F, wind chill -120°F+) Days 6-8
- Resupply NOT feasible Days 4-10
- Only 3 days to get supplies in

---

## PHASE 2: INVENTORY ASSESSMENT (5-7 min)

**Goal:** Identify what's running low and what's critical.

### Sample Prompts

**Natural language approach:**
Check our current inventory and flag anything that's CRITICAL or LOW. I need to know what we're short on, how many days of supply we have, and whether it'll last through the storm. Just the inventory status for this step.

**More specific prompts:**
Show me all inventory items with status CRITICAL or LOW. Include the current quantity, minimum level, and days of supply.

Which critical items have less than 10 days of supply? The storm could keep us isolated for 10+ days.

Are any of our heating, fuel, or cold weather gear items running low? Those are life-safety items.

**What You Should Find:**
- CRITICAL: Arctic diesel fuel (5 days supply)
- CRITICAL: Cold weather rations (4 days supply)
- CRITICAL: Arctic weapons lubricant (3 days supply)
- CRITICAL: Cold injury medical kits (3 days supply)
- LOW: Parkas, heaters, radio batteries, water containers

---

## PHASE 3: CROSS-REFERENCE WEATHER & INVENTORY (5-7 min)

**Goal:** Determine what we actually need to order based on storm duration.

### Sample Prompts

**Natural language approach:**
Now cross-reference the inventory shortfalls with the weather forecast. If we're going to be isolated for 10 days, which items won't make it? Factor in the lead times from vendors too - can we even get stuff here in time?

**More specific prompts:**
For each CRITICAL and LOW item, compare days of supply against the storm duration. Which items will run out during isolation?

Check the vendor lead times. With only 3 days until the resupply window closes, which vendors can deliver in time?

Calculate how much of each critical item we need to order to get through a 10-day isolation period with a safety buffer.

**What You Should Find:**
- Multiple items won't last through 10-day isolation
- Some vendors have 3-5 day lead times (might make it)
- Some vendors have 7-10 day lead times (won't make it before storm)
- Need to prioritize life-safety items: fuel, rations, medical, heating

---

## PHASE 4: REQUISITION PLANNING (5-7 min)

**Goal:** Determine quantities and priorities for each order.

### Sample Prompts

**Natural language approach:**
Based on what we're short on and what can actually get here in time, build me a requisition list. Prioritize life-safety stuff first - fuel, food, medical, heating. Show me what we need to order, how much, and the priority level.

**More specific prompts:**
Create a prioritized list of items to requisition. Include NSN, quantity needed, unit price, and extended cost.

Assign priority designators: 01-03 for life-safety items (fuel, rations, medical, heating), 04-08 for mission-essential items.

Calculate total weight and cube for shipment planning. Can this go on one aircraft?

**What You Should Find:**
- 4 items at PRIORITY 02-03 (life-safety critical)
- 4 items at PRIORITY 05-06 (mission essential)
- Total quantities based on personnel count + storm duration + safety buffer
- Estimated total cost and shipment size

---

## PHASE 5: DD FORM 1348 GENERATION (7-10 min)

**Goal:** Generate properly formatted DD Form 1348-1A requisitions.

### Sample Prompts

**Natural language approach:**
Now I need you to draft DD 1348 requisitions for the critical items. Use the base info for shipping address, pull the NSNs and pricing from the catalog, and generate proper document numbers. Start with the PRIORITY 02-03 items.

**More specific prompts:**
Generate a DD Form 1348-1A for Arctic diesel fuel. Include all required fields from the reference document.

Create requisitions for all CRITICAL items. Use document numbers starting with W81K2F6029001 (increment the serial for each).

Format the requisitions so they can be submitted - include consignee address, weights, and special handling instructions for cold weather items.

**Key DD 1348 Fields to Include:**
- Document Number: W81K2F + Julian date (029 for Jan 29) + serial (001, 002, etc.)
- NSN from inventory catalog
- Unit of Issue and Quantity
- Priority Designator (02 or 03 for critical items)
- Unit Price and Extended Price
- Ship-to address from base_info
- Special handling: "PRIORITY - ARCTIC STORM EMERGENCY"

**What the Output Should Look Like:**
```
DD FORM 1348-1A REQUISITION
---------------------------
DOCUMENT NUMBER: W81K2F6029001
NSN: 9140-01-352-4679
ITEM: FUEL, DIESEL, ARCTIC GRADE DF-A
UNIT OF ISSUE: DR
QUANTITY: 100
UNIT PRICE: $285.00
EXTENDED PRICE: $28,500.00
PRIORITY: 02
SHIP TO: FOB POLAR SENTINEL, Unit 4520, Box 150
         Deadhorse, AK 99734
SPECIAL HANDLING: PRIORITY - ARCTIC STORM EMERGENCY
REQUIRED DELIVERY: 3 DAYS
REQUISITIONER: MAJ David Chen, DSN 317-555-4520
```

---

## PHASE 6: SUMMARY REPORT (3-5 min)

**Goal:** Create a consolidated requisition package for approval.

### Sample Prompts

**Natural language approach:**
Put together a summary report I can send up for approval. Include the weather situation, what we're short on, the requisitions we're submitting, total cost, and why this is time-critical. Make it clear this is an emergency requisition package.

**More specific prompts:**
Create an executive summary of the Arctic resupply requisition package. Include total items, total cost, and delivery timeline.

Generate a PDF report with the weather analysis, inventory shortfalls, and all DD 1348 requisitions.

What's our risk if this requisition isn't approved and fulfilled in the next 72 hours?

---

## SUCCESS CRITERIA

By the end of this module, you should have:

✅ Assessed the incoming weather and identified the isolation window
✅ Identified all CRITICAL and LOW inventory items
✅ Cross-referenced shortfalls against storm duration and vendor lead times
✅ Created a prioritized requisition list with quantities and costs
✅ Generated properly formatted DD Form 1348-1A requisitions
✅ Produced a summary report for command approval

---

## BONUS CHALLENGES (If Time Permits)

If you complete the exercise early, try these:

1. **Cost Optimization:** Are there bulk discounts available? Could we save money by consolidating orders?

2. **Alternate Sourcing:** If primary vendors can't deliver in time, are there alternatives?

3. **Consumption Modeling:** Based on personnel count and weather severity, model the actual consumption rate during the storm.

4. **Contingency Planning:** What if only half the requisition gets approved? Prioritize the absolute minimum needed for survival.

---

## DATA FIELD REFERENCE

### Key Fields to Query

**base_inventory.csv:**
- `status` - CRITICAL, LOW, ADEQUATE, OVERSTOCKED
- `current_quantity` - Stock on hand
- `days_of_supply` - How long current stock will last
- `min_level`, `reorder_point` - Threshold levels

**weather_forecast.csv:**
- `temp_low_f`, `wind_chill_f` - Temperature conditions
- `storm_warning` - Alert level
- `resupply_feasible` - YES/NO for flight operations

**item_vendor_mapping.csv:**
- `standard_lead_time_days` - Normal delivery time
- `weather_adjusted_lead_time_days` - Delivery time with weather delays

**dd1348_field_reference.csv:**
- `block` - Field position on form
- `field_name` - Data element name
- `required` - YES/NO
- `example` - Sample value

---

## NOTES FOR INSTRUCTORS

**The "Aha" moments:**
1. Weather analysis reveals 10-day isolation window
2. Multiple critical items won't last that long
3. Only 3 days to get resupply in - some vendors won't make it
4. Must prioritize life-safety over nice-to-have
5. DD 1348 generation requires specific field formats

**If trainees get stuck:**
- Point them to the weather_forecast resupply_feasible column
- Remind them to check days_of_supply against isolation duration
- Reference dd1348_field_reference for form fields

**Expected conclusion:**
Emergency requisitions for Arctic diesel, cold weather rations, medical kits, and heating fuel are life-safety critical and must be submitted within 24 hours to arrive before the resupply window closes. Total emergency package approximately $50,000-75,000 depending on quantities calculated.
