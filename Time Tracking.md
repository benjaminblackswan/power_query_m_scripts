### 2025 first half

```
let
    Source = Excel.Workbook(File.Contents("C:\Users\benja\OneDrive\Onedrive\Productivity\2025\TimeTracking2025 First Half.xlsx"), null, true),
    Extracted_Sheet = Source{[Item="Extracted",Kind="Sheet"]}[Data],
    #"Promoted Headers" = Table.PromoteHeaders(Extracted_Sheet, [PromoteAllScalars=true]),
    #"Removed Top Rows" = Table.Skip(#"Promoted Headers",1)
in
    #"Removed Top Rows"
```


### 2025 second half

```
let
    Source = Excel.Workbook(File.Contents("C:\Users\benja\OneDrive\Onedrive\Productivity\2025\TimeTracking2025 Second Half.xlsx"), null, true),
    Extracted_Sheet = Source{[Item="Extracted",Kind="Sheet"]}[Data],
    #"Promoted Headers" = Table.PromoteHeaders(Extracted_Sheet, [PromoteAllScalars=true]),
    #"Removed Top Rows" = Table.Skip(#"Promoted Headers",1)
in
    #"Removed Top Rows"
```

### combine the two half
```
let
    Source = #"2025 Second Half",
    #"Appended Query" = Table.Combine({Source, #"2025 First Half"}),
    #"Sorted Rows" = Table.Sort(#"Appended Query",{{"Date", Order.Ascending}}),
    #"Changed Type" = Table.TransformColumnTypes(#"Sorted Rows",{{"Date", type date}, {"Week Number (Sunday Start)", type number}, {"Social - Romantic", type number}, {"Social - Parents and family", type number}, {"Social - Other", type number}, {"Public Transport", type number}, {"Private Transport (Car, Uber)", type number}, {"Emotional and Mental Health", type number}, {"Study", type number}, {"Reading", type number}, {"Gaming", type number}, {"Movies", type number}, {"TV shows", type number}, {"UFC", type number}, {"Entertainment - Other", type number}, {"Maintenance", type number}, {"Other Physical Health", type number}, {"Dental Health", type number}, {"Technology", type number}, {"Administrative Tasks", type number}, {"Data Management", type number}, {"Cycling", type number}, {"Running", type number}, {"Walking", type number}, {"Cleaning - General", type number}, {"Oral Hygiene and Shave", type number}, {"Shower", type number}, {"Laundry", type number}, {"Other", type number}, {"Strength Training", type number}, {"Work", type number}, {"Buying and Selling", type number}, {"Time Management", type number}, {"Personal Finance", type number}, {"Content Creation", type number}, {"Make coffee", type number}, {"Make Protein Shake", type number}, {"Toilet", type number}, {"Grocery Shopping", type number}, {"Pet", type number}, {"Sleep", type number}, {"Prepare meals or buy meals", type number}, {"Eat meal", type number}, {"Job Searching", type number}, {"Interviews", type number}, {"Unaccounted", type number}}),
    #"Removed Columns" = Table.RemoveColumns(#"Changed Type",{"CHECK", "Sheetpath", "Column"})
in
    #"Removed Columns"
```
