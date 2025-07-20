# M code for adding flags

This code is used to add flags to the hotel booking dataset.
Run this code in Power Query Editor Advanced Editor.

let
    Source = Csv.Document(File.Contents("C:\Users\DC\Downloads\hotel_booking.csv\hotel_booking.csv"),[Delimiter=",", Columns=36, Encoding=1252, QuoteStyle=QuoteStyle.None]),
    #"Promoted Headers" = Table.PromoteHeaders(Source, [PromoteAllScalars=true]),
    #"Changed Type" = Table.TransformColumnTypes(#"Promoted Headers",{{"hotel", type text}, {"is_canceled", Int64.Type}, {"lead_time", Int64.Type}, {"arrival_date_year", Int64.Type}, {"arrival_date_month", type text}, {"arrival_date_week_number", Int64.Type}, {"arrival_date_day_of_month", Int64.Type}, {"stays_in_weekend_nights", Int64.Type}, {"stays_in_week_nights", Int64.Type}, {"adults", Int64.Type}, {"children", Int64.Type}, {"babies", Int64.Type}, {"meal", type text}, {"country", type text}, {"market_segment", type text}, {"distribution_channel", type text}, {"is_repeated_guest", Int64.Type}, {"previous_cancellations", Int64.Type}, {"previous_bookings_not_canceled", Int64.Type}, {"reserved_room_type", type text}, {"assigned_room_type", type text}, {"booking_changes", Int64.Type}, {"deposit_type", type text}, {"agent", Int64.Type}, {"company", Int64.Type}, {"days_in_waiting_list", Int64.Type}, {"customer_type", type text}, {"adr", type number}, {"required_car_parking_spaces", Int64.Type}, {"total_of_special_requests", Int64.Type}, {"reservation_status", type text}, {"reservation_status_date", type date}, {"name", type text}, {"email", type text}, {"phone-number", type text}, {"credit_card", type text}}),
    #"Removed Other Columns" = Table.SelectColumns(#"Changed Type",{"hotel", "is_canceled", "lead_time", "arrival_date_year", "arrival_date_month", "arrival_date_day_of_month", "stays_in_weekend_nights", "stays_in_week_nights", "country", "distribution_channel", "market_segment", "reserved_room_type", "assigned_room_type", "customer_type", "adr", "reservation_status_date"}),
    #"Merged Queries" = Table.NestedJoin(#"Removed Other Columns", {"country"}, country_flags, {"Iso3"}, "country_flags", JoinKind.LeftOuter),
    #"Expanded country_flags" = Table.ExpandTableColumn(#"Merged Queries", "country_flags", {"FlagURL"}, {"country_flags.FlagURL"}),
    #"Renamed Columns" = Table.RenameColumns(#"Expanded country_flags",{{"country_flags.FlagURL", "FlagURL"}}),
    #"Unpivoted Only Selected Columns" = Table.Unpivot(#"Renamed Columns", {"reserved_room_type", "assigned_room_type"}, "Attribute", "Value"),
    #"Renamed Columns1" = Table.RenameColumns(#"Unpivoted Only Selected Columns",{{"Attribute", "Room type"}, {"Value", "room_class"}})
in
    #"Renamed Columns1"