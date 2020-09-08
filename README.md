# COVID-CRUISES
Methodology for the Miami Herald project COVID-CRUISES

GET THE MOST UPDATED DATA HERE: https://docs.google.com/spreadsheets/d/1KTJj94nWd88Gml98AbTZKYZejbEJ8q4Xa7oE6g5r9ec/edit?usp=sharing

Have questions or concerns about data or methodology? Please contact: 
Sarah Blaskey, sblaskey@miamiherald.com 
Nicholas Nehamas, nnehamas@miamiherald.com 
Taylor Dolven, tdolven@miamiherald.com

Basic Methodology
The Miami Herald tracked the total number of COVID-19 cases associated with cruises. 

Our analysis of hundreds of sources provides the most conservative tally of the number of people who have reportedly tested positive for COVID-19 within 14 days of being on a cruise. It is, of course, possible that some people who tested positive within 14 days contracted the virus after departing the ship. It is also possible that many more passengers and crew have contracted the disease but were either not tested, asymptomatic or didn’t report the results. 

COVID-19 tests were not available on cruise ships until after the industry halted all new cruises on March 13.

The Herald is tracking cases connected to ocean-going cruises and is not including information from river cruises or other ocean-going vessels.

These data do not reflect total cases, but rather total cases confirmed by Herald reporters as of the date updated.  

COVIDCRUISES_MIAMI_HERALD_DATA reflects a cleaned version of the data collected by Herald reporters. The Miami Herald data will be updated weekly. NOTE: The Herald switched to monthly updates in August 2020. 

The first tab provides a breakdown of cases by individual voyage and includes company and ship names, date/country of embarkation, and COVID-19 totals (Total Known Cases, Total Known Passenger Cases, Total Known Crew Cases, Total Known Deaths, Total Known Passenger Deaths, Total Known Crew Deaths).

The second tab provides a breakdown of cases by ship and includes company and ship names and COVID-19 totals (Total Known Cases, Total Known Passenger Cases, Total Known Crew Cases, Total Known Deaths, Total Known Passenger Deaths, Total Known Crew Deaths).

The third tab provides a breakdown of cases by company and includes company name and COVID-19 totals (Total Known Cases, Total Known Passenger Cases, Total Known Crew Cases, Total Known Deaths, Total Known Passenger Deaths, Total Known Crew Deaths).

The fourth tab provides a breakdown of Total Known Cases, Total Known Passenger Cases, Total Known Crew Cases, Total Known Deaths, Total Known Passenger Deaths, Total Known Crew Deaths.

Note: Total Known Cases is often more than the sum of the known passenger and crew cases because it is sometimes not indicated in the source whether a person who tested positive for COVID-19 was a passenger or a crew member. The difference between Total Cases and the sum of Passenger Cases and Crew Cases represents the unspecified cases that could not be differentiated based on our current information.

A source list is provided as the final tab. Often, there is more than one source per voyage. Sources are shown by Company_Ship_EmbarkationDate. 

Sources
The analysis uses data from a number of sources, including the U.S. Centers for Disease Control and Prevention, foreign governments, news reports, cruise companies, and information provided by passengers and crew. 

The CDC is tracking cruise voyages linked to COVID-19 cases. The CDC data shows the name of the cruise ship, date of embarkation, date of disembarkation, and whether the cruiser showed symptoms on board the ship or after leaving the cruise. It does not provide a total number of positive test results. Where no other data was available, reporters marked a single case on that voyage to provide the most conservative estimate.

Some foreign governments are tracking the number of cases linked to cruises. The Australian government and the Trinidad & Tobago health ministry include cruise ship cases in their daily COVID-19 advisories.

The Herald is monitoring news reports using daily Google Alerts with search terms “cruise, death, covid” and “cruise, test, positive, covid.” 

Some cruise passengers shared their test results with the Herald. 

Crew members shared announcements from their ships about the number of people on board who have tested positive. 

Herald reporters only include cases where positive tests came within 14 days of disembarkation.

Reporters used information from crew members and Crew Center itineraries to verify embarkation dates if the sources didn’t include them.
Raw data
Herald reporters hand entered data from information taken from the sources above. At least two reporters checked each entry for quality assurance. 

EMBARKATION DATE: Reporters included embarkation dates only for cruises that had passengers on them. Embarkation dates from unique passenger voyages that we could not confirm are listed as “UNKNOWN.” 

Cases of crew members reported more than 14 days after all passengers had disembarked from the ship were listed as “AT_SEA”

VOYAGE_ID: An ID is generated for unique voyages by combining ship name with the date of embarkation. 

INCIDENT_ID: A reporter-designated Incident ID was added to the raw data to delineate unique cases. This ID reflects reporters’ judgment on entry. If reporters could not be sure that cases reported by one source were distinct from those reported by other sources, reporters marked the entries with the same incident ID so as to prevent an over count.
How we calculated totals
This analysis was done in R. (Email sblaskey@maimiherald.com for a copy of the script.)

The analysis is done on three levels: by voyage, by ship and by company.*  

STEP ONE:
The algorithm groups by INCIDENT_ID and determines the highest number of cases reported in the following categories. (Total Cases, Total Passenger Cases, Total Crew Cases, Total Deaths, Total Passenger Deaths, Total Crew Deaths)

STEP TWO:
Using the output of step one, it groups by the unique ID for each level (Voyage_ID, Ship or Company) and sums together all of the cases by category. (Total Cases, Total Passenger Cases, Total Crew Cases, Total Deaths, Total Passenger Deaths, Total Crew Deaths)

STEP THREE:
Using the output of Step Two, the following steps are taken in order. 
If total deaths is less than the sum of crew deaths and passenger deaths then total deaths is replaced by the sum of crew deaths and passenger deaths.
If total cases does not equal 0 AND number of crew deaths is greater than the number of crew cases, then the number of crew cases is replaced with the number of crew deaths. 
If total cases does not equal 0 AND number of passenger deaths is greater than the number of passenger cases, then the number of passenger cases is replaced with the number of passenger deaths. 
If total cases is less than the sum of crew cases and passenger cases, then total cases is replaced with the sum of crew cases and passenger cases.

*For Ship and Company level data, after step two and before step three, totals from the outputs of previous level of data are compared to the outputs from the next level and the highest number of cases in each category are output and processed in step three. 
Other considerations

We used March 2, 2020 as the embarkation date for the Celebrity Eclipse voyage because the CDC cited that date. 
For cases cited using data from the state government of Western Australia, we used the date of embarkation of the most recent voyage for that ship.
Crew from the Ruby Princess who have tested positive since the ship offloaded all passengers on March 19 are included in the ship’s final voyage counts because the government links them to the ship but does not differentiate how many crew tested positive each day.

