# Cleaning-data: Changelog

In this repository I have this readme/changelog where I go over the changes I made, the original csv file prior to changing anything, and the file after I was done.
___
Data downloaded from: https://www.askamanager.org/2021/04/how-much-money-do-you-make-4.html
___

Change UTF-8 to Unicode Encoding.

  - Some people used letter accents so to display data correctly we need to change encoding.

Check and Remove Duplicate values.
   - Since data was collected by submitting forms, there might have been some technical issues prompting users to submit multiple times. To account for this use the “Remove Duplicates” Function but not include Timestamp. The likelihood that two/multiple entries have the exact same data but are from different people is very minimal so it's a small risk worth taking.

Column: Other Monetary - Comp
  - Some people left either blank or 0 to denote not receiving anything else. Since most values in this column are numerical, change all blanks to 0.

Check for “bad faith” responses.
  - Some exist but it is kind of hard to tell good responses from bad one e.g. some people entered their annual salary as values < 1000 but correctly answered all other sections. Do we take that to mean that they meant to enter their salary value in thousands/millions etc?  Ultimately it would depend on how an analyst intends to use the data so will keep them as is. 
   - Did delete the following: person wrote City-”dino”, Job title - “homie”. Person wrote annual salary - “56”, wrote “na” for all other fields.

Standardize Currency Format of Annual Salary and Other Monetary Comp.
   - Decided on “General” Format since its easier to work with for data analysis

Column: Currency - other
  - Context on Column: People were to use this column only if they could not find the currency they were paid with in the “Currency Column.” At which point they had to enter “Other” under Currency and then state the currency they were paid with in the “Currency - other” column.
  - Some people re-entered the currency they had already used under the “Currency” Column so remove the second instance in the “Currency - other” column
  - Some people entered “Other” under the “Currency” Column but under the “Currency - other” column, used one of the 10 currencies that were readily available in the Currency Column.  E.g. Wrote Other in the Currency column but typed USD in the Currency - other column So fix as was intended. 
  - Form had “AUD/NZD” as being the same currency when they are not. To fix, split into “AUD” and “NZD” and then update entries if possible. In other words, under this column people wrote their actual currency so update that in the previous column. Further from a person’s job location it is easy to infer what country they work in so update accordingly BUT only in this specific case with AUD/NZD.
   - Some users entered additional information about their salary here -> moved it into the additional context on income column
   - Some users entered N/A so just remove and leave as blank since the majority of people for whom this column did not apply left it as blank
   - Some people re-entered their salary so remove that
   - One person wrote “55” as annual salary and then wrote 55,000 under this column so removed “55,000” from this column and updated the annual salary column.
   - Since the Currency Column used currency symbols e.g. USD, EUR, CAD, etc, under this column use similar conventions. For example if a user entered Argentine Peso, update as “ARS”. Used this site as reference : https://justforex.com/education/currencies.


Fix City Values
  -	Some individuals did not want to enter their city so they entered data as random characters, gave vague answers (ex. “City” or “large city”), or wrote some variation of “Rather not say.” For all these entries I rewrote them as “Rather not say.” Reasoning for this is that for the most part these individuals did not want to reveal too much information so “Rather not say” standardizes this sentiment for future use.
  -	Changed some values where users entered redundant information e.g. “Los Angeles, CA” and also put "California" under "State" so change “Los Angeles, CA” to just "Los Angeles"


Fix Country Values
  - Decided to use the full name of countries to remove any doubt that using initials might bring. E.G. “united states”, “USA”, “U.S.,” etc become “United States of America”
  - Fix any typos e.g. “canad” becomes “Canada”
  - “Netherlands” vs “The Netherlands” went with Netherlands
   - Standardize how United Kingdom is entered will be either United Kingdom if no additional context is given or United Kingdom (Nation) e.g. United Kingdom (Ireland) if a user entered a city that could be traced to any of the Nations in the U.K.

Possible Improvements?
   - A central question is “Where do you work?” Some individuals answered this question by writing some variation that “even though they lived in Country A, they worked for a company in Country B”, or “worked remote.” However, this could be improved by creating additional columns such as “Remote?” and “Remote Location.” The reason why I didn’t do so is because some users entered their information “correctly” even though they also work remotely. So if these columns are created then we might assume we have all remote jobs when that is not the case. In short, it could lead to some issues with how we analyze data. I decided to leave as is, as ultimately it depends how a user/analyst will want to use the data. In other words, they can decide for themselves how they want to fix this problem and be conscious of how their solution (or lack thereof) may impact their analysis.
   - For the city column users would say things like “a suburb near Los Angeles.” Should we then change their answer to just “Los Angeles?” or something like “Not Specified”? In either case there is a possibility of misrepresenting a certain job market so again it should befall on the user/analyst to  decide how to fix this issue.
   - No changes were done to Job industries as the initial form had users click from a list of options. One option was “Other” and users were allowed to enter their own industry. Therefore, a possible improvement is to standardize these other industries as the form had done. Downside to this is that we/I would have to decide where a job could be placed and may not properly represent a person’s actual Job Industry.  For example, one user entered “‘Government’ - Lobbying”.  If we wanted to be strict, would we place them under the existing “Government and Public Administration” option or be lax and would we need to create a new “Lobbying” option? If we go with the latter option it might be the case that some people would have preferred that as opposed to their earlier choice - at which point we are underrepresented people in that industry. So similar to before this question should befall on the user/analyst so that they know how their fix (or lack thereof) will impact their analysis.
