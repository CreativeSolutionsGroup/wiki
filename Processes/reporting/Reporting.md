# Reporting

How to create a report using Tableau and Smart Events:

## Requirements

You must have access to the CSG email; thus, this task will likely be delegated to the executives.

## The Work Before the Work (The Real Step 1)

Export the data from Smart Events into the data source for Tableau.

1. On SE Admin Dashboard, scroll to the bottom and select the event you would like to generate a report for
2. Select `Get Report for Event`
3. Go to [this](https://docs.google.com/spreadsheets/d/1MnvnQCP7nCRaFSH5nir4aUzg6aATRVDshBpvh7jMpH8/edit#gid=1167158175) Google Sheet
3. Paste this data into a *separate*, blank Google Sheet and make the following columns:
- Timestamp (mm/dd/yyyy)
- Event (Name, basic string)
- ID (7 digit)
- Year (yyyy)
- Term (yyyyFA/SP - eg. 2023FA)

## How To

1. Go [here](https://sso.online.tableau.com/public/idp/SSO) and login with `creativesolutions@cedarville.edu`
- This should bring you to the SSO page for tableau
2. Go [here](https://prod-useast-a.online.tableau.com/#/site/cedarvilleuniversity/workbooks/1094976/views) after you have logged in
3. Select the event that you want to export
4. Select the top right button to download a PDF
5. Select the prompt `Specific sheets from this workbook`
6. Select `Select All`
7. Click `Download`

## The Sheets

The sheets are what is needed to export out of the current type of reports. We have a script in the `utils` repository that does the whole exporting for you. You *do* need the `creativesolutions@cedarville.edu` password, however.

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
    - Total Attendance
    - Relative Attendance
- Major
    - Highest
    - Lowest
- Gender
- Class

## The Script

To use the script, run the following:

1. Run `pip install argparse selenium`
2. Go [here](https://selenium-python.readthedocs.io/installation.html#drivers) and install the Chromium driver
- **This is not the same as having Chromium downloaded**
3. Run the script by typing `python3 ./generate-report.py -m` for monthly **OR** semester reports, and then `python3 ./generate-report.py -e` for specific event reports

Realize that whenever you get to the page, you will need to filter. Once you apply your filters, press enter in the terminal as it prompts you.

Here are the filters for each type of report:

### Monthly

Select the semester that covers the month. Then, in the month field, select *only* that month. We are unable to handle the special case of a month covering multiple semesters.

### Semester

Select the semester, and select all months for that semester. Usually this involves merely clicking the `all` button.

### Event

At the bottom, change it from `All` to `None`.

Then, select the specific event from the filter below that.

### The Rest

All done! Just make sure to press enter in the terminal when it prompts you after you finish your filters.

It should now automatically export and filter down the PDF for you.
