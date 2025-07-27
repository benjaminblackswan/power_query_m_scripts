### 2025 first half

```
let
    Source = Excel.Workbook(File.Contents("C:\Users\benja\OneDrive\Onedrive\Productivity\2025\TimeTracking2025 First Half.xlsx"), null, true),
    Extracted_Sheet = Source{[Item="Extracted",Kind="Sheet"]}[Data],
    #"Promoted Headers" = Table.PromoteHeaders(Extracted_Sheet, [PromoteAllScalars=true]),
    #"Removed Top Rows" = Table.Skip(#"Promoted Headers",1),
    #"Removed Columns" = Table.SelectColumns(#"Removed Top Rows",{"Date", "Week Number (Sunday Start)", "Cycling", "Running", "Walking", "Strength Training", "Make Protein Shake"}),
    #"Changed Type" = Table.TransformColumnTypes(#"Removed Columns",{{"Date", type date}, {"Week Number (Sunday Start)", type number}, {"Cycling", type number}, {"Running", type number}, {"Walking", type number}, {"Strength Training", type number}})
in
    #"Changed Type"
```


### 2025 second half

```
let
    Source = Excel.Workbook(File.Contents("C:\Users\benja\OneDrive\Onedrive\Productivity\2025\TimeTracking2025 Second Half.xlsx"), null, true),
    Extracted_Sheet = Source{[Item="Extracted",Kind="Sheet"]}[Data],
    #"Promoted Headers" = Table.PromoteHeaders(Extracted_Sheet, [PromoteAllScalars=true]),
    #"Removed Top Rows" = Table.Skip(#"Promoted Headers",1),
    #"Removed Other Columns" = Table.SelectColumns(#"Removed Top Rows",{"Date", "Week Number (Sunday Start)", "Cycling", "Running", "Walking", "Strength Training", "Make Protein Shake"}),
    #"Changed Type" = Table.TransformColumnTypes(#"Removed Other Columns",{{"Date", type date}, {"Week Number (Sunday Start)", type number}, {"Cycling", type number}, {"Running", type number}, {"Walking", type number}, {"Strength Training", type number}})
in
    #"Changed Type"
```

### combine the two half
```
let
    Source = #"2025 Second Half",
    #"Appended Query" = Table.Combine({Source, #"2025 First Half"}),
    #"Sorted Rows" = Table.Sort(#"Appended Query",{{"Date", Order.Ascending}}),
    #"Changed Type" = Table.TransformColumnTypes(#"Sorted Rows",{{"Make Protein Shake", type number}})
in
    #"Changed Type"
```
