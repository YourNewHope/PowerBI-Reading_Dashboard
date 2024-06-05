let
    Source = Csv.Document(File.Contents("X:\Users\X\X\goodreads\goodreads_library_export.csv"),[Delimiter=","]),
    #"Promoted Headers" = Table.PromoteHeaders(Source, [PromoteAllScalars=true]),
    #"Changed Type" = Table.TransformColumnTypes(#"Promoted Headers",{{"Book Id", Int64.Type}, {"Title", type text}, {"Author", type text}, {"Author l-f", type text}, {"Additional Authors", type text}, {"ISBN", type text}, {"ISBN13", type text}, {"My Rating", Int64.Type}, {"Average Rating", type text}, {"Publisher", type text}, {"Binding", type text}, {"Number of Pages", Int64.Type}, {"Year Published", Int64.Type}, {"Original Publication Year", Int64.Type}, {"Date Read", type text}, {"Date Added", type date}, {"Bookshelves", type text}, {"Bookshelves with positions", type text}, {"Exclusive Shelf", type text}, {"My Review", type text}, {"Spoiler", type text}, {"Private Notes", type text}, {"Read Count", Int64.Type}, {"Owned Copies", Int64.Type}}),
    #"Added Custom" = Table.AddColumn(#"Changed Type", "Series", each if Text.Contains([Title],"Star Wars", Comparer.OrdinalIgnoreCase) then "Star Wars" else 
(if Text.Contains([Title],"Inkwizytor", Comparer.OrdinalIgnoreCase) then "Cykl Inkwizytorski" else "Other"))
in
    #"Added Custom"
