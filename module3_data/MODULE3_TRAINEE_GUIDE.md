# Module 3: Intel Fusion
## "RFI Crusher" Scenario

**Duration:** ~30 minutes
**Objective:** Build a local RAG pipeline to analyze acquisition documents, extract key data, generate an RFI, and use a Red Team agent to identify bias.

---

## SCENARIO BRIEF

You are an acquisition analyst supporting the OVERWATCH program - a long-range surveillance drone procurement. You've received 46 documents from 5 competing vendors plus internal government assessments. Your mission is to:

1. Index and analyze the document corpus
2. Extract Range and Payload data into a comparison spreadsheet
3. Draft a Request for Information (RFI)
4. Act as Red Team to identify bias in the requirements

**Available Documents (46 total):**
- Vendor Data Sheets (5)
- Performance Test Reports (8)
- Technical Specifications (5)
- Flight Test Reports (5)
- Reliability Analyses (5)
- Environmental Assessments (5)
- Program documents: ORD, CDD, CONOPS, Trade Study, Market Survey, Cost Estimate, Risk Assessment, SOW, Safety Assessment, Benchmark Analysis, TEMP, ICD

**Vendors:**
- Northwind Aerospace: Sentinel-X (2,200 km range, 450 kg payload)
- Falcon Defense: Raptor-MQ (1,800 km range, 350 kg payload)
- SkyWatch Industries: Horizon-200 (1,200 km range, 200 kg payload)
- Arcturus Dynamics: Aurora-P (1,500 km range, 280 kg payload)
- Meridian UAV: Pathfinder-LR (1,600 km range, 320 kg payload)

---

## PHASE 1: DOCUMENT INDEXING (5-7 min)

**Goal:** Load and index the document corpus for "RAG" queries.

### Sample Prompts

**Natural language approach:**
I've got about 50 documents in the documents folder related to a drone acquisition program. Search through all the documents and extract the meaningful data. I need to build a comparison matrix of what each vendor is offering. Put it in a csv format.

**More specific prompts:**
Find all Range values (in km) mentioned in the documents. Group by vendor.

Find all Payload values (in kg) mentioned in the documents. Group by vendor.

Create a spreadsheet comparing all vendors with columns for: Vendor, System Name, Range (km), Payload (kg), Endurance (hr), Ceiling (ft), Unit Cost.

Cross-reference the vendor data sheets against the test reports - do the claimed specs match what was tested?

**What You Should Find:**

| Vendor | System | Range (km) | Payload (kg) | Ceiling (ft) |
|--------|--------|------------|--------------|--------------|
| Northwind | Sentinel-X | 2,200 | 450 | 50,000 |
| Falcon | Raptor-MQ | 1,800 | 350 | 45,000 |
| Meridian | Pathfinder-LR | 1,600 | 320 | 40,000 |
| Arcturus | Aurora-P | 1,500 | 280 | 42,000 |
| SkyWatch | Horizon-200 | 1,200 | 200 | 35,000 |

---

## PHASE 2: RFI GENERATION (7-10 min)

**Goal:** Generate a Request for Information document based on the requirements.

### Sample Prompts

**Natural language approach:**
Based on what you've learned from these documents, draft an RFI for the OVERWATCH program. Include the key performance requirements, what information we're requesting from vendors, and how submissions should be formatted. Make it a proper acquisition document.

**More specific prompts:**
What are the threshold and objective requirements from the ORD and CDD documents?

Draft an RFI that includes: program background, system requirements (range, payload, endurance, ceiling), requested vendor information, and submission instructions.

Generate the RFI as a PDF document.

**RFI Should Include:**
- Program: OVERWATCH Long-Range Surveillance UAS
- Range: 1,500 km threshold / 2,200 km objective
- Payload: 300 kg threshold / 450 kg objective
- Endurance: 24 hr threshold / 36 hr objective
- Ceiling: 45,000 ft threshold / 50,000 ft objective

---

## PHASE 3: RED TEAM ANALYSIS (7-10 min)

**Goal:** Switch to adversarial mindset and identify bias in the requirements.

### Sample Prompts

**Natural language approach:**
Now I need you to act as a Red Team. Look at the requirements documents and the RFI we just created. Find any specifications that unfairly favor one vendor over others. Look for language that's biased, requirements only one company can meet, or anything that would give someone grounds to protest this acquisition.

**More specific prompts:**
Which vendors can meet the 50,000 ft ceiling objective? Is this requirement necessary or does it unfairly narrow the competition?

The requirements mention "Type-VII data link preferred" - which vendor offers this? Is this a legitimate requirement or vendor-specific language?

What delivery timeline does the ORD specify as "strongly desired"? Which vendors can meet it?

Create a bias assessment report identifying every requirement that favors a specific vendor.

**Bias to Discover:**

| Biased Requirement | Only Met By | Issue |
|--------------------|-------------|-------|
| 50,000 ft ceiling (objective) | Northwind only | Eliminates 4 of 5 vendors |
| Type-VII data link "preferred" | Northwind only | Proprietary specification |
| 24-month delivery "strongly desired" | Northwind only | Unrealistic for others |
| 450 kg payload (objective) | Northwind only | Sets bar at one vendor's max |
| Arctic ops "desired" | Arcturus only | Not in original mission need |

---

## PHASE 4: BIAS REPORT (3-5 min)

**Goal:** Generate a formal Red Team report documenting the bias findings.

### Sample Prompts

**Natural language approach:**
Put together a Red Team report documenting all the bias issues you found. For each one, explain what the requirement is, who it favors, why it's problematic, and recommend how to fix it to ensure fair competition.

**More specific prompts:**
Generate a PDF report titled "Red Team Assessment: OVERWATCH RFI Bias Analysis"

For each biased requirement, recommend a revised threshold/objective that maintains capability while enabling competition.

What's the risk if we proceed with these requirements as written? Could we face a bid protest?

**Report Should Include:**
- Executive summary of bias findings
- Detailed analysis of each biased requirement
- Who benefits from current language
- Recommended revisions
- Risk assessment if unchanged

---

## SUCCESS CRITERIA

By the end of this module, you should have:

✅ Indexed 46 documents into a searchable corpus
✅ Extracted Range and Payload data into a comparison spreadsheet
✅ Identified all 5 vendors and their key specifications
✅ Generated a draft RFI document
✅ Switched to Red Team mindset
✅ Identified 4-5 biased requirements
✅ Produced a bias assessment report with recommendations

---

## BONUS CHALLENGES (If Time Permits)

If you complete the exercise early, try these:

1. **Fair RFI Revision:** Rewrite the RFI with bias removed. What threshold/objective values would allow fair competition while meeting mission needs?

2. **Cost-Capability Analysis:** Which vendor offers the best value (capability per dollar)? Create a visualization.

3. **Risk Matrix:** If we select the highest-capability vendor (Northwind), what are the risks? If we select the lowest-cost vendor (SkyWatch), what capability gaps exist?

4. **Source Selection Criteria:** Design fair evaluation criteria that don't predetermined the winner.

---

## DOCUMENT REFERENCE

### Document Naming Convention
- `VDS-[VENDOR]-001` = Vendor Data Sheet
- `PTR-[VENDOR]-00X` = Performance Test Report
- `SPEC-[VENDOR]-001` = Technical Specification
- `FTR-[VENDOR]-001` = Flight Test Report
- `ORD-OVERWATCH-001` = Operational Requirements Document
- `CDD-OVERWATCH-001` = Capability Development Document
- `TRD-OVERWATCH-001` = Trade Study Report

### Key Documents for Bias Analysis
- `ORD-OVERWATCH-001` - Contains biased KPPs
- `TRD-OVERWATCH-001` - Shows weighted scoring favoring Northwind
- `CDD-OVERWATCH-001` - Type-VII data link preference
- `ICD-OVERWATCH-001` - Interface requirements
- `URD-OVERWATCH-001` - User requirements with bias language

---

## NOTES FOR INSTRUCTORS

**The "Aha" moments:**
1. Data extraction reveals Northwind has highest specs across the board
2. Objective requirements exactly match Northwind's capabilities
3. Type-VII data link is Northwind proprietary
4. Only Northwind meets 24-month delivery timeline
5. Requirements seem designed to justify selecting highest-cost vendor

**If trainees get stuck:**
- Point them to the ORD document for threshold/objective values
- Suggest comparing ceiling requirements against vendor specs
- Ask "who benefits from this requirement?"

**Expected Red Team findings:**
The requirements as written would likely result in a sole-source justification for Northwind Aerospace, despite being framed as a competitive acquisition. A savvy competitor could file a bid protest based on:
- Overly restrictive ceiling requirement
- Proprietary data link specification
- Unrealistic delivery timeline
- Objective specs matching single vendor exactly

**Key teaching point:**
Even unintentional bias can derail acquisitions. Red Team analysis before release catches issues that would otherwise surface as protests or GAO findings.
