# Uber Ride Analytics Dashboard

An interactive, 6-page **Power BI** dashboard that turns 150,000 Uber ride bookings (January to December 2025) into clear KPIs and visual insights on revenue, vehicles, riders and locations.

![Overview](<Dashboard screenshot/Overview.png>) |

---

## Business Problem

Uber ride-booking data sat in a flat Excel file, which made it hard to track revenue, cancellations, rider behaviour and location demand in one place. The goal was to build an interactive dashboard so a business user can answer these questions with a few clicks and no queries.

## Dataset

| Item | Detail |
|---|---|
| Source | Uber ride booking dataset (Excel) |
| Period | January to December 2025 |
| Bookings | 150,000 |
| Customers | about 104,000 |
| Vehicle types | 7 (Auto, Bike, eBike, Go Mini, Go Sedan, Premier Sedan, Uber XL) |
| Locations | 176 pickup and drop areas |
| Statuses | Completed, Cancelled by Driver, Cancelled by Customer, No Driver Found, Incomplete |

## Key Metrics

| Metric | Value |
|---|---|
| Total bookings | 150K |
| Completed bookings | 93K |
| Cancelled or lost bookings | 57K |
| Total revenue | 51.85M |
| Total distance | 2.51M km |
| Average distance per ride | 24.64 km |
| Revenue per km | 20.63 |
| Average customer rating | 4.40 |

## Dashboard Pages

| Page | What it shows |
|---|---|
| **Home** | Headline KPIs and quick navigation to every page |
| **Overview** | KPI cards with month-over-month change, monthly bookings and revenue trends, revenue by vehicle type, top pickup and drop locations |
| **Vehicle** | Vehicle performance table with contribution %, monthly bookings by vehicle type, revenue share, and top vehicles by revenue with images |
| **Revenue** | Revenue by customer, vehicle and payment method, plus monthly and quarterly revenue |
| **Rider** | Rider segments (First Time, Return, Regular), rating distribution, customer cancellation reasons, rider trend |
| **Location** | Distance analysis, top pickup and drop areas, and a heatmap of busy time slots by day |

## Key Insights

- **Evening demand peaks.** Rides are highest between 6 PM and 9 PM on every day of the week, and lowest overnight.
- **Auto leads revenue.** Auto is the top vehicle type at about 12.88M, ahead of Go Mini and Go Sedan.
- **Most riders are new.** About 79% of customers are First Time riders, and only about 15% are Regular riders.
- **Ratings are high.** Ratings range from 3.0 to 5.0, and half of all rated rides score 4.5 or above.
- **Cancellation reasons are evenly spread.** Wrong address, change of plans, and drivers not moving toward the pickup point each account for roughly a fifth of the 10,500 customer cancellations.

## Data Model

A star-style model with one fact table and supporting lookups:

- **Bookings** (fact table)
- **Calendar** (date table, marked as the date table)
- **Veh_IMG** (vehicle type to image lookup)
- **Status icons** (booking status lookup)

Relationships are one-to-many, with single-direction filtering from each lookup to Bookings.

## DAX Highlights

```DAX
Total Rides = COUNTROWS(Bookings)

Completed Bookings =
CALCULATE([Total Rides], Bookings[Booking Status] = "Completed")

Revenue per Km = DIVIDE([Revenue], [Total Distance])

Contribution % =
DIVIDE([Revenue], CALCULATE([Revenue], ALL(Bookings[Vehicle Type])))

Revenue MoM % =
VAR ThisMonth = CALCULATE([Revenue], 'Calendar'[Month No] = 12)
VAR LastMonth = CALCULATE([Revenue], 'Calendar'[Month No] = 11)
RETURN DIVIDE(ThisMonth - LastMonth, LastMonth)
```

Other calculated columns include **Time Slot** (3-hour blocks), **Rider Type** (First Time, Return, Regular) and **Rating Band**.

## Features

- Custom Uber-style theme and 1920 x 1080 layout
- Sidebar page navigation with custom icons
- Month-over-month KPI deltas with dynamic green and red arrows
- Heatmaps with conditional formatting (time slot by day of week)
- Image-based ranking table with data bars
- Synced slicers (date, vehicle type, booking status)
- Bookmark-based filter show and hide toggle

## Tools Used

- Power BI Desktop
- DAX
- Power Query
- Microsoft Excel

## Project Structure

```
uber-ride-analytics-powerbi/
├── Uber_Ride_Analytics.pbix
├── data/
│   └── uber.xlsx
├── screenshots/
│   ├── home.png
│   ├── overview.png
│   ├── vehicle.png
│   ├── revenue.png
│   ├── rider.png
│   └── location.png
├── assets/
│   ├── Uber_Theme_1920x1080.json
│   └── icons/
└── README.md
```

## How to Open

1. Download `Uber_Ride_Analytics.pbix` and install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free).
2. Open the file in Power BI Desktop.
3. If Power BI shows a data source error, go to **Home → Transform data → Data source settings**, choose **Change Source**, and point it to `data/uber.xlsx` on your computer.
4. Click **Refresh**.


## Screenshots

| Home | Overview |
|---|---|
| ![Home](<Dashboard screenshot/Home.png>) | ![Overview](<Dashboard screenshot/Overview.png>) |

| Vehicle | Revenue |
|---|---|
| ![Vehicle](<Dashboard screenshot/Vehicle.png>) | ![Revenue](<Dashboard screenshot/Revenue.png>) |

| Rider | Location |
|---|---|
| ![Rider](<Dashboard screenshot/Rider.png>) | ![Location](<Dashboard screenshot/Location.png>) |

## Author

**Md Ejaj Ansari**
Aspiring Data Analyst | Navi Mumbai

[LinkedIn](https://linkedin.com/in/md-ejajansari) | [GitHub](https://github.com/ejajansari)
