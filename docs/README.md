<!-- README.md is generated from README.Rmd. Please edit that file -->

## Kathmandu

Average Annual Vehicle Kilometers Travel (AAVKT):

| Vehicle Type            | AAVKT  |
| ----------------------- | ------ |
| Bus                     | 44,105 |
| Minibus                 | 43,307 |
| LDVs                    |        |
| Private (Car/Jeep/Vans) | 12,310 |
| Public (Taxi)           | 25,356 |
| Microbus                | 38,520 |
| Motorbike               | 8952   |
| HDV                     | 37,800 |
| Mini truck              | 37,415 |

Emissions
Table:

| Vehicle Type | CO2 (kg/GJ) | CO (g/km) | NOx (g/km) | HC (g/km) | PM10 (g/km) |
| ------------ | ----------- | --------- | ---------- | --------- | ----------- |
| Bus          | 79.7        | 4.9       | 6.8        | 0.87      | 1.075       |
| Minibus      | 79.7        | 4.9       | 6.8        | 0.87      | 1.075       |
| LDV          |             |           |            |           |             |
| Gasoline car | 70.54       | 3.16      | 0.21       | 0.19      | 0.06        |
| Diesel car   | 54.82       | 3.16      | 0.26       | 0.14      | 0.18        |
| Jeep/Van     | 75.66       | 3.16      | 0.28       | 0.32      | 0.48        |
| Motorbike    | 34.71       | 2.4       | 0.19       | 0.52      | 0.06        |
| HDV          | 82.61       | 4.9       | 9.3        | 0.87      | 1.24        |
| Hybrid Car   | 58.85       | 0.18      | 0.019      | 0.013     | 0.01        |

or
alternatively

|            | Travel KM | Occupancy | Total No. | % On road | Total Run   | PKM           |
| ---------- | --------- | --------- | --------- | --------- | ----------- | ------------- |
| Bus        | 44,105    | 30        | 6127      | 3,676.2   | 162,138,801 | 5,404,626.7   |
| Minibus    | 43,307    | 20        | 5,307     | 3184.2    | 137,898,149 | 4,596,604.98  |
| Private (C | 12,310    | 2         | 62,500    | 37500     | 461,625,000 | 15,387,500    |
| Public (Ta | 25,356    | 3         | 6,700     | 4020      | 101,931,120 | 3,397,704     |
| Microbus   | 38,520    | 12        | 1,500     | 900       | 34,668,000  | 1,155,600     |
| Motorbik   | 8952      | 1.5       | 475,812   | 285,487.2 | 2.556E+09   | 85,189,380.48 |
| HDV        | 37,800    | 2         | 2995      | 1,797     | 67,926,600  | 2,264,220     |
| Mini truck | 37,415    | 2         | 20,869    | 12,521.4  | 468,488,181 | 15,616,272.7  |
| Cycling    |           |           |           |           |             | 52,000,000    |
| Walking    |           |           |           |           |             | 5,200,000,000 |
|            |           |           |           |           |             | 5,385,011,909 |

The routino profiles used in `dodgr` are given for foot, horse,
wheelchair, bicycle, moped, motorcycle, motorcar, goods, hgv, psv, which
map only these categories for Kathmandu:

| Type             | routing category |
| ---------------- | ---------------- |
| Bus              | psv              |
| Mini Bus         | psv              |
| Truck/Mini truck | goods or hgv     |
| car/Jeep/van     | motorcar         |
| Pickup           | otorcar          |
| Micro Bus        | motorcar         |
| Motorcycle       | motorcycle       |

The routino profiles for these are all identical, so only one routing
layer need be generated for all of these. The following converts these
to annual
emissions:

``` r
nms <- c ("bus", "minibus", "car", "taxi", "microbus", "motorbike", "hgv",
          "truck")
aavkt <- c (44105, 43307, 12310, 25356, 38520, 8952, 37800, 37415)
pm10 <- c (1.075, 1.075, 0.12, 0.12, 0.48, 0.06, 1.24, 1.1)
nvehicles <- c (6127, 5307, 62500, 6700, 1500, 475812, 2995, 20869)
daily_emissions <- aavkt * pm10 * nvehicles / (1000 * 365)
names (daily_emissions) <- nms
message ("Kathmandu aggregate daily PM10 emissions = ",
         format (round (sum (daily_emissions)), big.mark = ","), " kg")
#> Kathmandu aggregate daily PM10 emissions = 5,295 kg
```

This daily figure can then simply be distributed across the network
according to estimated flow densities.

## Accra

Estimated Vehicle Population in all of Ghana:

| vehicle   | population |
| --------- | ---------- |
| motorbike | 203756     |
| car       | 677292     |
| bus       | 145144     |
| truck     | 75175      |
| hgv       | 21993      |

Populations of Accra and Ghana are 2.27 and 28.3 Million, reducing these
figures to 16344, 54327, 11642, 6030, and 1764. Using the above AAVKT
figures for Kathmandu, this would give

``` r
nms <- c ("motorbike", "car", "bus", "truck", "hgv")
aavkt <- c (8952, 12310, 44105, 37415, 37800)
pm10 <- c (0.06, 0.12, 1.075, 1.1, 1.24)
nvehicles <- c (16344, 54327, 11642, 6030, 1764)
daily_emissions <- aavkt * pm10 * nvehicles / (1000 * 365)
names (daily_emissions) <- nms
message ("Accra aggregate daily PM10 emissions = ",
         format (round (sum (daily_emissions)), big.mark = ","), " kg")
#> Accra aggregate daily PM10 emissions = 2,663 kg
```

This figure can’t be assumed as reliable as the above Kathmandu figure,
because there is no information on average annual vehicle kilometres
travelled.
