```
/*
Version 1.0: This is importing all data from Master Date Table.xlsx. And change them to the correct format.
*/

let
    Source = Excel.Workbook(File.Contents("C:\Users\benja\OneDrive\Onedrive\Productivity\Master Date Table.xlsx"), null, true),
    #"Date Table Text_Sheet" = Source{[Item="Date Table Text",Kind="Sheet"]}[Data],
    #"Promoted Headers" = Table.PromoteHeaders(#"Date Table Text_Sheet", [PromoteAllScalars=true]),
    #"Filtered Rows" = Table.SelectRows(#"Promoted Headers", each [Date] >= #date(2020, 1, 1) and [Date] <= #date(2030, 1, 1)),
    #"Changed Week Number to Text" = Table.TransformColumnTypes(#"Filtered Rows",{{"Week Number", type text}}),
    #"Added Week Number Text" = Table.AddColumn(#"Changed Week Number to Text", "Week Number Text", each Text.Combine({"Week ", [Week Number]})),
    #"Reordered Columns" = Table.ReorderColumns(#"Added Week Number Text",{"Date", "Excel Date Number", "Calendar Year (4 dig)", "Calendar Year (2 dig)", "Month Number", "Month Name Short", "Month Name Full", "Day of month", "Weekday Number", "Weekday Short", "Weekday Long", "Calendar Quarter", "Week Number of the Quarter", "Quarter ID based on month", "ISO Week Number", "Week Number", "Week Number Text", "Epic Quarter", "Epic Year 4 Digits", "Epic Year 2 Digits", "Number of weeks in Epic Year", "Number of days in Epic Year", "Fortnight Number", "Fortnight ID", "Epic Quarter ID", "Week ID", "Fiscal Year first 2 digit", "Fiscal Year last 2 digit", "Fiscal Year", "Fiscal Quarter", "Fiscal Quarter ID"}),
    #"Changed Type" = Table.TransformColumnTypes(#"Reordered Columns",{{"Week Number Text", type text}, {"Date", type date}, {"Excel Date Number", Int64.Type}, {"Calendar Year (4 dig)", Int64.Type}, {"Calendar Year (2 dig)", Int64.Type}, {"Month Number", Int64.Type}, {"Day of month", Int64.Type}, {"Weekday Number", Int64.Type}, {"Month Name Short", type text}, {"Month Name Full", type text}, {"Weekday Short", type text}, {"Weekday Long", type text}, {"Calendar Quarter", type text}, {"Quarter ID based on month", type text}, {"Week Number of the Quarter", Int64.Type}, {"ISO Week Number", Int64.Type}, {"Week Number", Int64.Type}, {"Epic Quarter", type text}, {"Fortnight ID", type text}, {"Epic Quarter ID", type text}, {"Epic Year 4 Digits", Int64.Type}, {"Epic Year 2 Digits", Int64.Type}, {"Number of weeks in Epic Year", Int64.Type}, {"Number of days in Epic Year", Int64.Type}, {"Fortnight Number", Int64.Type}, {"Week ID", type text}, {"Fiscal Year", type text}, {"Fiscal Quarter", type text}, {"Fiscal Quarter ID", type text}, {"Fiscal Year first 2 digit", Int64.Type}, {"Fiscal Year last 2 digit", Int64.Type}})
in
    #"Changed Type"
```
