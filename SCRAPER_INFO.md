# Fields Being Pulled By Scraper

### Application Details
- **Function name: ** `get_application()`
- **Details:** This function returns legal reasons listed in document as to why the applicant  should not be deported.
- **Returns:** This function returns one to four strings:
	1. Asylum
	2. Withholding of Removal - *The U.S. government legally cannot remove someone to a country where their freedom would be threatened. In other words, if someone's political opinion, race, nationality, or politial opinion puts them at risk, they qualify for asylum.***
	3. Protection under the United Nations Convention Against Torture (CAT): *The U.S. Government cannot deport someone who is at risk of being tortured if sent back.*
	4. Other
- **Current Status:** Currently is pulled correctly by scraper.

### Date
- **Function name: ** `get_date()`
- **Details:** Returns date of case in format M-DD-YYYY. Specified as ‘date of notice’ within page 1 of an appeal
- **Returns:** String in format 'YYYY-DD-M'
- **Current Status:** Currently is pulled correctly by scraper.

### State
- **Function name: **`get_state()`
- **Details:** Returns state where case was filed
- **Returns:** String like 'AL'
- **Current Status:** Currently is pulled correctly by scraper.

### City
- **Function name: **`get_city()`
- **Details:** Returns city where case was filed
- **Returns:** String like 'Montgomery'
- **Current Status:** Currently is pulled correctly by scraper.

### Applicant's Country of Origin
- **Function name: **`get_country_of_origin()`
- **Details:** Returns country where applicant is from
- **Returns:** String like 'Tunisia'
- **Current Status:** While SpaCy's Matcher functionality was experimented with, nothing has been produced to show whether the current implementation is better or worse.

### Panel Members
- **Function name: **`get_panel()`
- **Details:** Returns list of panel members from an appeal. Panel members are judges, but they also have seats on the board of immigration appeals so they specifically have the last say on appeal cases. At this level, sometimes you will have as many as 7 panel members hear the same appeal. On cases that are not appeals, this field will return a null value. Panel members 
- **Returns:** A list of panel members as strings -> ["Guendelsberger, John","O'Leary, Brian M.","Grant, Edward"]
- **Current Status:** Merged and current.

### Judges
- **Function name: **`get_judges()`
- **Details:** Returns judge presiding over the original decision- this is located at the bottom of an original decision, if one exists in the document. Judges are not mentioned in appeals cases so those cases will return 'Null'
- **Returns:** String like ‘Clarease Rankin Yates’
- **Current Status:** There has been ongoing discussion about how to best pull out this field and the get_pannel field. When we inherited this code, every time the function was run it was scraping data about the judges from a Wikipedia page. As of 4/27, the conclusion was that we needed to create a database or some sort of storage in the backend to hold a static list of these judges. This has not been started yet. A basic implementation can be found in [this notebook](https://github.com/Lambda-School-Labs/human-rights-first-asylum-ds-a/blob/main/notebooks/get_judge_implementation.ipynb).

### Outcomes
- **Function name: **`get_outcome()`
- **Details:** Returns outcome of case
- **Returns:** A string consisting of one or more of the following:
            'reversed',
	    'remanded',
            'dismissed',
            'sustained',
            'terminated',
            'granted',
            'denied',
            'affirmed',
- **Current Status:** Currently getting 100% accuracy on training data. Contact River Bellamy with any questions.

### Protected Grounds
- **Function name: **`get_protected_grounds()`
- **Details:** In order to qualify for asylum, applicant must show they've experienced persecution based on one of the follow five categories: race, religion, nationality, membership in a particular social group or political opinion.
- **Returns:** String
- **Current Status:** Unknown. Contact Alex Krieger

### Based Violence
- **Function name: **`get_protected_grounds()`
- **Details:** Returns type of violence the applicant experienced if they experienced violence. Looks for words like *'abduct', 'abuse', 'assassinate', 'assault', 'coerce', 'exploit', 'fear', 'harm', 'hurt', 'kidnap', 'kill', 'murder', 'persecute', 'rape', 'scare', 'shoot', 'suffer', 'threat', 'torture'* and returns them if they exist with the document
- **Returns:** String
- **Current Status:** Unknown

### Gender
- **Function name: **`get_gender()`
- **Details:** Returns gender of applicant or unknown. Uses `PhraseMatcher` with 'LEMMA' attribute activated to match to root word. Suffers accuracy when refugee is a family or more than one.
- **Returns:** String example 'Male'
- **Current Status:** Updates were made 4/30/21 Labs 33. 

### Indigenous Status

### Applicant Language

### Credibility

### If Applicant Met Filing Deadline
- **Function name: **`check_for_one_year()`
- **Details:** An applicant for asylum is required to file their request for asylum within one year of arriving in the US, unless there are extraordinary or changed circumstances that justify the delay. This method determines whether the issue of this filing deadline is discussed in the case.
- **Returns:** Bool
- **Current Status:** Currently getting 100% accuracy on the trainign data. Contact River Bellamy with any questions.
### Statutes
