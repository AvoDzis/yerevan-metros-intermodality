# Yerevan metro–bus intermodality

Term project for **ENV 211 Sustainable Cities** at the American University of Armenia (fall 2022).

Yerevan has one metro line with ten stations. The project asks where people go by taxi when they leave a metro
station, and whether a bus from that station would get them to the same place. The final report recommends bus
stops closer to the metro, better route information, and dockless bikes/scooters for short trips.

## What's here

| Path | What it is |
| --- | --- |
| `code.Rmd` | R Markdown source of the final report: text, analysis and figures |
| `document.pdf` | The report knitted from `code.Rmd` (16 pages) |
| `phases/` | Earlier course deliverables: phase 1 problem definition and slides, phase 2 write-up, phase 3 report (Word) and the final presentation (`final_pres.pdf`) |

## Method

- **Taxi data:** 2016 orders from GG, a Yerevan ride-hailing service. The code keeps orders that start inside a
  small box (±0.001°, roughly 100 m) around each of 9 metro stations.
- **Figures:** order counts per station, monthly counts per station, and destination density heatmaps
  (`stat_density2d` on a Google Maps basemap via `ggmap`) for Republic Square, Yeritasardakan and Barekamutyun.
- **Bus tables:** for 4 stations, the walk to the nearest useful bus stop, the bus and minibus lines, and the ride time to
  6–7 districts. Collected by hand from route information and field visits in late 2022.

The analysis is descriptive: counts and density maps. There is no statistical model.

## Data is not included

The input file `gg.rda` (about 2.7 million 2016 GG orders with rider and driver IDs, exact pickup/drop-off
coordinates and timestamps) is not in this repository. It is personal location data and not mine to publish, so
`code.Rmd` does not run as it stands. `document.pdf` shows the output.

## Running it with your own data

1. R with `tidyverse`, `ggmap`, `RColorBrewer` and `rstudioapi`; LaTeX for PDF output.
2. Save a data frame named `gg` to `gg.rda`. It needs the columns `originLng`, `originLat`, `destLng`, `destLat`
   and `completed_at` (POSIXct).
3. Copy `.Renviron.example` to `.Renviron` and add a Google Maps Platform key with the Maps Static API enabled.
4. Knit `code.Rmd` (`rmarkdown::render("code.Rmd", "pdf_document")`).

## Limits

- One year (2016) from one taxi company, and only trips that start next to a station.
- Bus routes and travel times are from 2022 and have changed since.
- Heatmaps cover 3 of the 9 stations.
