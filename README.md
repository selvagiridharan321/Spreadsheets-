Phase 1: Prepare the Spreadsheet
Steps
Open a new Google Sheet.
In row 1, enter these headers: Employee ID, Employee Name, Email, Department, Location.
Add at least 6 rows of sample data:
Employee ID
Employee Name
Email
Department
Location
EMP-0001
Priya Nair
priya.nair@example.com
IT
Chennai
EMP-0002
Karthik Raj
karthik.raj@example.com
HR
Bengaluru
EMP-0003
Meena Sundar
meena.sundar@example.com
Finance
Chennai
EMP-0004
Arjun Das
arjun.das@example.com
IT
Hyderabad
EMP-0005
Divya Lakshmi
divya.l@example.com
HR
Chennai
EMP-0006
Suresh Babu
suresh.babu@example.com
Finance
Bengaluru
Go to File > Download > Microsoft Excel (.xlsx).
Save the file as Staff Data.xlsx.
Video narration
"First I prepare the data. This sheet has five columns: Employee ID, Employee Name, Email, Department and Location. I download it as an Excel file so ServiceNow can import it."
Result
A downloaded file named Staff Data.xlsx with 6 employee rows.
Phase 2: Create the Target Table
Navigation: All > System Definition > Tables > New
Steps
Label: Staff Directory
Name: u_staff_directory (auto-filled).
Click Submit/Save.
Open the table again and go to its form layout (form context menu > Configure > Form Layout).
Add these fields, all of type String:
Employee ID
Employee Name
Email
Department
Location
Click Save.
Check that all five fields appear on the form.
Video narration
"Next I create the table that will hold the final records. I call it Staff Directory and add five string fields that match my spreadsheet columns."
Result
A custom table, u_staff_directory, with five fields ready to receive data.
Phase 3: Load Data into an Import Set Table
Navigation: All > System Import Sets > Load Data
Steps
Import set table: Create table.
Label: Staff Import (name u_staff_import is auto-filled).
Source of the import: File.
Choose Staff Data.xlsx.
Sheet number: 1. Header row: 1.
Click Submit.
When the success message appears, click Create Transform Map.
Video narration
"The Import Set table is a staging area. The raw spreadsheet data lands here first, before it moves to the final table."
Result
The Staff Import table holds the 6 raw rows, and you are taken to create a transform map.
Phase 4: Create and Run the Transform Map
Steps
Name: Staff Spreadsheet Load.
Source table: Staff Import (auto-filled).
Target table: Staff Directory.
Click Auto Map Matching Fields.
Open Mapping Assist and check that each source field maps to the matching target field.
Click Save.
Click Transform and confirm the run finishes with a success message.
Video narration
"The Transform Map tells ServiceNow which source column goes to which target field. I use Auto Map, check it in Mapping Assist, then run the transform."
Result
The rows from Staff Import are copied into Staff Directory.
Phase 5: Verify the Imported Data
Steps
In the navigator, search for Staff Directory and open All.
Confirm all 6 rows from the spreadsheet appear as records.
Check that Employee ID, Name, Email, Department and Location are filled correctly.
Use Personalize List Columns to arrange the columns in a sensible order, then click OK.
Video narration
"Now I open the Staff Directory table to check that every row was created and that the values match my spreadsheet."
Result
Confirmed that the import and mapping worked correctly.
Phase 6: Enable Coalesce to Prevent Duplicates
Steps
Go to All > System Import Sets > Transform Maps.
Open Staff Spreadsheet Load.
In the Field Maps related list, open the Employee ID mapping.
Set Coalesce to true.
Click Save/Update.
Video narration
"In real projects the same data gets imported many times. Coalesce on Employee ID makes ServiceNow update an existing record instead of creating a duplicate."
Result
Re-importing a record with the same Employee ID updates it instead of adding a copy.
Phase 7: Test with Changed Data
Steps
Edit your spreadsheet:
Change one person's email.
Change another person's name.
Add two new employees.
Leave the other rows the same.
Download it again as .xlsx.
Go to All > System Import Sets > Load Data.
Choose the existing import table Staff Import, pick the file, sheet 1, header row 1, then click Submit.
Click Run Transform, select Staff Spreadsheet Load, and click Transform.
Open Transform History and check the counts: 2 inserted and 2 updated.
Open Staff Directory to confirm the changes.
Repeat the import with the same file. Nothing is inserted or updated this time, and the rows are ignored.
Video narration
"I upload a modified sheet. Changed rows are updated, new rows are inserted, and uploading the same file again changes nothing, which proves Coalesce works."
Result
Proof that Coalesce updates existing records and only adds new ones.
Phase 8: Create Reports
Navigation: All > Reports > View / Run > New
Report 1: Staff by Department
Table: Staff Directory.
Type: Pie chart.
Group by: Department. Aggregation: Count.
Click Run, then Save.
Report 2: Staff by Location
Table: Staff Directory.
Type: Bar chart.
Group by: Location. Aggregation: Count.
Click Run, then Save.
Report 3: Staff Master List
Table: Staff Directory.
Type: List.
Columns: Employee ID, Employee Name, Email, Department, Location.
Click Run, then Save.
Video narration
"To make the data useful, I create three reports: staff by department, staff by location, and a full staff list."
Result
Three saved reports on the Staff Directory table.
Phase 9: Build a Dashboard
Steps
In the navigator filter, type pa_dashboards.form and press Enter to open the dashboard form.
If it will not open, open the ACL record for pa_dashboards (operation: Create), turn on Admin overrides, and click Update. Then try again.
Name the dashboard Staff Insights Dashboard and save it.
Open each of the three reports in turn: Share > Add to Dashboards, select Staff Insights Dashboard, and click Add.
Open the dashboard and confirm all three reports show.
Optional: restrict who can see it by users, groups or roles.
Video narration
"Finally I bring the reports together on one dashboard, so department and location breakdowns and the staff list are visible in one place."
Result
A finished Staff Insights Dashboard with all three reports.
Closing line for the video
"That's the full flow: data prepared, imported, mapped, de-duplicated and reported. Thank you for watching."
