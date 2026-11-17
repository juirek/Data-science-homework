Data for lab03 (Data Cleaning), WS 26/27
========================================

Both files are SYNTHETIC. They were generated for this course (no portal export and no
official statistics were used), so that the lab can contain exactly the data-quality problems
the lecture discusses. Column names, the city and the district names are realistic (Hannover
rents in EUR), the values are not real market data. The planted problems stay in place on
purpose: empty fields, amounts written as text ("82,5 m²", "1.250,50 €", "447.56"), sentinel
values instead of missing values (999, -1), three different date formats in one column, one
district written in up to three spellings, and listings that appear twice with the address typed
slightly differently.

rents_export.csv: 58 rows, one row per flat listing
--------------------------------------------------
  listing_id       int      running number of the export, not unique per flat
  address          text     "number street", house number first
  district         text     district name as entered in the export, NOT standardized
  zip_code         int      five digits; a flat does not change its zip code (blocking key)
  city             text     Hannover, Laatzen, Garbsen; capitalization varies
  living_area      text/num living space in m2; unit suffix "m²" and decimal comma appear in
                            some rows
  cold_rent_eur    text/num monthly cold rent in EUR; "€" and German notation appear in some
                            rows. A thousands dot always comes with a decimal comma
                            ("1.179,00 €"), so a dot without a comma is a decimal point
  lease_date       text     lease start; three formats mixed: dd.mm.yyyy, d.m.yyyy, yyyy-mm-dd

district_rents.csv: 10 rows, one row per Hannover district
----------------------------------------------------------
  district         text     official spelling, umlauts included (Südstadt, Döhren, ...)
  avg_rent_per_m2  float    average rent in EUR per m2; invented, but the rents in
                            rents_export.csv are modelled on these values
  source_year      int      the year the index refers to (all rows: 2024)

Generated with a fixed seed by a script that is not part of the repository; rerunning the lab
always yields the same numbers, so the expected values in the test cells stay valid.
After generation, three rents were edited by hand ("1.179 €" -> "1.179,00 €", likewise
1.343 and 1.187): a thousands dot without a decimal comma could not be told apart from a
decimal point.
