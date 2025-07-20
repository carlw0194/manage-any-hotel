# Calculated Columns

```DAX
Booking Date = 
DATE (
    hotel_booking[arrival_date_year],
    SWITCH (
        TRUE(),
        hotel_booking[arrival_date_month] = "January", 1,
        hotel_booking[arrival_date_month] = "February", 2,
        hotel_booking[arrival_date_month] = "March", 3,
        hotel_booking[arrival_date_month] = "April", 4,
        hotel_booking[arrival_date_month] = "May", 5,
        hotel_booking[arrival_date_month] = "June", 6,
        hotel_booking[arrival_date_month] = "July", 7,
        hotel_booking[arrival_date_month] = "August", 8,
        hotel_booking[arrival_date_month] = "September", 9,
        hotel_booking[arrival_date_month] = "October", 10,
        hotel_booking[arrival_date_month] = "November", 11,
        hotel_booking[arrival_date_month] = "December", 12,
        BLANK()
    ),
    hotel_booking[arrival_date_day_of_month]
)

Lead Time Bucket = 
SWITCH ( TRUE(),
    'hotel_booking'[lead_time] <= 30,  "0‑30 Days",
    'hotel_booking'[lead_time] <= 60,  "31‑60 Days",
    'hotel_booking'[lead_time] <= 90,  "61‑90 Days",
    'hotel_booking'[lead_time] <= 120, "91‑120 Days",
    "120+ Days"
)
Nights = 
  hotel_booking[stays_in_weekend_nights]
+ hotel_booking[stays_in_week_nights]

Weekday = 
-- Weekday label for the bar‑chart
FORMAT ( [Booking Date], "dddd" )
```