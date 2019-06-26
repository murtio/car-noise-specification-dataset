# Car Noise Level and Specification Dataset README

### Authors
Murtadha


### Date

18th-Apr-2019

### Website

n/a

### License

GNU General Public License (version 3)-- GPLv3


### Kaggle page

[car_noise_specification](https://www.kaggle.com/murtio/car-noise-specification)

---


### Problem Statement


The noise level of cars could be an indicator of both car’s condition and manufacturing quality. Drivers could use noise level to determine if a potential car suits their needs, or if their current car is in a healthy state. On the other hand, manufactures could use noise level to assest their cars' quality compared to the market. Luxury cars compete to have low noise level, while sports car usually neglect this factor. In this project we compile data from different sources to arrive to a dataset having cars’ manufacturing specification mapped to its noise level at different speed. The compiled dataset could be utilized in evaluating cars noise level or in analyzing which technical specification has the major effect on cars’ noise level.

For more information about automobile noise level:

- [An overview of automobile noise and vibration control](https://www.researchgate.net/publication/270775858_An_overview_of_automobile_noise_and_vibration_control)

- [Noise, vibration, and harshness From Wikipedia](https://en.wikipedia.org/wiki/Noise,_vibration,_and_harshness)

---


### Executive Summary

Initially we scrape data from https://www.auto-decibel-db.com (hereafter referred AD). This website has nearly 2000 data entries about cars' cabin noise level. Each car in the website has its cabin noise (measured in decibel) at different speed. The website doesn't provide further information about the source or the methodology of its collected data, yet it's the most comprehensive data about the subject I could found. Another source which might be used for verification can be found at https://www.edmunds.com. While edmunds.com states its methodology of collecting noise level, its dataset is embedded in PDF files and is not comprehensive compared to the former.

After scrapping the noise level of cars, we use the available information we have about each car to find its specification. In the scrapped dataset from AD there's 4 features which can be used to identify same car's specification in other datasets: brand, model, year, and spec. After looking up the Web for websites and APIs having detailed and comprehensive data about cars, we decided on http://www.carqueryapi.com API (hereafter referred CQA). Though it's not accurate for some cars, and it has different spelling from our AD, it's the most accessible data we could find. In this section we map each car in AD to its equivalence in cqa using the 3 features: brand, model, and year. We first specify the model_id in CQA and then we will use model_id to retrieve the full specification of the car. Due to the limitation imposed by caranddriver.com on the number of requests (60 requests), we used Tor bridge to alternate IP address.

Finally, we look up for the full specification of each car in CQA using its model_id. In this section we added 60 features of specification of nearly a 1000 car in AD. We refer to each feature pulled from CQA by a postfix added to its column name: '_cqa'. At the end we succeeded in getting specification of 1067 car out of 1895 in AD. We couldn’t find specification for all cars in AD due to either different naming of cars between AD and QC, or the car doesn’t exist in QC.

---

### Web scrapping sources and API


[auto-decibel-db.com](https://www.auto-decibel-db.com): This website has nearly 2000 data entries about cars' cabin noise level. Each car in the website has its cabin noise (measured in decibel) at different speed.

[carqueryapi.com](http://www.carqueryapi.com): a JSON based API for retrieving detailed car and truck information, including year, make, model, trim, and specifications. It has 73419 vichle in its database.

---

### Data Dictionary


| Feature                            | Type    | Dataset | Description                                      |
|------------------------------------|---------|---------|--------------------------------------------------|
| 'brand'                            |  object | ad      | manufacture of the car                           |
|  'model'                           |  object | ad      | model of the car                                 |
|  'spec'                            |  object | ad      | the size engine or the car trim                  |
|  'year'                            |  object | ad      | year of releasing                                |
|  'dB_at_idle'                      |  object | ad      | noise level when car is idle measured in decibel |
|  'dB_at_50kmh'                     |  object | ad      | noise level at speed 50kmh measured in decibel   |
|  'dB_at_80kmh'                     |  object | ad      | noise level at speed 80kmh measured in decibel   |
|  'dB_at_100kmh'                    |  object | ad      | noise level at speed 100kmh measured in decibel  |
|  'dB_at_120kmh'                    |  object | ad      | noise level at speed 120kmh measured in decibel  |
|  'dB_at_140kmh'                    |  object | ad      | noise level at speed 140kmh measured in decibel  |
|  'model_id'                        |  object | cqa     | car id as in cqa database using the first query  |
|  'model_id_cqa'                    |  object | cqa     | car id as in cqa database using the second query |
|  'model_make_id_cqa'               |  object | cqa     | car technical specification pulled from cqa      |
|  'model_name_cqa'                  |  object | cqa     | car technical specification pulled from cqa      |
|  'model_trim_cqa'                  |  object | cqa     | car technical specification pulled from cqa      |
|  'model_year_cqa'                  |  object | cqa     | car technical specification pulled from cqa      |
|  'model_body_cqa'                  |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_position_cqa'       |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_cc_cqa'             |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_cyl_cqa'            |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_type_cqa'           |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_valves_per_cyl_cqa' |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_power_ps_cqa'       |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_power_rpm_cqa'      |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_torque_nm_cqa'      |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_torque_rpm_cqa'     |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_bore_mm_cqa'        |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_stroke_mm_cqa'      |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_compression_cqa'    |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_fuel_cqa'           |  object | cqa     | car technical specification pulled from cqa      |
|  'model_top_speed_kph_cqa'         | float64 | cqa     | car technical specification pulled from cqa      |
|  'model_0_to_100_kph_cqa'          | float64 | cqa     | car technical specification pulled from cqa      |
|  'model_drive_cqa'                 |  object | cqa     | car technical specification pulled from cqa      |
|  'model_transmission_type_cqa'     |  object | cqa     | car technical specification pulled from cqa      |
|  'model_seats_cqa'                 |  object | cqa     | car technical specification pulled from cqa      |
|  'model_doors_cqa'                 |  object | cqa     | car technical specification pulled from cqa      |
|  'model_weight_kg_cqa'             |  object | cqa     | car technical specification pulled from cqa      |
|  'model_length_mm_cqa'             |  object | cqa     | car technical specification pulled from cqa      |
|  'model_width_mm_cqa'              |  object | cqa     | car technical specification pulled from cqa      |
|  'model_height_mm_cqa'             |  object | cqa     | car technical specification pulled from cqa      |
|  'model_wheelbase_mm_cqa'          |  object | cqa     | car technical specification pulled from cqa      |
|  'model_lkm_hwy_cqa'               |  object | cqa     | car technical specification pulled from cqa      |
|  'model_lkm_mixed_cqa'             | float64 | cqa     | car technical specification pulled from cqa      |
|  'model_lkm_city_cqa'              |  object | cqa     | car technical specification pulled from cqa      |
|  'model_fuel_cap_l_cqa'            |  object | cqa     | car technical specification pulled from cqa      |
|  'model_sold_in_us_cqa'            |  object | cqa     | car technical specification pulled from cqa      |
|  'model_co2_cqa'                   | float64 | cqa     | car technical specification pulled from cqa      |
|  'model_make_display_cqa'          |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_l_cqa'              |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_ci_cqa'             |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_bore_in_cqa'        |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_stroke_in_cqa'      |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_valves_cqa'         |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_power_hp_cqa'       |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_power_kw_cqa'       |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_torque_lbft_cqa'    |  object | cqa     | car technical specification pulled from cqa      |
|  'model_engine_torque_kgm_cqa'     |  object | cqa     | car technical specification pulled from cqa      |
|  'model_top_speed_mph_cqa'         | float64 | cqa     | car technical specification pulled from cqa      |
|  'model_weight_lbs_cqa'            |  object | cqa     | car technical specification pulled from cqa      |
|  'model_length_in_cqa'             |  object | cqa     | car technical specification pulled from cqa      |
|  'model_width_in_cqa'              |  object | cqa     | car technical specification pulled from cqa      |
|  'model_height_in_cqa'             |  object | cqa     | car technical specification pulled from cqa      |
|  'model_wheelbase_in_cqa'          |  object | cqa     | car technical specification pulled from cqa      |
|  'model_mpg_hwy_cqa'               |  object | cqa     | car technical specification pulled from cqa      |
|  'model_mpg_city_cqa'              |  object | cqa     | car technical specification pulled from cqa      |
|  'model_mpg_mixed_cqa'             | float64 | cqa     | car technical specification pulled from cqa      |
|  'model_fuel_cap_g_cqa'            |  object | cqa     | car technical specification pulled from cqa      |
|  'make_display_cqa'                |  object | cqa     | car technical specification pulled from cqa      |
|  'make_country_cqa'                |  object | cqa     | car technical specification pulled from cqa      |
|  'ExtColors_cqa'                   | float64 | cqa     | car technical specification pulled from cqa      |
|  'IntColors_cqa'                   | float64 |         | car technical specification pulled from cqa      |
---
