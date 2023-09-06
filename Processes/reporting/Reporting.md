# Reporting

This is how you create a report using Tableau and Smart Events.

## Requirements

To do this, you must have access to the CSG email. This means that it will likely be delegated to execs.

## The Work Before the Work (The Real Step 1)

Here, we need to export data from Smart Events into the data source for Tableau.

1. On SE Admin Dashboard, scroll to the bottom and select your event.
2. Select "Get Report for Event"
3. Go to [this](https://docs.google.com/spreadsheets/d/1MnvnQCP7nCRaFSH5nir4aUzg6aATRVDshBpvh7jMpH8/edit#gid=1167158175) sheet.
3. Paste this data into ANOTHER blank Google Sheet and make the following columns:
- Timestamp (mm/dd/yyyy)
- Event (Name, basic string)
- ID (7 digit)
- Year (yyyy)
- Term (yyyyFA/SP - so, for example: 2023FA)

## How To

1. Go [here](https://sso.online.tableau.com/public/idp/SSO) and begin to log in with `creativesolutions@cedarville.edu`
- This should bring you to the SSO page for tableau.
2. Go to [here](https://prod-useast-a.online.tableau.com/#/site/cedarvilleuniversity/workbooks/1094976/views) after you have logged in.
3. Select the event that you want to export.
4. Select the top right button to download a PDF.
5. Select on the prompt "Specific sheets from this workbook"
6. Select "Select All"
7. Click "Download"

## The Sheets

These are the things that we need to export out of the current type of reports. Realize that we have a script in the utilities
that does the whole exporting for you. You *do* need the `creativesolutions@cedarville.edu` password though.

### Overall Exports

- Total Attendance by x
- Overall Event Attendance
- Overall Dorm Percentage
- Overall Dorm Attendance
- Overall Major
    - Highest
    - Lowest
- Overall Gender
- Overall Class

### Event

- Dorm
    - Total attendance
    - Relative attendance
- Major
    - Highest
    - Lowest
- Gender
- Class

## The Script

To use the script, run the following:

`pip install argparse selenium`

Then, go [here](https://selenium-python.readthedocs.io/installation.html#drivers) and install the chromium driver. **This is not the same as having Chromium downloaded**

Finally, run the script by typing `python3 ./generate-report.py -m` for monthly **OR** semester reports, and then `python3 ./generate-report.py -e` for specific event reports.

Realize that whenever you get to the page, you will need to filter down things. Once you apply your filters, press enter in the terminal as it prompts you.

Here are the filters for each type of report:

### Monthly

Select the semester that covers the month. Then, in the month field, select *only* that month. If multiple semesters cover it, that's weird and we don't really handle that. Sorry.

### Semester

Select the semester, and select all months for that semester. Usually this involves just clicking the `all` button.

### Event

At the bottom, change it from `All` to `None`.

Then, select the specific event from the filter below that.

### The Rest

All done! Just make sure to press enter in the terminal when it prompts you after you finish your filters.

After this point, it should automatically export and filter down the PDF for you.
