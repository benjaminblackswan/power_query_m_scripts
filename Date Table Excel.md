```
let
    Source = Excel.Workbook(File.Contents("C:\Users\benja\OneDrive\Onedrive\Productivity\Master Date Table.xlsx"), null, true),
    #"Date Table Text_Sheet" = Source{[Item="Date Table Text",Kind="Sheet"]}[Data],
    #"Promoted Headers" = Table.PromoteHeaders(#"Date Table Text_Sheet", [PromoteAllScalars=true]),
    #"Filtered Rows" = Table.SelectRows(#"Promoted Headers", each [Date] >= #date(2020, 1, 1) and [Date] <= #date(2030, 1, 1)),
    #"Changed Type" = Table.TransformColumnTypes(#"Filtered Rows",{{"Date", type date}, {"Excel Date Number", type text}, {"Calendar Year (4 dig)", type text}, {"Calendar Year (2 dig)", type text}, {"Month Number", type text}, {"Month Name Short", type text}, {"Month Name Full", type text}, {"Day of month", type text}, {"Weekday Number", type text}, {"Weekday Short", type text}, {"Weekday Long", type text}, {"Calendar Quarter", type text}, {"Week Number of the Quarter", type text}, {"Quarter ID based on month", type text}, {"ISO Week Number", type text}, {"Week Number", type text}, {"Epic Quarter", type text}, {"Epic Year 4 Digits", type text}, {"Epic Year 2 Digits", type text}, {"Number of weeks in Epic Year", type text}, {"Number of days in Epic Year", type text}, {"Fortnight Number", type text}, {"Fortnight ID", type text}, {"Epic Quarter ID", type text}, {"Week ID", type text}, {"Fiscal Year first 2 digit", type text}, {"Fiscal Year last 2 digit", type text}, {"Fiscal Year", type text}, {"Fiscal Quarter", type text}, {"Fiscal Quarter ID", type text}}),
    #"Added Week Number Text" = Table.AddColumn(#"Changed Type", "Week Number Text", each Text.Combine({"Week ", [Week Number]})),
    #"Added Week Number numeric" = Table.AddColumn(#"Added Week Number Text", "Week Number numeric", each [Week Number]),
    #"Changed Type1" = Table.TransformColumnTypes(#"Added Week Number numeric",{{"Week Number numeric", Int64.Type}, {"Week Number Text", type text}})
in
    #"Changed Type1"
```
