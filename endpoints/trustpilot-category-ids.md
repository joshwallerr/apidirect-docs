# Trustpilot Category IDs

Category slugs for the `category_id` parameter on [Category Companies](/docs/trustpilot-category-companies), [Category Newest](/docs/trustpilot-category-newest) and [Category Details](/docs/trustpilot-category). Trustpilot's taxonomy has three levels; this page lists the 22 top-level categories and their 189 subcategories, with the number of businesses in each. Deeper (third-level) slugs also work — find them with [Category Search](/docs/trustpilot-categories) or read a subcategory's own `subcategories` via [Category Details](/docs/trustpilot-category). A category ID is also the last segment of any `trustpilot.com/categories/<slug>` URL, and the endpoints accept that URL directly.

## Using a category ID

### Example: companies in Bank

```bash
curl "https://apidirect.io/v1/trustpilot/category/companies?category_id=bank" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Example: subcategories of Electronics & Technology

```bash
curl "https://apidirect.io/v1/trustpilot/category?category_id=electronics_technology" \
  -H "X-API-Key: YOUR_API_KEY"
```

## Top-level categories

| Category | ID | Businesses |
|----------|-----|-----------:|
| Animals & Pets | `animals_pets` | 4,695 |
| Beauty & Well-being | `beauty_wellbeing` | 22,160 |
| Business Services | `business_services` | 71,242 |
| Construction & Manufacturing | `construction_manufactoring` | 17,756 |
| Education & Training | `education_training` | 14,855 |
| Electronics & Technology | `electronics_technology` | 59,806 |
| Events & Entertainment | `events_entertainment` | 24,458 |
| Food, Beverages & Tobacco | `food_beverages_tobacco` | 11,665 |
| Health & Medical | `health_medical` | 19,408 |
| Hobbies & Crafts | `hobbies_crafts` | 8,949 |
| Home & Garden | `home_garden` | 24,046 |
| Home Services | `home_services` | 16,092 |
| Legal Services & Government | `legal_services_government` | 5,880 |
| Media & Publishing | `media_publishing` | 18,187 |
| Money & Insurance | `money_insurance` | 42,297 |
| Public & Local Services | `public_local_services` | 6,262 |
| Restaurants & Bars | `restaurants_bars` | 2,545 |
| Shopping & Fashion | `shopping_fashion` | 44,724 |
| Sports | `sports` | 7,173 |
| Travel & Vacation | `travel_vacation` | 12,727 |
| Utilities | `utilities` | 1,365 |
| Vehicles & Transportation | `vehicles_transportation` | 18,166 |

## Subcategories

### Animals & Pets (`animals_pets`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Animal Health | `animal_health` | 353 |
| Animal Parks & Zoo | `animal_parks_zoo` | 56 |
| Cats & Dogs | `cats_dogs` | 528 |
| Horses & Riding | `horses_riding` | 234 |
| Pet Services | `pet_services` | 645 |
| Pet Stores | `pet_stores` | 3,429 |

### Beauty & Well-being (`beauty_wellbeing`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Cosmetics & Makeup | `cosmetics_makeup` | 6,246 |
| Hair Care & Styling | `hair_care_styling` | 2,120 |
| Personal Care | `personal_care` | 9,214 |
| Salons & Clinics | `salons_clinics` | 5,845 |
| Tattoos & Piercings | `tattoos_piercings` | 175 |
| Wellness & Spa | `wellness_spa` | 2,494 |
| Yoga & Meditation | `yoga_meditation` | 465 |

### Business Services (`business_services`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Administration & Services | `administration_services` | 11,467 |
| Associations & Centers | `associations_centers` | 303 |
| HR & Recruiting | `hr_recruiting` | 4,635 |
| Import & Export | `import_export` | 343 |
| IT & Communication | `it_communication` | 25,324 |
| Office Space & Supplies | `office_space_supplies` | 2,096 |
| Print & Graphic Design | `print_graphic_design` | 5,276 |
| Research & Development | `research_development` | 3,170 |
| Sales & Marketing | `sales_marketing` | 26,641 |
| Shipping & Logistics | `shipping_logistics` | 4,212 |
| Wholesale | `wholesale` | 1,443 |

### Construction & Manufacturing (`construction_manufactoring`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Architects & Engineers | `architects_engineers` | 711 |
| Building Materials | `building_materials` | 1,449 |
| Chemicals & Plastic | `chemicals_plastic` | 569 |
| Construction Services | `construction_services` | 641 |
| Contractors & Consultants | `contractors_consultants` | 7,022 |
| Factory Equipment | `factory_equipment` | 991 |
| Garden & Landscaping | `garden_landscaping` | 1,512 |
| Industrial Supplies | `industrial_supplies` | 1,051 |
| Manufacturing | `manufacturing` | 3,225 |
| Production Services | `production_services` | 398 |
| Tools & Equipment | `tools_equipment` | 1,919 |

### Education & Training (`education_training`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Colleges & Universities | `colleges_universities` | 781 |
| Courses & Classes | `courses_classes` | 1,169 |
| Education Services | `education_services` | 11,170 |
| Language Learning | `language_learning` | 589 |
| Music & Theater Classes | `music_theater_classes` | 225 |
| School & High School | `school_high_school` | 375 |
| Specials Schools | `specials_schools` | 1,454 |
| Vocational Training | `vocational_training` | 781 |

### Electronics & Technology (`electronics_technology`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Appliances & Electronics | `appliances_electronics` | 5,569 |
| Audio & Visual | `audio_visual` | 1,807 |
| Computers & Phones | `computers_phones` | 8,342 |
| Internet & Software | `internet_software` | 45,334 |
| Repair & Services | `repair_services` | 2,857 |

### Events & Entertainment (`events_entertainment`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Adult Entertainment | `adult_entertainment` | 3,582 |
| Children's Entertainment | `childrens_entertainment` | 1,979 |
| Clubbing & Nightlife | `clubbing_nightlife` | 64 |
| Events & Venues | `events_venues` | 2,513 |
| Gambling | `gambling` | 5,017 |
| Gaming | `gaming` | 7,041 |
| Museums & Exhibits | `museums_exibits` | 478 |
| Music & Movies | `music_movies` | 1,061 |
| Theater & Opera | `theater_opera` | 126 |
| Wedding & Party | `wedding_party` | 3,570 |

### Food, Beverages & Tobacco (`food_beverages_tobacco`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Agriculture & Produce | `agriculture_produce` | 441 |
| Asian Grocery Stores | `asian_grocery_stores` | 99 |
| Bakery & Pastry | `bakery_pastry` | 601 |
| Beer & Wine | `beer_wine` | 933 |
| Beverages & Liquor | `beverages_liquor` | 1,284 |
| Candy & Chocolate | `candy_chocolate` | 740 |
| Coffee & Tea | `coffee_tea` | 1,210 |
| Food Production | `food_production` | 2,227 |
| Fruits & Vegetables | `fruits_vegetables` | 166 |
| Grocery Stores & Markets | `grocery_stores_markets` | 2,118 |
| Lunch & Catering | `lunch_catering` | 560 |
| Meat, Seafood & Eggs | `meat_seafood_eggs` | 561 |
| Smoking & Tobacco | `smoking_tobacco` | 2,682 |

### Health & Medical (`health_medical`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Clinics | `clinics` | 1,575 |
| Dental Services | `dental_services` | 1,103 |
| Diagnostics & Testing | `diagnostics_testing` | 424 |
| Doctors & Surgeons | `doctors_surgeons` | 833 |
| Health Equipment | `health_equipment` | 2,506 |
| Hospital & Emergency | `hospital_emergency` | 4,044 |
| Medical Specialists | `medical_specialists` | 1,414 |
| Mental Health | `mental_health` | 1,564 |
| Pharmacy & Medicine | `pharmacy_medicine` | 4,427 |
| Physical Aids | `physical_aids` | 478 |
| Pregnancy & Children | `pregnancy_children` | 825 |
| Therapy & Senior Health | `therapy_senior_health` | 2,449 |
| Vision & Hearing | `vision_hearing` | 907 |

### Hobbies & Crafts (`hobbies_crafts`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Art & Handicraft | `art_handicraft` | 2,132 |
| Astrology & Numerology | `astrology_numerology` | 463 |
| Fishing & Hunting | `fishing_hunting` | 716 |
| Hobbies | `hobbies` | 2,951 |
| Metal, Stone & Glass Work | `metal_stone_glass_work` | 171 |
| Music & Instruments | `music_instruments` | 753 |
| Needlework & Knitting | `needlework_knitting` | 1,010 |
| Outdoor Activities | `outdoor_activities` | 622 |
| Painting & Paper | `painting_paper` | 542 |

### Home & Garden (`home_garden`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Bathroom & Kitchen | `bathroom_kitchen` | 2,825 |
| Cultural Goods | `cultural_goods` | 145 |
| Decoration & Interior | `decoration_interior` | 4,363 |
| Energy & Heating | `energy_heating` | 721 |
| Fabric & Stationery | `fabric_stationary` | 402 |
| Furniture Stores | `furniture_stores` | 6,537 |
| Garden & Pond | `garden_pond` | 3,272 |
| Home & Garden Services | `home_garden_services` | 2,215 |
| Home Goods Stores | `home_goods_stores` | 4,526 |
| Home Improvements | `home_improvements` | 3,290 |

### Home Services (`home_services`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Cleaning Service Providers | `cleaning_service_providers` | 2,326 |
| Craftsman | `craftsman` | 7,307 |
| House Services | `house_services` | 885 |
| House Sitting & Security | `house_sitting_security` | 1,131 |
| Moving & Storage | `moving_storage` | 2,509 |
| Plumbing & Sanitation | `plumbing_sanitation` | 1,703 |
| Repair Service Providers | `repair_service_providers` | 291 |

### Legal Services & Government (`legal_services_government`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Customs & Toll | `customs_toll` | 231 |
| Government Department | `government_department` | 195 |
| Law Enforcement | `law_enforcement` | 355 |
| Lawyers & Attorneys | `lawyers_attorneys` | 2,375 |
| Legal Service Providers | `legal_service_providers` | 3,189 |
| Libraries & Archives | `libraries_archives` | 24 |
| Municipal Department | `municipal_department` | 146 |
| Registration Services | `registration_services` | 361 |

### Media & Publishing (`media_publishing`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Books & Magazines | `books_magazines` | 4,570 |
| Media & Information | `media_information` | 9,210 |
| Photography | `photography` | 1,528 |
| Video & Sound | `video_sound` | 3,704 |

### Money & Insurance (`money_insurance`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Accounting & Tax | `accounting_tax` | 2,084 |
| Banking & Money | `banking_money` | 15,040 |
| Credit & Debt Services | `credit_debt_services` | 1,389 |
| Insurance | `insurance` | 3,639 |
| Investments & Wealth | `investments_wealth` | 24,911 |
| Real Estate | `real_estate` | 4,243 |

### Public & Local Services (`public_local_services`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Employment & Career | `employment_career` | 1,748 |
| Funeral & Memorial | `funeral_memorial` | 158 |
| Housing Associations | `housing_associations` | 56 |
| Kids & Family | `kids_family` | 181 |
| Military & Veteran | `military_veteran` | 55 |
| Nature & Environment | `nature_environment` | 409 |
| Professional Organizations | `professional_organizations` | 1,937 |
| Public Services & Welfare | `public_services_welfare` | 649 |
| Religious Institutions | `religious_institutions` | 303 |
| Shelters & Homes | `shelters_homes` | 100 |
| Waste Management | `waste_management` | 641 |

### Restaurants & Bars (`restaurants_bars`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| African & Pacific Cuisine | `african_pacific_cuisine` | 8 |
| Bars & Cafes | `bars_cafes` | 312 |
| Chinese & Korean Cuisine | `chinese_korean_cuisine` | 14 |
| European Cuisine | `european_cuisine` | 17 |
| General Restaurants | `general_restaurants` | 1,215 |
| Japanese Cuisine | `japanese_cuisine` | 22 |
| Mediterranean Cuisine | `mediterranean_cuisine` | 149 |
| Middle Eastern Cuisine | `middle_eastern_cuisine` | 17 |
| North & South American Cuisine | `north_south_american_cuisine` | 119 |
| Southeast Asian Cuisine | `southeast_asian_cuisine` | 86 |
| Takeaway | `takeaway` | 1,096 |
| Vegetarian & Diet | `vegetarian_diet` | 53 |

### Shopping & Fashion (`shopping_fashion`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Accessories | `accessories` | 5,992 |
| Clothing & Underwear | `clothing_underwear` | 30,505 |
| Clothing Rental & Repair | `clothing_rental_repair` | 277 |
| Costume & Wedding | `costume_wedding` | 956 |
| Jewelry & Watches | `jewelry_watches` | 5,774 |
| Malls & Marketplaces | `malls_marketplaces` | 4,970 |

### Sports (`sports`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Ball Games | `ball_games` | 550 |
| Bat-and-ball Games | `bat-and-ball_games` | 83 |
| Bowls & Lawn Sports | `bowls_lawn_sports` | 35 |
| Dancing & Gymnastics | `dancing_gymnastics` | 120 |
| Equipment & Associations | `equipment_associations` | 1,936 |
| Extreme Sports | `extreme_sports` | 902 |
| Fitness & Weight Lifting | `fitness_weight_lifting` | 1,937 |
| Golf & Ultimate | `golf_ultimate` | 536 |
| Hockey & Ice Skating | `hockey_ice_skating` | 54 |
| Martial arts & Wrestling | `martial_arts_wrestling` | 205 |
| Outdoor & Winter Sports | `outdoor_winter_sports` | 1,234 |
| Shooting & Target Sports | `shooting_target_sports` | 151 |
| Swimming & Water Sports | `swimming_water_sports` | 181 |
| Tennis & Racquet Sports | `tennis_racquet_sports` | 133 |

### Travel & Vacation (`travel_vacation`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Accommodation & Lodging | `accomodations_lodging` | 2,186 |
| Activities & Tours | `activities_tours` | 8,430 |
| Airlines & Air Travel | `airlines_air_travel` | 1,429 |
| Hotels | `hotels` | 1,772 |
| Travel Agencies | `travel_agencies` | 1,833 |

### Utilities (`utilities`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Energy & Power | `energy_power` | 1,127 |
| Oil & Fuel | `oil_fuel` | 58 |
| Water Utilities | `water_utilities` | 134 |

### Vehicles & Transportation (`vehicles_transportation`)

| Subcategory | ID | Businesses |
|-------------|-----|-----------:|
| Air & Water Transport | `air_water_transport` | 708 |
| Airports & Parking | `airports_parking` | 276 |
| Auto Parts & Wheels | `auto_parts_wheels` | 7,386 |
| Bicycles | `bicycles` | 1,413 |
| Cars & Trucks | `cars_trucks` | 2,617 |
| Motorcycle & Powersports | `motorcycle_powersports` | 807 |
| Other Vehicles & Trailers | `other_vehicles_trailers` | 550 |
| Taxis & Public Transport | `taxis_public_transport` | 3,069 |
| Vehicle Rental | `vehical_rental` | 1,503 |
| Vehicle Repair & Fuel | `vehicle_repair_fuel` | 2,381 |

## Finding deeper category IDs

Subcategories can have their own subcategories (e.g. `computers_phones` contains `cell_phone_store`). To find them:

1. Call [Category Details](/docs/trustpilot-category) with a subcategory ID — its `subcategories` array lists the next level.
2. Or call [Category Search](/docs/trustpilot-categories) with a keyword — it returns matching category IDs at any level.
3. Or open any category on trustpilot.com and take the slug after `/categories/` in the URL.
